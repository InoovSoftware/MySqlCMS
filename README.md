# 🗃️ Base CMS Database Schema (MySQL) / Skeleton

This repository contains the MySQL schema for the **CMS Based** application — a tool for generating invoices, manging users and profiles. The schema is designed to support core functionality including user profiles, invoice management, client records.

It's a used to help quick dev of apps

---

## 📑 Tables Overview

### 1. `users`
Stores authenticated users of the application.

| Column         | Type          | Description                          |
|----------------|---------------|--------------------------------------|
| `id`           | INT           | Primary key                          |
| `uid`          | VARCHAR(100)  | Unique Firebase or external UID      |
| `email`        | VARCHAR(255)  | Email address                        |
| `password_hash`| VARCHAR(255)  | Hashed password (if applicable)      |
| `created_at`   | TIMESTAMP     | Account creation time                |

---

### 2. `profiles`
Extended profile data linked to users.

| Column         | Type           | Description                          |
|----------------|----------------|--------------------------------------|
| `user_id`      | INT            | FK to `users(id)`                    |
| `full_name`    | VARCHAR(255)   | Full name                            |
| `company_name` | VARCHAR(255)   | Business name                        |
| `logo_url`     | VARCHAR(512)   | Logo storage URL                     |
| `address`      | TEXT           | Physical or billing address          |
| `phone`        | VARCHAR(20)    | Contact number                       |
| `currency`     | VARCHAR(10)    | Default currency (e.g., MAD, USD)    |

---

### 3. `clients`
Client records per user.

| Column       | Type           | Description                          |
|--------------|----------------|--------------------------------------|
| `user_id`    | INT            | FK to `users(id)`                    |
| `name`       | VARCHAR(255)   | Client full name or company name     |
| `email`      | VARCHAR(255)   | Client email                         |
| `phone`      | VARCHAR(20)    | Phone number                         |
| `address`    | TEXT           | Client billing address               |
| `created_at` | TIMESTAMP      | Creation timestamp                   |

---

### 5. `invoices`
Holds all invoices per user.

| Column       | Type           | Description                          |
|--------------|----------------|--------------------------------------|
| `user_id`    | INT            | FK to `users(id)`                    |
| `client_id`  | INT            | FK to `clients(id)`                  |
| `rfq_id`     | INT (nullable) | Optional FK to RFQ                   |
| `number`     | VARCHAR(50)    | Unique invoice number                |
| `status`     | ENUM           | `draft`, `sent`, `paid`, etc.        |
| `due_date`   | DATE           | Payment deadline                     |
| `currency`   | VARCHAR(10)    | Currency used                        |
| `total`      | DECIMAL        | Total amount                         |
| `created_at` | TIMESTAMP      | Creation timestamp                   |

---

### 6. `invoice_items`
Line items associated with an invoice.

| Column        | Type           | Description                          |
|---------------|----------------|--------------------------------------|
| `invoice_id`  | INT            | FK to `invoices(id)`                 |
| `description` | VARCHAR(255)   | Line item description                |
| `quantity`    | INT            | Units                                |
| `unit_price`  | DECIMAL        | Price per unit                       |
| `total`       | DECIMAL        | Quantity * Unit Price                |

---

## 🧪 Usage

You can import this schema into MySQL using the standard CLI or tools like **phpMyAdmin**, **Sequel Ace**, or **DBeaver**:

```bash
mysql -u root -p your_db_name < schema.sql
