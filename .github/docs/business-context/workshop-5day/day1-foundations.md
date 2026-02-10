# Day 1: Foundations & Environment Setup

## 🎯 Building the Foundation for Production Pipelines

---

## Day Overview

| Attribute | Details |
|-----------|---------|
| **Day Theme** | Understanding WHY before HOW |
| **Duration** | 9:00 AM – 5:00 PM |
| **Morning Focus** | Pipeline concepts, architecture patterns, Singapore data landscape |
| **Afternoon Focus** | Environment setup, first extraction, team formation |
| **End-of-Day Deliverable** | Working dev environment + extracted sample dataset |

---

## 📚 Learning Objectives

By the end of Day 1, you will be able to:

| # | Objective | Measurable Outcome |
|---|-----------|-------------------|
| 1 | **Articulate** the business value of data pipelines in Singapore enterprises | Explain to a colleague in 60 seconds |
| 2 | **Differentiate** ETL vs ELT and when to use each approach | Correctly classify 5 scenarios |
| 3 | **Diagram** a Medallion Architecture (Bronze→Silver→Gold) | Complete architecture sketch |
| 4 | **Configure** a complete local development environment | All validation checks pass |
| 5 | **Execute** a basic data extraction from file source | Data visible in Databricks |

---

## 🕐 Detailed Timetable

### Morning Session: Strategic Theory (9:00 AM – 12:30 PM)

---

#### 9:00 – 9:30 | Opening & Program Kickoff (30 mins)

| Time | Activity | Facilitator Notes |
|------|----------|-------------------|
| 9:00 – 9:10 | **Arrival & Networking** | Name tags, coffee, background music |
| 9:10 – 9:20 | **Welcome & Introductions** | Facilitator intro, ITE coordinator welcome |
| 9:20 – 9:25 | **Housekeeping** | Wifi, facilities, phones, safety |
| 9:25 – 9:30 | **Week Overview** | Walk through 5-day journey map on wall poster |

**Icebreaker Activity (during introductions):**
*"Share your name, department, and complete this sentence: 'The messiest data I've ever seen was...'"*

**Confidence Baseline:**
*"On a scale of 1-10, how confident are you building a data pipeline from scratch? Write on sticky note and post on the Day 1 column."*

---

#### 9:30 – 10:10 | Block 1: Why Data Pipelines Matter

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 9:30 – 9:40 | **LECTURE (10 min)** | **The Singapore Data Landscape** |
| | | • 78% of SG enterprises investing in data infrastructure |
| | | • Skills gap: 8,000 unfilled data roles in Singapore |
| | | • ITE's role: Producing industry-ready graduates |
| | | • Real story: How Grab processes 1B+ events daily |
| 9:40 – 10:00 | **ACTIVITY (20 min)** | **Data Flow Mapping** |
| | | Groups of 3: Pick an organization (Grab, DBS, NTUC) |
| | | Map: What data comes IN? What decisions come OUT? |
| | | Identify 3 potential pipeline use cases |
| | | Each group presents in 90 seconds |
| 10:00 – 10:10 | **DEBRIEF (10 min)** | Synthesize patterns, connect to Higher Nitec curriculum relevance |

**Key Takeaway:** *"Every digital decision in Singapore is powered by a data pipeline. Your students will build these."*

---

#### 10:10 – 10:25 | ☕ Morning Coffee Break (15 mins)

*Facilitator: Display "Journey Map" poster showing 5-day progression*

---

#### 10:25 – 11:05 | Block 2: ETL vs ELT – The Modern Shift

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 10:25 – 10:35 | **LECTURE (10 min)** | **The Evolution: Extract-Transform-Load to Extract-Load-Transform** |
| | | • ETL: Transform before loading (traditional, on-prem era) |
| | | • ELT: Load first, transform in warehouse (cloud era) |
| | | • Why the shift: Storage is cheap, compute is powerful, schemas change |
| | | • When ETL still wins: Compliance, data minimization, edge cases |
| 10:35 – 10:55 | **ACTIVITY (20 min)** | **ETL or ELT? Decision Exercise** |
| | | 8 scenario cards distributed to pairs |
| | | Classify each: ETL or ELT? Justify your choice. |
| | | Scenarios: "Bank transaction data", "IoT sensors", "HR records", etc. |
| | | Vote with cards, facilitator reveals correct answers |
| 10:55 – 11:05 | **DEBRIEF (10 min)** | Discuss edge cases, no "always right" answer, context matters |

**Key Takeaway:** *"ELT is winning because we'd rather have the raw data and transform later than realize we threw away something important."*

---

#### 11:05 – 11:45 | Block 3: The Medallion Architecture

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 11:05 – 11:15 | **LECTURE (10 min)** | **Bronze → Silver → Gold: The Data Lake Pattern** |
| | | • Bronze: Raw, immutable, source of truth |
| | | • Silver: Cleaned, conformed, validated |
| | | • Gold: Business-ready, aggregated, modeled |
| | | • Why layers: Reproducibility, debugging, performance |
| | | • Example: Netflix's data platform architecture |
| 11:15 – 11:35 | **ACTIVITY (20 min)** | **Design Your Architecture** |
| | | Using the capstone project scenario you chose: |
| | | Sketch the 3-layer architecture on the template |
| | | Label: What data in each layer? What transformations between? |
| | | Peer review: Exchange with neighbor, give feedback |
| 11:35 – 11:45 | **DEBRIEF (10 min)** | Gallery walk of 3 architectures, highlight best practices |

**Key Takeaway:** *"Bronze is your insurance policy. When something goes wrong downstream, you can always replay from raw."*

---

#### 11:45 – 12:25 | Block 4: The Tool Landscape

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 11:45 – 11:55 | **LECTURE (10 min)** | **Modern Data Stack: What's Hot in 2026** |
| | | • Orchestration: Airflow vs Azure Data Factory vs Prefect |
| | | • Transformation: dbt (data build tool) revolution |
| | | • Compute: Spark vs SQL engines |
| | | • Storage: Data lakes vs warehouses vs lakehouses |
| | | • The tools we'll use this week and why |
| 11:55 – 12:15 | **ACTIVITY (20 min)** | **Tool Selection Exercise** |
| | | Given 3 different company scenarios (startup, enterprise, government) |
| | | Select appropriate tools from a menu, justify budget vs capability |
| | | Compare choices with another group |
| 12:15 – 12:25 | **DEBRIEF (10 min)** | No perfect stack, trade-offs everywhere, what matters for ITE context |

**Key Takeaway:** *"Tools change every 2 years. Concepts last a career. We'll teach you patterns that transfer."*

---

#### 12:25 – 12:30 | Morning Wrap-Up (5 mins)

- Quick 5-question Kahoot quiz on morning concepts
- Preview afternoon: "We're going to get our hands dirty now"

---

### 12:30 – 1:30 PM | 🍽️ Lunch Break (60 mins)

*Facilitator: Ensure all environment setup materials are ready, test demo*

---

### Afternoon Session: Practical Lab (1:30 PM – 5:00 PM)

---

#### 1:30 – 2:30 | Lab 1: Environment Setup (60 mins)

**Objective:** Every participant has a fully working development environment

| Time | Activity |
|------|----------|
| 1:30 – 1:40 | **Facilitator Demo:** Walk through complete environment |
| 1:40 – 2:20 | **Hands-On Setup:** Participants follow setup guide |
| 2:20 – 2:30 | **Troubleshooting Round:** Raise hand if stuck, peer help |

**Environment Checklist:**

| # | Component | Validation Test | ✓ |
|---|-----------|-----------------|---|
| 1 | Databricks Community | Login successful, can create notebook | |
| 2 | Docker Desktop | `docker run hello-world` works | |
| 3 | VS Code + Extensions | Python, Docker, YAML extensions installed | |
| 4 | Git | `git --version` returns 2.x | |
| 5 | Python 3.9+ | `python --version` returns 3.9+ | |
| 6 | Workshop Repo Cloned | Can see files in VS Code | |
| 7 | Airflow Container | `localhost:8080` shows Airflow UI | |

**Troubleshooting Stations:**
- Station A: Databricks issues
- Station B: Docker issues
- Station C: VS Code/Git issues

**Checkpoint @ 2:30:** *"Raise green card if all 7 checks pass. Red card if stuck."*

---

#### 2:30 – 2:45 | ☕ Afternoon Coffee Break (15 mins)

*Facilitator: Quick survey of who's stuck, prioritize support*

---

#### 2:45 – 3:45 | Lab 2: Your First Data Extraction (60 mins)

**Objective:** Extract sample data to Databricks

| Time | Activity |
|------|----------|
| 2:45 – 3:00 | **Facilitator Demo:** Live coding extraction |
| 3:00 – 3:45 | **Hands-On Build:** Participants extract their chosen dataset |

**Extraction Exercise:**

```
Task: Extract the provided sample CSV to Databricks

Steps:
1. Upload sample_data.csv to Databricks DBFS
2. Create a notebook called "day1_extraction"
3. Read the CSV into a Spark DataFrame
4. Display first 10 rows
5. Count total records
6. Write to Bronze table: bronze.raw_sample
```

**Starter Code Provided:**
```python
# Day 1: First Extraction
from pyspark.sql import SparkSession

# Read source file
df = spark.read.format("csv") \
    .option("header", "true") \
    .option("inferSchema", "true") \
    .load("/FileStore/sample_data.csv")

# Explore
df.printSchema()
df.show(10)
print(f"Total records: {df.count()}")

# Write to Bronze
df.write.mode("overwrite").saveAsTable("bronze.raw_sample")
```

**Checkpoint @ 3:45:** *"Run `SELECT COUNT(*) FROM bronze.raw_sample`. What number do you get?"*

---

#### 3:45 – 4:30 | Lab 3: Capstone Project Kickoff (45 mins)

**Objective:** Form teams and scope capstone projects

| Time | Activity |
|------|----------|
| 3:45 – 3:55 | **Project Options Review:** Walk through 4 scenarios |
| 3:55 – 4:10 | **Team Formation:** Self-select into project groups (2-3 per team) |
| 4:10 – 4:30 | **Project Scoping:** Complete Project Charter template |

**Project Charter Template:**

| Section | Your Response |
|---------|---------------|
| **Project Name** | |
| **Team Members** | |
| **Scenario Chosen** | A / B / C / D |
| **Business Question** | What decision will this pipeline support? |
| **Data Sources (3)** | 1. 2. 3. |
| **Bronze Tables Needed** | |
| **Gold Output** | (Dashboard / Report / API) |
| **Teaching Connection** | Which Higher Nitec module does this support? |

**Team Presentations (2 min each):** Quick pitch of project scope

---

#### 4:30 – 4:50 | Reflection & Teaching Bridge (20 mins)

**Teaching Adaptation Exercise:**

| Time | Activity |
|------|----------|
| 4:30 – 4:40 | **Solo Reflection:** Complete Day 1 of Teaching Journal |
| 4:40 – 4:50 | **Pair Share:** Discuss with partner: "What concept from today would you teach first to students?" |

**Teaching Journal - Day 1:**

1. Which concept was hardest to grasp? How would you simplify it for students?
2. What real-world Singapore example would resonate with ITE students?
3. What hands-on exercise would you create for your class?

---

#### 4:50 – 5:00 | Day 1 Closing (10 mins)

| Activity | Details |
|----------|---------|
| **Confidence Re-check** | New sticky note: 1-10, post next to morning one |
| **Day 2 Preview** | "Tomorrow we go multi-source: APIs, databases, and handling failures" |
| **Homework (Optional)** | Explore your project's data sources, identify 3 potential issues |
| **Group Photo** | Capture Day 1 cohort |

---

## 🛠️ Day 1 Toolkit

### Materials Distributed

| Item | Format |
|------|--------|
| Week journey map poster | A1 printed |
| Architecture template | A4 printout |
| Environment setup guide | PDF |
| Scenario cards (8) | Laminated cards |
| Project charter template | A4 printout |
| Teaching journal | Booklet |

### Code Files

| File | Purpose |
|------|---------|
| `setup_validation.py` | Environment check script |
| `day1_extraction_starter.py` | Extraction exercise starter |
| `sample_data.csv` | Practice dataset |

---

## 👨‍🏫 Facilitator Guide - Day 1

### Critical Moments

| Time | Watch For | Intervention |
|------|-----------|--------------|
| 9:30 | Low energy after intro | Energetic delivery, move around room |
| 11:00 | Concept overload | Summarize key point, "breathe" moment |
| 2:00 | Environment setup frustration | Peer support stations, "it's normal to struggle" |
| 3:30 | Varying completion speeds | Fast finishers help others, stretch goals ready |

### Common Day 1 Issues

| Issue | Solution |
|-------|----------|
| Databricks signup failing | Use backup accounts (pre-created) |
| Corporate laptop restrictions | Docker alternative: Gitpod cloud environment |
| Overwhelmed by concepts | "Today is about exposure, mastery comes by Day 5" |
| Imposter syndrome showing | Normalize: "Everyone started somewhere" |

### End-of-Day Success Criteria

- [ ] 100% have working environment (all 7 checks)
- [ ] 90% completed first extraction
- [ ] All teams formed with charter drafted
- [ ] Average confidence increase of +1.5 points

---

## 📋 Pre-Day 2 Checklist

For participants:
- [ ] All environment checks passing
- [ ] Joined WhatsApp group
- [ ] Reviewed project data sources
- [ ] Read Day 2 pre-reading (optional)

For facilitator:
- [ ] Day 2 slide deck ready
- [ ] API demo endpoints tested
- [ ] Database connections verified
- [ ] Sample API keys distributed

---

*Day 1 Complete | Next: Day 2 - Data Extraction & Ingestion →*
