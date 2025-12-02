# [SQL] How Can a Digital Bank Optimize Data Allocation and Customer Growth? — Banking Analytics

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

#### Query 02: Average deposit count & amount per customer

Deposit behavior is aggregated per customer, then averaged.

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:6b8258d35855473794164b2d88dfea52)
* SQL code

<img width="1200" height="377" alt="image" src="https://github.com/user-attachments/assets/93a3520d-a777-4215-b471-85bdb9ff1601" />

* Query results

<img width="1200" height="160" alt="image" src="https://github.com/user-attachments/assets/b9dbfbb0-003e-4151-8308-3914de4aa8d5" />

#### Query 03: Monthly customers with >1 deposit AND ≥1 purchase/withdrawal

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:49df1453294d4f1d89d3e4da3c62993c)
* SQL code

<img width="1200" height="397" alt="image" src="https://github.com/user-attachments/assets/ef2198ca-d4ed-45ff-8510-13206c0e6693" />

* Query results

<img width="1200" height="256" alt="image" src="https://github.com/user-attachments/assets/0f70181f-40ff-4238-ae15-e8a77530c26a" />

#### Query 04: Monthly closing balance

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:3bc153f8c8a8446b9062f4c2a6d89527)
* SQL code

```ruby
WITH ordered_tx AS (
  SELECT
    customer_id
    ,txn_date
    ,txn_type
    ,txn_amount
    ,CASE
      WHEN txn_type = 'deposit' THEN txn_amount
      ELSE -txn_amount
    END AS amount_adj
  FROM academic-arcade-452814-b8.Data_bank.customer_transactions
),
running AS (
  SELECT
    customer_id
    ,txn_date
    ,SUM(amount_adj) OVER (
      PARTITION BY customer_id
      ORDER BY txn_date
      ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_balance
  FROM ordered_tx
),
month_end AS (
  SELECT
    customer_id
    ,DATE_TRUNC(txn_date, MONTH) AS month
    ,LAST_VALUE(running_balance) OVER (
      PARTITION BY customer_id, DATE_TRUNC(txn_date, MONTH)
      ORDER BY txn_date
      ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
    ) AS closing_balance
  FROM running
)
SELECT DISTINCT *
FROM month_end
ORDER BY customer_id, month
;
```

* Query results

<img width="1327" height="486" alt="image" src="https://github.com/user-attachments/assets/b74938db-ca88-44e3-8c21-10dffc817417" />

#### Query 05: Percentage of customers whose balance grew >5%

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:be1dea841bdc471dbd39514b577cbb3b)
* SQL code

```ruby
WITH ordered_tx AS (
  SELECT
    customer_id
    ,txn_date
    ,txn_type
    ,txn_amount
    ,CASE
      WHEN txn_type = 'deposit' THEN txn_amount
      ELSE -txn_amount
    END AS amount_adj
  FROM academic-arcade-452814-b8.Data_bank.customer_transactions
),
running AS (
  SELECT
    customer_id
    ,txn_date
    ,SUM(amount_adj) OVER (
      PARTITION BY customer_id
      ORDER BY txn_date
      ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_balance
  FROM ordered_tx
),
month_end AS (
  SELECT
    customer_id
    ,DATE_TRUNC(txn_date, MONTH) AS month
    ,LAST_VALUE(running_balance) OVER (
      PARTITION BY customer_id, DATE_TRUNC(txn_date, MONTH)
      ORDER BY txn_date
      ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
    ) AS closing_balance
  FROM running
),
mb AS (
  SELECT DISTINCT customer_id, month, closing_balance
  FROM month_end
),
growth AS (
  SELECT
    customer_id
    ,month
    ,closing_balance
    ,LAG(closing_balance) OVER (PARTITION BY customer_id ORDER BY month) AS prev_balance
  FROM mb
)
SELECT
  COUNTIF(closing_balance > prev_balance * 1.05) / COUNT(*) AS pct_increased
FROM growth
;
```

* Query results

<img width="1200" height="171" alt="image" src="https://github.com/user-attachments/assets/4724f89a-e5a5-4b64-9874-263017364f8c" />

### 🅒 Data Allocation Challenge (Options 1–3)

#### Query 01 (Op 1): Previous month closing balance

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:c1226121700343d4b64c32f16cb70c25)
* SQL code

```ruby
WITH tx AS (
  SELECT
    customer_id
    ,txn_date
    ,CASE WHEN txn_type = 'deposit' THEN txn_amount ELSE -txn_amount END AS adj
  FROM academic-arcade-452814-b8.Data_bank.customer_transactions
),
running AS (
  SELECT
    customer_id
    ,txn_date
    ,SUM(adj) OVER (
      PARTITION BY customer_id
      ORDER BY txn_date
      ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_balance
  FROM tx
)

SELECT
  customer_id
  ,DATE_TRUNC(txn_date, MONTH) AS month
  ,LAST_VALUE(running_balance) OVER (
    PARTITION BY customer_id, DATE_TRUNC(txn_date, MONTH)
    ORDER BY txn_date
    ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
  ) AS closing_balance
FROM running
;
```

* Query results

<img width="1200" height="478" alt="image" src="https://github.com/user-attachments/assets/ea8af0db-6c29-4303-b1e5-c5713d6e7e56" />

#### Query 02 (Op 2): 30-day average balance

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:06f652a6dbe94d0f90d852beeccd5cfe)
* SQL code

```ruby
WITH tx AS (
  SELECT
    customer_id
    ,txn_date
    ,CASE WHEN txn_type = 'deposit' THEN txn_amount ELSE -txn_amount END AS adj
  FROM academic-arcade-452814-b8.Data_bank.customer_transactions
),
running AS (
  SELECT
    customer_id
    ,txn_date
    ,SUM(adj) OVER (
      PARTITION BY customer_id
      ORDER BY txn_date
      ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_balance
  FROM tx
)

SELECT
  customer_id
  ,txn_date
  ,AVG(running_balance) OVER (
    PARTITION BY customer_id
    ORDER BY txn_date
    ROWS BETWEEN 30 PRECEDING AND CURRENT ROW
  ) AS avg_30d_balance
FROM running
;
```

* Query results

<img width="1200" height="510" alt="image" src="https://github.com/user-attachments/assets/d4a45551-62e0-4bae-8231-6a5adbdae1d6" />

#### Query 03 (Op 3): Real-time balance

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:80151ed089e948b283a7b48b801a27c7)
* SQL code

```ruby
WITH tx AS (
  SELECT
    customer_id
    ,txn_date
    ,CASE WHEN txn_type = 'deposit' THEN txn_amount ELSE -txn_amount END AS adj
  FROM academic-arcade-452814-b8.Data_bank.customer_transactions
),
running AS (
  SELECT
    customer_id
    ,txn_date
    ,SUM(adj) OVER (
      PARTITION BY customer_id
      ORDER BY txn_date
      ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_balance
  FROM tx
)

SELECT
  customer_id
  ,txn_date
  ,running_balance AS realtime_balance
FROM running
;
```

* Query results

<img width="1200" height="567" alt="image" src="https://github.com/user-attachments/assets/6853b68b-6902-44e6-8b44-72e37e5d7f75" />

### 🅓 Extra Challenge — Daily Interest Allocation

#### Query 01: Simple interest (no compounding)

Interest = balance * daily rate.

No compounding → simple proportional growth.

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:f4ead3ac4b344e3ebbb53d4d4d0c7694)
* SQL code

```ruby
WITH tx AS (
  SELECT
    customer_id
    ,txn_date
    ,CASE WHEN txn_type = 'deposit' THEN txn_amount ELSE -txn_amount END AS adj
  FROM academic-arcade-452814-b8.Data_bank.customer_transactions
),
running AS (
  SELECT
    customer_id
    ,txn_date
    ,SUM(adj) OVER (
      PARTITION BY customer_id
      ORDER BY txn_date
      ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_balance
  FROM tx
),

days AS (
  SELECT
    customer_id
    ,txn_date
    ,running_balance
    ,DATE(txn_date) AS day
  FROM running
),
daily_interest AS (
  SELECT
    customer_id
    ,day
    ,running_balance * (0.06 / 365) AS daily_interest
  FROM days
)

SELECT
  di.customer_id
  ,DATE_TRUNC(di.day, MONTH) AS month
  ,SUM(di.daily_interest) AS monthly_interest
FROM daily_interest AS di
GROUP BY di.customer_id, month
ORDER BY di.customer_id, month
;
```

* Query results

<img width="1200" height="544" alt="image" src="https://github.com/user-attachments/assets/db6585d4-a23f-4247-83e4-86cd6bbe4389" />

#### Query 02: How many unique nodes are there?

[Link to code](https://console.cloud.google.com/bigquery?sq=322729696559:1d9201f0837248d4b658f057b5df709c)
* SQL code

```ruby
WITH tx AS (
  SELECT
    customer_id
    ,txn_date
    ,CASE WHEN txn_type = 'deposit' THEN txn_amount ELSE -txn_amount END AS adj
  FROM academic-arcade-452814-b8.Data_bank.customer_transactions
),
running AS (
  SELECT
    customer_id
    ,txn_date
    ,SUM(adj) OVER (
      PARTITION BY customer_id
      ORDER BY txn_date
      ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_balance
  FROM tx
),

day_sequence AS (
  SELECT
    customer_id,
    txn_date,
    running_balance,
    ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY txn_date) AS day_num
  FROM running
),
compound AS (
  SELECT
    customer_id,
    txn_date,
    running_balance,
    POW(1 + 0.06/365, day_num) * running_balance - running_balance AS compounded_interest
  FROM day_sequence
)
SELECT
  customer_id,
  DATE_TRUNC(txn_date, MONTH) AS month,
  SUM(compounded_interest) AS monthly_compounded_interest
FROM compound
GROUP BY customer_id, month
;
```

* Query results

<img width="1200" height="570" alt="image" src="https://github.com/user-attachments/assets/62cf68b3-c233-4d83-8aab-67c185fa940a" />

## V. Conclusion

📌 Security & Node Management Insights (for investors)

* Data Bank reallocates customers frequently, reducing hacking attack windows.

* Median reallocation duration shows strong security rotation cycles.

* Nodes are globally distributed across 5 regions → enabling redundancy & resilience.

* Customer allocation is evenly distributed, preventing regional overload.

📌 Data Provisioning Summary (for executives)

| Option                                | Description         | Pros                                          | Cons                                 |
| ------------------------------------- | ------------------- | --------------------------------------------- | ------------------------------------ |
| **1. Previous Month Closing Balance** | Simple & stable     | Predictable provisioning                      | Slower to adjust to customer changes |
| **2. 30-Day Average Balance**         | Smoothed workload   | More accurate reflection of customer activity | Heavy calculation                    |
| **3. Real-Time Balance**              | Most accurate       | Real-time processing                          | Requires largest compute capacity    |
| **4. Daily-Interest Based**           | Incentivizes saving | Attractive to customers                       | Complex + costly                     |

📌 Recommendation

💡 Option 2 (30-day average) provides the best balance between accuracy and computational efficiency.

Option 3 is accurate but too costly; Option 1 is low accuracy; Option 4 is best for marketing but expensive.
