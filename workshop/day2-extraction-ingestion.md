# Day 2: Data Extraction & Ingestion

## 🎯 Mastering Multi-Source Data Ingestion

---

## Day Overview

| Attribute | Details |
|-----------|---------|
| **Day Theme** | Getting data from anywhere, reliably |
| **Duration** | 9:00 AM – 5:00 PM |
| **Morning Focus** | Data sources, APIs, batch vs streaming, data contracts |
| **Afternoon Focus** | Build multi-source ingestion for capstone project |
| **End-of-Day Deliverable** | Bronze layer with data from 3 different sources |

---

## 📚 Learning Objectives

By the end of Day 2, you will be able to:

| # | Objective | Measurable Outcome |
|---|-----------|-------------------|
| 1 | **Connect** to various data sources (files, APIs, databases) | Successfully pull from 3 source types |
| 2 | **Handle** common extraction failures (timeouts, auth, rate limits) | Pipeline recovers from simulated failure |
| 3 | **Implement** incremental extraction patterns | Only new/changed records extracted |
| 4 | **Define** data contracts between source and pipeline | Contract document for each source |
| 5 | **Populate** Bronze layer tables with raw source data | 3 Bronze tables with data |

---

## 🕐 Detailed Timetable

### Morning Session: Strategic Theory (9:00 AM – 12:30 PM)

---

#### 9:00 – 9:20 | Day 2 Opening (20 mins)

| Time | Activity | Facilitator Notes |
|------|----------|-------------------|
| 9:00 – 9:05 | **Arrival & Settle** | Quick environment check: "Who had issues overnight?" |
| 9:05 – 9:15 | **Day 1 Recap Quiz** | 5 quick questions on architecture, ETL vs ELT |
| 9:15 – 9:20 | **Day 2 Roadmap** | "Today is about the 'E' in ELT – getting data in" |

**Energizer:** *"Share with your neighbor: What's the weirdest data source you've encountered?"*

---

#### 9:20 – 10:00 | Block 1: The World of Data Sources

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 9:20 – 9:30 | **LECTURE (10 min)** | **Taxonomy of Data Sources** |
| | | • Files: CSV, JSON, Parquet, Excel (the good, bad, ugly) |
| | | • APIs: REST, GraphQL, Webhooks |
| | | • Databases: JDBC/ODBC, CDC (Change Data Capture) |
| | | • Streams: Kafka, Event Hubs, real-time feeds |
| | | • SaaS: Salesforce, HubSpot, custom connectors |
| 9:30 – 9:50 | **ACTIVITY (20 min)** | **Source Classification Challenge** |
| | | 12 data source cards laid out on tables |
| | | Teams categorize: Which extraction method? What challenges? |
| | | Sources: "HDB resale API", "Student attendance CSV", "IoT MQTT stream", etc. |
| | | Speed competition: First team with all correct wins |
| 9:50 – 10:00 | **DEBRIEF (10 min)** | Reveal answers, discuss tricky ones, common Singapore sources |

**Key Takeaway:** *"The source dictates the extraction pattern. Know your source, know your approach."*

---

#### 10:00 – 10:15 | ☕ Morning Coffee Break (15 mins)

*Facilitator: Display poster "5 Extraction Patterns at a Glance"*

---

#### 10:15 – 10:55 | Block 2: API Extraction Mastery

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 10:15 – 10:25 | **LECTURE (10 min)** | **REST API Extraction: The Complete Picture** |
| | | • Authentication: API keys, OAuth, tokens (when they expire!) |
| | | • Pagination: Offset, cursor, link-based |
| | | • Rate limiting: What happens when you hit the wall? |
| | | • Error handling: 4xx vs 5xx, retry strategies |
| | | • Demo: Extracting from data.gov.sg API |
| 10:25 – 10:45 | **ACTIVITY (20 min)** | **API Extraction Exercise** |
| | | Using Postman/curl, extract from provided demo API: |
| | | 1. Get your API key |
| | | 2. Fetch first page of results |
| | | 3. Handle pagination (get all pages) |
| | | 4. Deliberately trigger rate limit, observe behavior |
| | | 5. Write extracted data to file |
| 10:45 – 10:55 | **DEBRIEF (10 min)** | What surprised you? Common pitfalls shared |

**Key Takeaway:** *"APIs are conversations. Be polite (rate limits), patient (pagination), and persistent (retries)."*

---

#### 10:55 – 11:35 | Block 3: Batch vs Streaming – When to Use What

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 10:55 – 11:05 | **LECTURE (10 min)** | **The Latency-Complexity Trade-off** |
| | | • Batch: Scheduled, predictable, easier to debug |
| | | • Micro-batch: Best of both (Spark Structured Streaming) |
| | | • Real-time: Event-driven, complex, expensive |
| | | • Decision framework: When does "fresh" matter? |
| | | • Singapore examples: MRT real-time vs HDB quarterly reports |
| 11:05 – 11:25 | **ACTIVITY (20 min)** | **Latency Requirement Mapping** |
| | | For your capstone project: |
| | | List each data source. For each, answer: |
| | | • How fresh must data be? (real-time / hourly / daily / weekly) |
| | | • What's the cost of stale data? |
| | | • Batch or stream? Justify. |
| | | Pair review with another team |
| 11:25 – 11:35 | **DEBRIEF (10 min)** | Most projects are batch – and that's okay! Overengineering warning |

**Key Takeaway:** *"Real-time sounds sexy, but batch pays the bills. Match latency to business need, not technical ambition."*

---

#### 11:35 – 12:15 | Block 4: Data Contracts & Source Documentation

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 11:35 – 11:45 | **LECTURE (10 min)** | **The Contract That Saves Your Pipeline** |
| | | • What is a data contract? Agreement between producer and consumer |
| | | • Key elements: Schema, freshness SLA, quality expectations |
| | | • Why contracts fail: Undocumented changes, assumptions |
| | | • Schema evolution: What happens when source adds a column? |
| | | • Real story: The "surprise NULL" that broke production |
| 11:45 – 12:05 | **ACTIVITY (20 min)** | **Write Your Data Contracts** |
| | | For each of your 3 capstone data sources, complete: |
| | | **Data Contract Template** (see below) |
| | | Include: Schema, update frequency, owner contact, known issues |
| 12:05 – 12:15 | **DEBRIEF (10 min)** | Share one contract, discuss what's often missing |

**Data Contract Template:**

| Field | Your Response |
|-------|---------------|
| Source Name | |
| Owner/Contact | |
| Update Frequency | |
| Expected Record Count | |
| Schema (columns + types) | |
| Nullable Fields | |
| Primary Key | |
| Known Data Quality Issues | |
| SLA (freshness guarantee) | |
| Access Method | |
| Authentication | |

**Key Takeaway:** *"A data contract isn't bureaucracy—it's the first line of defense against 3 AM pages."*

---

#### 12:15 – 12:30 | Morning Wrap-Up (15 mins)

| Activity | Details |
|----------|---------|
| Concept check | Quick poll: "Which source type are you most nervous about?" |
| Afternoon preview | "We're building your actual Bronze layer this afternoon" |
| Questions parking lot | Capture complex questions for later |

---

### 12:30 – 1:30 PM | 🍽️ Lunch Break (60 mins)

*Facilitator: Set up API endpoint access, verify database connections*

---

### Afternoon Session: Practical Lab (1:30 PM – 5:00 PM)

---

#### 1:30 – 2:30 | Lab 1: Multi-Source Extraction Workshop (60 mins)

**Objective:** Extract data from 3 different source types

| Station | Source Type | Task |
|---------|-------------|------|
| **Station A** | CSV/File | Extract student records CSV with error handling |
| **Station B** | REST API | Pull from demo API with pagination |
| **Station C** | Database | Query PostgreSQL demo database |

**Rotation Schedule (20 mins each station):**

| Time | Team 1-4 | Team 5-8 | Team 9-12 |
|------|----------|----------|-----------|
| 1:30-1:50 | Station A | Station B | Station C |
| 1:50-2:10 | Station B | Station C | Station A |
| 2:10-2:30 | Station C | Station A | Station B |

**Station A: File Extraction**
```python
# Handle messy CSV with issues
df = spark.read.format("csv") \
    .option("header", "true") \
    .option("mode", "PERMISSIVE")  # Handle malformed rows \
    .option("columnNameOfCorruptRecord", "_corrupt") \
    .load("/path/to/messy_file.csv")

# Log quality issues
bad_records = df.filter(df._corrupt.isNotNull())
print(f"Found {bad_records.count()} malformed records")
```

**Station B: API Extraction**
```python
import requests

def extract_paginated_api(base_url, api_key):
    all_records = []
    page = 1
    
    while True:
        response = requests.get(
            f"{base_url}?page={page}",
            headers={"Authorization": f"Bearer {api_key}"},
            timeout=30
        )
        
        if response.status_code == 429:  # Rate limited
            time.sleep(60)
            continue
            
        data = response.json()
        all_records.extend(data["results"])
        
        if not data.get("next_page"):
            break
        page += 1
    
    return all_records
```

**Station C: Database Extraction**
```python
# JDBC connection to PostgreSQL
jdbc_url = "jdbc:postgresql://host:5432/demo_db"

df = spark.read.format("jdbc") \
    .option("url", jdbc_url) \
    .option("dbtable", "public.transactions") \
    .option("user", "readonly_user") \
    .option("password", dbutils.secrets.get("scope", "pg_password")) \
    .load()
```

**Checkpoint @ 2:30:** *"Show data from all 3 sources in your notebook"*

---

#### 2:30 – 2:45 | ☕ Afternoon Coffee Break (15 mins)

---

#### 2:45 – 3:45 | Lab 2: Build Your Bronze Layer (60 mins)

**Objective:** Create Bronze tables for your capstone project

| Phase | Task | Time |
|-------|------|------|
| 2:45-2:55 | **Facilitator Demo:** Bronze table creation patterns | 10 min |
| 2:55-3:45 | **Team Build:** Create 3 Bronze tables for capstone | 50 min |

**Bronze Table Requirements:**

| Requirement | Implementation |
|-------------|----------------|
| Naming convention | `bronze.<source>_<entity>` (e.g., `bronze.api_orders`) |
| Metadata columns | `_ingested_at`, `_source_file`, `_batch_id` |
| Partitioning | By ingestion date for large tables |
| Format | Delta Lake (for time travel) |

**Bronze Table Template:**
```python
from pyspark.sql.functions import current_timestamp, lit, input_file_name

# Add metadata columns
df_bronze = df \
    .withColumn("_ingested_at", current_timestamp()) \
    .withColumn("_source_file", input_file_name()) \
    .withColumn("_batch_id", lit("batch_001"))

# Write as Delta table  
df_bronze.write \
    .format("delta") \
    .mode("append") \
    .partitionBy("_ingested_date") \
    .saveAsTable("bronze.raw_orders")
```

**Team Checkpoint @ 3:45:** *"Show 3 Bronze tables with record counts"*

| Team | Source 1 | Count | Source 2 | Count | Source 3 | Count |
|------|----------|-------|----------|-------|----------|-------|
| Team A | | | | | | |
| Team B | | | | | | |
| ... | | | | | | |

---

#### 3:45 – 4:30 | Lab 3: Error Handling & Recovery (45 mins)

**Objective:** Make extraction resilient to failures

| Time | Activity |
|------|----------|
| 3:45 – 3:55 | **Facilitator Demo:** Injecting and handling failures |
| 3:55 – 4:30 | **Chaos Engineering:** Break your pipeline, then fix it |

**Failure Scenarios to Implement:**

| Scenario | Failure Type | Your Solution |
|----------|--------------|---------------|
| **A** | API returns 500 error | Implement retry with exponential backoff |
| **B** | Source file is corrupted | Log bad records, continue with good ones |
| **C** | Database connection timeout | Connection pooling, reconnection logic |
| **D** | Source schema changed | Schema evolution handling |

**Error Handling Pattern:**
```python
from tenacity import retry, stop_after_attempt, wait_exponential

@retry(
    stop=stop_after_attempt(3),
    wait=wait_exponential(multiplier=1, min=4, max=60)
)
def extract_with_retry(url):
    response = requests.get(url, timeout=30)
    response.raise_for_status()
    return response.json()

# Usage
try:
    data = extract_with_retry(api_url)
except Exception as e:
    log.error(f"Extraction failed after 3 retries: {e}")
    send_alert("Extraction failure", str(e))
    raise
```

**Checkpoint @ 4:30:** *"Demonstrate your pipeline recovering from a simulated failure"*

---

#### 4:30 – 4:50 | Reflection & Teaching Bridge (20 mins)

**Teaching Adaptation Exercise:**

| Time | Activity |
|------|----------|
| 4:30 – 4:40 | **Solo Reflection:** Complete Day 2 of Teaching Journal |
| 4:40 – 4:50 | **Group Discussion:** "What extraction challenges would ITE students face?" |

**Teaching Journal - Day 2:**

1. Which source type would you start students with? Why?
2. How would you explain API rate limiting without losing them?
3. What simplified exercise could demonstrate error handling?

---

#### 4:50 – 5:00 | Day 2 Closing (10 mins)

| Activity | Details |
|----------|---------|
| **Bronze Layer Showcase** | Quick demo: 2 teams show their Bronze layer |
| **Confidence Check** | Sticky note: 1-10, post on Day 2 column |
| **Day 3 Preview** | "Tomorrow we transform this raw data into something useful" |
| **Homework** | Document any remaining data quality issues discovered |

---

## 🛠️ Day 2 Toolkit

### Materials Distributed

| Item | Format |
|------|--------|
| Source classification cards | Laminated cards |
| Data contract template | A4 printout |
| API extraction cheat sheet | PDF |
| Error handling patterns reference | PDF |

### Lab Resources

| Resource | Details |
|----------|---------|
| Demo API endpoint | `https://api.demo.ite-training.sg/v1/` |
| API key | Provided in workshop materials |
| PostgreSQL demo DB | Connection string in setup guide |
| Sample files (messy) | 3 CSV files with intentional issues |

---

## 👨‍🏫 Facilitator Guide - Day 2

### Critical Moments

| Time | Watch For | Intervention |
|------|-----------|--------------|
| 10:30 | API frustration | Provide working Postman collection |
| 2:00 | Station rotation chaos | Clear timing signals, visible timer |
| 3:30 | Teams with empty Bronze | Pair struggling teams with strong ones |
| 4:00 | Chaos engineering too chaotic | Provide "easy mode" failures first |

### Common Day 2 Issues

| Issue | Solution |
|-------|----------|
| API key not working | Pre-generated backup keys ready |
| Database connection refused | Whitelist all ITE campus IPs |
| Confusion about Bronze requirements | Show completed example |
| Error handling too advanced | Focus on try-except, skip retry decorators |

### End-of-Day Success Criteria

- [ ] 100% have data from at least 2 sources
- [ ] 80% have all 3 Bronze tables populated
- [ ] Every team has data contracts documented
- [ ] At least one error handling pattern implemented

---

*Day 2 Complete | Next: Day 3 - Transformation & Data Modeling →*
