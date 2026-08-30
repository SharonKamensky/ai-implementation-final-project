# Step F – Implementation Plan (Change Management)

## Goal of the implementation plan

The goal is to roll out the AI solution into UrbanKitchen's customer service department gradually and in a controlled way, while reducing risk, protecting service quality and ensuring successful adoption by employees.

The solution is not meant to replace customer service representatives — it is meant to reduce manual work, shorten response times and improve the quality of customer replies.

## 1. Gradual rollout model – the pilot stage

The rollout will start as a focused pilot inside the customer service department, initially covering **email inquiries only**.

This choice keeps complexity low and allows the system to be tested in a controlled way before connecting additional channels such as WhatsApp Business or direct integrations with the company's core systems.

### Pilot scope

The pilot will focus on four inquiry types:

- Order status inquiries
- General product questions
- Complaints and refund requests
- Unclear inquiries that require human review

Initially, only simple, low-risk inquiries will receive an automatic reply. Sensitive inquiries — complaints, refunds, or unclear cases — will be routed to a representative through the Human-in-the-Loop mechanism.

### Pilot duration

Recommended pilot duration: **4 weeks**.

| Week | Main activity |
|---|---|
| Week 1 | Train representatives, test scenarios, and run a controlled trial on a small sample of emails (via a dedicated pilot address or manual forwarding of selected inquiries). |
| Week 2 | Expand usage to more email inquiries and monitor issues daily. |
| Week 3 | Take initial KPI measurements, collect feedback from representatives, and refine prompts. |
| Week 4 | Analyze pilot results and decide whether to expand usage. |

### Success criteria for moving to broader rollout

The pilot will be considered successful if:

- Average initial response time decreases.
- At least 30% of simple inquiries are handled automatically or semi-automatically.
- Representatives' manual work time decreases.
- No automatic replies are sent for sensitive cases (complaints, refunds).
- The customer service manager and representatives report positive satisfaction with the system.
- Inquiries are fully logged for measurement and control.

## 2. Implementation team

A small internal team will be responsible for supporting the pilot, checking output quality, and answering employee questions:

| Role | Responsibility in the rollout |
|---|---|
| Efrat – Customer Service Manager | Business process owner; checks reply quality; defines inquiry-handling policy; leads the representatives. |
| Gil – IT Manager | Owns technical connections, permissions, system stability, troubleshooting and coordination with company systems. |
| Nir – Business Analyst | Measures KPIs, analyzes pilot results and produces management reports. |

**Division of responsibility:** Efrat ensures the system serves the service department's needs; Gil ensures the scenario runs reliably from a technical standpoint; Nir evaluates whether the solution generates measurable business value. Together, these three roles let the solution be assessed from three angles: service, technology, and ROI.

## 3. Employee training plan

A short training session will be run for customer service representatives before the pilot starts.

**Training content:**

- A short explanation of the system's purpose.
- A live demo of an incoming inquiry and how it's analyzed.
- An explanation of the four handling routes.
- Examples of cases where the system replies automatically.
- Examples of cases where the inquiry is handed to a representative.
- How to read tasks created in the `Agent_Tasks` sheet.
- What to do when the AI makes a mistake or produces an unsuitable draft.

**Format:** a short, roughly 45-minute workshop for the service team. A short reference sheet with day-to-day guidelines will also be prepared for representatives.

## 4. Quick-reference guide – what to do if the AI gets it wrong

| Situation | Recommended action |
|---|---|
| The AI misclassified the inquiry | Flag it for review and manually correct the handling type. |
| The draft reply isn't appropriate | Edit the draft before sending, or write a new reply. |
| Missing customer or order information | Check manually in company systems, or route to the right person. |
| Sensitive complaint or refund case | Do not send an automatic reply; route for approval by the service manager. |
| The system didn't create a task as expected | Notify the implementation owner and document the case. |
| Recurring technical issue | Contact the IT manager for review. |

The goal of this reference sheet is to give representatives a sense of control and confidence, and to make clear that the AI is a decision-support tool, not a replacement for their professional judgment.

## 5. Transparency and ethics toward employees

Building trust with employees is one of the conditions for a successful rollout.

At the launch meeting, it should be emphasized that the system is not meant to replace service representatives — it is meant to reduce repetitive manual work and let them focus on delivering higher-quality service.

**Core message to employees:** *The AI does not replace you. It helps you work faster, reduces manual lookups, and improves the quality of service you provide to customers.* The system handles simple inquiries and prepares initial information, but for complex or sensitive cases, the decision stays with a human representative.

This framing matters especially in an organization where employees already experience workload and burnout from heavy manual work. Presenting the system as a tool that reduces load — not one that replaces employees — will help increase cooperation and adoption.

## 6. Risk management during the rollout

| Risk | Mitigation |
|---|---|
| An inaccurate reply is sent to a customer | Automatic replies are limited to simple inquiries only; sensitive cases are routed to a representative. |
| Employee resistance | Early communication, training, and involving representatives in the testing process. |
| Technical failure in the scenario | Error handling, storing incomplete runs, and daily monitoring during the pilot. |
| Metrics fall short of targets | Refine prompts, adjust Filters, and reassess the handling routes. |
| Task overload on representatives | Monitor `Agent_Tasks` and evaluate whether the knowledge base needs improvement. |

## 7. Future expansion after a successful pilot

If the pilot meets its success criteria, the solution can be expanded gradually. The goal of expansion is not to connect every organizational system at once, but to progress in stages based on business value, complexity, and the organization's operational capacity.

### Expansion stage 1 – Stabilize and expand within customer service

- Connect Outlook or Gmail as a permanent input channel, replacing the pilot channel.
- Improve the customer and order tables so they better reflect what representatives need.
- Build a management dashboard in Looker Studio or Monday, depending on the organization's preference and existing tools.
- Build an official knowledge base for product questions (FAQs, specs, warranty terms, service policy).

This stage is a realistic, near-term expansion since it builds on the process already validated in the pilot and does not yet require deep changes to the organization's core systems.

### Expansion stage 2 – Gradual connection to core systems

- Connect to **Shopify** to retrieve orders and customer details in real time.
- Connect to **Priority** for stock levels, payment status and invoices.
- Connect to **Monday.com** to create tasks and manage service/sales workflows.

This stage requires API review, permissions, data security, and coordination with the IT manager, and should therefore be rolled out gradually rather than all at once.

### Expansion stage 3 – Data layer and advanced AI capabilities

- Build a **Customer 360** layer unifying data from across the organization's systems into a single customer view.
- Expand the solution to additional service channels such as WhatsApp Business.
- Analyze service trends, recurring workloads, and common complaints.
- Identify problematic products or recurring processes that generate service inquiries.
- Produce management insights to support improvements in service, logistics, and sales.

This stage is a broader strategic expansion, and should only be pursued once the pilot and initial expansion have demonstrated measurable value to the organization.

## 8. Implementation plan summary

The implementation plan is based on a gradual, controlled and measurable approach.

In the first stage, the solution will run as a pilot in the customer service department, limited to email inquiries. After measuring performance, collecting employee feedback and refining the process, the solution can be expanded to additional channels and to the organization's core systems.

This approach reduces risk, allows learning along the way, and ensures that the AI rollout is carried out responsibly, transparently, and with clear business value.
