Budgetly - High Level Architecture
Technology Stack
Frontend
- React.js
- TypeScript
- Redux Toolkit
- Tailwind CSS
- Chart library (to be finalized)
Backend
- Python
- FastAPI
- SQLAlchemy ORM
- Alembic
Database
- PostgreSQL
Cache
- Redis
Authentication
- JWT authentication
- Refresh token based authentication
- Access token expiry: 30 minutes
Repository
Monorepo structure:
budgetly/
  frontend/
  backend/
  docs/
System Architecture
Users
 |
React Application
 |
FastAPI Backend
 |
--------------------------------
Auth | Users | Expenses | Groups
Split Engine | Settlements
Analytics
--------------------------------
 |
PostgreSQL
 |
Redis
Frontend Architecture
frontend/

src/
├── app
├── components
├── pages
├── features
│   ├── auth
│   ├── expenses
│   ├── income
│   ├── groups
│   └── dashboard
├── services
├── hooks
├── utils
└── store
Responsibilities: - UI rendering - API communication - State
management - Charts - Forms
Backend Architecture
backend/

app/
├── core
├── database
├── models
├── schemas
├── services
├── repositories
└── modules
    ├── auth
    ├── users
    ├── temporary_users
    ├── expenses
    ├── income
    ├── groups
    ├── splits
    ├── settlements
    └── analytics
Core Modules
Authentication
Handles: - Signup - Login - Password hashing - JWT access tokens -
Refresh tokens - Session management
User Module
Handles: - User profile - User settings - Active sessions
Temporary User Module
Temporary users represent people who are not registered.

Stores: - Name - Mobile - Email - Created by user

Temporary users can: - Join groups - Participate in splits - Have
balances

Future conversion:
TemporaryUser -> User
Historical expenses, splits, and settlements must remain intact.
Expense Module
Handles: - Create expense - Update expense - Delete expense - Expense
history

Expense types:
PERSONAL
GROUP
Rules:

No group:
PERSONAL
Created inside group:
GROUP
Group Module
Handles: - Group creation - 6 character join code - Join requests -
Member approval - Member management

Supports: - Registered users - Temporary users

Maximum group members: 500
Split Engine
Supported:
Equal Split
Example:
₹3000 / 3 members
Each = ₹1000
Percentage Split
Example:
A 50%
B 30%
C 20%
Manual Split
Example:
A ₹5000
B ₹3000
C ₹2000
Settlement Module
Handles: - Payment records - Settlement history - Comments - Balance
tracking

Payment integration is planned for future.
Database Entities
User
TemporaryUser
Session
Income
Expense
Category
Group
GroupMember
ExpenseSplit
Settlement
Data Flow
Personal Expense
Create Expense
 |
Validate
 |
Save
 |
Return Response
Group Expense
Create Expense
 |
Validate Group
 |
Create Expense
 |
Create Split Records
 |
Update Balances
Redis Usage
Redis will be used for:
- Sessions
- Cache
- Dashboard optimization
- Temporary calculations
API Style
REST API

Examples:
POST /auth/login
GET /expenses
POST /groups
POST /groups/{id}/expenses
GET /dashboard
Security
Required:
- Password hashing
- JWT validation
- Refresh token security
- Input validation
- SQL injection prevention
- Authorization checks
- Secure sessions
Future Extensions
AI Assistant
Financial insights and recommendations.
Real Time Updates
WebSocket based group updates.
Payments
UPI/payment provider integration.
Bank Integration
Automatic transaction importing.