# Specification & Implementation Document

### AI & Automation Solution for Improving the Customer Service Process
#### UrbanKitchen

This is the client-facing specification document prepared and presented as part of the final project — a condensed, business-oriented version of the full technical analysis in [`/docs`](../docs), written for the client rather than for a technical audience.

---

## 1. Executive Summary

UrbanKitchen sells to both private and business customers, using several information systems: Shopify, Priority, Monday.com, Outlook, WhatsApp Business and Excel.

The diagnosis identified a central problem: the information needed to serve customers is scattered across disconnected systems. As a result, service representatives have to manually search multiple sources before responding to a customer.

The proposed solution is an AI- and automation-based customer service assistant, built with Make. The system receives customer inquiries, analyzes them with Google Gemini, retrieves information from a Google Sheets layer simulating the company's systems, routes the inquiry to the right path, and either sends an automatic reply or creates a task for a representative, depending on the inquiry type.

The solution is designed as a controlled pilot in the customer service department, with a Human-in-the-Loop mechanism for sensitive cases such as complaints, refund requests, or unclear inquiries.

## 2. Current State & Diagnosis Findings

The organization runs several core systems:

| System | Main use |
|---|---|
| Shopify | Customer orders and website purchases |
| Priority | Inventory, invoices and payments |
| Monday.com | B2B sales management |
| Outlook | Customer email inquiries |
| WhatsApp Business | Communication with customers and drivers |
| Excel | Manual tracking of complaints and issues |

The core problem is not a lack of information — it's that information is scattered across systems. A representative handling an inquiry has to move between several tools just to understand who the customer is, what they ordered, and what the current status is.

Three main improvement areas were identified during the diagnosis:

| Area | Description | Recommendation |
|---|---|---|
| Lack of system integration | No unified customer view | Future infrastructure stage |
| Fragmented customer service | Representatives manually search for information before replying | **Recommended starting point** |
| Delivery errors | Wrong addresses or missing items cause return trips | Future stage |

The recommendation was to start with the customer service process, since it carries high business value, fits well with AI, and its improvement can be measured clearly.

## 3. The Business Problem Selected

The current customer service process is slow and manual. Inquiries arrive by email and WhatsApp, but the information needed to answer them lives in different systems.

Key figures:

| Metric | Value |
|---|---|
| Service inquiries per month | ~500 |
| Average response time | ~24 hours |
| Average handling time per inquiry | 45 minutes |
| Representative hourly cost | ₪70 |
| Average handling cost per inquiry | ₪52.5 |

This process is well suited to AI because it involves understanding free text, classifying inquiries, extracting information, summarizing, and drafting an initial reply.

## 4. The Proposed Solution

The solution is an AI-based customer service assistant designed to support representatives, not replace them.

The system:

- Receives an email inquiry.
- Analyzes it using AI.
- Classifies the inquiry type.
- Extracts the order number, if present.
- Looks up the customer and order in the data sheet.
- Routes the inquiry to the right path.
- Sends an automatic reply for simple inquiries.
- Creates a task for a representative for complex cases.

**Core principle:** *the AI analyzes the inquiry, but Make manages the business logic and routing.* This keeps the process transparent, controlled and safe.

## 5. Process Flow

1. A customer sends an email.
2. Mailhook triggers the scenario.
3. Gemini analyzes the inquiry and returns structured JSON.
4. Google Sheets looks up the customer by email address.
5. The Router sends the inquiry to one of four paths.
6. The inquiry is logged in `Inquiry_Log`.
7. Depending on the path, an automatic email is sent, or a task is created for a representative.

## 6. AI Logic & Routing

The first AI module, **Analyze Customer Inquiry**, analyzes the inquiry content and returns a structured JSON output including: inquiry type, order number (if present), a summary, a handling recommendation, a confidence score, and — where relevant — an initial draft reply for the representative.

The draft produced by the first module is not the final customer-facing reply — it mainly supports representatives on inquiries routed for human handling. When an automatic reply is sent, a second AI module generates the final response based on the data retrieved from the system.

Once the output is returned, Make's Router routes the inquiry based on inquiry type and confidence score:

| Route | Routing condition | Action |
|---|---|---|
| Order Status | Order status inquiry | Retrieve order, draft reply, send email |
| Product Question | General product question | Cautious reply, no invented information |
| Complaint / Refund | Complaint or refund request | Create representative task and log |
| Human Review | Unclear inquiry or low confidence | Create representative task and log |

## 7. Implementation in Make

The scenario was built in Make using these core modules:

| Module | Role |
|---|---|
| Receive Customer Email | Receives the inquiry via Mailhook |
| Analyze Customer Inquiry | Analyzes and classifies the inquiry using Gemini |
| Find Customer | Looks up the customer by email |
| Router | Routes to the right path |
| Find Customer Order | Retrieves the order on the status route |
| Generate Reply | Generates the automatic reply |
| Create Agent Task | Creates a task for a representative |
| Log Inquiry | Logs the inquiry |
| Send Reply | Sends the email to the customer |

For the pilot, Google Sheets simulates the organization's systems:

| Sheet | Role |
|---|---|
| Customers | Customer details |
| Orders | Order details |
| Inquiry_Log | Inquiry log |
| Agent_Tasks | Tasks for representatives |

## 8. System Output

The automation ends in one of two states:

1. **Automatic reply to the customer** — for simple inquiries such as order status.
2. **Task created for a representative** — for complex inquiries such as complaints, refunds, or unclear cases.

In addition, every inquiry is logged in `Inquiry_Log` for control and KPI measurement.

## 9. Human-in-the-Loop & Exception Handling

Not every inquiry receives an automatic reply. Simple, clear inquiries can be answered automatically, but sensitive or uncertain cases are handed to a human representative:

- Complaints
- Refund requests
- Unclear inquiries
- Low AI confidence
- Unrecognized customer or order
- Cases where the system lacks an authoritative source of information

This approach balances operational efficiency with service quality and professional accountability.

## 10. Error Handling & Reliability

The scenario includes error handling at several levels:

| Component | Handling type | Reason |
|---|---|---|
| Analyze Customer Inquiry | Retry | Critical module — retry on a temporary failure |
| Log Inquiry | Resume | A logging failure shouldn't stop the rest of the process |
| Scenario settings | Store incomplete executions | Failed runs are saved for review and re-run |

The goal is to make sure a customer inquiry never disappears or receives a wrong reply because of a technical glitch.

## 11. Operations Optimization

To reduce operations and unnecessary calls to external systems:

- The Router routes early in the process.
- Filters ensure only the relevant path runs.
- Order lookup happens only on the Order Status route.
- Reply-generation modules run only where an automatic reply is possible.
- A representative task is created only where human intervention is required.
- Structured JSON output from the AI removes the need for extra parsing (e.g. Regex) modules.

## 12. Tests Performed

| Test | Input | Actual result |
|---|---|---|
| Order status inquiry | Customer requests order status | Automatic reply sent |
| Product question | Customer asks about a product | Cautious reply, no invented information |
| Product complaint | Customer reports a damaged product | Representative task created, no email sent |
| Unclear inquiry | Ambiguous inquiry | Human Review task created |

## 13. KPIs & Success Measurement

Three core success metrics were defined:

| KPI | Current state | Target |
|---|---|---|
| Average response time | 24 hours | Under 4 hours |
| Automatic-resolution rate | Not currently measured | 30% |
| Average handling cost per inquiry | ₪52.5 | ~₪31.5 |

These metrics will be monitored through a management dashboard built on `Inquiry_Log` data.

## 14. Implementation Plan

The rollout starts as a controlled pilot in the customer service department, covering email inquiries only. During the pilot, the automation is not connected to the entire organizational inbox, but to a controlled input channel (a dedicated pilot address, or manual forwarding of selected inquiries).

Recommended pilot duration: 4 weeks.

| Week | Main activity |
|---|---|
| 1 | Train representatives and test scenarios on a small sample |
| 2 | Expand usage to more inquiries with daily monitoring |
| 3 | Measure KPIs, collect feedback, refine prompts |
| 4 | Analyze results and decide on expansion |

Recommended implementation team:

| Role | Responsibility |
|---|---|
| Customer Service Manager | Process owner, checks reply quality |
| IT Manager | Connections, permissions, troubleshooting |
| Business Analyst | KPI measurement and reporting |

**Core message to employees:** *The AI does not replace service representatives. It reduces manual work and lets them focus on cases that require human judgment.*

## 15. Future Expansion

If the pilot meets its success criteria, the solution can be expanded gradually:

**Stage 1 – Stabilize and expand within customer service**
- Connect Outlook or Gmail as a permanent input channel.
- Improve the customer and order tables.
- Build a management dashboard.
- Build a product knowledge base.

**Stage 2 – Connect to core systems**
- Connect to Shopify for real-time orders.
- Connect to Priority for stock, payments and invoices.
- Connect to Monday.com for task management.

**Stage 3 – Advanced capabilities**
- Build a Customer 360 layer.
- Expand to WhatsApp Business.
- Analyze service trends and recurring complaints.

## 16. Conclusion & Recommendation

The solution lets UrbanKitchen begin adopting AI in a high-value business process, in a controlled, measurable and responsible way.

The system supports representatives by analyzing inquiries, retrieving information, routing automatically, and drafting initial replies — while preserving human involvement for sensitive or uncertain cases.

**Recommendation:** start with a focused pilot in the customer service department, measure results through KPIs, and — once value is proven — gradually expand the solution to additional channels and to the organization's core systems.
