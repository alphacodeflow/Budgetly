# 💰 Budgetly

Budgetly is a modern expense-sharing application that makes it easy to split bills, track shared expenses, and settle balances with friends, roommates, families, and teams.

Inspired by applications like Splitwise, Budgetly focuses on providing a clean user experience, real-time expense management, and accurate balance calculations.

> 🚧 **Status:** Under Active Development

---

# ✨ Features

### User Management
- Secure Authentication
- User Profiles
- Invite Friends

### Groups
- Create Groups
- Add & Remove Members
- Group Expense History

### Expense Management
- Add Expenses
- Split Equally
- Split by Percentage
- Split by Exact Amount
- Unequal Splits
- Recurring Expenses *(Planned)*

### Settlements
- View Who Owes Whom
- Record Settlements
- Simplified Debt Calculation
- Balance History

### Dashboard
- Overall Balance
- Total You Owe
- Total You're Owed
- Recent Activity

### Notifications *(Planned)*
- Expense Updates
- Settlement Reminders
- Group Invitations

---

# 🛠 Tech Stack

## Frontend
- React
- Vite
- Tailwind CSS
- Redux Toolkit
- React Router
- Axios

## Backend
- Python
- FastAPI
- PostgreSQL
- SQLAlchemy

## DevOps
- Docker
- Docker Compose

## Future Integrations
- Redis
- WebSockets
- Celery
- JWT Authentication
- Email Notifications
- Cloud Storage

---

# 📂 Project Structure

```text
budgetly/

├── client/                 # React Application
│
├── server/                 # FastAPI Backend
│
├── docker/                 # Docker Configuration
│
├── docs/                   # Documentation
│
└── README.md
```

---

# 🚀 Planned Workflow

1. Create an account
2. Add friends
3. Create a group
4. Add expenses
5. Split expenses
6. View balances
7. Settle debts
8. Track expense history

---

# 🧠 Core Features

- Expense Splitting
- Group Management
- Individual Expenses
- Smart Balance Calculation
- Settlement Tracking
- Activity Timeline
- Search & Filters
- Responsive Design
- Dark Mode

---

# 🔮 Future Enhancements

- Multi-Currency Support
- OCR Receipt Scanner
- AI Expense Categorization
- Voice Expense Entry
- UPI Integration
- Bank Account Sync
- Monthly Spending Analytics
- Budget Tracking
- Recurring Bills
- Expense Reminders
- Export to PDF/CSV
- Mobile App
- Push Notifications

---

# 🏗️ Getting Started

## Clone Repository

```bash
git clone https://github.com/your-username/budgetly.git

cd budgetly
```

## Frontend

```bash
cd client

npm install

npm run dev
```

Frontend runs on:

```
http://localhost:5173
```

## Backend

```bash
cd server

python -m venv venv

# Windows
venv\Scripts\activate

# Linux / macOS
source venv/bin/activate

pip install -r requirements.txt

uvicorn app.main:app --reload
```

Backend runs on:

```
http://localhost:8000
```

Swagger API:

```
http://localhost:8000/docs
```

---

# 📅 Roadmap

- [ ] Authentication
- [ ] Friend Requests
- [ ] Group Creation
- [ ] Expense CRUD
- [ ] Expense Splitting Algorithms
- [ ] Balance Calculation
- [ ] Settlements
- [ ] Notifications
- [ ] Activity Feed
- [ ] Multi-Currency Support
- [ ] Receipt Upload
- [ ] Reports & Analytics
- [ ] Testing
- [ ] Docker Deployment
- [ ] CI/CD Pipeline

---

# 🤝 Contributing

Contributions, feature suggestions, and bug reports are welcome.

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Open a Pull Request

---

# 📜 License

MIT License

---

## ⭐ Support

If you like this project, consider giving it a ⭐ on GitHub.
