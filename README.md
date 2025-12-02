# SQL_xBank

<img width="1200" height="675" alt="image" src="https://github.com/user-attachments/assets/681b56b7-05c2-4cbb-a626-c3db43660e89" />

## Table of Contents
I. [📌 Introduction](#I.-Introduction)

II. [📂 Dataset](#II.-Dataset)

III. [🧠 Main Process](#III.-Main-Process)

IV. [📊 Exploring the Dataset](#IV.-Exploring-the-Dataset)

V. [🔎 Final Conclusion](#V.-Conclusion)

## I. Introduction
🎉 Overview:

This project analyzes a fictional banking system called Data Bank, focusing on customer nodes, transactional behaviors, balance simulations, and data provisioning strategies. The case study mimics real-world banking datasets and helps develop SQL skills such as window functions, aggregation, running balances, interest calculations, and scenario modeling.

🏹 Objective:

The main objective is to:

✔️ Explore customer allocation across secure data nodes.

✔️ Analyze historical customer transactions (deposit, purchase, withdrawal).

✔️ Simulate three data allocation options + an interest-based option.

✔️ Produce insights useful for business decisions, security marketing, and capacity planning.

👤 Who is this project for?

This project is designed for:

✔️ Data Analysts/Data Engineers

✔️ Businesses wanting example logic for balance calculations and interest simulations

✔️ Business Analysts & Decision-makers

## II. Dataset

The dataset consists of 3 tables:

| Table                     | Description                                                                       |
| ------------------------- | --------------------------------------------------------------------------------- |
| **regions**               | Region-level metadata.                                                            |
| **customer_nodes**        | Customer → node allocation history. Includes reallocation dates.                  |
| **customer_transactions** | Customer-level daily transactions. Includes deposits, withdrawals, and purchases. |

Key Fields

* customer_id

* region / node_id

* txn_type (deposit, withdrawal, purchase)

* transaction_date

* amount

→ This dataset resembles typical financial systems and is designed to test analytical reasoning with realistic constraints.

## III. Main Process

### A. Customer Nodes Exploration

* Calculate unique nodes

* Count nodes per region

* Count customers per region

* Compute average days between reallocations

* Compute median, 80th, 95th percentile reallocation time per region

### B. Customer Transactions Analysis

* Unique count & total amount by transaction type

* Avg deposit count & amount per customer

* Monthly behavioral filtering (customers with >1 deposit & ≥1 purchase/withdrawal)

* Monthly closing balance

* Percentage of customers with >5% balance growth

### C. Data Allocation Challenge

Simulate 3 strategies:

* Option 1: Based on previous month ending balance

* Option 2: Based on 30-day average balance

* Option 3: Real-time (running) balance

Additional computed fields:

* Running balance (after each transaction)

* Monthly closing balance

* Min/Avg/Max running balance per customer

### D. Extra Challenge: Daily Interest-Based Allocation

Two interest models implemented:

1. Simple Interest (No Compounding)

Interest is calculated daily:

interest = daily_closing_balance * (0.06 / 365)

→ Summed into monthly totals for provisioning.

2. Daily Compounding Interest (Bonus)

FV = balance * (1 + 0.06/365) ^ day_number
interest = FV - balance

## IV. Full SQL

Below is the complete SQL for all parts A → D

### 🅐 Customer Nodes Exploration

#### Query 01: How many unique nodes are there?

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:a0f30bf8de3844b591b224cc5b4b3dc7)
* SQL code

<img width="1200" height="151" alt="image" src="https://github.com/user-attachments/assets/dd0829e7-a3a9-4b5a-b727-f834d8b8e961" />

* Query results

<img width="1200" height="349" alt="image" src="https://github.com/user-attachments/assets/3f1c2717-1033-40cf-aa2d-1f1994ba1c3d" />

#### Query 02: Number of nodes per region

Shows how nodes are distributed geographically.

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:86658119cf2147e8971f80476ac7a7a7)
* SQL code

<img width="1200" height="260" alt="image" src="https://github.com/user-attachments/assets/2a36cea1-c5d8-4a3f-a901-765658a28ef2" />

* Query results

<img width="1200" height="273" alt="image" src="https://github.com/user-attachments/assets/0c23b0ae-51e0-4e0b-b707-0fdb8e5d3ae3" />

#### Query 03: How many customers are allocated to each region?

Distinct customers are counted to avoid duplication across date ranges.

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:d5732cfe386443b0a21c0a2bf63cc3a5)
* SQL code

<img width="1200" height="203" alt="image" src="https://github.com/user-attachments/assets/4a35fce1-a46a-4c7b-8873-8d97fab53788" />

* Query results

<img width="1200" height="279" alt="image" src="https://github.com/user-attachments/assets/1f23da07-07b9-4cf5-a36b-a306f9e5a8db" />

#### Query 04: Average number of days before a customer is reallocated

Duration = end_date − start_date.

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:d97961119c40453bb142ca2c1dfb60fb)
* SQL code

<img width="1200" height="140" alt="image" src="https://github.com/user-attachments/assets/a7f432f9-4f2d-40e0-82ea-6fd50e69eb96" />

* Query results

<img width="1200" height="165" alt="image" src="https://github.com/user-attachments/assets/3be40e8f-eb3e-4302-96ba-1e366da067be" />

#### Query 05: Median, 80th, 95th percentile reallocation days per region

Percentile calculation provides insights into security-driven reallocation patterns.

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:823803a3bc2141fdb1f45ffded7a3a4a)
* SQL code

<img width="1200" height="331" alt="image" src="https://github.com/user-attachments/assets/fe8e0a09-3df8-4eef-a1fd-084435aeea00" />

* Query results

<img width="1200" height="479" alt="image" src="https://github.com/user-attachments/assets/157d1c93-b912-484e-b3f6-cad2c63be6d4" />

### 🅑 Customer Transactions

#### Query 01: Unique count & total amount per transaction type

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:86aaebcc7e3d4543ab8fda46261aee79)
* SQL code

<img width="1200" height="197" alt="image" src="https://github.com/user-attachments/assets/91fb70aa-e392-4256-97f2-7c1ea0390ca7" />

* Query results

<img width="1200" height="276" alt="image" src="https://github.com/user-attachments/assets/5afd113f-3d52-4f53-8394-4cc7b7ffa391" />

#### Query 01: How many unique nodes are there?

[Link to code]()
* SQL code


* Query results


#### Query 01: How many unique nodes are there?

[Link to code]()
* SQL code


* Query results















