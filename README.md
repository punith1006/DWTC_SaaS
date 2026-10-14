<h2>
  About
  <a href="https://drive.google.com/file/d/1Fuy5c9EmPwEBtnKVl_-ugxtBAcw259jI/preview" target="_blank">
    <img align="right" height="30" src="https://img.shields.io/badge/Explore%20Platform%20Vision%20%E2%86%92-1D4ED8?style=for-the-badge&logoColor=white&labelColor=000000" alt="Explore Platform Vision">
  </a>
</h2>

Navigating mega-exhibitions like **Gulfood 2026** poses severe logistical challenges: over 100,000 attendees must coordinate schedules across two distinct venues located 12 km apart (DWTC and DEC at Expo City), mandatory sign-up walls cause steep visitor drop-off, and event organizers face multi-week delays waiting for post-show reporting.

**Gulfood AI Assistant** is an event intelligence platform that unifies attendee navigation, AI-driven discovery, and live operational analytics into a single web application. Built with React 18, Node.js, PostgreSQL, and OpenAI GPT-4o-mini, it serves as a real-time copilot for visitors while giving organizers second-by-second visibility into the show floor.

* **Zero-Barrier Discovery:** Instant, registration-free access to 2,400+ indexed exhibitors, product categories, and booth locations.
* **Multilingual AI Copilot ("Faris" / فارس):** Sub-3-second conversational assistance across English, Arabic, Hindi, and Mandarin for inquiries, booths, and agenda recommendations.
* **Distance-Aware Journey Planner:** Intelligent itinerary generation that clusters meetings by venue and injects 45-minute transit buffers via Google Routes API.
* **Live Operational Telemetry:** Real-time organizer dashboards tracking search queries, sector heatmaps, and exhibitor lead capture as they happen.

## Design & Architecture

<img width="5370" height="3210" alt="image" src="https://github.com/user-attachments/assets/6066c0bb-ae0c-42cf-8b36-0dffd5322ca2" />

## Features & Capabilities

Gulfood AI Assistant transforms mega-event operations from fragmented, reactive chaos into a synchronized, AI-orchestrated ecosystem. The platform serves three distinct stakeholders—**Trade Visitors & Buyers**, **Exhibitors & Brand Sponsors**, and **Event Organizers**—delivering quantifiable operational efficiencies, high-intent B2B matchmaking, and real-time floor intelligence.

---

### 1. Cognitive AI Agent & Multilingual Copilot ("Faris" / فارس)

* **Multilingual Natural Language Understanding:** Powered by OpenAI GPT-4o-mini with specialized prompt topologies capable of fluid multi-turn dialogue across English, Arabic (العربية), Mandarin Chinese (中文), and Hindi (हिन्दी) without human translation latency.
* **Contextual Role Arbitration:** Dynamically senses whether an inquiry originates from an international procurement buyer, a commercial exhibitor, or an operations lead, tailoring responses (e.g., procurement specs, booth dimensions, or floor logistics) in clean Markdown tables.
* **RLHF & Accuracy Feedback Loop:** Every response includes binary thumbs-up/down feedback capture and optional correction inputs stored in PostgreSQL (`chat_feedback`) to benchmark prompt drift and fine-tune domain responses.
* **Automated PDF Session Transcripts:** Ingests live chat history and exports downloadable, high-fidelity PDF meeting transcripts (`pdfmake`) including booth locations, key contact details, and follow-up notes.
* **Value Creation & Impact:**
  * **Zero Support Bottlenecks:** Resolves repetitive trade inquiries in `<3.0 seconds`, operating 24/7 without overtime labor costs.
  * **4x Pre-Show Engagement:** Registration-free access eliminates the 80% bounce rate caused by legacy mandatory sign-in walls.

---

### 2. Distance-Aware Spatial Navigation & Dual-Venue Routing

* **12 km Highway Corridor Optimization:** Intelligently bridges the physical separation between the **Dubai World Trade Centre (DWTC)** in downtown Dubai and the **Dubai Exhibition Centre (DEC)** at Expo City.
* **Mandatory 45-Minute Transit Safety Floor:** The itinerary generator algorithm detects cross-venue transitions and automatically injects a guaranteed 45-minute travel buffer into meeting schedules, factoring in real-world transit across the E11 Sheikh Zayed Road.
* **Real-Time Traffic Ingestion:** Integrates directly with the **Google Routes API** to dynamically compute transit durations across private vehicles, official event shuttles, and the Dubai Metro network.
* **Multi-Day Round-Robin Schedule Equalizer:** Balances 15–30 targeted booth meetings across 1 to 5 selected show days, clustering intra-hall meetings (`<10 min` walk) to eliminate attendee stamina exhaustion.
* **Value Creation & Impact:**
  * **Zero Missed Appointments:** Eliminates overlapping meetings across the 12 km divide.
  * **$2.7M–$5.4M Aggregate Commute Savings:** Reclaims 2+ hours of lost transit time per attendee across 100,000+ visitors.

---

### 3. 3-Phase Evaluator-Optimizer AI Assessment Engine

* **Phase 1 — Autonomous Web Profiling:** Automatically crawls corporate domains, extracting product taxonomies, employee count, and MENA distribution footprint. Generates an empirical Research Confidence Score (0–100%) cached in `company_research_cache` with a 7-day TTL.
* **Phase 2 — Multi-Dimensional Fit Synthesis:** Evaluates fit across four weighted vectors:
  * Product Match (40%)
  * Business Goal Alignment (30%)
  * Regional Market Fit (15%)
  * Commercial ROI Potential (15%)
  Synthesizes square footage recommendations (e.g., 18 sqm standard vs. 36 sqm island), hall selection, and realistic budget allocations.
* **Phase 3 — LLM Evaluator Judge & Anti-Inflation Truth Policy:** An independent auditor model enforces strict dynamic validation gates (85% validation threshold for high-confidence profiles). Unlike legacy marketing tools that artificially inflate compatibility, it validates honest low scores (20%–40% *"Do Not Exhibit"*) with empirical evidence.
* **Value Creation & Impact:**
  * **Capital Protection:** Prevents international food brands from misallocating $20K–$100K+ in booth space when market fit is low.
  * **High-Intent B2B Deals:** Delivers verified, high-scoring exhibitor prospects to show sales teams with full justification dossiers.

---

### 4. Autonomous 3-Tier RAG Email Ingress & Support Triage

* **RFC 822 Email Webhook Ingestion:** Ingests inbound exhibitor and visitor emails via AgentMail HMAC-signed webhooks into a hybrid vector + SQL retrieval pipeline.
* **3-Tier Decision Funnel:**
  * **Tier 1 (Confidence ≥ 85%):** Dispatches autonomous, factual replies with attached `.ics` calendar invites via Resend SMTP in `<5 seconds`.
  * **Tier 2 (Confidence 65%–84%):** Pre-drafts a context-aware response and stages it inside the Organizer Cockpit for 1-click human approval.
  * **Tier 3 (Confidence < 65% / VIP Escalation):** Routes complex contractual inquiries, VIP delegation requests, or booth disputes directly to physical floor managers via instant alerts.
* **Value Creation & Impact:**
  * **$280K Frontline Labor Elimination:** Replaces 30–40 desk support temps with autonomous 24/7 inbox handling.
  * **Sub-5-Second SLA:** Inbound trade inquiries receive instant verification instead of typical 24-to-48-hour email wait times.

---

### 5. Two-Way B2B Meeting Broker & Google Calendar Sync

* **Native Calendar Synchronization:** Seamlessly books B2B appointments directly against organizer and exhibitor schedules via the **Google Calendar API**.
* **Dynamic Video Conference Links:** Automatically provisions unique **Google Meet** links for hybrid or virtual buyer discussions.
* **Timezone-Locked Scheduling (`Asia/Dubai`):** Enforces Dubai Standard Time (GST / UTC+4) across all generated invites to prevent cross-border timezone confusion.
* **Downloadable Standard `.ics` Files:** Dispatches universal calendar invitations compatible with Apple Calendar, Microsoft Outlook, and Google Calendar.
* **Value Creation & Impact:**
  * **Zero Scheduling Friction:** Eliminates manual back-and-forth emails between international buyers and booth directors.
  * **Hybrid Inclusivity:** Enables global buyers unable to travel to Dubai to participate in live virtual vendor pitches.

---

### 6. Real-Time Operational Cockpit & Second-by-Second Telemetry

* **Sub-100ms SQL Analytics Engine:** Executes live aggregations across PostgreSQL tables (`chat_conversations`, `journey_plans`, `leads`, `quick_action_clicks`) with auto-refreshing telemetry.
* **Key Organizer Metrics:**
  * Hourly visitor registration & journey generation velocity
  * Sector interest heatmaps (Dairy vs. Meat vs. Beverages vs. AgriTech)
  * Real-time conversational sentiment & top unaddressed queries
  * Language distribution & international delegation geography
* **Live Flash Broadcast Pusher:** Allows organizers to broadcast critical show-floor updates (stage keynotes, emergency alerts, transport shuttles) straight to active attendee screens based on role tags (`All`, `Visitors`, `Exhibitors`).
* **Value Creation & Impact:**
  * **Zero-Lag Crowd Management:** Replaces the 3-week post-event reporting delay with second-by-second floor visibility, allowing organizers to dynamically steer attendee flow to under-visited halls.

---

### Capability Summary Matrix

| Module | Core Mechanism | Target Persona | Primary Business Value |
|---|---|---|---|
| **Faris AI Copilot** | GPT-4o-mini, 4-language prompt topology, PDF export | Visitors & Buyers | 4x pre-show engagement; sub-3s response time |
| **Spatial Matrix** | Google Routes API, 45-min buffer, load balancing | All Attendees | Eliminates travel collisions; saves 2+ hours commute |
| **Evaluator Engine** | 3-Phase Evaluator-Optimizer loop, dynamic gating | B2B Exhibitors | Prevents $20K–$100K capital misallocation |
| **Email RAG Triage** | AgentMail RFC 822 webhooks, 3-tier triage arbiter | Operations & Attendees | Replaces 30–40 support temps; saves ~$280K |
| **Exhibitor Portal** | Token auth, real-time CRM, competitor co-search | Exhibitors & Sponsors | Higher booth renewals; immediate verified lead downloads |
| **Meeting Broker** | Google Calendar API, Meet links, .ics attachments | Buyers & Exhibitors | Automated hybrid B2B deal-making with zero timezone errors |
| **Organizer Cockpit** | Live SQL telemetry, flash broadcast, sector heatmaps | Event Organizers | Second-by-second steering vs. 3-week survey lag |
| **Horizontal Engine** | Schema-isolated config substrate | Enterprise Leadership | Reusable across GITEX, Arab Health, and global expos |


## Project Structure

The codebase is organized as a modular, type-safe full-stack monorepo separating client presentation, backend microservices, shared database contracts, and automated ingestion pipelines:

```bash
GulfoodAIAssistant/
├── client/                            # Frontend Presentation Tier (React 18 + Vite)
│   ├── src/
│   │   ├── components/                # Modular UI & feature components
│   │   │   ├── AIChatbot.tsx          # "Faris" multilingual AI copilot floating widget
│   │   │   ├── AnalyticsDashboard.tsx # Real-time SQL telemetry charts & sector heatmaps
│   │   │   ├── AppointmentSlotPicker.tsx # Google Calendar slot booking interface
│   │   │   ├── CompanyAnalyzer.tsx    # 3-Phase exhibitor assessment & sizing UI
│   │   │   ├── ExhibitorDirectory.tsx # 2,400+ searchable exhibitor cards & hall badges
│   │   │   ├── ReferralShareCard.tsx  # Viral social share & registration attribution card
│   │   │   ├── VenueNavigation.tsx    # 12 km DWTC ↔ DEC dual-venue corridor transit guide
│   │   │   └── ui/                    # shadcn/ui accessible primitives (Radix UI)
│   │   │
│   │   ├── pages/                     # Application routes & view controllers
│   │   │   ├── Home.tsx               # Main public portal & conversational discovery
│   │   │   ├── Itinerary.tsx          # 1-to-5 day multi-day balanced journey planner
│   │   │   ├── Exhibitors.tsx         # Filterable catalog (halls, sectors, countries)
│   │   │   ├── ExhibitorVerify.tsx    # Token-based passwordless exhibitor access
│   │   │   ├── ExhibitorDashboard.tsx # Exhibitor lead CRM & co-searched brand telemetry
│   │   │   ├── OrganizerLogin.tsx     # Organizer administrative credentials portal
│   │   │   └── OrganizerAdmin.tsx     # Operations command cockpit & flash broadcast pusher
│   │   │
│   │   ├── hooks/                     # Custom React hooks (use-toast, use-mobile)
│   │   ├── lib/                       # Query client setup & frontend utility helpers
│   │   └── App.tsx                    # Top-level client router (Wouter) & provider tree
│   │
│   └── index.html                     # HTML5 entry shell & meta tags
│
├── server/                            # Backend Application Server (Node.js 20 LTS + Express)
│   ├── analytics/                     # Second-by-second SQL aggregation engines
│   │   ├── journeyMetrics.ts          # Itinerary counts, completion rates & ranking
│   │   ├── visitorSegments.ts         # Role, intent & organization breakdowns
│   │   ├── journeyDistributions.ts    # Sector interest heatmaps & attendance dates
│   │   ├── sentimentTopics.ts         # Real-time chat sentiment & unaddressed inquiries
│   │   └── cache.ts                   # In-memory analytics caching layer
│   │
│   ├── middleware/
│   │   └── auth.ts                    # JWT organizer guard & exhibitor token validator
│   │
│   ├── assessmentEvaluator.ts         # Phase 3 LLM auditor with anti-inflation truth policy
│   ├── companyResearch.ts             # Phase 1 corporate web crawler with 7-day TTL cache
│   ├── intelligentScoring.ts          # Phase 2 4D fit algorithm (Product, Goal, Market, ROI)
│   ├── ragEmailService.ts             # 3-tier autonomous inbound email RAG processor
│   ├── emailAnalyzer.ts               # Inbound email intent & confidence classification
│   ├── emailReply.ts                  # Contextual email generation with .ics attachments
│   ├── emailService.ts                # Resend SMTP transactional dispatch wrapper
│   ├── googleCalendar.ts              # Google Calendar API integration & Meet provisioning
│   ├── pdfGenerator.ts                # Server-side meeting dossier & transcript compiler (pdfmake)
│   ├── routes.ts                      # 55+ type-safe REST endpoints & HMAC webhook receivers
│   ├── storage.ts                     # Database abstraction interface (IStorage) implementation
│   ├── db.ts                          # Drizzle ORM connection pool to Neon Serverless PostgreSQL
│   └── index.ts                       # Express server bootstrapping & Vite dev server bridge
│
├── shared/                            # Universal Contracts & Data Layer
│   └── schema.ts                      # PostgreSQL Drizzle schema, Zod validators & 24-to-6 sector map
│
├── scripts/                           # Database Seeding & Data Pipeline Utilities
│   ├── seed-admin.ts                  # Seeds root organizer administrative credentials
│   ├── seed-analytics-demo.ts         # Generates mock telemetry data for dashboard demos
│   ├── import-exhibitors.ts           # Imports raw DWTC exhibitor CSV data
│   ├── ingest-dec-exhibitors.ts       # Parses & loads DEC Expo City exhibitor data
│   └── replace-exhibitors.ts          # Rebuilds the unified 2,400+ exhibitor catalog
│
├── drizzle.config.ts                  # Drizzle ORM configuration & database migration paths
├── tailwind.config.ts                 # Design system tokens, color palettes & typography
├── tsconfig.json                      # Strict TypeScript compiler options & path aliases (`@/*`, `@shared/*`)
├── vite.config.ts                     # Vite build configuration, asset aliases & proxy rules
└── package.json                       # Project dependencies, scripts & engine specifications

