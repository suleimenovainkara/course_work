# Bank Application with Fraud Detection

A desktop banking application with an integrated machine learning fraud detection system, built as a coursework project. The system allows customers to manage accounts, deposits, credits, and transfers — while employees can monitor and flag suspicious transactions in real time using a trained Logistic Regression model.

## Overview
Fraud detection in financial transactions has grown increasingly critical as the volume and complexity of digital transactions continue to expand. Fraudulent activities can result in significant financial losses, reputational harm, and severe security breaches.

This project combines a fully functional banking desktop application with a fraud detection pipeline powered by machine learning, enabling identification of suspicious activities and reducing false positives.

## Project Goals
- Design a desktop banking application with role-based access (Customer / Employee)
- Build a relational database to store customers, accounts, transactions, deposits, and credits
- Integrate a machine learning model for real-time fraud detection on pending transactions
- Flag suspicious transactions automatically based on predicted fraud probability

## Dataset
- Name - Synthetic Financial Datasets for Fraud Detection
- Source - https://www.kaggle.com/datasets/ealaxi/paysim1
- Description - Simulates mobile money transactions with injected fraudulent behavior
- Use in project - Training the Logistic Regression fraud detection model

## Tech Stack
- UI - Python, CustomTkinter
- Database - Microsoft SQL Server (SSMS)
- ORM / DB Access - SQLAlchemy
- ML Model - Logistic Regression

## Database Schema
The application uses Microsoft SQL Server with the following tables:
- customer: Registered bank customers
- accounts: Bank accounts linked to customers
- transactions: All transfers with fraud detection fields
- deposit: Customer deposit records
- credit: Issued credits and repayment tracking
- employees: Bank staff with role-based access

Key transaction fields used for fraud detection:
- oldBalanceOrig  -- Sender balance before transaction
- newBalanceOrig  -- Sender balance after transaction
- oldBalanceDest  -- Receiver balance before transaction
- newBalanceDest  -- Receiver balance after transaction
- isFlaggedFraud  -- ML prediction flag (0 / 1)
- status          -- pending → completed / failed

## Fraud Detection
Fraud detection is performed by an employee via the Employee Dashboard. The pipeline works as follows:


1. All transactions with status = 'pending' are fetched from the database
2. Numerical features are transformed using Box-Cox normalization
3. A pre-trained Logistic Regression model predicts fraud probability for each transaction
4. Transactions with fraud probability ≥ 90% are flagged as isFlaggedFraud = 1
5. All pending transactions are marked completed and account balances are updated

## Roles & Features
### Customer
- Register and log in via phone + password
- View account balance and live exchange rates (USD, EUR, RUB, KZT, GBP, CHF, CNY)
- Make transfers to other accounts
- Open, replenish, and withdraw from deposits (3.5% interest rate)
- Apply for credits and make monthly repayments

### Employee
- View all active credits across customers
- Manage customer accounts (create / block / delete)
- Generate credit status reports
- Add and remove employee accounts
- Run fraud detection on pending transactions

## Technologies
- customtkinter
- sqlalchemy
- pandas
- numpy
- scipy
- scikit-learn
- joblib
- requests
