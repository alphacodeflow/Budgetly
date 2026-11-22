# Budgetly Database Design

## 1. Overview

Budgetly is a personal expense management and shared expense tracking application.

The database is designed to support:

- User management
- Expense tracking
- Shared expenses
- Group expenses
- Settlements
- Categories
- Budgets
- Recurring expenses
- Notifications
- Audit history
- External/non-system participants

The database follows a relational model using PostgreSQL.

---

# 2. Database Technology

| Component    | Technology                    |
| ------------ | ----------------------------- |
| Database     | PostgreSQL                    |
| ORM          | SQLAlchemy / Prisma / TypeORM |
| Migration    | Alembic / Prisma Migration    |
| Cache        | Redis (optional)              |s

---

# 3. Entity Relationship Overview
```
Users
|
|---- Expenses
| |
| |---- Expense Participants
| |
| |---- Categories
|
|---- Groups
|
|---- Group Members
|
|---- Group Expenses

Expenses
|
|---- Settlements

Users
|
|---- Budgets

Users
|
|---- Recurring Expenses
```

---

# 4. Users Table

Stores application users.

## Table: users

| Column        | Type         | Constraints          |
| ------------- | ------------ | -------------------- |
| id            | UUID         | Primary Key          |
| name          | VARCHAR(100) | NOT NULL             |
| email         | VARCHAR(255) | UNIQUE               |
| phone         | VARCHAR(20)  | UNIQUE               |
| password_hash | TEXT         | NULL                 |
| profile_image | TEXT         | NULL                 |
| currency      | VARCHAR(10)  | DEFAULT INR          |
| timezone      | VARCHAR(50)  | DEFAULT Asia/Kolkata |
| created_at    | TIMESTAMP    |                      |
| updated_at    | TIMESTAMP    |                      |

## Purpose

Stores registered Budgetly users.

---

# 5. Categories Table

Stores expense categories.

## Table: categories

| Column     | Type         | Constraints |
| ---------- | ------------ | ----------- |
| id         | UUID         | Primary Key |
| user_id    | UUID         | FK users.id |
| name       | VARCHAR(100) | NOT NULL    |
| icon       | VARCHAR(50)  |             |
| color      | VARCHAR(20)  |             |
| created_at | TIMESTAMP    |             |

## Examples

Food
Travel
Shopping
Rent
Bills
Entertainment

Users can create custom categories.

---

# 6. Expenses Table

Main expense transaction table.

## Table: expenses

| Column         | Type          | Constraints      |
| -------------- | ------------- | ---------------- |
| id             | UUID          | Primary Key      |
| user_id        | UUID          | FK users.id      |
| category_id    | UUID          | FK categories.id |
| title          | VARCHAR(255)  | NOT NULL         |
| description    | TEXT          |                  |
| amount         | DECIMAL(12,2) | NOT NULL         |
| currency       | VARCHAR(10)   |                  |
| expense_date   | DATE          |                  |
| payment_method | VARCHAR(50)   |                  |
| type           | ENUM          | PERSONAL/GROUP   |
| status         | ENUM          | ACTIVE/DELETED   |
| created_at     | TIMESTAMP     |                  |
| updated_at     | TIMESTAMP     |                  |

## Example

Dinner with friends

Amount:
1200 INR

Paid By:
Pavan

Category:
Food

---

# 7. Expense Participants Table

Handles splitting expenses between users.

Supports:

- Equal split
- Percentage split
- Custom amount split

## Table: expense_participants

| Column      | Type          | Constraints    |
| ----------- | ------------- | -------------- |
| id          | UUID          | Primary Key    |
| expense_id  | UUID          | FK expenses.id |
| user_id     | UUID          | FK users.id    |
| amount      | DECIMAL(12,2) |                |
| percentage  | DECIMAL(5,2)  |                |
| paid_amount | DECIMAL(12,2) |                |
| status      | ENUM          | OWED/PAID      |
| created_at  | TIMESTAMP     |                |

## Example

Expense:

Dinner = 3000

Participants:

Pavan 1000
Rahul 1000
Amit 1000

---

# 8. External Participants Table

Handles people who are not registered in Budgetly.

Example:

User creates expense with friends who don't use the app.

## Table: external_participants

| Column     | Type          | Constraints    |
| ---------- | ------------- | -------------- |
| id         | UUID          | Primary Key    |
| expense_id | UUID          | FK expenses.id |
| name       | VARCHAR(100)  |                |
| phone      | VARCHAR(20)   | NULL           |
| email      | VARCHAR(255)  | NULL           |
| amount     | DECIMAL(12,2) |                |
| status     | ENUM          | PENDING/PAID   |
| created_at | TIMESTAMP     |                |

## Example

Trip expense:

Pavan
Rahul (not registered)
Ajay (not registered)

---

# 9. Groups Table

Represents shared expense groups.

Examples:

- Goa Trip
- Roommates
- Office Lunch

## Table: groups

| Column      | Type         | Constraints |
| ----------- | ------------ | ----------- |
| id          | UUID         | Primary Key |
| created_by  | UUID         | FK users.id |
| name        | VARCHAR(100) |             |
| description | TEXT         |             |
| created_at  | TIMESTAMP    |             |

---

# 10. Group Members Table

Stores users belonging to groups.

## Table: group_members

| Column    | Type      | Constraints  |
| --------- | --------- | ------------ |
| id        | UUID      | Primary Key  |
| group_id  | UUID      | FK groups.id |
| user_id   | UUID      | FK users.id  |
| role      | ENUM      | ADMIN/MEMBER |
| joined_at | TIMESTAMP |              |

---

# 11. Group Expenses Table

Connects expenses with groups.

## Table: group_expenses

| Column     | Type |
| ---------- | ---- |
| id         | UUID |
| group_id   | UUID |
| expense_id | UUID |

---

# 12. Settlements Table

Tracks payments between users.

Example:

Rahul owes Pavan 500

Rahul paid Pavan

## Table: settlements

| Column          | Type      |
| --------------- | --------- |
| id              | UUID      |
| from_user_id    | UUID      |
| to_user_id      | UUID      |
| amount          | DECIMAL   |
| status          | ENUM      |
| settlement_date | DATE      |
| created_at      | TIMESTAMP |

Status:

PENDING
COMPLETED
CANCELLED

---

# 13. Budgets Table

Allows users to set spending limits.

## Table: budgets

| Column       | Type      |
| ------------ | --------- |
| id           | UUID      |
| user_id      | UUID      |
| category_id  | UUID      |
| amount_limit | DECIMAL   |
| month        | INTEGER   |
| year         | INTEGER   |
| created_at   | TIMESTAMP |

Example:

Food Budget

January

Limit:
5000 INR

---

# 14. Recurring Expenses Table

Stores automatic recurring transactions.

Examples:

- Rent
- Subscription
- Insurance

## Table: recurring_expenses

| Column     | Type      |
| ---------- | --------- |
| id         | UUID      |
| user_id    | UUID      |
| title      | VARCHAR   |
| amount     | DECIMAL   |
| frequency  | ENUM      |
| next_date  | DATE      |
| active     | BOOLEAN   |
| created_at | TIMESTAMP |

Frequency:

DAILY
WEEKLY
MONTHLY
YEARLY

---

# 15. Notifications Table

Stores user notifications.

## Table: notifications

| Column     | Type      |
| ---------- | --------- |
| id         | UUID      |
| user_id    | UUID      |
| title      | VARCHAR   |
| message    | TEXT      |
| read       | BOOLEAN   |
| created_at | TIMESTAMP |

---

# 16. Audit Logs

Tracks important activities.

## Table: audit_logs

| Column     | Type      |
| ---------- | --------- |
| id         | UUID      |
| user_id    | UUID      |
| action     | VARCHAR   |
| entity     | VARCHAR   |
| entity_id  | UUID      |
| metadata   | JSONB     |
| created_at | TIMESTAMP |

Example:

USER_CREATED_EXPENSE

Expense_ID:
abc123

---

# 17. Database Indexes

## Users

INDEX(email)
INDEX(phone)

## Expenses

INDEX(user_id)
INDEX(category_id)
INDEX(expense_date)

## Expense Participants

INDEX(expense_id)
INDEX(user_id)

## Groups

INDEX(created_by)

---

# 18. Soft Delete Strategy

Important tables support soft deletion.

Instead of deleting records:

DELETE FROM expenses

Use:

status = DELETED

Benefits:

- Data recovery
- Audit history
- Financial accuracy

---

# 19. Data Consistency Rules

## Expense Amount Validation

SUM(participant_amounts)
expense.amount

## Settlement Validation

from_user != to_user

## Group Expense Validation

Expense participants must belong to group members.

---

# 20. Future Extensions

Possible additions:

- Bank account linking
- UPI integration
- AI expense categorization
- Receipt scanning
- OCR based expense creation
- Multi currency support
- Investment tracking
- Financial reports

---
