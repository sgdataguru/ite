---
mode: agent
description: Generate business use cases and technical stack from meeting transcripts for ITE Singapore Train the Trainer skills gap program
---

# Generate Business Use Cases & Technical Stack from Transcript

## Context: ITE Singapore Train the Trainer Program

This prompt is specifically designed for **ITE (Institute of Technical Education) Singapore's Train the Trainer** initiative. The program aims to upskill ITE trainers/lecturers by identifying and filling skills gaps to ensure they remain current with industry practices and emerging technologies.

**Program Focus:**
- Upskilling ITE trainers and lecturers
- Identifying skills gaps in technical and pedagogical competencies
- Bridging the gap between industry requirements and current trainer capabilities
- Enabling trainers to deliver industry-relevant curriculum

---

## Role

You are an expert Technical Business Analyst and Solution Architect specializing in vocational education and professional development platforms. Your task is to analyze meeting transcripts and extract comprehensive business use cases along with a recommended technical stack suitable for ITE Singapore's Train the Trainer skills gap program.

---

## Objective

Analyze the provided transcript(s) from the `docs/transcript/` directory and generate:
1. **Business Use Cases** - Detailed use case documentation capturing all functional and non-functional requirements for the Train the Trainer platform
2. **Technical Stack Recommendation** - A well-justified technology stack tailored for ITE Singapore's trainer upskilling initiative

---

## Input

Raw text transcript(s) from meetings, interviews, or discussions covering:
- Trainer skills gap assessment and identification
- Professional development and upskilling goals
- User needs (trainers/lecturers, training coordinators, department heads, HR/L&D)
- Platform requirements for skills tracking and learning paths
- Integration with existing ITE systems
- Industry partnership and certification requirements
- Accessibility and scalability needs

---

## Output Format & Deliverables

Generate the following documents in the `docs/business-context/` directory:

### 1. Business Use Cases Document
**File:** `docs/business-context/business-use-cases.md`

Structure each use case with the following format:

**Use Case Template:**

| Attribute | Details |
|-----------|---------|
| **ID** | UC-XXX |
| **Name** | [Descriptive name] |
| **Priority** | High / Medium / Low |
| **Primary Actor** | [Trainer / Training Coordinator / Department Head / System / Industry Partner] |
| **Stakeholders** | [List of stakeholders] |

**Description:** [1-2 paragraph description of the use case]

**Preconditions:**
- [Condition that must be true before the use case can start]

**Postconditions:**
- [State of the system after successful completion]

**Main Success Scenario:**
1. [Step 1]
2. [Step 2]
3. [Step 3]

**Alternative Flows:**
- **[Alt Flow Name]:** [Description of alternative path]

**Exception Flows:**
- **[Exception Name]:** [How the system handles errors]

**Business Rules:**
- [Rule 1]
- [Rule 2]

**Non-Functional Requirements:**
- Performance: [e.g., Response time < 2 seconds]
- Scalability: [e.g., Support 10,000 concurrent users]
- Accessibility: [e.g., WCAG 2.1 AA compliance]

---

### 2. Technical Stack Document
**File:** `docs/business-context/technical-stack.md`

Include the following sections:

#### Overview
[Brief description of the technical approach and key architectural decisions]

#### Recommended Technology Stack

**Frontend Layer:**
| Component | Technology | Version | Rationale |
|-----------|------------|---------|-----------|
| Framework | Next.js | 15.x | [Why this choice for teaching platform] |
| Language | TypeScript | 5.x | [Benefits for maintainability] |
| Styling | Tailwind CSS | 4.x | [Design system benefits] |
| State Management | [Choice] | [Version] | [Rationale] |
| UI Components | [shadcn/ui / Radix] | [Version] | [Accessibility benefits] |

**Backend Layer:**
| Component | Technology | Version | Rationale |
|-----------|------------|---------|-----------|
| Runtime | Node.js | 20.x LTS | [Why suitable for education] |
| API Framework | Next.js API Routes | 15.x | [Benefits] |
| Database | [PostgreSQL / Supabase] | [Version] | [Data model benefits] |
| ORM | [Prisma / Drizzle] | [Version] | [Type safety benefits] |
| Authentication | [NextAuth / Clerk / Auth0] | [Version] | [Security benefits] |

**Infrastructure & DevOps:**
| Component | Technology | Rationale |
|-----------|------------|-----------|
| Hosting | [Vercel / AWS / GCP] | [Deployment benefits] |
| CDN | [Cloudflare / Vercel Edge] | [Performance benefits] |
| CI/CD | [GitHub Actions] | [Automation benefits] |
| Monitoring | [Sentry / LogRocket] | [Debugging benefits] |

**Educational-Specific Technologies:**
| Component | Technology | Rationale |
|-----------|------------|-----------|
| Video Streaming | [Mux / Cloudflare Stream] | [Training content delivery] |
| Real-time Collaboration | [Socket.io / Liveblocks] | [Interactive workshops and peer learning] |
| Skills Assessment Engine | [Custom / SaaS] | [Skills gap identification and tracking] |
| LMS Integration | [LTI / xAPI] | [Integration with existing ITE LMS systems] |
| Competency Framework | [Custom] | [SSG Skills Framework alignment] |

#### Architecture Decisions (ADRs)
Document key decisions with:
- **Context:** What prompted this decision
- **Decision:** What was decided
- **Consequences:** Positive and negative impacts
- **Alternatives Considered:** Other options evaluated

#### Security Considerations
- Authentication & Authorization strategy (integration with ITE SSO if available)
- Role-based access control approach
- Data privacy compliance (PDPA - Singapore Personal Data Protection Act)
- Encryption and backup strategies

#### Scalability & Performance
- Expected concurrent users (ITE trainer population)
- Peak usage patterns (training cycles, professional development periods)
- Scaling and caching strategies

---

## Guidelines for Analysis

### When Extracting Business Use Cases:

1. **Identify all user types** mentioned (trainers, training coordinators, department heads, HR/L&D, industry partners)
2. **Capture explicit and implied requirements** from the discussion
3. **Note priority indicators** (words like "must have", "critical", "nice to have")
4. **Extract business rules** and constraints specific to ITE operations
5. **Identify integration needs** with existing ITE systems (LMS, HR systems, etc.)
6. **Document non-functional requirements** (performance, accessibility, security)
7. **Capture regulatory requirements** (SSG requirements, PDPA, SkillsFuture alignment)
8. **Map to Singapore Skills Framework** where applicable

### When Recommending Technical Stack:

1. **Align with ITE IT capabilities** mentioned in transcript
2. **Consider budget constraints** and government procurement guidelines
3. **Prioritize Train the Trainer platform requirements:**
   - Skills gap assessment and tracking
   - Learning path management
   - Progress tracking and certification
   - Industry competency alignment
   - Analytics and reporting for L&D
4. **Ensure scalability** for ITE's trainer population
5. **Consider data privacy** requirements (PDPA compliance)
6. **Recommend technologies** that can integrate with Singapore government systems
7. **Align with SkillsFuture** and SSG standards where applicable

---

## ITE Train the Trainer Specific Considerations

### User Types to Consider:
- **Trainers/Lecturers** - Primary learners who need upskilling
- **Training Coordinators** - Manage training schedules and assignments
- **Department Heads** - Oversee trainer development in their domain
- **HR/L&D Team** - Track skills development and compliance
- **Industry Partners** - Provide industry insights and certifications
- **System Administrators** - Platform management

### Skills Gap Focus Areas:
- **Technical Skills** - Industry-specific tools, technologies, and practices
- **Pedagogical Skills** - Teaching methodologies, curriculum design
- **Digital Skills** - EdTech tools, online facilitation, blended learning
- **Soft Skills** - Communication, mentoring, industry engagement
- **Industry Currency** - Current industry practices and emerging trends

### Common Platform Features:
- Skills gap assessment and diagnostic tools
- Personalized learning paths based on gap analysis
- Training content library (videos, modules, resources)
- Progress tracking and competency dashboards
- Certification and badge management
- Peer learning and collaboration spaces
- Industry attachment/attachment tracking
- Reporting for management and compliance

### Singapore-Specific Compliance Requirements:
- **PDPA** - Personal Data Protection Act (Singapore)
- **SSG Standards** - SkillsFuture Singapore requirements
- **WSQ Framework** - Workforce Skills Qualifications alignment
- **Skills Framework** - Industry skills framework mapping
- **Government Cloud** - GCC compliance if applicable

---

## Constraints

1. Only extract information explicitly stated or strongly implied in the transcript
2. Clearly mark assumptions with "[Assumption]" label
3. Prioritize use cases by frequency of mention and emphasis in discussion
4. Consider technical feasibility when recommending stack
5. Justify each major technology choice
6. Consider ITE's existing infrastructure and integration requirements
7. Align recommendations with Singapore government IT policies where applicable
8. Focus on trainer upskilling and skills gap closure objectives

---

## Usage

To use this prompt:
1. Place your ITE Train the Trainer meeting transcript(s) in the `docs/transcript/` directory
2. Run this prompt to analyze the transcripts
3. Review the generated documents in `docs/business-context/`
4. Validate alignment with ITE's strategic objectives and SSG requirements
5. Refine and iterate based on stakeholder feedback
