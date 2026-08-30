# AI & Automation Final Project – UrbanKitchen Customer Service Assistant

Final project for an AI & automation implementation course. The assignment: act as an AI implementation consultant for a company (from a set of provided client files), diagnose its systems and workflows, identify a business bottleneck worth solving with AI, design and build a working automation, define success metrics, and present a rollout plan — as if presenting to the client.

**Live client presentation:** https://sharonkamensky.github.io/ai-implementation-final-project/ (also in [`/docs/index.html`](./docs/index.html))
**Live Make scenario (view-only):** https://eu1.make.com/public/shared-scenario/DXwtum02BQ2/urban-kitchen-ai-customer-service-assis

> All company names, people and data in this project — UrbanKitchen included — are fictional and were created for the course assignment.

## The assignment

The course provided several client case files, each describing a fictional company's systems, people and pain points (simulating the discovery interviews an implementation consultant would run before recommending a solution). The task was to:

1. Pick one client file and map its organization: systems, information flows and stakeholders.
2. Identify its operational bottlenecks and choose **one** to solve with AI.
3. Design an AI-based solution and its workflow.
4. Define KPIs to measure success.
5. Build a working Proof-of-Concept automation implementing the solution.
6. Write an implementation (change management) plan for rolling it out in the organization.
7. Present the whole thing to the "client" as a consultant would.

I chose **client file #1 — UrbanKitchen**, a mid-size kitchen-equipment company whose customer data lives scattered across five disconnected systems (Shopify, Priority, Monday.com, Outlook, WhatsApp Business), forcing service reps to manually hunt for customer information before replying — with a ~24 hour average response time and ~500 inquiries a month.

## What I built

An AI customer service assistant, built end-to-end in **Make**, that:

1. Receives an incoming customer email (via Mailhook).
2. Analyzes it with **Google Gemini** — classifies the inquiry type, extracts the customer's details and order number, summarizes it, and estimates a confidence score.
3. Looks up the customer and order in a Google Sheets layer that simulates the company's systems.
4. Routes the inquiry through one of four business paths: order status / product question / complaint-refund / human review.
5. Either sends an automatic AI-drafted reply (simple, low-risk inquiries) **or** creates a task for a human representative (complaints, refunds, low-confidence or unclear cases) — a **Human-in-the-Loop** safeguard by design.
6. Logs every inquiry for KPI tracking.

Everything except the client case file itself (see [`/sources`](./sources)) — the diagnosis, the bottleneck analysis, the solution design, the Make scenario, the KPI framework, the implementation plan and the client presentation — was researched, designed and written by me for this assignment.

## Repository structure

| Path | Content |
|---|---|
| [`/docs`](./docs) | The full project write-up, step by step, as requested by the assignment (organization mapping → bottlenecks → solution design → KPIs → Make build → rollout plan). Also hosts the live client presentation ([`index.html`](./docs/index.html)). |
| [`/make`](./make) | The exported Make scenario ([blueprint](./make/UrbanKitchen.blueprint.json)) and a link to the live, view-only scenario. |
| [`/deliverables`](./deliverables) | The condensed, client-facing specification document — the business-level write-up actually handed to "the client." |
| [`/sources`](./sources) | The course-provided client case file used as the research input (not written by me — see its own README). |

### The step-by-step write-up ([`/docs`](./docs))

1. [Organization mapping](./docs/step_A_organization_mapping.md) — systems, information flows and stakeholders.
2. [Bottleneck analysis](./docs/step_B_bottlenecks.md) — three candidate bottlenecks, and why the fragmented service process was chosen.
3. [Solution design](./docs/step_C_solution_design.md) — the AI workflow, routing logic, privacy/ethics considerations and edge cases.
4. [KPIs & measurement](./docs/step_D_kpis_and_measurement.md) — the three success metrics and how they're tracked.
5. [Make implementation](./docs/step_E_make_implementation.md) — the scenario module by module, error handling, and optimization.
6. [Implementation / change management plan](./docs/step_F_change_management.md) — the pilot plan, team, training, risks and future rollout stages.

## Key results (POC targets)

| KPI | Current state | Target |
|---|---|---|
| Average response time | 24 hours | Under 4 hours |
| Automatic-resolution rate | Not measured | 30% |
| Average handling cost per inquiry | ₪52.5 | ~₪31.5 |

## Tools used

Make (automation/orchestration), Google Gemini 3.1 Flash Lite (AI classification & drafting), Google Sheets (simulated data layer for the POC), Gmail (inbound/outbound email).
