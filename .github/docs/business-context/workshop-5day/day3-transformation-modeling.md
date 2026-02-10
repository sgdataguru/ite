# Day 3: Transformation & Data Modeling

## 🎯 From Raw to Ready: Building Your Silver & Gold Layers

---

## Day Overview

| Attribute | Details |
|-----------|---------|
| **Day Theme** | Transforming messy data into analytics-ready assets |
| **Duration** | 9:00 AM – 5:00 PM |
| **Morning Focus** | dbt fundamentals, testing, data modeling patterns |
| **Afternoon Focus** | Build Silver and Gold layers for capstone |
| **End-of-Day Deliverable** | Complete Bronze → Silver → Gold transformations with tests |

---

## 📚 Learning Objectives

By the end of Day 3, you will be able to:

| # | Objective | Measurable Outcome |
|---|-----------|-------------------|
| 1 | **Write** dbt models with proper documentation | 3 documented dbt models |
| 2 | **Apply** data quality tests using dbt | Tests on every model |
| 3 | **Implement** star schema design patterns | Fact + dimension tables created |
| 4 | **Transform** Bronze data into Silver (cleaned) | Silver layer populated |
| 5 | **Aggregate** Silver into Gold (analytics-ready) | Gold tables with metrics |

---

## 🕐 Detailed Timetable

### Morning Session: Strategic Theory (9:00 AM – 12:30 PM)

---

#### 9:00 – 9:20 | Day 3 Opening (20 mins)

| Time | Activity | Facilitator Notes |
|------|----------|-------------------|
| 9:00 – 9:05 | **Arrival & Settle** | Bronze layer check: "Any overnight discoveries?" |
| 9:05 – 9:15 | **Day 2 Recap Quiz** | 5 questions on sources, contracts, error handling |
| 9:15 – 9:20 | **Day 3 Roadmap** | "Today we turn raw data into business value" |

**Energizer:** *"On a sticky note: What's the messiest data problem you've seen?"*

---

#### 9:20 – 10:00 | Block 1: The dbt Revolution

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 9:20 – 9:30 | **LECTURE (10 min)** | **Why dbt Changed Everything** |
| | | • The old way: Stored procedures, undocumented SQL |
| | | • dbt approach: Transforms as code, version controlled |
| | | • Key concepts: Models, sources, refs, materialization |
| | | • The dbt project structure |
| | | • Demo: A simple dbt model running |
| 9:30 – 9:50 | **ACTIVITY (20 min)** | **Your First dbt Models** |
| | | Each participant: |
| | | 1. Create a new dbt project (dbt init) |
| | | 2. Configure connection to Databricks |
| | | 3. Write a simple SELECT model |
| | | 4. Run dbt run, see the magic |
| | | Challenge: Who can run their first model fastest? |
| 9:50 – 10:00 | **DEBRIEF (10 min)** | Common errors, what just happened under the hood |

**dbt Project Structure:**
```
my_project/
├── dbt_project.yml      # Project configuration
├── profiles.yml         # Connection details (NOT in git!)
├── models/
│   ├── staging/        # Bronze → Silver
│   │   └── stg_orders.sql
│   ├── marts/          # Silver → Gold
│   │   └── fct_daily_sales.sql
│   └── schema.yml      # Documentation + tests
└── tests/              # Custom tests
```

**Key Takeaway:** *"dbt isn't just SQL—it's software engineering applied to data transformations."*

---

#### 10:00 – 10:15 | ☕ Morning Coffee Break (15 mins)

*Facilitator: Display "dbt Command Cheat Sheet" poster*

---

#### 10:15 – 10:55 | Block 2: Data Quality Testing

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 10:15 – 10:25 | **LECTURE (10 min)** | **Trust But Verify: Testing Your Data** |
| | | • Why tests matter: Garbage in, garbage out |
| | | • Built-in tests: unique, not_null, accepted_values, relationships |
| | | • Custom tests: Business logic validation |
| | | • When tests fail: Alerts, blocking, and quarantine |
| | | • The testing pyramid for data |
| 10:25 – 10:45 | **ACTIVITY (20 min)** | **Test Everything Challenge** |
| | | For one of your Bronze tables: |
| | | 1. Add not_null test to required fields |
| | | 2. Add unique test to primary key |
| | | 3. Add accepted_values test (e.g., status codes) |
| | | 4. Run dbt test - expect some failures! |
| | | 5. Investigate failures - is it bad data or bad test? |
| 10:45 – 10:55 | **DEBRIEF (10 min)** | Share interesting failures, discuss test strategy |

**dbt Test Examples:**
```yaml
# schema.yml
version: 2

models:
  - name: stg_orders
    description: Cleaned orders from Bronze layer
    columns:
      - name: order_id
        description: Unique identifier for order
        tests:
          - unique
          - not_null
      
      - name: order_status
        description: Current status of order
        tests:
          - not_null
          - accepted_values:
              values: ['pending', 'confirmed', 'shipped', 'delivered', 'cancelled']
      
      - name: customer_id
        tests:
          - relationships:
              to: ref('dim_customers')
              field: customer_id
```

**Key Takeaway:** *"Untested data is unreliable data. Every model needs at least one test."*

---

#### 10:55 – 11:35 | Block 3: Dimensional Modeling Essentials

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 10:55 – 11:05 | **LECTURE (10 min)** | **Star Schema: The Analytics Foundation** |
| | | • Fact tables: Events, transactions, measurements |
| | | • Dimension tables: Who, what, where, when, how |
| | | • Star vs Snowflake: When to normalize dimensions |
| | | • Surrogate keys: Why natural keys aren't enough |
| | | • SCD (Slowly Changing Dimensions): Type 1 vs Type 2 |
| 11:05 – 11:25 | **ACTIVITY (20 min)** | **Design Your Capstone Schema** |
| | | On whiteboard/paper, design star schema: |
| | | 1. Identify the central fact (what are we measuring?) |
| | | 2. List 4-5 dimensions (who/what/where/when) |
| | | 3. Define grain (one row = what?) |
| | | 4. Draw the star diagram |
| | | Table rotation: Each team reviews another's design |
| 11:25 – 11:35 | **DEBRIEF (10 min)** | Common modeling mistakes, facilitate fixes |

**Star Schema Example:**
```
                  ┌─────────────┐
                  │ dim_date    │
                  │─────────────│
                  │ date_key    │
                  │ date        │
                  │ month       │
                  │ quarter     │
                  │ year        │
                  └──────┬──────┘
                         │
┌─────────────┐    ┌─────┴─────┐    ┌─────────────┐
│ dim_customer│    │ fct_sales │    │ dim_product │
│─────────────│    │───────────│    │─────────────│
│ customer_key│◄───│ date_key  │───►│ product_key │
│ customer_id │    │ cust_key  │    │ product_id  │
│ name        │    │ prod_key  │    │ name        │
│ segment     │    │ quantity  │    │ category    │
│ region      │    │ revenue   │    │ unit_price  │
└─────────────┘    │ cost      │    └─────────────┘
                   └───────────┘
```

**Key Takeaway:** *"Good dimensional modeling makes complex queries simple. Get the grain right first."*

---

#### 11:35 – 12:15 | Block 4: Bronze → Silver → Gold Journey

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 11:35 – 11:45 | **LECTURE (10 min)** | **The Medallion Transformation Pattern** |
| | | • Silver transformations: Clean, dedupe, standardize, type cast |
| | | • Gold transformations: Aggregate, join, calculate metrics |
| | | • Incremental processing: Don't reprocess everything |
| | | • Idempotency: Same input always produces same output |
| | | • Data lineage: Track where everything came from |
| 11:45 – 12:05 | **ACTIVITY (20 min)** | **Transformation Mapping Exercise** |
| | | For your capstone, document: |
| | | | Bronze Table | Silver Transformations | Gold Aggregations | |
| | | Complete the transformation mapping worksheet |
| 12:05 – 12:15 | **DEBRIEF (10 min)** | Quick shares, clarify complex transformations |

**Transformation Mapping Worksheet:**

| Bronze Table | Transformation Type | Silver Output | Description |
|--------------|--------------------|--------------|-----------| 
| bronze.raw_orders | Deduplication | silver.orders | Remove duplicate order IDs |
| bronze.raw_orders | Type casting | silver.orders | Convert date strings to dates |
| bronze.raw_orders | Standardization | silver.orders | Uppercase status codes |
| bronze.raw_customers | NULL handling | silver.customers | Fill missing region with 'UNKNOWN' |

**Key Takeaway:** *"Each layer has a purpose. Bronze = raw truth. Silver = clean truth. Gold = business truth."*

---

#### 12:15 – 12:30 | Morning Wrap-Up (15 mins)

| Activity | Details |
|----------|---------|
| Architecture check | Point to diagram: "Where are we now?" |
| Afternoon preview | "We're building ALL the layers this afternoon" |
| Quick wins celebration | "Who ran their first dbt model successfully?" |

---

### 12:30 – 1:30 PM | 🍽️ Lunch Break (60 mins)

*Facilitator: Verify dbt projects are configured, prepare demo datasets*

---

### Afternoon Session: Practical Lab (1:30 PM – 5:00 PM)

---

#### 1:30 – 2:30 | Lab 1: Build Your Silver Layer (60 mins)

**Objective:** Transform all Bronze tables into Silver using dbt

| Time | Activity |
|------|----------|
| 1:30 – 1:40 | **Facilitator Demo:** Complex Silver transformation |
| 1:40 – 2:30 | **Team Build:** Create Silver models for capstone |

**Silver Layer Requirements:**

| Requirement | Example |
|-------------|---------|
| Naming | `stg_<source>__<entity>.sql` |
| Deduplication | Remove exact duplicates |
| Type casting | Strings → proper types |
| Null handling | Replace/flag nulls |
| Standardization | Consistent formats |
| Documentation | Column descriptions |

**Silver Model Template:**
```sql
-- models/staging/stg_api__orders.sql

{{
  config(
    materialized='incremental',
    unique_key='order_id'
  )
}}

WITH source AS (
    SELECT * FROM {{ source('bronze', 'raw_orders') }}
    {% if is_incremental() %}
    WHERE _ingested_at > (SELECT max(_ingested_at) FROM {{ this }})
    {% endif %}
),

deduplicated AS (
    SELECT *,
        ROW_NUMBER() OVER (
            PARTITION BY order_id 
            ORDER BY _ingested_at DESC
        ) AS row_num
    FROM source
),

cleaned AS (
    SELECT
        -- Primary key
        order_id,
        
        -- Type casting
        CAST(order_date AS DATE) AS order_date,
        CAST(quantity AS INT) AS quantity,
        CAST(unit_price AS DECIMAL(10,2)) AS unit_price,
        
        -- Standardization
        UPPER(TRIM(order_status)) AS order_status,
        
        -- Null handling
        COALESCE(shipping_region, 'UNKNOWN') AS shipping_region,
        
        -- Calculated fields
        quantity * unit_price AS line_total,
        
        -- Metadata
        _ingested_at,
        CURRENT_TIMESTAMP() AS _transformed_at
        
    FROM deduplicated
    WHERE row_num = 1  -- Keep latest version only
)

SELECT * FROM cleaned
```

**Checkpoint @ 2:30:** *"Show at least 2 Silver models running with dbt run"*

---

#### 2:30 – 2:45 | ☕ Afternoon Coffee Break (15 mins)

---

#### 2:45 – 3:30 | Lab 2: Testing & Documentation (45 mins)

**Objective:** Add comprehensive tests and documentation to Silver layer

| Time | Activity |
|------|----------|
| 2:45 – 2:55 | **Facilitator Demo:** Full schema.yml with tests |
| 2:55 – 3:30 | **Team Work:** Document and test your models |

**Minimum Test Coverage:**

| Model | Required Tests |
|-------|---------------|
| Every Silver model | Primary key: unique + not_null |
| All date fields | not_null, valid date range |
| Status/category fields | accepted_values |
| Foreign keys | relationships test |
| Custom business rule | At least 1 per model |

**Complete schema.yml Example:**
```yaml
version: 2

sources:
  - name: bronze
    description: Raw ingested data from various sources
    schema: bronze
    tables:
      - name: raw_orders
        description: Raw order data from API
        freshness:
          warn_after: {count: 24, period: hour}
          error_after: {count: 48, period: hour}

models:
  - name: stg_api__orders
    description: |
      Cleaned and standardized orders from the API source.
      Deduplicated on order_id, keeping most recent version.
    
    columns:
      - name: order_id
        description: Unique order identifier
        tests:
          - unique
          - not_null
      
      - name: order_date
        description: Date order was placed
        tests:
          - not_null
          - dbt_utils.expression_is_true:
              expression: ">= '2020-01-01'"
      
      - name: order_status
        tests:
          - accepted_values:
              values: ['PENDING', 'CONFIRMED', 'SHIPPED', 'DELIVERED', 'CANCELLED']
      
      - name: line_total
        description: Calculated field (quantity * unit_price)
        tests:
          - dbt_utils.expression_is_true:
              expression: ">= 0"
```

**Checkpoint @ 3:30:** *"Run dbt test - how many pass? How many fail?"*

Test Results Board:

| Team | Tests Passed | Tests Failed | Notes |
|------|-------------|--------------|-------|
| | | | |

---

#### 3:30 – 4:30 | Lab 3: Build Your Gold Layer (60 mins)

**Objective:** Create analytics-ready Gold tables with aggregations

| Time | Activity |
|------|----------|
| 3:30 – 3:40 | **Facilitator Demo:** Fact table with metrics |
| 3:40 – 4:30 | **Team Build:** Create fact + dimension tables |

**Gold Layer Requirements:**

| Requirement | Implementation |
|-------------|----------------|
| Fact table | At least 1 with 3+ metrics |
| Dimension tables | At least 2 dimensions |
| Joins | Dimensions properly joined to facts |
| Aggregations | Daily/weekly/monthly views |
| Business metrics | Calculated KPIs |

**Fact Table Template:**
```sql
-- models/marts/fct_daily_sales.sql

{{
  config(
    materialized='table',
    partition_by={'field': 'sales_date', 'granularity': 'month'}
  )
}}

WITH orders AS (
    SELECT * FROM {{ ref('stg_api__orders') }}
    WHERE order_status IN ('CONFIRMED', 'SHIPPED', 'DELIVERED')
),

customers AS (
    SELECT * FROM {{ ref('dim_customers') }}
),

products AS (
    SELECT * FROM {{ ref('dim_products') }}
)

SELECT
    -- Keys
    DATE_TRUNC('day', o.order_date) AS sales_date,
    c.customer_key,
    p.product_key,
    
    -- Metrics
    COUNT(DISTINCT o.order_id) AS order_count,
    SUM(o.quantity) AS total_quantity,
    SUM(o.line_total) AS gross_revenue,
    SUM(o.line_total * (1 - COALESCE(o.discount_pct, 0))) AS net_revenue,
    AVG(o.line_total) AS avg_order_value,
    
    -- Derived metrics
    SUM(o.quantity * p.unit_cost) AS total_cost,
    SUM(o.line_total) - SUM(o.quantity * p.unit_cost) AS gross_profit,
    
    -- Metadata
    CURRENT_TIMESTAMP() AS _processed_at

FROM orders o
LEFT JOIN customers c ON o.customer_id = c.customer_id
LEFT JOIN products p ON o.product_id = p.product_id
GROUP BY 1, 2, 3
```

**Dimension Table Template:**
```sql
-- models/marts/dim_customers.sql

{{
  config(
    materialized='table'
  )
}}

WITH customers AS (
    SELECT * FROM {{ ref('stg_internal__customers') }}
)

SELECT
    -- Surrogate key
    {{ dbt_utils.generate_surrogate_key(['customer_id']) }} AS customer_key,
    
    -- Natural key
    customer_id,
    
    -- Attributes
    customer_name,
    email,
    
    -- Demographics
    segment,
    region,
    country,
    
    -- Flags
    CASE 
        WHEN lifetime_value > 10000 THEN 'VIP'
        WHEN lifetime_value > 1000 THEN 'Premium'
        ELSE 'Standard'
    END AS customer_tier,
    
    -- Dates (for SCD tracking)
    created_date,
    CURRENT_TIMESTAMP() AS _valid_from

FROM customers
```

**Checkpoint @ 4:30:** *"Show dbt run for full DAG (Bronze → Silver → Gold)"*

---

#### 4:30 – 4:50 | Reflection & Teaching Bridge (20 mins)

**Teaching Adaptation Exercise:**

| Time | Activity |
|------|----------|
| 4:30 – 4:40 | **Solo Reflection:** Complete Day 3 Teaching Journal |
| 4:40 – 4:50 | **Group Discussion:** "How would you teach star schema to absolute beginners?" |

**Teaching Journal - Day 3:**

1. What analogy would you use to explain Bronze/Silver/Gold to students?
2. How would you simplify dbt for first-time users?
3. What's the minimum viable testing students should learn?

**Teaching Analogy Bank:**

| Concept | Suggested Analogy |
|---------|-------------------|
| Bronze layer | Raw ingredients delivered to kitchen |
| Silver layer | Ingredients washed, chopped, prepped |
| Gold layer | Finished dishes on serving platters |
| Fact table | Receipt showing what was bought |
| Dimension | Labels describing what/who/where |

---

#### 4:50 – 5:00 | Day 3 Closing (10 mins)

| Activity | Details |
|----------|---------|
| **DAG Showcase** | Display dbt lineage graph on screen |
| **Full Pipeline Demo** | Volunteer runs Bronze → Gold transformation |
| **Day 4 Preview** | "Tomorrow we orchestrate - automate everything!" |
| **Homework** | Add one custom dbt test, review documentation |

---

## 🛠️ Day 3 Toolkit

### Materials Distributed

| Item | Format |
|------|--------|
| dbt command cheat sheet | Laminated card |
| Star schema template | A3 paper |
| Testing pyramid poster | Wall display |
| Transformation mapping worksheet | A4 printout |

### Lab Resources

| Resource | Location |
|----------|----------|
| dbt starter project | `/workshop/day3/dbt_starter/` |
| Sample schema.yml | `/workshop/day3/templates/` |
| Model templates | `/workshop/day3/templates/` |
| dbt packages (pre-installed) | dbt_utils, dbt_expectations |

---

## 👨‍🏫 Facilitator Guide - Day 3

### Critical Moments

| Time | Watch For | Intervention |
|------|-----------|--------------|
| 9:45 | dbt init failures | Have pre-configured projects ready |
| 10:30 | Test overwhelm | Focus on 3 core tests only |
| 2:00 | Silver model errors | Provide working example to debug against |
| 4:00 | Gold layer confusion | Draw grain discussion on whiteboard |

### Common Day 3 Issues

| Issue | Solution |
|-------|----------|
| dbt connection failures | Verify profile.yml configuration |
| Model compile errors | Check ref() syntax, model naming |
| Tests failing unexpectedly | Often reveals real data issues - celebrate! |
| Confusion about incremental | Default to table materialization first |

### End-of-Day Success Criteria

- [ ] Every team has at least 2 Silver models
- [ ] Every team has at least 1 Gold table
- [ ] All models have basic tests
- [ ] dbt run --full-refresh works for full pipeline
- [ ] Lineage graph shows complete DAG

---

## 📊 Day 3 Architecture Progress

```
DAY 1: [Environment] ✓
         ↓
DAY 2: [Bronze Layer] ✓
         ↓
DAY 3: [Silver Layer] ✓ → [Gold Layer] ✓  ← YOU ARE HERE
         ↓
DAY 4: [Orchestration]
         ↓
DAY 5: [Production]
```

---

*Day 3 Complete | Next: Day 4 - Orchestration & Monitoring →*
