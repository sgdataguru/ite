# Day 5: Production Deployment & Teaching Adaptation

## 🎯 From Workshop to Classroom: Making It Real

---

## Day Overview

| Attribute | Details |
|-----------|---------|
| **Day Theme** | Deploying to production + creating your curriculum |
| **Duration** | 9:00 AM – 5:00 PM |
| **Morning Focus** | CI/CD, deployment best practices, documentation |
| **Afternoon Focus** | Capstone presentations, curriculum creation |
| **End-of-Day Deliverable** | Production-deployed pipeline + teaching materials |

---

## 📚 Learning Objectives

By the end of Day 5, you will be able to:

| # | Objective | Measurable Outcome |
|---|-----------|-------------------|
| 1 | **Deploy** a data pipeline to production environment | Pipeline running in production |
| 2 | **Implement** CI/CD for data engineering projects | GitHub Actions workflow running |
| 3 | **Document** a production-ready data pipeline | Runbook completed |
| 4 | **Adapt** workshop content for student curriculum | Lesson plan created |
| 5 | **Present** and defend technical implementation | Capstone presentation delivered |

---

## 🕐 Detailed Timetable

### Morning Session: Production Readiness (9:00 AM – 12:30 PM)

---

#### 9:00 – 9:20 | Day 5 Opening (20 mins)

| Time | Activity | Facilitator Notes |
|------|----------|-------------------|
| 9:00 – 9:05 | **Arrival & Settle** | "Last day! Show your working DAG" |
| 9:05 – 9:15 | **Week Recap** | Quick visual journey through Days 1-4 |
| 9:15 – 9:20 | **Day 5 Roadmap** | "Today we make it real and shareable" |

**Energizer:** *"On a scale of 1-10, how production-ready do you feel? We're getting everyone to 10."*

---

#### 9:20 – 10:00 | Block 1: Production Checklist

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 9:20 – 9:30 | **LECTURE (10 min)** | **What "Production-Ready" Really Means** |
| | | • Development mindset vs Production mindset |
| | | • The production checklist: Security, reliability, observability |
| | | • Environment separation: Dev, staging, production |
| | | • Secrets management: Never hardcode credentials! |
| | | • Disaster recovery: Backups, rollback plans |
| | | • Cost optimization: Don't bankrupt ITE! |
| 9:30 – 9:50 | **ACTIVITY (20 min)** | **Production Readiness Audit** |
| | | Using the checklist below, audit your capstone: |
| | | • Score each item 0-2 (Not done, Partial, Complete) |
| | | • Identify top 3 gaps |
| | | Partner swap: Review each other's audit |
| 9:50 – 10:00 | **DEBRIEF (10 min)** | Share common gaps, prioritize fixes |

**Production Readiness Checklist:**

| Category | Item | Score (0-2) |
|----------|------|-------------|
| **Security** | No hardcoded credentials | |
| | Secrets stored in proper vault | |
| | Minimal permissions (principle of least privilege) | |
| | PDPA compliance for any personal data | |
| **Reliability** | All tasks have retries configured | |
| | Error handling for all failure modes | |
| | SLAs defined for critical paths | |
| | Rollback procedure documented | |
| **Observability** | Alerting on failures configured | |
| | Logging with proper levels | |
| | Metrics dashboard exists | |
| | Runbook for common issues | |
| **Performance** | Appropriate scheduling (not too frequent) | |
| | Parallelization where possible | |
| | Incremental processing implemented | |
| **Documentation** | README with setup instructions | |
| | DAG documentation complete | |
| | Data dictionary exists | |

**Key Takeaway:** *"Production is not 'it works on my machine.' Production is 'it works reliably at 3 AM when you're asleep.'"*

---

#### 10:00 – 10:15 | ☕ Morning Coffee Break (15 mins)

*Facilitator: Prepare GitHub Actions demo*

---

#### 10:15 – 10:55 | Block 2: CI/CD for Data Pipelines

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 10:15 – 10:25 | **LECTURE (10 min)** | **Continuous Integration for Data** |
| | | • Why CI/CD for pipelines? Catch errors early, deploy safely |
| | | • Testing pyramid: Unit → Integration → Contract → E2E |
| | | • GitHub Actions basics: Workflows, jobs, steps |
| | | • dbt testing in CI: Run tests on every PR |
| | | • Deployment patterns: Blue-green, canary for data |
| 10:25 – 10:45 | **ACTIVITY (20 min)** | **Create Your First CI Pipeline** |
| | | 1. Create `.github/workflows/data-pipeline-ci.yml` |
| | | 2. Configure dbt test step |
| | | 3. Add SQL linting step |
| | | 4. Push and watch it run |
| | | Bonus: Add deployment step |
| 10:45 – 10:55 | **DEBRIEF (10 min)** | Review successful/failed runs, discuss improvements |

**GitHub Actions Workflow Template:**
```yaml
# .github/workflows/data-pipeline-ci.yml

name: Data Pipeline CI

on:
  push:
    branches: [main, develop]
    paths:
      - 'dbt/**'
      - 'dags/**'
  pull_request:
    branches: [main]
    paths:
      - 'dbt/**'
      - 'dags/**'

env:
  DBT_PROFILES_DIR: ./dbt

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.10'
      
      - name: Install sqlfluff
        run: pip install sqlfluff
      
      - name: Lint SQL
        run: sqlfluff lint dbt/models --dialect databricks

  test:
    runs-on: ubuntu-latest
    needs: lint
    steps:
      - uses: actions/checkout@v4
      
      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.10'
      
      - name: Install dependencies
        run: |
          pip install dbt-databricks
          cd dbt && dbt deps
      
      - name: Run dbt tests
        env:
          DATABRICKS_HOST: ${{ secrets.DATABRICKS_HOST }}
          DATABRICKS_TOKEN: ${{ secrets.DATABRICKS_TOKEN }}
        run: |
          cd dbt
          dbt debug
          dbt test --select staging.*
      
      - name: Upload test results
        uses: actions/upload-artifact@v4
        if: always()
        with:
          name: dbt-test-results
          path: dbt/target/run_results.json

  deploy:
    runs-on: ubuntu-latest
    needs: test
    if: github.ref == 'refs/heads/main'
    steps:
      - uses: actions/checkout@v4
      
      - name: Deploy DAGs to Airflow
        run: |
          echo "Deploying to production..."
          # rsync dags/ production:/airflow/dags/
          # Or use Astronomer/MWAA deployment
```

**Key Takeaway:** *"If merging to main breaks production, your CI is incomplete. Fail fast, fail in CI, not in production."*

---

#### 10:55 – 11:35 | Block 3: Documentation & Runbooks

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 10:55 – 11:05 | **LECTURE (10 min)** | **Documentation That Actually Gets Used** |
| | | • README: Quick start for new team members |
| | | • Data dictionary: What does each column mean? |
| | | • Runbook: What to do when things break |
| | | • Architecture diagrams: One picture, thousand words |
| | | • Decision logs: Why we chose this approach |
| | | • dbt docs: Auto-generated lineage and descriptions |
| 11:05 – 11:25 | **ACTIVITY (20 min)** | **Create Your Runbook** |
| | | Complete the runbook template for your pipeline: |
| | | • What monitors exist? |
| | | • What alerts fire when? |
| | | • Common failures and fixes |
| | | • Escalation path |
| 11:25 – 11:35 | **DEBRIEF (10 min)** | Share best runbook sections, integrate feedback |

**Runbook Template:**

```markdown
# [Pipeline Name] Runbook

## Overview
Brief description of what this pipeline does and why it matters.

## Key Contacts
| Role | Name | Contact |
|------|------|---------|
| Pipeline Owner | | |
| Data Platform Team | | |
| Business Stakeholder | | |

## Monitoring

### Dashboards
- [Pipeline Dashboard](link)
- [Data Quality Dashboard](link)

### Alerts
| Alert | Severity | Meaning | Action |
|-------|----------|---------|--------|
| Pipeline Failed | Critical | DAG did not complete | See troubleshooting below |
| SLA Miss | Warning | Pipeline slower than expected | Check source delays |
| Data Quality | Warning | dbt tests failed | Review test results |

## Troubleshooting

### Issue: API Extraction Failed
**Symptoms:** `extract_api` task shows red in Airflow
**Likely Causes:**
1. API rate limit exceeded
2. API endpoint changed
3. Authentication expired

**Resolution Steps:**
1. Check Airflow logs for specific error
2. If rate limit: Wait 1 hour, manually retry
3. If auth: Refresh token in Airflow Connections
4. If endpoint: Contact data source owner

### Issue: dbt Tests Failing
**Symptoms:** `dbt_test` task red
**Resolution:**
1. Run `dbt test` locally to see failures
2. Check if source data changed
3. If legitimate data issue: Contact upstream
4. If test too strict: Adjust threshold with approval

### Issue: Pipeline Running Slowly
**Symptoms:** Duration 2x normal
**Resolution:**
1. Check cluster sizing
2. Review recent model changes
3. Check source data volume spike

## Rollback Procedure
1. Identify last good run from Airflow history
2. Truncate Gold tables
3. Re-run from last good checkpoint
4. Verify data quality with test script
```

**Key Takeaway:** *"The best time to write a runbook is before you need it. The second best time is now."*

---

#### 11:35 – 12:15 | Block 4: Teaching Adaptation Workshop

**10-20-10 Structure:**

| Time | Type | Content |
|------|------|---------|
| 11:35 – 11:45 | **LECTURE (10 min)** | **From Practitioner to Educator** |
| | | • Scaffolding: Build on what students know |
| | | • Cognitive load: One concept at a time |
| | | • Worked examples: Show, then do |
| | | • Common misconceptions: What trips students up? |
| | | • Assessment: How do you know they learned? |
| | | • ITE student context: Practical, industry-relevant |
| 11:45 – 12:05 | **ACTIVITY (20 min)** | **Create Your First Lesson Plan** |
| | | Pick ONE topic from this week. Create: |
| | | 1. Learning objective (specific, measurable) |
| | | 2. 10-minute mini-lecture outline |
| | | 3. 20-minute student activity |
| | | 4. Assessment: How do you check understanding? |
| | | Use the 10-20-10 structure! |
| 12:05 – 12:15 | **DEBRIEF (10 min)** | Gallery walk: View other lesson plans, vote on best |

**Lesson Plan Template:**

| Section | Your Content |
|---------|--------------|
| **Topic** | |
| **Duration** | 40 minutes (10-20-10) |
| **Learning Objective** | By the end of this lesson, students will be able to... |
| **Prerequisites** | What students must already know |
| **10 min LECTURE** | Key points (max 3): |
| | 1. |
| | 2. |
| | 3. |
| **20 min ACTIVITY** | What students will DO: |
| | Expected outcome: |
| **10 min DEBRIEF** | Questions to ask: |
| | Common errors to address: |
| **Assessment** | How you'll know they learned: |
| **Materials** | What you need: |

**Key Takeaway:** *"You don't really understand something until you can teach it. Teaching makes you a better engineer."*

---

#### 12:15 – 12:30 | Morning Wrap-Up (15 mins)

| Activity | Details |
|----------|---------|
| Production deployment check | "Who has pushed to production?" |
| Afternoon preview | "Capstone presentations after lunch!" |
| Questions before presentations | Last chance clarifications |

---

### 12:30 – 1:30 PM | 🍽️ Lunch Break (60 mins)

*Facilitator: Set up presentation area, test screen sharing*

---

### Afternoon Session: Showcase & Synthesis (1:30 PM – 5:00 PM)

---

#### 1:30 – 3:00 | Capstone Presentations (90 mins)

**Format:** Each team presents their capstone project

| Team | Time | Format |
|------|------|--------|
| Each team | 8 mins | 5 min presentation + 3 min Q&A |
| Total teams | ~10 | 80 mins + buffer |

**Presentation Requirements:**

| Section | Duration | Content |
|---------|----------|---------|
| **Problem Statement** | 1 min | What business problem does this solve? |
| **Architecture** | 1 min | Show the diagram (Bronze → Gold) |
| **Demo** | 2 min | Trigger DAG, show data flowing |
| **Challenges & Solutions** | 1 min | What was hardest? How did you solve it? |

**Evaluation Rubric:**

| Criteria | Excellent (4) | Good (3) | Needs Work (2) | Incomplete (1) |
|----------|---------------|----------|----------------|----------------|
| **Technical Completeness** | All layers working, tested | Minor gaps | Major gaps | Not functional |
| **Code Quality** | Clean, documented, CI passing | Minor issues | Significant issues | Not reviewed |
| **Presentation** | Clear, confident, good demo | Minor hitches | Hard to follow | Unprepared |
| **Teaching Potential** | Ready to adapt for students | Some adaptation needed | Major simplification needed | Not suitable |

**Feedback Format:** (Written on cards)
- 🌟 **One thing that impressed me:**
- 💡 **One suggestion for improvement:**

---

#### 3:00 – 3:15 | ☕ Afternoon Coffee Break (15 mins)

*Facilitator: Tally scores, identify winning team*

---

#### 3:15 – 4:00 | Lab 4: Curriculum Development Workshop (45 mins)

**Objective:** Create teaching materials for your institution

| Time | Activity |
|------|----------|
| 3:15 – 3:25 | **Facilitator Demo:** Model lesson delivery |
| 3:25 – 4:00 | **Team Work:** Create curriculum modules |

**Curriculum Output Requirements:**

Each team creates materials for ONE topic they'll teach:

| Deliverable | Template |
|-------------|----------|
| **Lesson Plan** | 10-20-10 format (completed earlier) |
| **Slides (5-7)** | Key concepts with visuals |
| **Hands-on Lab** | Step-by-step student worksheet |
| **Assessment** | 3-5 quiz questions + 1 practical task |
| **Resources** | Further reading links |

**Simplified Student Lab Template:**
```markdown
# Lab: [Topic]

## Objective
By completing this lab, you will be able to...

## Prerequisites
- [x] Completed previous lab
- [x] Access to [tools]

## Estimated Time
30-45 minutes

## Instructions

### Step 1: Setup
1. Open your terminal
2. Navigate to `/workshop/lab-X`
3. Verify environment: `python --version`
`

### Step 2: [First Task]
**What you'll do:** [Description]

**Commands:**
```bash
[exact commands]
```

**Expected output:**
```
[what they should see]
```

⚠️ **Common Error:** If you see [error], try [solution]

### Step 3: [Second Task]
...

## Checkpoint Questions
1. What does [concept] do?
2. Why is [practice] important?
3. How would you modify the code to [variation]?

## Submission
Save your output to `lab-X-output.txt` and submit via LMS.
```

**Checkpoint @ 4:00:** *"Show your lesson plan + one lab worksheet"*

---

#### 4:00 – 4:30 | Final Synthesis & Integration (30 mins)

**Bringing It All Together:**

| Time | Activity |
|------|----------|
| 4:00 – 4:10 | **Architecture Review:** Full journey wall (sticky notes journey) |
| 4:10 – 4:20 | **Knowledge Check:** Final quiz (10 questions, all days) |
| 4:20 – 4:30 | **Resource Sharing:** Export all materials |

**Final Quiz (Quick-Fire):**

1. What's the difference between ETL and ELT?
2. Name the three layers of Medallion Architecture.
3. What does `dbt test` do?
4. Write a cron expression for "every weekday at 7 AM"
5. What's a data contract?
6. When should you use a Client Component in Next.js?
7. What does `trigger_rule='all_success'` mean in Airflow?
8. Name two types of dbt tests.
9. What information goes in a runbook?
10. What's the 10-20-10 rule?

**Resource Package Delivered:**

| Resource | Format |
|----------|--------|
| All workshop materials | USB drive + cloud link |
| Capstone project code | GitHub repository access |
| Template repository | Fork-ready for students |
| Slide decks (editable) | PowerPoint/Google Slides |
| Lab worksheets | Word/Markdown |
| Assessment question bank | Excel |
| Tool setup guides | PDF |

---

#### 4:30 – 4:50 | Closing Ceremony (20 mins)

| Activity | Details |
|----------|---------|
| **Recognition** | Awards for Best Capstone, Best Presenter, Most Improved |
| **Certificates** | Completion certificates distributed |
| **Testimonials** | Volunteers share key takeaways (video if permitted) |
| **Group Photo** | Workshop cohort photo |

**Award Categories:**

| Award | Criteria |
|-------|----------|
| 🏆 **Best Capstone** | Highest rubric score |
| 🎤 **Best Presenter** | Audience vote |
| 🚀 **Most Improved** | Biggest growth from Day 1 |
| 💡 **Best Teaching Adaptation** | Best lesson plan |
| 🔧 **Most Resilient** | Best error handling |

---

#### 4:50 – 5:00 | Final Closing & Next Steps (10 mins)

| Activity | Details |
|----------|---------|
| **What's Next** | Post-workshop support channels |
| **Feedback Form** | Complete workshop survey (5 mins) |
| **Final Words** | Facilitator closing message |

**Post-Workshop Support:**

| Resource | Details |
|----------|---------|
| **Slack Channel** | Stay connected: `#ite-data-engineering-trainers` |
| **Office Hours** | Monthly virtual Q&A sessions |
| **GitHub Discussions** | Template repository discussions |
| **Email Support** | 30 days post-workshop support |

**Next Steps for Trainers:**

1. **Week 1:** Finalize curriculum adaptation
2. **Week 2:** Test environment setup at your institution
3. **Week 3:** Pilot lesson with small group
4. **Week 4:** Iterate based on feedback
5. **Month 2:** Full course delivery

---

## 🛠️ Day 5 Toolkit

### Materials Distributed

| Item | Format |
|------|--------|
| Production checklist | Laminated card |
| Runbook template | A4 printout |
| Lesson plan template | A4 printout |
| Lab worksheet template | Digital (editable) |
| Certificate of Completion | Printed |

### Resources Provided

| Resource | Access |
|----------|--------|
| GitHub template repository | Fork access granted |
| Slide deck templates | Google Slides / PPTX |
| Assessment question bank | Excel export |
| dbt project starter | GitHub download |
| Airflow DAG templates | GitHub download |

---

## 👨‍🏫 Facilitator Guide - Day 5

### Critical Moments

| Time | Watch For | Intervention |
|------|-----------|--------------|
| 10:30 | GitHub Actions failures | Provide working workflow file |
| 2:00 | Presentation nerves | Provide timer, encourage |
| 3:30 | Curriculum block | Show completed example |
| 4:45 | Running late | Shorten final activities |

### Common Day 5 Issues

| Issue | Solution |
|-------|----------|
| CI/CD secrets not working | Use demo secrets temporarily |
| Presentation equipment fails | Have backup laptop ready |
| Curriculum too complex | Focus on ONE lesson plan |
| Missing materials | Digital backups ready |

### End-of-Day Success Criteria

- [ ] All capstone projects presented
- [ ] CI/CD configured for production
- [ ] Runbook documented
- [ ] At least one lesson plan per team
- [ ] Feedback forms completed
- [ ] Resources distributed

---

## 📊 Workshop Complete - Architecture Summary

```
WEEK JOURNEY:

Day 1: 🏗️ Foundations
       ├── Environment Setup
       ├── Tool Installation
       └── Capstone Kickoff

Day 2: 📥 Ingestion
       ├── Multi-Source Extraction
       ├── Data Contracts
       └── Bronze Layer

Day 3: 🔄 Transformation
       ├── dbt Fundamentals
       ├── Data Quality Testing
       ├── Silver + Gold Layers
       └── Star Schema

Day 4: 🤖 Orchestration
       ├── Airflow DAGs
       ├── Scheduling
       ├── Error Handling
       └── Monitoring Dashboard

Day 5: 🚀 Production
       ├── CI/CD Pipeline
       ├── Documentation
       ├── Capstone Presentations
       └── Curriculum Creation

OUTPUT: Production-Ready Data Pipeline + ITE Teaching Materials
```

---

## 📝 Post-Workshop Feedback Form

*(To be completed before leaving)*

| Question | Rating 1-5 | Comments |
|----------|------------|----------|
| Overall workshop quality | | |
| Facilitator effectiveness | | |
| Hands-on lab usefulness | | |
| Materials quality | | |
| Preparedness to teach | | |
| Would recommend to colleagues | | |

**Open-ended:**
1. What was the most valuable thing you learned?
2. What would you change about the workshop?
3. What additional support do you need?

---

## 🎓 Certificate of Completion

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│          CERTIFICATE OF COMPLETION                      │
│                                                         │
│    This certifies that                                  │
│                                                         │
│         [PARTICIPANT NAME]                              │
│                                                         │
│    has successfully completed the                       │
│                                                         │
│    ITE Singapore Data Pipelining Workshop               │
│    (5-Day Train the Trainer Program)                    │
│                                                         │
│    Competencies Achieved:                               │
│    ✓ Data Ingestion & Bronze Layer                     │
│    ✓ dbt Transformation & Testing                      │
│    ✓ Airflow Orchestration                             │
│    ✓ Production Deployment                             │
│    ✓ Curriculum Development                            │
│                                                         │
│    Date: [DATE]                                         │
│    Facilitator: [NAME]                                  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

*🎉 Congratulations! Workshop Complete.*

*You are now equipped to build production data pipelines AND teach the next generation of data engineers.*

---

*Return to: [Program Overview](./program-overview.md)*
