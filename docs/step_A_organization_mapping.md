# Step A – Organization Mapping

## 1. Systems Currently Used

| System | Purpose | Department | Information Stored |
|--------|---------|------------|-------------------|
| Shopify | E-commerce storefront | E-commerce | Customer orders, purchase history |
| Priority | ERP for accounting, inventory and invoicing | Finance, Logistics | Inventory levels, invoices, payment status |
| Monday.com | Sales CRM and B2B deal management | B2B Sales | Leads, deals, sales pipeline |
| WhatsApp Business | Customer communication channel | Customer Service, Logistics | Customer inquiries, complaint photos, logistics messages |
| Outlook | Email communication | Customer Service, Sales | Customer emails, inquiries, complaints |
| Excel | Ad-hoc manual tracking | Multiple employees | Complaints, product defects, logistics notes |

## 2. Information Types

| Information | Source | Format | Where It Is Used |
|-------------|--------|--------|-----------------|
| Customer orders | Shopify | Structured digital data | Used by service and finance teams; manually checked against Priority |
| Invoices | Priority | Structured business data | Finance and customer service |
| Payment status | Priority | Structured business data | Customer service and sales |
| Inventory levels | Priority | Structured business data | Sales, logistics and customer service |
| B2B sales deals | Monday.com | Structured CRM data | Manually re-entered into Priority |
| Customer inquiries | Outlook, WhatsApp | Unstructured text | Customer service agents |
| Product defect photos | WhatsApp | Image | Customer service agents |
| Logistics complaints | WhatsApp, Excel | Unstructured text / manual spreadsheet | Logistics and customer service |
| Driver and shipment updates | WhatsApp groups | Unstructured messages | Logistics coordination |

## 3. Stakeholders

| Role | Responsibility | Systems Used | Decisions / Needs |
|------|----------------|--------------|------------------|
| Noa – CEO | Overall management, financial stability and growth | Not specified | Wants ROI, efficiency and operational cost reduction |
| Daniel – Co-founder and Chairman | Promotes adoption of new technologies | Not specified | Supports innovation initiatives |
| Efrat – Customer Service Manager | Manages customer inquiries and service quality | Outlook, WhatsApp | Needs faster response and better customer visibility |
| Gil – IT Manager | Responsible for information systems and integrations | Multiple organizational systems | Needs better system connectivity |
| Galit – HR Manager | Responsible for employee wellbeing and workload | Not specified | Wants to reduce repetitive manual work and burnout |
| Nir – Analyst | Provides operational and financial data | Not specified | Measures cost, response time and service performance |
| B2B Sales Representatives | Manage leads and close deals | Monday.com | Need deal information to reach Priority without manual re-entry |
| Customer Service Agents | Handle inquiries end-to-end | Outlook, WhatsApp, Shopify, Priority | Need unified customer and order information |
| Warehouse Workers | Prepare and dispatch shipments | Not specified | Need accurate order and address details |
| Drivers | Perform last-mile deliveries | WhatsApp groups | Need accurate delivery information and fewer return trips |

## 4. Human Touchpoints

| # | Who | Manual Action | Systems / Flow |
|---|-----|---------------|----------------|
| 1 | Sales representative | Re-enters closed B2B deals from Monday.com into Priority to generate invoices | Monday.com → Priority |
| 2 | Customer service agent | Searches several systems to identify the customer and understand their history | Shopify, Priority, Monday.com |
| 3 | Customer service agent | Checks Shopify for purchase details and Priority for payment or inventory status | Shopify → Priority |
| 4 | Customer service agent | Handles defect photos from WhatsApp while customer communication may continue by email | WhatsApp → Outlook |
| 5 | Customer service agent | Spends an average of 45 minutes handling one inquiry due to manual lookups | Service systems |
| 6 | Employees | Track complaints, product defects and logistics issues in personal Excel files | WhatsApp / Outlook → Excel |
| 7 | Logistics staff | Coordinate delivery status through multiple WhatsApp groups | WhatsApp groups |
| 8 | Warehouse / logistics staff | Prepare shipments based on manually transferred order and address information | Manual order information → shipment process |
| 9 | Drivers | Perform return trips when there are delivery errors such as wrong address or missing item | Delivery process → WhatsApp coordination |

## Key Findings

UrbanKitchen operates with several disconnected systems across sales, e-commerce, finance, logistics and customer service. The main operational pattern is manual data transfer between systems rather than automated synchronization. Customer service agents are especially affected because they need to search across Shopify, Priority, Monday.com, Outlook and WhatsApp before responding to customers. This creates slow response times, employee workload, fragmented customer visibility and a higher risk of logistics and service errors.