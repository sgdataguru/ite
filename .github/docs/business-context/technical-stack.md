# Technical Stack Specification

## ITE Singapore - Train the Trainer Platform
### Higher Nitec in Data Engineering Curriculum Support

---

## Overview

This document specifies the recommended technology stack for ITE Singapore's Train the Trainer program supporting the Higher Nitec in Data Engineering curriculum. The stack is designed to:

1. **Enable Training Delivery** - Support hands-on workshops for data pipelining, analytics, and governance
2. **Align with Industry Standards** - Use tools that match DACUM and SkillsFuture Singapore competencies
3. **Integrate with ITE Systems** - Compatible with existing ITE infrastructure and GBS procurement
4. **Comply with Singapore Regulations** - PDPA compliance and government cloud standards

The platform supports both the training management aspects and the technical lab environments required for hands-on learning.

---

## Training Technology Stack

### Workshop 1: Data Pipelining & Orchestration

| Component | Technology | Version | Rationale |
|-----------|------------|---------|-----------|
| **Orchestration** | Apache Airflow | 2.x | Industry-standard for data pipeline orchestration; open-source, enterprise-ready |
| **Alternative Orchestration** | Azure Data Factory | Latest | If Microsoft ecosystem preferred; managed service reduces infrastructure overhead |
| **Pipeline Framework** | dbt (data build tool) | Latest | Modern ELT transformation; version control friendly; growing industry adoption |
| **Data Integration** | Apache Spark | 3.x | Scalable data processing; Databricks or Azure Synapse integration |
| **CI/CD** | GitHub Actions | Latest | Pipeline automation; integrates with Git-based development workflow |
| **Containerization** | Docker | Latest | Consistent development and deployment environments |
| **Cloud Platforms** | Azure / AWS | Latest | Multi-cloud readiness; both widely used in Singapore enterprises |

**Lab Environment Options:**

| Option | Technology | Rationale |
|--------|------------|-----------|
| Option A | Databricks Community Edition | Free tier for learning; industry-aligned; Spark integrated |
| Option B | Snowflake Education Account | Growing enterprise adoption; free credits for education |
| Option C | Azure Synapse Analytics | Microsoft ecosystem; strong in Singapore government sector |

---

### Workshop 2: Data Solutions & Analytics Platforms

| Component | Technology | Version | Rationale |
|-----------|------------|---------|-----------|
| **BI Platform (Primary)** | Microsoft Power BI | Latest | Strong enterprise adoption in Singapore; DAX for advanced analytics |
| **BI Platform (Alternative)** | Tableau | Latest | Industry standard; excellent visualization capabilities |
| **Low-Code Data Apps** | Microsoft Power Apps | Latest | Enterprise low-code platform; integrates with Power BI |
| **Low-Code Analytics** | Streamlit | Latest | Python-based; excellent for data science prototyping |
| **Low-Code Alternative** | Retool | Latest | Rapid internal tool development; database connectors |
| **Predictive Analytics** | Azure ML Designer | Latest | No-code ML; accessible for beginners; Microsoft ecosystem |
| **ML Alternative** | AWS SageMaker Canvas | Latest | No-code ML; AWS ecosystem option |
| **Schema Design** | Star/Snowflake Schema | N/A | Dimensional modeling fundamentals |

**Real-Time Dashboard Stack:**

| Component | Technology | Rationale |
|-----------|------------|-----------|
| Streaming | Azure Stream Analytics / Kafka | Event processing for real-time feeds |
| Cache | Redis | Low-latency data access for dashboards |
| Visualization | Power BI DirectQuery | Real-time without data duplication |

---

### Workshop 3: Data Security, Governance & Compliance

| Component | Technology | Version | Rationale |
|-----------|------------|---------|-----------|
| **Data Catalog** | Microsoft Purview | Latest | Azure-native; comprehensive data governance |
| **Data Catalog Alternative** | Collibra | Latest | Enterprise-grade; strong in governance features |
| **IAM** | Azure AD / AWS IAM | Latest | Cloud-native identity and access management |
| **Encryption** | TLS 1.3 / AES-256 | Latest | Industry-standard encryption at-rest and in-transit |
| **Data Lineage** | Apache Atlas / Purview | Latest | Track data flow through pipelines |
| **Compliance Monitoring** | Azure Policy / AWS Config | Latest | Automated compliance checking |
| **Ethical AI** | Fairlearn / AI Fairness 360 | Latest | Bias detection and mitigation |

---

## Training Management Platform (Optional)

If ITE requires a platform to manage training program administration:

### Frontend Layer

| Component | Technology | Version | Rationale |
|-----------|------------|---------|-----------|
| Framework | Next.js | 15.x | Server-first architecture; excellent performance; React ecosystem |
| Language | TypeScript | 5.x | Type safety for maintainable codebase |
| Styling | Tailwind CSS | 4.x | Rapid UI development; consistent design system |
| UI Components | shadcn/ui | Latest | Accessible components; customizable for ITE branding |
| State Management | React Server Components | 15.x | Minimal client-side state; server-first approach |

### Backend Layer

| Component | Technology | Version | Rationale |
|-----------|------------|---------|-----------|
| Runtime | Node.js | 20.x LTS | Stable LTS release; excellent ecosystem |
| API | Next.js API Routes | 15.x | Integrated with frontend; serverless-friendly |
| Database | PostgreSQL (Supabase) | 16.x | Open-source; row-level security for multi-tenant |
| ORM | Prisma | 5.x | Type-safe database access; excellent DX |
| Authentication | NextAuth.js | 5.x | Flexible auth; can integrate with ITE SSO |

### Infrastructure & DevOps

| Component | Technology | Rationale |
|-----------|------------|-----------|
| Hosting | Vercel | Optimal for Next.js; edge network in Singapore |
| Alternative Hosting | Azure App Service | If government cloud (GCC) required |
| Database Hosting | Supabase | Managed PostgreSQL; real-time features |
| CI/CD | GitHub Actions | Automated testing and deployment |
| Monitoring | Sentry | Error tracking and performance monitoring |
| Analytics | PostHog | Privacy-focused product analytics |

### Educational Features

| Component | Technology | Rationale |
|-----------|------------|-----------|
| Video Hosting | Cloudflare Stream | Cost-effective video delivery; performs well in Singapore |
| Document Storage | Supabase Storage / S3 | Course materials and resources |
| Skills Assessment | Custom (Next.js) | Tailored to ITE competency framework |
| Progress Tracking | Custom (Next.js + DB) | Aligned with SSG/SkillsFuture requirements |
| Notifications | Resend | Transactional email for training reminders |
| LMS Integration | LTI 1.3 | Integration with existing ITE LMS if needed |

---

## Architecture Decisions

### ADR-001: Multi-Cloud Lab Environment Strategy

- **Context:** ITE needs lab environments for hands-on training that align with industry tools while managing costs
- **Decision:** Provide training on multiple cloud platforms (Azure primary, AWS secondary) with emphasis on transferable concepts
- **Consequences:** 
  - Positive: Graduates are multi-cloud ready; matches diverse Singapore job market
  - Negative: Slightly higher training complexity; need to manage multiple environments
- **Alternatives Considered:** 
  - Single cloud (Azure only) - rejected as too limiting for job readiness
  - On-premises - rejected as not industry-aligned

### ADR-002: Power BI as Primary BI Tool

- **Context:** Need to select primary BI tool for analytics training module
- **Decision:** Use Microsoft Power BI as primary tool with Tableau as secondary exposure
- **Consequences:**
  - Positive: Strong enterprise adoption in Singapore; Microsoft ecosystem integration; DAX skills valuable
  - Negative: Tableau skills still demanded; may need supplementary content
- **Alternatives Considered:**
  - Tableau primary - rejected due to higher licensing costs for education
  - Metabase/Apache Superset - rejected as less enterprise adoption

### ADR-003: Use Managed Cloud Services for Training

- **Context:** Need to balance infrastructure management overhead with learning objectives
- **Decision:** Use managed services (Databricks, Azure Data Factory, Snowflake) over self-hosted alternatives
- **Consequences:**
  - Positive: Less setup time; focus on concepts not infrastructure; industry-aligned
  - Negative: Potential costs after free tier; some infrastructure concepts abstracted
- **Alternatives Considered:**
  - Self-hosted Airflow/Spark - rejected as too much overhead for training context

### ADR-004: Free/Education Tier Priority

- **Context:** Budget constraint (~5-6K total) requires cost-effective tooling
- **Decision:** Prioritize platforms with robust education/free tiers (Databricks Community, Snowflake Education, Azure Free Tier)
- **Consequences:**
  - Positive: Maximizes training value within budget; sustainable for ongoing learning
  - Negative: Some enterprise features unavailable; may need upgrade for advanced scenarios
- **Alternatives Considered:**
  - Full enterprise licenses - rejected due to budget constraints

---

## Security Considerations

### Authentication & Authorization

- **ITE SSO Integration:** If ITE has existing Single Sign-On, integrate via SAML or OAuth 2.0
- **Role-Based Access:** 
  - Lecturer (learner): Access to training materials and labs
  - Coordinator: Manage schedules, participants, reporting
  - Admin: Full platform management
- **Lab Environment Security:** Isolated sandboxed environments per participant

### Data Privacy Compliance (PDPA)

- **Data Classification:** Training participant data classified; PII minimized
- **Consent:** Explicit consent for data collection and processing
- **Data Retention:** Clear retention policies; delete after training completion unless consent given
- **Access Logging:** Audit trail for all data access
- **Cross-Border:** Ensure data remains in Singapore or approved jurisdictions

### Encryption Strategy

| Data Type | At Rest | In Transit |
|-----------|---------|------------|
| Participant Data | AES-256 | TLS 1.3 |
| Lab Credentials | Vault/Secrets Manager | TLS 1.3 |
| Training Materials | Storage encryption | HTTPS |

### Government Cloud Compliance (if applicable)

- Consider Azure GCC (Government Community Cloud) if required
- Ensure hosting providers meet G-Cloud standards if processing government data

---

## Scalability & Performance

### Expected Load

| Metric | Value | Notes |
|--------|-------|-------|
| Concurrent Participants | 12-15 per session | Max 15 per class, split if larger |
| Total Lecturer Population | ~100-500 (estimate) | Across all ITE campuses |
| Peak Usage | Training days | Concentrated during workshop sessions |
| Lab Environment Sessions | 15 concurrent | One per participant |

### Scaling Strategy

- **Horizontal:** Lab environments auto-scale based on active sessions
- **Vertical:** Use appropriately sized compute for training workloads
- **Caching:** Static training materials served via CDN
- **Database:** Connection pooling for concurrent access during assessment

### Performance Requirements

| Scenario | Requirement |
|----------|-------------|
| Lab Environment Spin-up | < 2 minutes |
| Dashboard Load | < 3 seconds |
| Pipeline Execution (demo) | Real-time visibility |
| Material Download | < 5 seconds for typical document |

---

## Integration Points

| System | Integration Type | Purpose |
|--------|-----------------|---------|
| ITE LMS | LTI 1.3 / API | Course enrollment, completion tracking |
| GBS Procurement | Manual/Process | Vendor payment and procurement |
| ITE HR System | [Assumption] Manual or API | Participant verification |
| SkillsFuture System | [Assumption] Manual/Export | Competency reporting |
| Cloud Vendors (Databricks/Snowflake) | API/Console | Lab environment provisioning |
| Email System | SMTP/API | Training notifications |

---

## Development Standards

### Code Quality (for custom platform development)

- **Linting:** ESLint with strict TypeScript rules
- **Formatting:** Prettier for consistent code style
- **Testing:** 
  - Jest + React Testing Library for unit tests
  - Playwright for E2E tests
- **Type Safety:** No `any` types; strict TypeScript mode

### Accessibility Standards

- WCAG 2.1 Level AA compliance
- Screen reader compatible
- Keyboard navigation support
- Color contrast minimum 4.5:1

### Documentation

- All training materials version-controlled
- API documentation for any integrations
- Runbooks for lab environment management

---

## Estimated Complexity

| Area | Complexity | Notes |
|------|------------|-------|
| Lab Environments | Medium | Multi-cloud provisioning; credential management |
| Training Content | Low-Medium | Subject matter expertise required; standard documentation |
| BI/Analytics Setup | Low | Managed services; standard configurations |
| Security/Governance | Medium | PDPA compliance; IAM across environments |
| LMS Integration | Medium | Depends on ITE system capabilities |
| Custom Platform (if built) | Medium-High | Full-stack development; ongoing maintenance |

---

## Cost Considerations

### Free/Education Tier Options

| Platform | Education Offering | Estimate |
|----------|-------------------|----------|
| Databricks | Community Edition | Free |
| Snowflake | Education Credits | Free (application required) |
| Azure | Free Tier / Education | Free/subsidized |
| Power BI | Desktop (free) / Pro trial | Free (Desktop) / ~$10/user/mo (Pro) |
| GitHub | Free for education | Free |

### Training Provider Costs

| Item | Baseline Rate | Notes |
|------|---------------|-------|
| Full Day Training | ~$1,100/day | Reference rate from discussion |
| Half Day Training | ~$550/day | If split sessions needed |
| Curriculum Development | TBD | One-time setup cost |

### Budget Alignment

- Available Budget: ~$5,000-6,000
- Recommended: Prioritize Workshop 1 & 2 in FY26; Workshop 3 in FY27
- Leverage vendor education credits to maximize training ROI

---

## Vendor Contacts & Resources

### Cloud Platforms (Education Programs)

| Vendor | Program | Contact |
|--------|---------|---------|
| Databricks | Education Licensing | education@databricks.com |
| Snowflake | Education Services | Maltem can connect via partner contacts |
| Microsoft Azure | Azure for Education | azure.com/education |
| AWS | AWS Educate | aws.amazon.com/education |

### Training Provider

| Role | Contact | Channel |
|------|---------|---------|
| Curriculum & Delivery | Mahesh | WhatsApp (quick), Email (formal) |
| Procurement & Pricing | Marius/Marcus (Maltem) | Email |

---

## Implementation Roadmap

### Phase 1: FY26 Q1 (February-March)

- [ ] Finalize training specifications
- [ ] Complete GBS procurement
- [ ] Deliver Workshop 1: Data Pipelining & Orchestration
- [ ] Evaluate and iterate

### Phase 2: FY26 Q2-Q3

- [ ] Deliver Workshop 2: Data Solutions & Analytics
- [ ] Apply for vendor education credits
- [ ] Evaluate need for custom training platform

### Phase 3: FY26 Q4 or FY27

- [ ] Deliver Workshop 3: Data Security & Governance
- [ ] Full curriculum rollout to students
- [ ] Continuous improvement and updates
