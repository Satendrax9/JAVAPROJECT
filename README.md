# AlomGoodDeals — E-commerce Platform

A reference Java/Spring Boot backend project for an IT-equipment e-commerce platform associated with [alomgooddeals.in](https://alomgooddeals.in/).

> **Project note:** This repository contains a reference backend design for the project report. The live website, https://alomgooddeals.in/, is built using a website builder and does not run this code.

## Overview

The project models backend functionality for an IT-equipment store, including product browsing, cart and GST billing, orders, bulk quotation enquiries, and customer support tickets.

## Features

- Product catalogue with category and keyword filtering
- Cart and GST billing concepts
- Order placement and invoice endpoint
- Bulk quotation enquiries
- Customer support tickets
- Customer registration
- Role-protected product management for administrators
- HTTP Basic authentication

## Technology Stack

- **Language:** Java 17
- **Backend framework:** Spring Boot 3.2.5
- **Build and dependency management:** Maven
- **Database:** MySQL 8
- **Database access:** Spring JDBC
- **Web APIs:** Spring Web
- **Security:** Spring Security
- **Input validation:** Spring Boot Validation
- **Testing:** Spring Boot Starter Test
- **Container support:** Docker, using Eclipse Temurin Java 17 JRE

## Requirements

Install the following before running the backend:

- Java 17 or newer
- Maven 3.8+
- MySQL 8

## Setup

1. Clone or download this repository and open a terminal in the project root.
2. Create the MySQL database and tables using the project's schema file:

   ```bash
   mysql -u root -p < src/main/resources/schema.sql
   ```

3. Configure a database user with access to the `alom_shop` database. The default username noted in the project is `shop_user`; check `src/main/resources/application.properties` for the configured value.
4. Set the database password in the `DB_PASSWORD` environment variable. On macOS/Linux:

   ```bash
   export DB_PASSWORD='your-password'
   ```

   On Windows PowerShell:

   ```powershell
   $env:DB_PASSWORD = "your-password"
   ```

5. Create an administrator account in the `users` table using a BCrypt password hash and the `ADMIN` role, as required by the project configuration.

## Build and Run

Build the application:

```bash
mvn clean package
```

Run the generated JAR:

```bash
java -jar target/ecommerce-platform-1.0.0.jar
```

The Dockerfile expects the built JAR at `target/ecommerce-platform-1.0.0.jar` and exposes port `8080`.

## Run Tests

```bash
mvn test
```

## API Endpoints

| Method | Endpoint | Purpose | Access |
|---|---|---|---|
| GET | `/api/products` | List products; supports `category` or `q` filtering | Public |
| POST | `/api/products` | Add a product | Admin |
| POST | `/api/orders` | Place an order | Customer |
| GET | `/api/orders/{id}/invoice` | Get a text invoice | Customer |
| POST | `/api/quotes` | Submit a bulk quotation enquiry | Public |
| POST | `/api/tickets` | Raise a support ticket | Customer |
| POST | `/api/auth/register` | Register a customer | Public |

Authentication is documented as HTTP Basic using email and password. Use HTTPS in production.

## Console Demo

The repository README describes a console demo that runs without a database or Spring. From the project root, with a JDK installed:

```bash
javac -d out src/main/java/in/alomgooddeals/shop/model/*.java demo/ConsoleDemo.java
java -cp out ConsoleDemo
```

## Repository Files

- `pom.xml` — Maven project configuration and dependencies
- `Dockerfile` — container image instructions for running the packaged JAR
- `.gitignore` — excludes generated build output and IDE files
- `src/` — application source and resources (including database schema and configuration, if present)
- `demo/` — console demo files, if present

## Live Website

Visit [https://alomgooddeals.in/](https://alomgooddeals.in/) to view the live website.

---

**Before running:** confirm that the source files and configuration referenced above are present in the repository, and never commit real database passwords or other secrets.
