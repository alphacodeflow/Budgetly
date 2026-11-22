# Budgetly - Product Overview

## 1. Introduction

Budgetly is a personal and group expense management application that
helps users track income, expenses, shared expenses, settlements, and
understand spending patterns.

Budgetly helps users answer:

-   Where is my money going?
-   How much am I spending?
-   What categories consume most money?
-   Who owes money to whom?
-   How much money have I received and recorded?

Budgetly is not a banking application.

It does not connect to bank accounts, show actual bank balances, or
process payments.

It is a financial record-keeping and expense analysis system.

------------------------------------------------------------------------

# 2. Product Vision

Build a simple platform where users can manage:

-   Personal finances
-   Group expenses
-   Shared settlements
-   Spending analytics

------------------------------------------------------------------------

# 3. Core Product Concept

A single user account can contain:

-   Personal records
-   Group records

There are no separate personal and group accounts.

All records belong to the user and are classified using record type.

Example:

    User: Pavan

    Personal:
    - Salary income
    - Food expense
    - Shopping expense

    Groups:
    - Goa Trip
    - Office Lunch
    - Room Expenses

------------------------------------------------------------------------

# 4. Expense Management

Budgetly uses one expense system.

Expense types:

    PERSONAL
    GROUP

A personal expense is created without a group.

A group expense is created from a group and automatically becomes a
group expense.

------------------------------------------------------------------------

# 5. Personal Expense Conversion

A personal expense can later become a group expense.

Example:

    Dinner
    ₹3000

    Initially:
    Personal Expense

Later:

    Add Rahul and Ajay
    Split expense

System should:

1.  Convert PERSONAL expense to GROUP expense
2.  Create split records
3.  Preserve history

------------------------------------------------------------------------

# 6. Group Management

Users can create groups for:

-   Trips
-   Friends
-   Family expenses
-   Office expenses
-   Shared living expenses

Any registered user can create a group.

A unique 6-character code is generated.

Joining requires approval.

Flow:

    Enter code
        |
    Join request
        |
    Owner accepts/rejects

Maximum group members:

    500

------------------------------------------------------------------------

# 7. Temporary Users (External Members)

Budgetly supports people who are not registered in the system.

A user can create a temporary member using:

-   Name
-   Mobile number
-   Email address

Temporary users can participate in:

-   Groups
-   Expense splits
-   Balances
-   Settlements

They cannot:

-   Login
-   Create groups
-   Access the application

until they create an account.

Example:

    Goa Trip

    Members:

    Pavan  (Registered)
    Rahul  (Temporary)
    Ajay   (Temporary)

------------------------------------------------------------------------

# 8. Temporary User Conversion

Future functionality:

A temporary user can become a registered user.

Example:

    Temporary Rahul

            |

    Creates Budgetly account

            |

    Converted to User Rahul

Historical data must be preserved:

-   Expenses
-   Splits
-   Settlements
-   Group membership

------------------------------------------------------------------------

# 9. Expense Splitting

Supported split methods:

## Equal Split

    ₹3000 / 3 members

    Each owes ₹1000

## Percentage Split

    Pavan 50%
    Rahul 30%
    Ajay 20%

## Manual Split

    Pavan ₹5000
    Rahul ₹3000
    Ajay ₹2000

------------------------------------------------------------------------

# 10. Settlement Management

Budgetly does not process payments.

Settlement only records payment information.

Example:

    From:
    Rahul

    To:
    Pavan

    Amount:
    ₹1000

    Comment:
    Paid through UPI

------------------------------------------------------------------------

# 11. Income Management

Income is personal only.

Examples:

-   Salary
-   Freelance
-   Business
-   Gift

Income does not represent bank balance.

Budgetly only records:

    Money received
    Money spent

------------------------------------------------------------------------

# 12. Categories

Default categories:

    Food
    Travel
    Shopping
    Bills
    Entertainment
    Health
    Education
    Others

Users can create custom categories.

------------------------------------------------------------------------

# 13. Dashboard

Dashboard provides:

-   Total income
-   Total expenses
-   Category breakdown
-   Monthly trends
-   Graphs

------------------------------------------------------------------------

# 14. Authentication

Current:

-   Email
-   Password

Future:

-   Google Login
-   OTP Login

------------------------------------------------------------------------

# 15. Session Management

Only one active device session is allowed.

A new login invalidates the previous session.

------------------------------------------------------------------------

# 16. Data Synchronization

Current:

-   Manual refresh
-   No real-time updates

Future:

-   WebSocket updates

------------------------------------------------------------------------

# 17. Group Visibility

Group members can view:

-   Group expenses
-   Expense creator
-   Paid amount
-   Split details
-   Balances
-   Settlement history

------------------------------------------------------------------------

# 18. Main Business Entities

    User

    TemporaryUser

    Income

    Expense

    Category

    Group

    GroupMember

    ExpenseSplit

    Settlement

    Session

------------------------------------------------------------------------

# 19. Future Features

-   UPI/payment integration
-   AI financial assistant
-   Bank integration
-   Notifications
-   Real-time updates

------------------------------------------------------------------------

# 20. Product Summary

Budgetly combines:

    Splitwise
    +
    Expense Tracker
    +
    Income Logger
    +
    Financial Analytics

Purpose:

Help users understand their money flow, manage shared expenses, and make
better financial decisions.
