# Step C – AI Solution Design

## Selected Solution

The proposed solution is an AI-powered customer service assistant that supports the initial handling of incoming customer inquiries.

UrbanKitchen currently receives customer inquiries through several channels, mainly email/Outlook and WhatsApp Business. For this Proof of Concept (POC), the email channel is used as the entry point through Make Mailhook, because it allows the full business logic to be demonstrated clearly within the assignment constraints.

The solution does not replace customer service representatives. Instead, it reduces the time spent collecting information, classifying inquiries and drafting responses, allowing agents to focus on customer service and decision-making.

---

## Workflow Overview

Customer Email (POC Input)  
↓  
Mailhook  
↓  
AI Analysis  
↓  
Google Sheets Lookup  
↓  
Router  
↓  
Action according to inquiry type  
↓  
Logging & Human Review when required

---

## Workflow Description

### 1. Trigger

The process starts when a customer sends an email.

The email is received by a Mailhook module in Make. In a full organizational implementation, the same logic could later be expanded to additional channels such as WhatsApp Business or website forms.

---

### 2. AI Processing

The AI analyzes the email and performs the following tasks:

- Classifies the inquiry.
- Extracts customer information.
- Extracts order number if available.
- Creates a short summary.
- Detects the confidence level.
- Suggests the next action.
- Drafts a professional response.

---

### 3. Data Lookup

Google Sheets simulates the company's operational systems and acts as a simplified Customer 360 layer for the POC.

Instead of connecting directly to Shopify, Priority and Monday.com, the workflow uses Google Sheets to represent customer, order and inquiry data that is currently scattered across several systems.

The workflow searches:

- Customer details.
- Order information.
- Previous inquiry history.

In a full implementation, this layer would be replaced by direct integrations with the company's real systems or by a centralized Customer 360 database.

---

### 4. Decision Logic

The Router contains three business routes.

#### Route 1 – Simple Inquiry

Examples:

- Order status
- Product question

Action:

- AI prepares a response.
- Inquiry is logged.
- Automatic response is sent to the customer.

---

#### Route 2 – Complaint / Refund

Examples:

- Damaged product
- Missing item
- Refund request

Action:

- AI summarizes the inquiry.
- AI prepares a suggested response.
- AI recommends the next action.
- A task is created for a customer service representative.
- The representative reviews, edits if necessary and approves the final response.

---

#### Route 3 – Human Review Required

Examples:

- Unknown customer
- Missing order number
- Low AI confidence
- Unclear inquiry

Action:

- No automatic response is sent.
- A customer service task is created.
- The AI summary, recommended action and suggested response are attached for the representative.

---

## Human-in-the-Loop

Only low-risk inquiries with high AI confidence receive an automatic response.

Complaints, refund requests, unknown customers and low-confidence cases always require human review before communicating with the customer.

This approach balances operational efficiency with responsible AI use.

---

## Privacy and Ethics

The solution follows several responsible AI principles:

- Customer data is used only for handling the inquiry.
- Sensitive information should not be unnecessarily sent to the AI model.
- AI recommendations remain under human supervision.
- Every AI action is logged for transparency and auditing.
- Financial decisions such as refunds are never made automatically by the AI.

---

## Edge Cases (Exception Handling)

The solution includes predefined handling for situations where the AI cannot safely continue the workflow.

| Scenario | System Behavior |
|----------|-----------------|
| Unclear or ambiguous inquiry | The AI marks the inquiry as Low Confidence, creates an agent task and does not send an automatic response. |
| Missing order number | The AI prepares a response asking the customer to provide the missing order number before further processing. |
| Customer not found | The inquiry is logged and automatically assigned to a customer service representative for manual review. |
| Complaint or refund request | The AI prepares a summary and suggested response, but the final decision remains with a human representative. |
| AI confidence below the defined threshold | The workflow automatically routes the inquiry to the Human Review path. |
| Unsupported language | The inquiry is logged and routed to a human representative for manual handling. |
| AI service failure or invalid output | The Make error handler logs the event and creates an agent task so that no customer inquiry is lost. |

---

## Expected Business Value

The solution is expected to:

- Reduce customer response time.
- Reduce manual work.
- Improve service consistency.
- Reduce repetitive administrative tasks.
- Increase employee productivity while maintaining human oversight.