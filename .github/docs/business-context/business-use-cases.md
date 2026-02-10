# Business Use Cases

## ITE Singapore - Train the Trainer Program
### Higher Nitec in Data Engineering Curriculum Upskilling

---

## Executive Summary

ITE (Institute of Technical Education) Singapore is undertaking a strategic initiative to revise the **Higher Nitec in Data Engineering** curriculum to align with the latest industry DACUM (Developing A Curriculum) standards and SkillsFuture Singapore competencies. The updated curriculum places strong emphasis on modern data pipelining, end-to-end data solutions, and data security & governance—areas currently under-represented in existing modules.

To ensure successful curriculum delivery, ITE requires a **customized, hands-on Train the Trainer program** for their lecturers. The program will enable ITE lecturers to confidently teach the updated curriculum with current industry tools and practices. The training will be delivered face-to-face at ITE premises, with an ideal class size of 12-15 participants per session.

The initiative spans three priority training workshops, with two targeted for delivery in FY26 (February-March). The program addresses identified skills gaps in data automation, pipeline development, analytics platforms, and data governance—upskilling lecturers from basic-to-intermediate levels to industry-ready competencies.

---

## Stakeholder Analysis

| Stakeholder | Role | Interest |
|-------------|------|----------|
| ITE Lecturers | Primary learners | Gain skills to deliver updated curriculum |
| Ching (ITE Training Coordinator) | Program sponsor | Ensure budget alignment and training effectiveness |
| Department Heads | Oversight | Quality assurance and curriculum alignment |
| Mahesh (Training Provider) | Instructor/Consultant | Curriculum design and delivery |
| Marius/Marcus (Maltem) | Account Manager | Procurement, pricing, coordination |
| ITE Students | End beneficiaries | Receive industry-relevant education |

---

## Use Case Catalog

### UC-001: Data Pipelining & Orchestration Training

| Attribute | Details |
|-----------|---------|
| **ID** | UC-001 |
| **Name** | Data Pipelining & Orchestration Training Workshop |
| **Priority** | High (Highest Priority) |
| **Primary Actor** | ITE Lecturer |
| **Stakeholders** | Training Coordinator, Department Heads, Training Provider |

**Description:**
ITE lecturers participate in a hands-on workshop to learn production-grade ETL/ELT pipeline development, orchestration, monitoring, and CI/CD practices for data pipelines. This is the highest priority training area identified in the curriculum gap analysis, addressing the core technical competency required for the updated Higher Nitec in Data Engineering program.

**Preconditions:**
- Lecturers have basic-to-intermediate knowledge of database concepts and programming
- Training venue arranged at ITE premises
- Training materials and environment prepared by instructor
- Budget approved through GBS procurement

**Postconditions:**
- Lecturers can independently design, build, schedule and monitor production data pipelines
- Lecturers receive completion certification
- Course materials updated for student curriculum delivery

**Main Success Scenario:**
1. ITE coordinator confirms training dates and participant list
2. Instructor prepares customized curriculum with practical problem statements
3. Lecturers attend face-to-face training session (weekly format with theory + practical blocks)
4. Lecturers complete hands-on exercises building ETL/ELT pipelines
5. Lecturers practice pipeline monitoring, error handling, and retry logic
6. Lecturers implement CI/CD for data pipeline deployment
7. Assessment confirms competency achievement
8. Lecturers receive course completion documentation

**Alternative Flows:**
- **Extended Learning:** If lecturers require additional time, follow-up sessions can be scheduled
- **Remote Support:** Post-training WhatsApp/email support for questions

**Exception Flows:**
- **Participant Absence:** Catch-up materials provided; one-on-one session if needed
- **Technical Issues:** Backup cloud environment available

**Business Rules:**
- Class size must not exceed 15 participants (split into groups if larger)
- Training must be face-to-face at ITE premises
- Theory and practical blocks must be balanced to maintain engagement
- Procurement through GBS is required

**Non-Functional Requirements:**
- Performance: Hands-on lab environments must support all participants simultaneously
- Accessibility: Materials adapted for varying skill levels (basic-to-intermediate)
- Engagement: Monitor attention span throughout day-long sessions

---

### UC-002: Data Solutions & Analytics Platforms Training

| Attribute | Details |
|-----------|---------|
| **ID** | UC-002 |
| **Name** | Data Solutions & Analytics Platforms Workshop |
| **Priority** | High |
| **Primary Actor** | ITE Lecturer |
| **Stakeholders** | Training Coordinator, Department Heads, Training Provider |

**Description:**
ITE lecturers participate in training covering advanced BI & Analytics (Power BI + DAX, Tableau), low-code data application development (Power Apps, Streamlit, Retool), real-time dashboards, and predictive analytics basics. This enables lecturers to teach students how to build complete data solutions from problem statement to deployment.

**Preconditions:**
- UC-001 completed or equivalent pipeline knowledge
- Access to BI tools (Power BI, Tableau) and cloud analytics platforms
- Training venue arranged at ITE premises

**Postconditions:**
- Lecturers can design and build interactive dashboards with real-time data
- Lecturers can develop low-code data applications
- Lecturers understand predictive analytics and model deployment basics

**Main Success Scenario:**
1. Training coordinator schedules workshop following data pipelining training
2. Instructor prepares applied data-solution scenarios (business problem → solution)
3. Lecturers learn advanced Power BI/DAX and Tableau features
4. Lecturers build low-code applications using Power Apps/Streamlit
5. Lecturers create interactive dashboards with real-time data feeds
6. Lecturers explore Azure ML Designer or AWS SageMaker Canvas for predictive analytics
7. Practical assessment validates competency
8. Module materials updated with new tools and practices

**Alternative Flows:**
- **Tool Preference:** Can focus on specific platform (Microsoft vs AWS) based on ITE strategy
- **Vendor Credits:** Leverage education credits from Databricks/Snowflake if available

**Exception Flows:**
- **License Issues:** Use trial/education licenses for evaluation period
- **Platform Unavailability:** Switch to alternative cloud provider

**Business Rules:**
- Schema design (star/snowflake) concepts must be covered
- Training must address applied problem-solving (problem statement → feature identification → architecture)
- Balance theoretical concepts with hands-on practice

**Non-Functional Requirements:**
- Performance: Cloud environments must handle concurrent dashboard development
- Scalability: Training approach must be replicable for future cohorts

---

### UC-003: Data Security, Governance & Compliance Training

| Attribute | Details |
|-----------|---------|
| **ID** | UC-003 |
| **Name** | Data Security, Governance & Compliance Workshop |
| **Priority** | Medium (Target FY27 or late FY26) |
| **Primary Actor** | ITE Lecturer |
| **Stakeholders** | Training Coordinator, Department Heads, Training Provider, Compliance Team |

**Description:**
ITE lecturers learn data security fundamentals including data classification, encryption, IAM in cloud pipelines, data lineage, cataloguing, and governance tools. Training covers PDPA/GDPR compliance, secure handling of sensitive data, and ethical AI practices—ensuring lecturers can incorporate security and compliance into every module.

**Preconditions:**
- UC-001 and UC-002 completed or equivalent knowledge
- Understanding of cloud pipeline architectures
- Access to governance tools (Collibra/Purview basics)

**Postconditions:**
- Lecturers can teach data security and compliance as integral part of curriculum
- Lecturers understand Singapore PDPA requirements for data handling
- Lecturers can identify and address ethical AI concerns and bias detection

**Main Success Scenario:**
1. Training coordinator schedules governance workshop
2. Instructor covers data classification and encryption (at-rest & in-transit)
3. Lecturers learn IAM implementation in cloud pipelines
4. Lecturers practice data lineage and cataloguing with governance tools
5. Lecturers understand PDPA/GDPR compliance requirements
6. Lecturers learn secure handling of sensitive data in BI and low-code environments
7. Ethical AI practices and bias detection workshop conducted
8. Compliance assessment and certification provided

**Alternative Flows:**
- **Regulatory Focus:** Additional emphasis on Singapore-specific PDPA if required
- **Tool Selection:** Use Purview (Microsoft) or Collibra based on ITE platform strategy

**Exception Flows:**
- **Compliance Updates:** Training materials updated if regulations change
- **Tool Access:** Mock/sandbox environments for governance tools if production access unavailable

**Business Rules:**
- PDPA compliance must be emphasized for Singapore context
- Security practices must be integrated with previously learned pipeline concepts
- Ethical AI module mandatory for analytics curriculum

**Non-Functional Requirements:**
- Security: Training environment must not expose real sensitive data
- Compliance: All materials must align with SSG/SkillsFuture standards

---


---

## Skills Gap Summary

Based on transcript analysis, the following skills gaps were identified:

| Current State | Target State | Gap Area |
|---------------|--------------|----------|
| Basic-to-intermediate knowledge | Production-ready competency | Data Pipeline Development |
| Self-taught, limited industrial projects | Industry-aligned practices | Applied Data Solutions |
| Under-represented in curriculum | Integral to all modules | Data Security & Governance |
| Familiar with database concepts | Expert in modern architectures | Schema Design (Star/Snowflake) |
| Limited pipeline experience | CI/CD for data pipelines | DevOps for Data |

---

## Priority Alignment

| Use Case | Priority | Target FY | Budget Impact |
|----------|----------|-----------|---------------|
| UC-001 | Highest | FY26 (Feb-Mar) | Primary allocation |
| UC-002 | High | FY26 | Primary allocation |
| UC-003 | Medium | FY26/FY27 | Secondary allocation |


---

## Target Outcomes

By the end of the program, lecturers should be able to:
- Design, build, schedule and monitor production data pipelines independently
- Teach students how to build secure, governed BI solutions and low-code data apps
- Incorporate data security and compliance into every module
- Update module materials with current industry tools and practices

---

## Next Steps

1. **Immediate:** Ching to send detailed specification of training requirements
2. **Short-term:** Mahesh to prepare proposed lesson plan/curriculum
3. **Budget Review:** Mahesh and Marcus to review budget alignment
4. **Scheduling:** Target training delivery Feb-March FY26
5. **Procurement:** Process through GBS
6. **Communication:** Use WhatsApp for quick clarification, email for formal items
