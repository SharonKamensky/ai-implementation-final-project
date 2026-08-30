# Step E – Make Implementation & System Documentation

## 1. Input Interface (Trigger & Webhooks)

### How the automation is triggered

The automation starts with a **Mailhook** module in Make, which listens for incoming customer emails.

Every new email that arrives automatically triggers the inquiry-handling process, with no manual intervention required.

### Why Mailhook was chosen

For this Proof of Concept, the email channel was selected as the entry point because it makes it possible to demonstrate the full business logic of the solution in a simple and clear way.

In a real deployment, the same logic could be connected to Outlook, Gmail, WhatsApp Business, website forms, or any other input channel in the same way.

## 2. Logic, AI Models and Agents

### Automation scenario

The automation is built around four handling routes, based on the type of inquiry:

- Order status inquiries
- General product questions
- Complaints and refund requests
- Human review (unclear / high-risk cases)

Every inquiry is first analyzed by an AI module, then routed to the appropriate path by a Router.

### Core modules

| Module | Role |
|---|---|
| Receive Customer Email | Receives the incoming email and triggers the automation. |
| Analyze Customer Inquiry | Analyzes the inquiry using Google Gemini: classifies the type, extracts information, creates a summary and recommends a handling path. |
| Find Customer | Looks up the customer in the database by email address. |
| Router | Routes the inquiry to the matching path based on the AI classification. |
| Find Customer Order | Retrieves order data when needed. |
| Generate Order Status Reply | Generates the automatic reply for order-status inquiries. |
| Generate Product Reply | Generates a reply for general product questions. |
| Create Agent Task | Creates a task for a customer service representative. |
| Log Inquiry | Logs the inquiry for control, KPI tracking and monitoring. |
| Send Reply | Sends the reply email to the customer. |

### Make features and capabilities used

- Webhook
- Google Gemini AI
- Google Sheets – Search Rows
- Google Sheets – Add Row
- Router
- Filters
- Mapping between modules
- JSON output
- Gmail

## 3. AI Model

The project uses **Google Gemini 3.1 Flash Lite**.

The system uses two AI modules:

**First module** – responsible for:
- Classifying the inquiry type
- Extracting customer details
- Extracting the order number
- Creating a short summary
- Estimating a confidence score
- Recommending a next action
- Drafting a first response

This module returns a structured JSON output, which Make uses to make routing decisions.

**Second module** – runs only on routes where an automatic reply can be sent, and is responsible for writing the final, professional customer-facing reply based on the data retrieved from the sheets.

### Router logic

Once the JSON output is received, Make uses the returned fields to make an operational decision. The Router checks the inquiry type and the confidence score, and routes the inquiry accordingly:

- **ORDER_STATUS** – order status inquiry.
- **PRODUCT_QUESTION** – general product question.
- **COMPLAINT / REFUND_REQUEST** – complaint or refund request.
- **UNCLEAR / HUMAN REVIEW** – unclear, incomplete, or otherwise requires human review.

The AI is responsible for understanding the inquiry; the actual business decision is made in a controlled way through the routing rules defined in Make.

### Route 1 – Order Status

**Trigger condition:** the AI-returned inquiry type is `ORDER_STATUS`.

**Actions:**
1. The system looks up the order in the `Orders` sheet.
2. Relevant order data is retrieved (order number, product, quantity, delivery status).
3. A dedicated AI module drafts a professional, personalized reply.
4. The inquiry is logged in `Inquiry_Log`.
5. An automatic reply is sent to the customer via Gmail.

This route is fully automated because it deals with a relatively simple inquiry based on structured data.

### Route 2 – Product Question

**Trigger condition:** the AI-returned inquiry type is `PRODUCT_QUESTION`.

**Actions:**
1. An AI module drafts an initial reply to the customer's question.
2. The inquiry is logged in `Inquiry_Log`.
3. When a safe, general answer is possible, a reply is sent via Gmail.
4. When the system does not have enough authoritative information, the inquiry is routed to a human agent via a created task.

At the POC stage, there is no official company knowledge base (FAQs, technical specs, full product information). The system therefore never invents information and never provides a full factual answer without an authoritative source.

When information is missing, the system can send a cautious first reply (e.g., confirming the question was received and will be reviewed), while also creating a follow-up task for a representative.

**Future improvement:** in a more advanced version, an official company knowledge base — FAQs, product specs, warranty terms, stock availability and service guidelines — should be built and connected to the AI, allowing it to answer product questions more accurately and increasing the automatic-resolution rate.

### Route 3 – Complaint / Refund

**Trigger condition:** the AI-returned inquiry type is `COMPLAINT` or `REFUND_REQUEST`.

**Actions:**
1. The system creates a task for a customer service representative in `Agent_Tasks`.
2. The task includes the inquiry type, a summary, a priority level and an AI-drafted response.
3. The inquiry is logged in `Inquiry_Log`.
4. No automatic reply is sent to the customer.

This route is kept for human handling because complaints and refund requests are sensitive inquiries that can affect customer satisfaction, financial decisions and the company's service policy. The AI supports the representative with a summary and a draft response, but the final decision stays with a human agent.

### Route 4 – Human Review

This route is used when the system cannot safely make an automatic decision.

**Possible trigger conditions:**
- Inquiry type is `UNCLEAR`.
- AI confidence score is below the defined threshold.
- Important information is missing from the inquiry.
- The customer is not found in the system.
- The inquiry doesn't match any of the other routes.

**Actions:**
1. A task is created in `Agent_Tasks`.
2. The task includes a summary of the inquiry and an initial recommendation.
3. The inquiry is logged in `Inquiry_Log`.
4. No automatic reply is sent to the customer.

This route implements the **Human-in-the-Loop** principle: whenever there is uncertainty or risk of error, the system does not act on its own and hands the inquiry to a person instead.

## 4. Output

The automation ends in one of four ways:

1. An automatic reply is sent to the customer.
2. A task is created for a customer service representative.
3. The inquiry is logged in `Inquiry_Log`.
4. A combination of the above, depending on the route.

Every inquiry is fully logged for control and performance measurement.

### Exception handling

The scenario built in Make handles exceptions by combining AI, the Router, Filters, an agent-task sheet and Make's built-in error handling.

The system does not default to an automatic reply in every situation — it separates simple inquiries that can be handled automatically from inquiries that require human review.

**Business exceptions** — cases where the inquiry was received correctly, but an automatic reply would not be appropriate:

| Case | How it's implemented in Make |
|---|---|
| Unclear inquiry | Classified as `UNCLEAR` and routed to Human Review. |
| Complaint or refund request | Routed to the Complaint/Refund path; a task is opened and no automatic email is sent. |
| Low confidence score | Routed to Human Review based on a Filter condition. |
| Customer not found / missing information | Routed to human handling instead of sending an unfounded reply. |
| Product question without sufficient information | The system avoids inventing information and either gives a cautious reply or hands off to a human. |

**Technical exceptions** — handled through Make's error handlers:

- The **Analyze Customer Inquiry** module has a **Retry** handler, to deal with temporary AI-service failures.
- The **Log Inquiry** module has a **Resume** handler, so that a logging failure does not stop the rest of the process.
- **Store incomplete executions** is enabled in the scenario settings, so incomplete runs are saved for review and re-execution.

This way, the system handles both complex business cases and technical failures, while keeping one core principle: when in doubt, the inquiry goes to a human rather than receiving a wrong automatic answer.

## 5. Operations Optimization

During the build, effort was made to reduce the number of operations and calls to external systems, to improve scenario performance, shorten processing time and reduce cost. This was achieved by:

- Using the **Router** to send each inquiry to the relevant path early in the process, so only the relevant branch keeps running.
- Using **Filters** to prevent unnecessary modules from running for a given inquiry type.
- Looking up order data only on the **Order Status** route, where it's actually needed.
- Running AI reply-generation modules only on routes where an automatic reply is possible.
- Creating an agent task only on routes that require human intervention.
- Logging every inquiry exactly once in `Inquiry_Log`, with no duplicate records.
- Having the main AI module return a **structured JSON output**, which Make can use directly for decisions and routing — removing the need for extra parsing modules (e.g. Regex) and reducing both operations and scenario complexity.

This approach reduces unnecessary actions, lowers API calls, and improves the efficiency, speed and stability of the process.

## 6. Stress Tests

**Test 1 – Order status inquiry**
- Input: a customer email including an order number.
- Expected: the system identifies the inquiry type, retrieves the order data, generates an automatic reply and sends it.
- Actual result: worked as expected.

**Test 2 – Product question**
- Input: a customer asks a general product question.
- Expected: the system identifies the inquiry type and generates an appropriate reply; when information isn't available, it avoids inventing information and routes to a human.
- Actual result: worked as expected.

**Test 3 – Product complaint**
- Input: a customer reports a damaged product.
- Expected: the system identifies it as a complaint, creates an agent task, logs the inquiry and sends no automatic reply.
- Actual result: worked as planned.

## Summary

The system demonstrates how AI can be integrated into a customer service process to classify inquiries, support decision-making, generate automatic replies and support service representatives.

The solution combines automation with a Human-in-the-Loop mechanism, improving response speed while preserving quality, reliability and human oversight for complex or sensitive cases.
