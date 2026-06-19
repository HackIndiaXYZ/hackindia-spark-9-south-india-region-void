# Smart FinOps – Real-Time Policy-Driven Financial Governance Platform

## Overview

Smart FinOps is a real-time financial governance platform designed to improve transparency, accountability, and compliance in organizational spending. The system enforces department-level budget controls, policy-driven transaction validation, role-based approvals, and tamper-evident audit logging.

The platform combines traditional web technologies with blockchain principles to create an immutable financial audit trail, ensuring that every approved transaction can be verified and traced.

Developed as a prototype for the Tamil Nadu Hackathon, Smart FinOps demonstrates how modern governance systems can leverage automation and blockchain-inspired mechanisms to prevent financial misuse and strengthen public trust.

---

# Problem Statement

Organizations and government bodies often struggle with fragmented financial systems, delayed audits, and limited transparency in expenditure management. This leads to budget overruns, policy violations, and difficulties in detecting unauthorized spending. Existing solutions primarily focus on post-event auditing rather than proactive governance. There is a need for a secure and transparent platform that can validate transactions in real time, enforce financial policies, and maintain an immutable audit trail for accountability.

---

# Key Objectives

- Enforce financial policies before expenditure occurs
- Prevent budget overruns through real-time validation
- Maintain complete transparency in financial operations
- Provide tamper-evident audit records
- Enable hierarchical approval workflows
- Improve accountability and compliance

---

# System Architecture

```text
                    ┌─────────────────────┐
                    │      Web Client     │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │   Flask Backend     │
                    └──────────┬──────────┘
                               │
                ┌──────────────┼──────────────┐
                │              │              │
                ▼              ▼              ▼

       Policy Engine    Budget Validator   RBAC Module

                │              │              │
                └───────┬──────┴──────┬───────┘
                        │             │
                        ▼             ▼

                Transaction Workflow
                        │
                        ▼

             Immutable Audit Logging
                (SHA-256 Hash Chain)

                        │
                        ▼

       Optional Ethereum Smart Contract
                 Transaction Anchor
```

---

# Core Features

## Role-Based Governance

The platform supports multiple user roles with controlled permissions.

### Supported Roles

- Super Admin
- Manager
- Employee
- Auditor

Each role operates within predefined financial limits and access controls.

---

## Budget Allocation & Enforcement

The system ensures financial discipline through budget tracking and validation.

### Features

- Department-level budget allocation
- Real-time budget utilization monitoring
- Automatic overspending prevention
- Policy-based transaction rejection
- Remaining budget visibility

---

## Hierarchical Approval Workflow

Every financial request follows a structured approval process.

### Workflow

1. Employee submits transaction request
2. Request enters Pending state
3. Manager reviews request
4. Approved request updates department budget
5. Audit record is generated
6. Transaction becomes immutable

---

## Policy-Driven Validation Engine

Transactions are validated before approval using configurable financial policies.

### Validation Checks

- Budget availability
- Spending thresholds
- Department restrictions
- Policy compliance
- Transaction limits

Non-compliant transactions are automatically rejected.

---

## Immutable Audit Logging

Each approved transaction is permanently recorded using blockchain-inspired principles.

### Audit Process

For every approved transaction:

1. Transaction details are collected
2. SHA-256 hash is generated
3. Previous block hash is linked
4. New audit block is created
5. Block is stored in audit_logs

This creates a tamper-evident chain of records.

---

## Tamper Detection

The platform verifies audit integrity using cryptographic hash validation.

### Verification Process

- Recalculate hashes
- Compare stored hashes
- Validate previous hash links
- Detect modifications

If any record is altered, chain verification immediately fails.


# System Workflow

```text
User Login
    │
    ▼

Create Transaction
    │
    ▼

Policy Validation
    │
    ├── Invalid → Rejected
    │
    └── Valid
            │
            ▼

      Pending Approval
            │
            ▼

      Manager Approval
            │
            ▼

      Budget Deduction
            │
            ▼

    Audit Log Generation
            │
            ▼

 Blockchain Verification
```

---


# API Documentation

## Authentication APIs

| Method | Endpoint | Description |
|----------|----------|-------------|
| POST | /register | Register a new user |
| POST | /login | Authenticate user |

---

## User Management APIs

| Method | Endpoint | Description |
|----------|----------|-------------|
| GET | /users | Get all users |
| GET | /users/<id> | Get user details |
| DELETE | /users/<id> | Remove user |

---

## Budget Management APIs

| Method | Endpoint | Description |
|----------|----------|-------------|
| POST | /set-budget | Allocate department budget |
| GET | /budget | View budget details |
| PUT | /update-budget | Modify budget allocation |

---

## Transaction APIs

| Method | Endpoint | Description |
|----------|----------|-------------|
| POST | /transaction | Create transaction |
| GET | /transactions | View all transactions |
| GET | /transactions/<id> | View transaction |
| PUT | /approve/<id> | Approve transaction |
| DELETE | /transaction/<id> | Delete transaction |

---

## Policy Engine APIs

| Method | Endpoint | Description |
|----------|----------|-------------|
| POST | /validate-transaction | Validate transaction |
| POST | /add-policy | Add new policy |
| GET | /policies | View policies |

---

## Reports & Audit APIs

| Method | Endpoint | Description |
|----------|----------|-------------|
| GET | /dashboard-summary | Financial summary |
| GET | /department-report | Department spending report |
| GET | /audit-log | Audit history |
| GET | /verify_chain | Verify blockchain integrity |

---

# Technology Stack

## Backend
- Flask
- Python

## Database
- SQLite

## Security
- Role-Based Access Control (RBAC)
- SHA-256 Cryptographic Hashing

## Governance Engine
- Budget Validation Engine
- Policy Enforcement Engine
- Approval Workflow Engine

## Blockchain Layer
- Hash Chain Audit Logging

---

# Installation & Setup

## Prerequisites

Make sure the following are installed:

- Python 3.10+
- Git
- pip
- Virtual Environment (venv)

---

## Clone the Repository

```bash
git clone https://github.com/your-username/smart-finops.git
cd smart-finops
```

---

## Create Virtual Environment

### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

### Linux / Mac

```bash
python3 -m venv venv
source venv/bin/activate
```

---

## Install Dependencies

```bash
pip install -r requirements.txt
```

If requirements.txt is not available:

```bash
pip install flask flask-sqlalchemy flask-cors
```

---

## Initialize Database

```bash
python app.py
```

The SQLite database will be automatically created if it does not exist.

---

## Run the Application

```bash
python app.py
```

Expected output:

```text
* Running on http://127.0.0.1:5000
```

Open:

```text
http://127.0.0.1:5000
```

---

# API Testing

You can test APIs using:

- Postman
- Thunder Client
- cURL

Base URL:

```text
http://127.0.0.1:5000
```

---

# Sample Workflow

## 1. Register User

```http
POST /register
```

Request Body:

```json
{
    "name": "John",
    "email": "john@example.com",
    "password": "123456",
    "role": "employee"
}
```

---

## 2. Login

```http
POST /login
```

Request Body:

```json
{
    "email": "john@example.com",
    "password": "123456"
}
```

---

## 3. Set Department Budget

```http
POST /set-budget
```

```json
{
    "department": "Finance",
    "budget": 100000
}
```

---

## 4. Create Transaction

```http
POST /transaction
```

```json
{
    "department": "Finance",
    "amount": 5000,
    "description": "Equipment Purchase"
}
```

---

## 5. Approve Transaction

```http
PUT /approve/1
```

After approval:

- Budget is updated
- Audit block is created
- Transaction becomes immutable

---

## 6. Verify Audit Chain

```http
GET /verify_chain
```

Expected Response:

```json
{
    "status": "Blockchain Valid"
}
```

If any audit record is tampered:

```json
{
    "status": "Blockchain Corrupted"
}
```

---

# Project Structure

```text
smart-finops/
│
├── app.py
├── models.py
├── blockchain.py
├── policy_engine.py
├── requirements.txt
├── README.md
│
├── database/
│   └── smartfinops.db
│
├── routes/
│   ├── auth.py
│   ├── budget.py
│   ├── transaction.py
│   └── audit.py
│
└── static/
```

---

# Stopping the Server

Press:

```bash
CTRL + C
```

to stop the Flask server.

---

# Future Enhancements

- AI-powered fraud detection
- Risk scoring engine
- Predictive budget analytics
- Multi-department governance dashboard
- Hyperledger Fabric integration
- Real-time compliance monitoring
- Automated audit reporting

---

# Conclusion

Smart FinOps transforms traditional financial management into a transparent, policy-driven governance system. By combining real-time validation, automated approvals, and blockchain-inspired audit logging, the platform ensures accountability, prevents unauthorized spending, and creates a verifiable record of every financial decision.

---

# hackindia-spark-9-south-india-region-void
TEAM NAME: VOID


Hackathon team repository for VOID - [hackindia-team:hackindia-spark-9-south-india-region:void]
