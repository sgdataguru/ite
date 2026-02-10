# Workshop Day 1: Production-Ready Data Pipelining

## ITE Singapore Train the Trainer Program
### Higher Nitec in Data Engineering | Workshop 1 of 3

---

## 🎯 Workshop Overview

| Attribute | Details |
|-----------|---------|
| **Title** | Building Production-Ready Data Pipelines: From Concept to Deployment |
| **Duration** | Full Day (9:00 AM – 5:00 PM) |
| **Format** | Face-to-face at ITE Premises |
| **Class Size** | 12-15 Participants |
| **Target Audience** | ITE Lecturers (Basic-to-Intermediate Level) |
| **Delivery Style** | 10-20-10 Theory Blocks + Hands-On Build Lab |

**The WHY Behind This Workshop:**
Your students will enter a job market where 78% of Singapore enterprises are investing in data infrastructure. But here's the gap: most tutorials teach *toy pipelines*. Your students need to build pipelines that **don't fail at 3 AM on a Sunday**. Today, you'll build exactly that—and walk away ready to teach it.

---

## 📚 Learning Objectives

By the end of this workshop, you will be able to:

| # | Objective | Measurable Outcome |
|---|-----------|-------------------|
| 1 | **Design** a production-grade ETL/ELT pipeline architecture | Complete architecture diagram with data flow |
| 2 | **Build** an end-to-end pipeline using industry-standard tools (Airflow/ADF + dbt) | Working pipeline extracting, transforming, and loading real data |
| 3 | **Implement** error handling, logging, and retry logic | Pipeline recovers gracefully from simulated failures |
| 4 | **Configure** pipeline monitoring and alerting | Dashboard showing pipeline health metrics |
| 5 | **Adapt** today's build into a student-ready teaching module | Draft lesson outline for your Higher Nitec class |

---

## 🕐 Detailed Timetable

### Morning Session: Strategic Theory (9:00 AM – 12:30 PM)

*Focus: Understanding the "WHY" before the "HOW"*

---

#### 9:00 – 9:20 | Opening & Context Setting (20 mins)

| Time | Activity | Facilitator Notes |
|------|----------|-------------------|
| 9:00 – 9:05 | **Arrival & Settle** | Music playing, coffee available |
| 9:05 – 9:10 | **Welcome & Housekeeping** | Wifi, toilets, fire exits, phones on silent |
| 9:10 – 9:20 | **The Singapore Data Landscape** | Share: 78% of SG enterprises investing in data infra. Ask: "What pipeline failures have you seen or heard about?" Collect 3-4 stories on whiteboard |

**Icebreaker Question:** *"On a scale of 1-10, how confident are you building a pipeline that runs unsupervised for 6 months? Write your number on a sticky note."*

---

#### 9:20 – 10:00 | Block 1: Pipeline Architecture Foundations

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 9:20 – 9:30 | **LECTURE (10 min)** | **ETL vs ELT: The Modern Shift** |
| | | • Why ELT is winning (cheap storage, powerful compute) |
| | | • The Medallion Architecture: Bronze → Silver → Gold |
| | | • Real example: Shopee's data pipeline serving 10M+ daily orders |
| 9:30 – 9:50 | **ACTIVITY (20 min)** | **Pair Exercise: Map Your Data** |
| | | In pairs, sketch a pipeline for: *"A polytechnic needs to track student attendance across 5 campuses and generate weekly reports for MOE."* |
| | | Each pair presents in 60 seconds |
| 9:50 – 10:00 | **DEBRIEF (10 min)** | Facilitator synthesizes patterns, highlights best approaches, addresses misconceptions |

**Key Takeaway:** *"Most pipelines fail not because of code, but because of unclear data contracts between source and target."*

---

#### 10:00 – 10:15 | ☕ Morning Coffee Break (15 mins)

*Facilitator: Circulate, have informal chats, identify struggling participants*

---

#### 10:15 – 10:55 | Block 2: Orchestration & Scheduling

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 10:15 – 10:25 | **LECTURE (10 min)** | **The Orchestra Conductor: Why Scheduling Matters** |
| | | • DAGs explained (Directed Acyclic Graphs) |
| | | • Airflow vs Azure Data Factory vs Prefect: When to use what |
| | | • The "dependency hell" problem and how to avoid it |
| 10:25 – 10:45 | **ACTIVITY (20 min)** | **Build a DAG on Paper** |
| | | Given this scenario: *"Extract sales from 3 regions (can run parallel) → Merge into single table → Apply currency conversion → Load to warehouse → Trigger email report"* |
| | | Draw the DAG. Identify: What can run in parallel? What must be sequential? |
| 10:45 – 10:55 | **DEBRIEF (10 min)** | Walk through optimal DAG, discuss parallelization gains, common mistakes |

**Key Takeaway:** *"A well-designed DAG isn't just about sequence—it's about maximizing parallel execution while respecting dependencies."*

---

#### 10:55 – 11:35 | Block 3: When Things Go Wrong (Error Handling)

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 10:55 – 11:05 | **LECTURE (10 min)** | **The 3 AM Problem: Designing for Failure** |
| | | • Types of failures: Transient vs Permanent |
| | | • Retry strategies: Exponential backoff, dead-letter queues |
| | | • Idempotency: "Can I run this twice safely?" |
| | | • Real story: The $50K mistake from missing idempotency |
| 11:05 – 11:25 | **ACTIVITY (20 min)** | **Failure Mode Analysis** |
| | | Groups of 3: Given a pipeline diagram, identify 5 potential failure points |
| | | For each: (1) What could fail? (2) How would you detect it? (3) How would you recover? |
| 11:25 – 11:35 | **DEBRIEF (10 min)** | Groups share top failure scenario, facilitator adds industry examples |

**Key Takeaway:** *"The best pipelines aren't the ones that never fail—they're the ones that fail gracefully and tell you exactly what went wrong."*

---

#### 11:35 – 12:15 | Block 4: Monitoring, Logging & Observability

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 11:35 – 11:45 | **LECTURE (10 min)** | **Pipeline Observability: The Three Pillars** |
| | | • Logs: What happened (structured logging best practices) |
| | | • Metrics: Is it healthy? (latency, throughput, error rates) |
| | | • Traces: Following a record through the pipeline |
| | | • Demo: Airflow UI dashboard walkthrough |
| 11:45 – 12:05 | **ACTIVITY (20 min)** | **Design Your Alerts** |
| | | Solo exercise: For the student attendance pipeline (Block 1), define: |
| | | • 3 critical alerts (wake-me-up-at-3AM level) |
| | | • 3 warning alerts (check-tomorrow level) |
| | | • What dashboard would you build? |
| 12:05 – 12:15 | **DEBRIEF (10 min)** | Share examples, discuss alert fatigue, the "boy who cried wolf" problem |

**Key Takeaway:** *"The right alert is one that's actionable. If you can't do anything about it, don't alert on it."*

---

#### 12:15 – 12:30 | Morning Wrap-Up & Afternoon Preview (15 mins)

| Time | Activity |
|------|----------|
| 12:15 – 12:20 | **Concept Review Quiz** (Kahoot or paper-based) – 5 quick questions |
| 12:20 – 12:25 | **Afternoon Preview:** "You will build a complete pipeline from scratch. Choose your dataset now." |
| 12:25 – 12:30 | **Dataset Selection:** Participants choose from 3 prepared datasets or bring their own |

**Dataset Options:**
1. 🏫 **Student Records** – Attendance, grades, demographics (ITE-relevant)
2. 🛒 **E-commerce Transactions** – Orders, products, customers (industry-relevant)
3. 🌡️ **IoT Sensor Data** – Temperature, humidity, timestamps (emerging field)
4. 📂 **Bring Your Own** – Must be CSV/JSON, <100MB, non-sensitive

---

### 12:30 – 1:30 PM | 🍽️ Lunch Break (60 mins)

*Facilitator: Set up afternoon lab environments, test connections, prepare troubleshooting notes*

---

### Afternoon Session: Practical Build Lab (1:30 PM – 5:00 PM)

*Focus: "Bring Your Own Project" – Build a Production Pipeline*

---

#### 1:30 – 1:45 | Lab Setup & Environment Check (15 mins)

| Time | Activity |
|------|----------|
| 1:30 – 1:35 | **Environment Access:** Confirm all participants logged into Databricks/Airflow |
| 1:35 – 1:40 | **Quick Demo:** Navigating the lab environment |
| 1:40 – 1:45 | **Troubleshoot:** Address any login/access issues |

**Lab Environment:** Databricks Community Edition + Apache Airflow (Docker)

---

#### 1:45 – 2:30 | Build Phase 1: Extract & Load (45 mins)

**Objective:** Get data from source to Bronze layer

| Milestone | Task | Success Criteria |
|-----------|------|------------------|
| 1.1 | Connect to data source (CSV/API) | Connection test passes |
| 1.2 | Write extraction script | Data loads into staging area |
| 1.3 | Implement basic logging | Logs show record counts, timestamps |
| 1.4 | Create Bronze table | Raw data stored in Bronze layer |

**Facilitator Walkthrough (1:45 - 2:00):**
- Live coding: Building the extraction component
- Participants follow along, then customize for their dataset

**Independent Build Time (2:00 - 2:30):**
- Participants complete their extraction
- Facilitator circulates for 1-on-1 support

**Checkpoint @ 2:30:** "Show your Bronze table. How many records loaded?"

---

#### 2:30 – 2:45 | ☕ Afternoon Coffee Break (15 mins)

*Facilitator: Quick check on progress, identify anyone stuck*

---

#### 2:45 – 3:30 | Build Phase 2: Transform (dbt) (45 mins)

**Objective:** Clean and transform data to Silver and Gold layers

| Milestone | Task | Success Criteria |
|-----------|------|------------------|
| 2.1 | Create dbt project structure | Project initialized |
| 2.2 | Write Bronze → Silver transformation | NULL handling, type casting, deduplication |
| 2.3 | Write Silver → Gold business logic | Aggregations, business rules applied |
| 2.4 | Add dbt tests | Schema tests pass |

**Facilitator Walkthrough (2:45 - 3:05):**
- Live coding: Building dbt models
- Key transformations: Data cleansing, type casting, business logic

**Independent Build Time (3:05 - 3:30):**
- Participants build their transformation layer
- Facilitator supports with SQL/dbt questions

**Checkpoint @ 3:30:** "Run `dbt test`. How many tests pass?"

---

#### 3:30 – 4:15 | Build Phase 3: Orchestrate & Monitor (45 mins)

**Objective:** Schedule pipeline with error handling and monitoring

| Milestone | Task | Success Criteria |
|-----------|------|------------------|
| 3.1 | Create Airflow DAG | DAG visible in Airflow UI |
| 3.2 | Set schedule (daily run) | Cron expression configured |
| 3.3 | Add retry logic | Retry on failure (3 attempts, exponential backoff) |
| 3.4 | Configure alerts | Email/Slack notification on failure |
| 3.5 | Trigger test run | Pipeline executes end-to-end |

**Facilitator Walkthrough (3:30 - 3:50):**
- Live coding: Building DAG with Airflow
- Adding error handling and retry logic

**Independent Build Time (3:50 - 4:15):**
- Participants complete their orchestration
- Trigger and monitor pipeline execution

**Checkpoint @ 4:15:** "Trigger your DAG. Did it complete successfully? What logs do you see?"

---

#### 4:15 – 4:45 | Stress Test & Break It! (30 mins)

**Objective:** Validate pipeline resilience

| Scenario | Test | Expected Behavior |
|----------|------|-------------------|
| **Scenario A** | Corrupt source file | Pipeline fails gracefully, logs error, sends alert |
| **Scenario B** | Duplicate data insert | Idempotency: No duplicate records in Gold |
| **Scenario C** | Network timeout | Retry kicks in, eventually succeeds |

**Activity:**
1. Facilitator provides "broken" test files
2. Participants inject failures into their pipelines
3. Observe: Does your pipeline handle it?
4. Fix and re-test

**Discussion:** "What surprised you? What would you add to your student curriculum based on this?"

---

#### 4:45 – 5:00 | Wrap-Up & Teaching Bridge (15 mins)

| Time | Activity |
|------|----------|
| 4:45 – 4:50 | **Gallery Walk:** Quick demos – 3 volunteers show their pipeline |
| 4:50 – 4:55 | **Teaching Reflection:** "How would you break today's content into 3 student lessons?" – Quick pair discussion |
| 4:55 – 5:00 | **Closing:** Certificate of completion, next workshop preview, post-workshop support channels (WhatsApp group) |

**Confidence Check:** *"Remember your 1-10 sticky note from this morning? What's your number now?"*

---

## 🛠️ The Practical Toolkit

### Pre-Workshop Setup (Participants)

| Item | Purpose | Access |
|------|---------|--------|
| Laptop | Personal development machine | Participant-provided |
| Databricks Community Account | Cloud data platform | Sign up: databricks.com/try |
| Docker Desktop | Run Airflow locally | Download: docker.com |
| VS Code | Code editor | Download: code.visualstudio.com |
| Git | Version control | Pre-installed check |
| Python 3.9+ | Runtime | Pre-installed check |

### Software & Tools (Provided)

| Tool | Purpose | License |
|------|---------|---------|
| Apache Airflow 2.x | Orchestration | Open Source |
| dbt Core | Transformation | Open Source |
| Databricks Community | Compute + Storage | Free Tier |
| Sample Datasets (3) | Lab exercises | Provided |

### Templates & Documents

| Template | Description | Format |
|----------|-------------|--------|
| `pipeline-architecture-template.pptx` | Blank architecture diagram template | PowerPoint |
| `dag-template.py` | Starter Airflow DAG with best practices | Python |
| `dbt-project-starter.zip` | Pre-configured dbt project structure | Zip |
| `monitoring-checklist.pdf` | Alert design checklist | PDF |
| `error-handling-patterns.md` | Common error scenarios + solutions | Markdown |
| `student-lesson-outline.docx` | Template for adapting to curriculum | Word |

### Checklists

#### ✅ Pre-Workshop Checklist (Participant)

- [ ] Databricks Community account created and verified
- [ ] Docker Desktop installed and running
- [ ] VS Code installed with Python extension
- [ ] Git installed (`git --version` works)
- [ ] Python 3.9+ installed (`python --version` works)
- [ ] Downloaded workshop materials from shared drive
- [ ] Chosen dataset (or prepared own dataset)

#### ✅ Environment Validation Checklist

- [ ] Can login to Databricks workspace
- [ ] Can create and run a notebook
- [ ] Docker runs `hello-world` successfully
- [ ] Can access Airflow UI at localhost:8080
- [ ] dbt CLI installed (`dbt --version` works)

---

## 👨‍🏫 Facilitator Guide

### Handling Common Roadblocks

#### Technical Issues

| Issue | Quick Fix | Escalation |
|-------|-----------|------------|
| **Can't login to Databricks** | Clear cookies, try incognito, check email for verification | Pair with neighbor temporarily |
| **Docker not starting** | Restart Docker Desktop, check virtualization enabled in BIOS | Use cloud-based Airflow alternative |
| **Airflow UI blank** | Wait 60 seconds for containers to initialize, check `docker ps` | Share screen with facilitator's instance |
| **dbt test failures** | Check YAML indentation, verify column names match | Provide working example to compare |
| **Python version issues** | Use pyenv or conda to switch Python versions | Pre-configured VM fallback |

#### Pacing Issues

| Scenario | Adjustment |
|----------|------------|
| **Group moving faster than planned** | Add stretch goals: "Can you make your pipeline handle schema evolution?" |
| **Group moving slower** | Drop Phase 3 stretch goals, focus on core pipeline completion |
| **Mixed speeds** | Pair fast participants with slower ones (peer teaching) |
| **Energy dip after lunch** | 2-minute stretch break, energizer question, or quick demo |

#### Engagement Issues

| Scenario | Intervention |
|----------|-------------|
| **Quiet participant** | Direct question: "Siti, what's your experience with this at ITE?" |
| **Dominating participant** | "Great point, Ahmad. Let's hear from someone who hasn't shared yet." |
| **Side conversations** | Walk toward the group, pause, make eye contact |
| **Checking phones** | "Quick phone check – if it's urgent, step out briefly" |

### Key Facilitation Moments

#### Morning Blocks
- **Block 1:** Watch for confusion between ETL and ELT – clarify with "storage is cheap, compute is powerful"
- **Block 3:** This is where engagement drops – use horror stories (The $50K mistake) to regain attention
- **Lunch Preview:** Critical to get dataset choice locked in before lunch

#### Afternoon Lab
- **First 15 mins:** Make or break time – solve ALL access issues before building starts
- **Phase 1 → 2 transition:** Clean checkpoint – don't proceed until 80% have Bronze layer working
- **Phase 3:** Most will struggle here – have working example ready to share if needed

### Facilitator Materials

| Material | Purpose |
|----------|---------|
| Slide deck (PDF) | Morning theory backup |
| Live coding scripts | Complete solutions for each phase |
| "Broken" test files | For stress test exercise |
| Backup cloud environment | If local Docker fails |
| Kahoot quiz | Morning wrap-up quiz |
| Printed checklists | Distribute at start |

---

## 📊 Success Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| Completion Rate | 90% complete working pipeline | End-of-day checkpoint |
| Confidence Increase | +3 points average (vs morning) | Sticky note comparison |
| Satisfaction Score | 4.0+ / 5.0 | Post-workshop survey |
| Curriculum Adaptation | 100% have draft lesson outline | Photo of outline at closing |

---

## 📝 Post-Workshop Support

| Channel | Purpose | Response Time |
|---------|---------|---------------|
| WhatsApp Group | Quick questions, troubleshooting | < 24 hours |
| Email (Mahesh) | Formal queries, materials request | < 48 hours |
| Follow-up Session | Deep-dive on specific topics | Schedule as needed |
| Resource Repository | Updated materials, industry examples | Shared Drive link |

---

## 🔜 Next Workshop Preview

**Workshop 2: Data Solutions & Analytics Platforms**
- Power BI + DAX deep dive
- Building low-code data applications (Streamlit)
- Real-time dashboards
- Predictive analytics basics

*Target Date: 2 weeks after Workshop 1*

---

## 📎 Appendix

### A. Sample DAG Code

```python
from airflow import DAG
from airflow.operators.python import PythonOperator
from datetime import datetime, timedelta

default_args = {
    'owner': 'ite-lecturer',
    'retries': 3,
    'retry_delay': timedelta(minutes=5),
    'email_on_failure': True,
    'email': ['lecturer@ite.edu.sg']
}

with DAG(
    dag_id='student_attendance_pipeline',
    default_args=default_args,
    description='Daily student attendance ETL pipeline',
    schedule_interval='0 6 * * *',  # 6 AM daily
    start_date=datetime(2026, 2, 1),
    catchup=False,
    tags=['attendance', 'production']
) as dag:
    
    extract_task = PythonOperator(
        task_id='extract_attendance_data',
        python_callable=extract_from_source
    )
    
    transform_task = PythonOperator(
        task_id='transform_to_silver',
        python_callable=clean_and_transform
    )
    
    load_task = PythonOperator(
        task_id='load_to_gold',
        python_callable=load_to_warehouse
    )
    
    extract_task >> transform_task >> load_task
```

### B. dbt Model Example

```sql
-- models/silver/stg_student_attendance.sql

WITH source AS (
    SELECT * FROM {{ source('bronze', 'raw_attendance') }}
),

cleaned AS (
    SELECT
        student_id,
        campus_code,
        attendance_date,
        CASE 
            WHEN status IS NULL THEN 'UNKNOWN'
            ELSE UPPER(TRIM(status))
        END AS attendance_status,
        recorded_at,
        -- Deduplication
        ROW_NUMBER() OVER (
            PARTITION BY student_id, attendance_date 
            ORDER BY recorded_at DESC
        ) AS row_num
    FROM source
    WHERE student_id IS NOT NULL
)

SELECT * FROM cleaned WHERE row_num = 1
```

### C. Monitoring Checklist Template

| Alert Type | Condition | Severity | Action |
|------------|-----------|----------|--------|
| Pipeline Failure | DAG run fails after retries | Critical | Page on-call, investigate immediately |
| Data Freshness | No new data in 4 hours | Warning | Check source system availability |
| Row Count Drop | >30% decrease vs previous day | Warning | Validate source completeness |
| Duplicate Records | Duplicate keys detected | Critical | Stop pipeline, investigate source |
| Late Arrival | Pipeline doesn't complete by 8 AM | Warning | Notify consumers, extend SLA |

---

*Document Version: 1.0 | Last Updated: February 2026 | Author: Train the Trainer Program*
