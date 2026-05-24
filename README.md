# Database Transition & Business Optimization Dashboard | Power BI

## Dashboard Link :
https://app.powerbi.com/view?r=eyJrIjoiODcxZWU1NDYtZTRlOS00ODU1LWFkZmItZDk4ZjIxNjAxODllIiwidCI6IjA2Y2Q0ZWQ1LTNiN2YtNDdiMC04ZWY2LTI5ZGVlMWM1MDYwYiJ9&embedImagePlaceholder=true&pageName=369007a6b71205be20d4

## Dashboard Preview :
![d1](https://github.com/user-attachments/assets/d75c166c-5717-424a-ade1-2877e3d215e9)

![d2](https://github.com/user-attachments/assets/511e3f11-3f0c-46e9-b63e-f8d01352613a)


## Problem Statement : 

This project demonstrates a real-world database transition workflow involving:

- SQL Server
- MySQL
- Power BI

The objective of the project is to showcase how Power BI reports can be seamlessly migrated:

 - From Test Environment → Production Environment
 - From SQL Server → MySQL

without rebuilding the dashboard from scratch.

The dashboard also provides business optimization insights related to:

- Demand
- Availability
- Supply Shortage
- Profit & Loss Analysis

This project simulates enterprise-level scenarios where organizations migrate reporting systems across different database technologies and environments.

## Data Source & Database Integration

The project uses:

- Microsoft SQL Server
- MySQL
- Power BI Desktop
- Power BI Service

### Dataset Structure :
**Inventory Dataset :**
- Order Date (DD/MM/YYYY)
- Product ID
- Availability
- Demand

**Products Dataset :**
- Product ID
- Product Name
- Unit Price ($)

## SQL Server Data Preparation

Initially, both datasets were imported into SQL Server.

1. Left Join operation using Product ID
Created a combined table:
new_table

2. This table was then imported into Power BI for reporting and analysis.

    ```
    select * into new_table from 
    (select a.[Order_Date_DD_MM_YYYY],
    a.product_id,a.availability,a.demand,b.product_name,b.unit_price

    from [dbo].[Test Environment Inventory Dataset] as a
    left join products as b on a.product_id=b.product_id) x
    ```

![sqlstudio](https://github.com/user-attachments/assets/6af215ed-f47d-4f30-94e0-02f62fcf0e58)

## Power BI Report Migration Workflow :

1. Test Environment → Production Environment

The project demonstrates how Power BI reports can be migrated between:

Test Environment (test_env) to 
Production Environment (prod_env)

using:

Power BI → Transform Data → Data Source Settings → Change Source

![ds](https://github.com/user-attachments/assets/db16b6bd-c7d9-4f21-92d8-90c2ef9ed6e0)

2. **Migration Validation Steps :**

Before transitioning environments:

- Verified no blank or null values
- Executed SQL validation commands
- Ensured data consistency before production deployment
- SQL Server → MySQL Transition

A major objective of the project was transitioning Power BI reports from:

SQL Server → MySQL

without recreating visuals or reports.

3. **MySQL Setup Process:**

MySQL Configuration:
- Created MySQL database using MySQL Workbench
- Imported inventory datasets using:
- Table Data Import Wizard

Data Validation

Executed queries to validate imported data:
```
SELECT * FROM prod.`prod env inventory dataset`;

```
![mysql](https://github.com/user-attachments/assets/c66f9dfa-07f6-4a07-ad98-1b23d1f4d90b)

4. **MySQL Data Transformation :**

Performed update operations:
```
update prod.`prod env inventory dataset`
set `Product ID` = 7 where `Product ID` =21;
update prod.`prod env inventory dataset`
set `Product ID` = 11 where `Product ID` =22;
```

5. **Safe Update Mode Handling :**

Encountered MySQL safe update restriction:

Error Code: 1175

Resolved by:

Edit → Preferences → SQL Editor → Disable Safe Updates

Then reconnected MySQL Workbench and executed update queries successfully.

6. **Power BI Source Transition Using Advanced Editor :**

Unlike SQL environment switching, transitioning from SQL Server to MySQL required:

Power Query → Advanced Editor

MySQL Source Used :

    Source = MySQL.Database(
    "localhost",
    "prod",
    [
        ReturnSingleDatabase=true,
        Query="select * from new_table"
    ]
    )

This source was copied and replaced inside the previous SQL query source in Power Query Advanced Editor.

![advance](https://github.com/user-attachments/assets/d4b28a5b-15e2-4239-8200-21347f965220)

## DAX Measures Used : 

**Availability & Demand Metrics :**

    Average Availability Per Day = 
    DIVIDE([Total Availability],[Total Number of Days])

**Average Demand Per Day :** = 

    DIVIDE([Total Demand],[Total Number of Days])

**Loss Metrics :**

    Average Loss Per Day = 
    DIVIDE([Total Loss],[Total Number of Days])

    Total Loss =
    SUMX(
    FILTER(
        'Demand/Availability Data',
        'Demand/Availability Data'[LOSS/PROFIT] < 0
    ),
    'Demand/Availability Data'[LOSS/PROFIT] *
    'Demand/Availability Data'[unit_price]
    ) * -1

**Profit Metrics :**

    Total Profit =
    SUMX(
    FILTER(
        'Demand/Availability Data',
        'Demand/Availability Data'[LOSS/PROFIT] > 0
    ),
    'Demand/Availability Data'[LOSS/PROFIT] *
    'Demand/Availability Data'[unit_price]
    )

**Supply Shortage :**

    Total Supply Shortage =
    [Total Demand] - [Total Availability]

## Dashboard Design & UI Enhancements :

**Implemented advanced dashboard customization techniques :**

- Transparent KPI Cards
- Neon-themed business dashboard design
- Custom filter pane formatting
- Background image integration using:
- Canvas Background → Transparency = 0

**Interactive Features :**
- Collapsible filter pane
- Dynamic KPI cards
- Environment-based report transition
- SQL to MySQL source migration
- Transparent visual layering
- Advanced card formatting

## Dashboard Features :

The dashboard provides:

- Average Demand Analysis
- Availability Tracking
- Supply Shortage Monitoring
- Profit & Loss Visualization
- Daily Loss Metrics
- Environment transition workflow demonstration

## Key Insights :

**Demand vs Availability :**

- Demand significantly exceeds availability in several scenarios, leading to noticeable supply shortages.
Average daily demand remains higher than average daily availability.

**Profit & Loss Analysis :**

- Profit-generating transactions contribute significantly to business optimization.
Loss analysis helps identify operational inefficiencies and inventory gaps.

**Supply Chain Insights :**
- Supply shortages directly impact profitability and business continuity.
Better inventory planning can reduce loss and improve operational efficiency.

**Database Transition Insights :**
- Power BI reports can be successfully migrated across:
Different environments
Different database technologies
without rebuilding reports.

- Advanced Editor in Power Query plays a critical role in SQL-to-MySQL migration workflows.

## Tools & Technologies Used :
- Power BI Desktop
- Power BI Service
- SQL Server
- MySQL Workbench
- Power Query
- DAX
- SQL
- Data Modeling & Visualization

## Conclusion :

This project demonstrates an enterprise-level reporting migration workflow involving:

- SQL Server environment transitions
- SQL-to-MySQL migration
- Power BI source reconfiguration
- Business optimization analytics

The dashboard combines:

- Database transition concepts
- Business KPI monitoring
- Advanced Power BI customization
- Real-world reporting workflows
  to simulate practical enterprise BI migration scenarios.
