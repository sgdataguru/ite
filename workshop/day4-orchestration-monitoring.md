# Day 4: Orchestration & Monitoring

## 🎯 Automating and Observing Your Data Pipeline

---

## Day Overview

| Attribute | Details |
|-----------|---------|
| **Day Theme** | Making pipelines run themselves (reliably) |
| **Duration** | 9:00 AM – 5:00 PM |
| **Morning Focus** | Airflow fundamentals, DAGs, scheduling, alerting |
| **Afternoon Focus** | Orchestrate capstone pipeline with monitoring |
| **End-of-Day Deliverable** | Fully orchestrated pipeline with alerts and dashboard |

---

## 📚 Learning Objectives

By the end of Day 4, you will be able to:

| # | Objective | Measurable Outcome |
|---|-----------|-------------------|
| 1 | **Build** an Airflow DAG from scratch | Working DAG submitted |
| 2 | **Configure** scheduling and dependencies | Cron-based schedule running |
| 3 | **Implement** error handling and retries | Pipeline recovers from failure |
| 4 | **Set up** alerting for pipeline failures | Slack/email notification triggered |
| 5 | **Create** an observability dashboard | Dashboard showing key metrics |

---

## 🕐 Detailed Timetable

### Morning Session: Strategic Theory (9:00 AM – 12:30 PM)

---

#### 9:00 – 9:20 | Day 4 Opening (20 mins)

| Time | Activity | Facilitator Notes |
|------|----------|-------------------|
| 9:00 – 9:05 | **Arrival & Settle** | "Show your dbt lineage graph" - quick visual check |
| 9:05 – 9:15 | **Day 3 Recap Quiz** | 5 questions on dbt, testing, star schema |
| 9:15 – 9:20 | **Day 4 Roadmap** | "Today: Set it and forget it (almost)" |

**Energizer:** *"Raise your hand if you've ever been woken up by a failed job. We're preventing that today."*

---

#### 9:20 – 10:00 | Block 1: Why Orchestration Matters

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 9:20 – 9:30 | **LECTURE (10 min)** | **From Manual to Managed** |
| | | • The cron job problems: No dependencies, no visibility |
| | | • What orchestration provides: Scheduling, dependencies, retries, logging |
| | | • Orchestrator landscape: Airflow, Prefect, Dagster, Databricks Workflows |
| | | • Why Airflow: Industry standard, huge community, ITE curriculum aligned |
| | | • Core concept: DAGs (Directed Acyclic Graphs) explained simply |
| 9:30 – 9:50 | **ACTIVITY (20 min)** | **Design Your Pipeline DAG** |
| | | On paper/whiteboard: |
| | | 1. List all extraction tasks from Day 2 |
| | | 2. List all transformation tasks from Day 3 |
| | | 3. Draw dependencies: What must complete before what? |
| | | 4. Identify parallelization opportunities |
| | | 5. Mark failure points: Where could things break? |
| 9:50 – 10:00 | **DEBRIEF (10 min)** | Share DAG designs, identify common patterns |

**DAG Design Template:**
```
┌──────────────┐
│   trigger    │  (manual/schedule/event)  
└──────┬───────┘
       │
       ▼
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ extract_api  │     │ extract_file │     │ extract_db   │
└──────┬───────┘     └──────┬───────┘     └──────┬───────┘
       │                    │                    │
       └─────────┬──────────┴──────────┬─────────┘
                 │ (wait for all)      │
                 ▼                     ▼
         ┌──────────────┐      ┌──────────────┐
         │ bronze_load  │      │ bronze_load  │
         └──────┬───────┘      └──────┬───────┘
                └─────────┬────────────┘
                          ▼
                  ┌──────────────┐
                  │ dbt_silver   │
                  └──────┬───────┘
                         ▼
                  ┌──────────────┐
                  │  dbt_gold    │
                  └──────┬───────┘
                         ▼
                  ┌──────────────┐
                  │   notify     │
                  └──────────────┘
```

**Key Takeaway:** *"Think of an orchestrator as an intelligent air traffic controller for your data."*

---

#### 10:00 – 10:15 | ☕ Morning Coffee Break (15 mins)

*Facilitator: Display Airflow UI demo on projector*

---

#### 10:15 – 10:55 | Block 2: Airflow Deep Dive

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 10:15 – 10:25 | **LECTURE (10 min)** | **Airflow Architecture & Concepts** |
| | | • Components: Scheduler, Webserver, Workers, Metadata DB |
| | | • DAG file structure: Python code that defines the pipeline |
| | | • Operators: Python, Bash, Databricks, HTTP, Sensors |
| | | • XComs: Passing data between tasks (carefully!) |
| | | • Connections: Secure credential storage |
| | | • Variables: Configuration outside of code |
| 10:25 – 10:45 | **ACTIVITY (20 min)** | **Your First Airflow DAG** |
| | | Using the Airflow UI and provided template: |
| | | 1. Create a new DAG file |
| | | 2. Define 3 tasks with dependencies |
| | | 3. Set schedule to run every 5 minutes (for testing) |
| | | 4. Trigger manually, watch it execute |
| | | 5. View logs for each task |
| 10:45 – 10:55 | **DEBRIEF (10 min)** | Troubleshoot errors, explain task states |

**Minimal Airflow DAG Template:**
```python
# dags/my_first_dag.py

from datetime import datetime, timedelta
from airflow import DAG
from airflow.operators.python import PythonOperator
from airflow.operators.bash import BashOperator

# Define default arguments
default_args = {
    'owner': 'ite_workshop',
    'depends_on_past': False,
    'email_on_failure': True,
    'email': ['trainer@ite.edu.sg'],
    'retries': 2,
    'retry_delay': timedelta(minutes=5),
}

# Define the DAG
with DAG(
    dag_id='my_first_dag',
    default_args=default_args,
    description='My first Airflow DAG',
    schedule_interval='0 6 * * *',  # Run at 6 AM daily
    start_date=datetime(2025, 1, 1),
    catchup=False,  # Don't backfill
    tags=['workshop', 'learning'],
) as dag:

    # Task 1: Start task
    start = BashOperator(
        task_id='start',
        bash_command='echo "Starting pipeline at $(date)"',
    )

    # Task 2: Extract data
    def extract_data():
        print("Extracting data from source...")
        return "Extracted 1000 records"

    extract = PythonOperator(
        task_id='extract_data',
        python_callable=extract_data,
    )

    # Task 3: Transform data
    def transform_data(ti):
        result = ti.xcom_pull(task_ids='extract_data')
        print(f"Transforming: {result}")
        return "Transformation complete"

    transform = PythonOperator(
        task_id='transform_data',
        python_callable=transform_data,
    )

    # Task 4: End task
    end = BashOperator(
        task_id='end',
        bash_command='echo "Pipeline complete!"',
    )

    # Define dependencies
    start >> extract >> transform >> end
```

**Key Takeaway:** *"DAGs are Python code—all your SE skills apply. Version control, test, review."*

---

#### 10:55 – 11:35 | Block 3: Scheduling & Dependencies

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 10:55 – 11:05 | **LECTURE (10 min)** | **The Art of Scheduling** |
| | | • Cron expressions demystified: * * * * * explained |
| | | • Execution date vs logical date (confusing but critical!) |
| | | • Catchup: When to use, when to avoid |
| | | • Task dependencies: >> operator, trigger rules |
| | | • Sensors: Waiting for external events (file appears, API ready) |
| | | • Time zones: UTC always, convert for display |
| 11:05 – 11:25 | **ACTIVITY (20 min)** | **Cron Expression Challenge** |
| | | Match the schedule to the cron expression: |
| | | 1. Every Monday at 7 AM |
| | | 2. Every 15 minutes during business hours |
| | | 3. First day of each month at midnight |
| | | 4. Every weekday at 6 PM |
| | | Use: https://crontab.guru to verify |
| | | Bonus: Set YOUR capstone's ideal schedule |
| 11:25 – 11:35 | **DEBRIEF (10 min)** | Review answers, discuss cron gotchas |

**Cron Expression Cheat Sheet:**

```
 ┌─────── minute (0 - 59)
 │ ┌───── hour (0 - 23)
 │ │ ┌─── day of month (1 - 31)
 │ │ │ ┌─ month (1 - 12)
 │ │ │ │ ┌ day of week (0 - 6, Sunday = 0)
 │ │ │ │ │
 * * * * *
```

| Expression | Meaning |
|------------|---------|
| `0 6 * * *` | Daily at 6:00 AM |
| `0 */4 * * *` | Every 4 hours |
| `*/15 * * * *` | Every 15 minutes |
| `0 7 * * 1` | Every Monday at 7:00 AM |
| `0 0 1 * *` | First of each month at midnight |
| `0 18 * * 1-5` | Weekdays at 6:00 PM |
| `0 8-17 * * 1-5` | Every hour 8 AM - 5 PM on weekdays |

**Key Takeaway:** *"Schedule defensively. Account for source delays, time zones, and overlap."*

---

#### 11:35 – 12:15 | Block 4: Failure Handling & Alerting

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 11:35 – 11:45 | **LECTURE (10 min)** | **When Things Go Wrong (They Will)** |
| | | • Retry strategies: How many? How long to wait? |
| | | • Trigger rules: all_success, one_success, all_failed |
| | | • SLAs: When late is really late |
| | | • Alerting: Email, Slack, PagerDuty |
| | | • Runbook: What to do when alert fires |
| | | • Dead-letter patterns: Don't lose failed data |
| 11:45 – 12:05 | **ACTIVITY (20 min)** | **Failure Simulation Exercise** |
| | | 1. Add a task that intentionally fails 50% of the time |
| | | 2. Configure retries (2 attempts, 1 min delay) |
| | | 3. Add on_failure_callback to send alert |
| | | 4. Run multiple times, observe behavior |
| | | 5. Check retry logs, verify alerts received |
| 12:05 – 12:15 | **DEBRIEF (10 min)** | Discuss failure patterns observed, production stories |

**Failure Handling Pattern:**
```python
from airflow.providers.slack.callbacks.slack import send_slack_notification
from airflow.models import Variable

def alert_on_failure(context):
    """Custom failure callback with detailed info"""
    task_instance = context['task_instance']
    dag_id = context['dag'].dag_id
    task_id = task_instance.task_id
    execution_date = context['execution_date']
    log_url = task_instance.log_url
    
    message = f"""
    🚨 *Pipeline Failure Alert*
    DAG: {dag_id}
    Task: {task_id}
    Execution Date: {execution_date}
    
    [View Logs]({log_url})
    
    Please investigate according to runbook.
    """
    
    # Send to Slack/Teams/email
    send_slack_notification(
        slack_conn_id='slack_webhook',
        text=message,
    )

# Use in task
task_with_alerts = PythonOperator(
    task_id='critical_task',
    python_callable=critical_function,
    retries=3,
    retry_delay=timedelta(minutes=5),
    retry_exponential_backoff=True,
    max_retry_delay=timedelta(hours=1),
    on_failure_callback=alert_on_failure,
    sla=timedelta(hours=2),  # Alert if not complete in 2 hours
)
```

**Key Takeaway:** *"Expect failure. Design for graceful recovery. Always alert humans when automation can't fix it."*

---

#### 12:15 – 12:30 | Morning Wrap-Up (15 mins)

| Activity | Details |
|----------|---------|
| Concept check | "Point to the task state icons: Running, Success, Failed, Retry" |
| Afternoon preview | "We're building your complete orchestrated pipeline" |
| Questions parking lot | Complex scheduling questions for lab time |

---

### 12:30 – 1:30 PM | 🍽️ Lunch Break (60 mins)

*Facilitator: Ensure Airflow environment stable, prepare monitoring tools*

---

### Afternoon Session: Practical Lab (1:30 PM – 5:00 PM)

---

#### 1:30 – 2:30 | Lab 1: Orchestrate Your Capstone Pipeline (60 mins)

**Objective:** Create a production-style Airflow DAG for your capstone

| Time | Activity |
|------|----------|
| 1:30 – 1:45 | **Facilitator Demo:** Complete orchestration pattern |
| 1:45 – 2:30 | **Team Build:** Create capstone DAG |

**Capstone DAG Requirements:**

| Requirement | Details |
|-------------|---------|
| Minimum 7 tasks | Extract × 3, Bronze × 3, dbt Silver, dbt Gold |
| Parallel execution | Independent extractions run in parallel |
| Dependencies | Correct order: Extract → Bronze → Silver → Gold |
| Schedule | Daily at 6 AM (or project-appropriate time) |
| Retries | All tasks have retry configuration |
| Documentation | DAG and task descriptions filled in |

**Capstone DAG Template:**
```python
# dags/capstone_pipeline.py

from datetime import datetime, timedelta
from airflow import DAG
from airflow.operators.python import PythonOperator
from airflow.operators.bash import BashOperator
from airflow.operators.dummy import DummyOperator
from airflow.utils.task_group import TaskGroup

default_args = {
    'owner': 'capstone_team',
    'depends_on_past': False,
    'email_on_failure': True,
    'email': ['team@ite.edu.sg'],
    'retries': 2,
    'retry_delay': timedelta(minutes=5),
}

with DAG(
    dag_id='capstone_data_pipeline',
    default_args=default_args,
    description='End-to-end data pipeline for capstone project',
    schedule_interval='0 6 * * *',  # 6 AM daily (SGT configure in Airflow)
    start_date=datetime(2025, 1, 1),
    catchup=False,
    tags=['capstone', 'production'],
    max_active_runs=1,  # Prevent overlap
) as dag:

    start = DummyOperator(task_id='start')
    
    # Extraction task group (parallel)
    with TaskGroup(group_id='extraction') as extraction_group:
        extract_api = PythonOperator(
            task_id='extract_api',
            python_callable=extract_from_api,
            op_kwargs={'endpoint': Variable.get('api_endpoint')},
        )
        
        extract_file = PythonOperator(
            task_id='extract_file',
            python_callable=extract_from_file,
            op_kwargs={'path': '/data/source/'},
        )
        
        extract_db = PythonOperator(
            task_id='extract_db',
            python_callable=extract_from_database,
        )
    
    # Bronze loading (depends on all extractions)
    wait_extraction = DummyOperator(
        task_id='wait_extraction',
        trigger_rule='all_success',
    )
    
    with TaskGroup(group_id='bronze_load') as bronze_group:
        bronze_api = PythonOperator(task_id='bronze_api', ...)
        bronze_file = PythonOperator(task_id='bronze_file', ...)
        bronze_db = PythonOperator(task_id='bronze_db', ...)
    
    # dbt transformations
    dbt_silver = BashOperator(
        task_id='dbt_silver',
        bash_command='cd /dbt && dbt run --select staging.*',
    )
    
    dbt_gold = BashOperator(
        task_id='dbt_gold',
        bash_command='cd /dbt && dbt run --select marts.*',
    )
    
    dbt_test = BashOperator(
        task_id='dbt_test',
        bash_command='cd /dbt && dbt test',
    )
    
    # Notification
    def notify_success(context):
        print("Pipeline completed successfully!")
        # Send Slack notification
    
    notify = PythonOperator(
        task_id='notify_success',
        python_callable=notify_success,
        trigger_rule='all_success',
    )
    
    end = DummyOperator(task_id='end')
    
    # Define dependencies
    start >> extraction_group >> wait_extraction >> bronze_group
    bronze_group >> dbt_silver >> dbt_gold >> dbt_test >> notify >> end
```

**Checkpoint @ 2:30:** *"Show your DAG in Airflow UI, trigger manual run"*

---

#### 2:30 – 2:45 | ☕ Afternoon Coffee Break (15 mins)

---

#### 2:45 – 3:30 | Lab 2: Add Comprehensive Alerting (45 mins)

**Objective:** Implement monitoring and alerts for your pipeline

| Time | Activity |
|------|----------|
| 2:45 – 2:55 | **Facilitator Demo:** Slack/email alerting setup |
| 2:55 – 3:30 | **Team Work:** Add alerting to capstone DAG |

**Alerting Requirements:**

| Scenario | Alert Type | Channel |
|----------|------------|---------|
| Task failure | Immediate | Slack + Email |
| SLA miss | Warning | Email |
| Pipeline success | Summary | Slack |
| All retries exhausted | Critical | Email + PagerDuty (optional) |

**Alert Configuration:**
```python
# Define alert functions
def task_failure_alert(context):
    """Immediate alert on any task failure"""
    # Slack notification
    webhook_url = Variable.get('slack_webhook')
    message = {
        "blocks": [
            {
                "type": "header",
                "text": {"type": "plain_text", "text": "🚨 Pipeline Task Failed"}
            },
            {
                "type": "section",
                "fields": [
                    {"type": "mrkdwn", "text": f"*DAG:* {context['dag'].dag_id}"},
                    {"type": "mrkdwn", "text": f"*Task:* {context['task'].task_id}"},
                    {"type": "mrkdwn", "text": f"*Time:* {datetime.now().strftime('%Y-%m-%d %H:%M')}"},
                    {"type": "mrkdwn", "text": f"*Owner:* {context['dag'].owner}"},
                ]
            },
            {
                "type": "actions",
                "elements": [
                    {
                        "type": "button",
                        "text": {"type": "plain_text", "text": "View Logs"},
                        "url": context['task_instance'].log_url
                    }
                ]
            }
        ]
    }
    requests.post(webhook_url, json=message)

def pipeline_success_alert(context):
    """Summary message on successful completion"""
    dag_run = context['dag_run']
    duration = dag_run.end_date - dag_run.start_date
    
    message = f"""
    ✅ *Pipeline Completed Successfully*
    • DAG: {context['dag'].dag_id}
    • Duration: {duration}
    • Records Processed: (query from metadata)
    """
    # Send to Slack
```

**Checkpoint @ 3:30:** *"Trigger a failure, show alert in Slack/email"*

---

#### 3:30 – 4:30 | Lab 3: Build Observability Dashboard (60 mins)

**Objective:** Create monitoring dashboard for pipeline health

| Time | Activity |
|------|----------|
| 3:30 – 3:45 | **Facilitator Demo:** Dashboard creation in Streamlit |
| 3:45 – 4:30 | **Team Build:** Create team monitoring dashboard |

**Dashboard Requirements:**

| Panel | Metrics |
|-------|---------|
| **Health Overview** | Success/fail ratio, current status |
| **Duration Trends** | Task durations over time |
| **Data Quality** | dbt test pass rates |
| **Volume Metrics** | Records processed per run |
| **Alert History** | Recent failures and resolutions |

**Streamlit Dashboard Template:**
```python
# monitoring/dashboard.py

import streamlit as st
import pandas as pd
import plotly.express as px
from datetime import datetime, timedelta

st.set_page_config(page_title="Pipeline Monitor", page_icon="📊", layout="wide")

st.title("📊 Data Pipeline Monitoring Dashboard")

# Sidebar - date range filter
st.sidebar.header("Filters")
date_range = st.sidebar.date_input(
    "Date Range",
    value=(datetime.now() - timedelta(days=7), datetime.now())
)

# Row 1: Key Metrics
col1, col2, col3, col4 = st.columns(4)

with col1:
    st.metric(
        label="Success Rate (7d)",
        value="94.5%",
        delta="2.3%"
    )

with col2:
    st.metric(
        label="Avg Duration",
        value="23 min",
        delta="-5 min"
    )

with col3:
    st.metric(
        label="Records Today",
        value="1.2M",
        delta="125K"
    )

with col4:
    st.metric(
        label="Active Failures",
        value="0",
        delta="0"
    )

# Row 2: Run History
st.header("📈 Pipeline Run History")

# Mock data - replace with actual Airflow metadata query
run_data = pd.DataFrame({
    'date': pd.date_range(start='2025-01-01', periods=14, freq='D'),
    'duration_mins': [22, 24, 21, 35, 23, 22, 25, 21, 23, 24, 22, 45, 23, 21],
    'status': ['success']*10 + ['failed'] + ['success']*3,
    'records': [1000000 + i*50000 for i in range(14)]
})

col1, col2 = st.columns(2)

with col1:
    fig = px.bar(run_data, x='date', y='duration_mins', color='status',
                 color_discrete_map={'success': 'green', 'failed': 'red'})
    fig.update_layout(title="Run Duration by Day")
    st.plotly_chart(fig, use_container_width=True)

with col2:
    fig2 = px.line(run_data, x='date', y='records')
    fig2.update_layout(title="Records Processed")
    st.plotly_chart(fig2, use_container_width=True)

# Row 3: dbt Test Results
st.header("🧪 Data Quality Tests")

test_data = pd.DataFrame({
    'model': ['stg_orders', 'stg_customers', 'fct_sales', 'dim_products'],
    'tests_passed': [8, 5, 10, 6],
    'tests_failed': [0, 0, 1, 0],
})

st.dataframe(test_data, use_container_width=True)

# Row 4: Recent Alerts
st.header("🚨 Recent Alerts")

alerts = [
    {"time": "2025-01-14 15:23", "severity": "WARNING", "message": "SLA miss: dbt_gold task"},
    {"time": "2025-01-13 06:45", "severity": "ERROR", "message": "Task failed: extract_api (retry succeeded)"},
]

for alert in alerts:
    severity_color = "🟡" if alert['severity'] == 'WARNING' else "🔴"
    st.write(f"{severity_color} **{alert['time']}** - {alert['message']}")
```

**Checkpoint @ 4:30:** *"Show your dashboard with real or mock data"*

---

#### 4:30 – 4:50 | Reflection & Teaching Bridge (20 mins)

**Teaching Adaptation Exercise:**

| Time | Activity |
|------|----------|
| 4:30 – 4:40 | **Solo Reflection:** Complete Day 4 Teaching Journal |
| 4:40 – 4:50 | **Group Discussion:** "How would you simplify orchestration concepts for students?" |

**Teaching Journal - Day 4:**

1. What's the simplest orchestration example you could start students with?
2. How would you explain DAG dependencies without overwhelming them?
3. What monitoring metric is most important for students to understand?

**Simplified Teaching Examples:**

| Concept | Simple Analogy | Code Example |
|---------|----------------|--------------|
| DAG | Recipe with steps | Task A >> Task B |
| Schedule | Alarm clock | `schedule_interval='@daily'` |
| Retry | "Try again if you fail" | `retries=3` |
| Alert | "Text me if there's a problem" | `on_failure_callback` |
| Sensor | "Wait until file appears" | `FileSensor` |

---

#### 4:50 – 5:00 | Day 4 Closing (10 mins)

| Activity | Details |
|----------|---------|
| **Live Demo** | Trigger one team's DAG, watch it run in UI |
| **Dashboard Showcase** | Quick walkthrough of best monitoring dashboard |
| **Day 5 Preview** | "Tomorrow: Production deployment and curriculum creation" |
| **Homework** | Review DAG, ensure all tasks have documentation |

---

## 🛠️ Day 4 Toolkit

### Materials Distributed

| Item | Format |
|------|--------|
| Cron expression cheat sheet | Laminated card |
| Airflow operator reference | PDF |
| DAG design template | A3 paper |
| Alert message templates | PDF |

### Lab Resources

| Resource | Details |
|----------|---------|
| Airflow UI | http://localhost:8080 (local) or cloud URL |
| Slack workspace | Pre-configured with webhook |
| Streamlit | Pre-installed in environment |
| Sample dashboard | `/workshop/day4/dashboard_template/` |

---

## 👨‍🏫 Facilitator Guide - Day 4

### Critical Moments

| Time | Watch For | Intervention |
|------|-----------|--------------|
| 10:00 | DAG parsing errors | Common: imports, indentation |
| 11:00 | Cron confusion | Use crontab.guru on screen |
| 2:00 | Task groups complexity | Show flat DAG alternative |
| 3:30 | Streamlit errors | Provide working template |

### Common Day 4 Issues

| Issue | Solution |
|-------|----------|
| DAG not appearing in UI | Check DAGs folder path, import errors |
| Tasks stuck in "scheduled" | Scheduler not running, clear queue |
| Slack webhook failing | Verify connection in Admin → Connections |
| Dashboard not updating | Refresh interval, caching issues |

### End-of-Day Success Criteria

- [ ] Every team has working Airflow DAG
- [ ] DAG runs successfully end-to-end
- [ ] At least one alert type configured
- [ ] Basic dashboard created
- [ ] Schedule configured (even if paused)

---

## 📊 Day 4 Architecture Progress

```
DAY 1: [Environment] ✓
         ↓
DAY 2: [Bronze Layer] ✓
         ↓
DAY 3: [Silver Layer] ✓ → [Gold Layer] ✓
         ↓
DAY 4: [Orchestration] ✓ → [Monitoring] ✓  ← YOU ARE HERE
         ↓
DAY 5: [Production]
```

---

*Day 4 Complete | Next: Day 5 - Production Deployment & Curriculum Creation →*
