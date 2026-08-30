# Step D – KPI Definition and Performance Measurement

## KPI 1 – Average Response Time

**Category:** Efficiency

### Description

Measures the average time between receiving a customer inquiry and sending the initial response.

### Why was it selected?

The client file identifies slow customer response as one of the organization's main business problems. The current average response time is approximately **24 hours**.

Reducing this metric directly improves customer experience and operational efficiency.

### Required Data

* Email received timestamp
* First response timestamp

### Current Value

24 hours

### Target (6 months)

Less than 4 hours

---

## KPI 2 – Automatic Resolution Rate

**Category:** Efficiency

### Description

Measures the percentage of customer inquiries that are fully handled automatically without requiring a customer service representative.

### Why was it selected?

The proposed AI solution automatically handles low-risk inquiries such as order status requests and product questions.

This KPI directly measures the operational efficiency created by the AI automation.

### Required Data

* Total number of inquiries
* Number of automatically resolved inquiries

### Formula

Automatic Resolution Rate =

(Number of Automatically Resolved Inquiries / Total Inquiries) × 100

### Current Value

Not currently measured.

### Initial Target

30%

---

## KPI 3 – Labor Cost per Inquiry

**Category:** ROI

### Description

Measures the average labor cost required to handle a single customer inquiry.

### Why was it selected?

According to the client file, the average handling time is **45 minutes** and the hourly labor cost of a customer service representative is **₪70**.

This KPI demonstrates the direct financial value of the AI solution by measuring the reduction in operational costs after implementation.

### Required Data

* Average handling time per inquiry
* Hourly labor cost

### Formula

Labor Cost per Inquiry =

Average Handling Time (hours) × Hourly Labor Cost

### Current Calculation

45 minutes = 0.75 hours

0.75 × ₪70 = **₪52.5 per inquiry**

### Current Value

₪52.5 per inquiry

### Target (6 months)

Approximately **₪31.5 per inquiry** (about 40% reduction)

---

# KPI Summary

| KPI                       | Category   | Current      | Target    |
| ------------------------- | ---------- | ------------ | --------- |
| Average Response Time     | Efficiency | 24 hours     | < 2 hours |
| Automatic Resolution Rate | Efficiency | Not measured | 30%       |
| Labor Cost per Inquiry    | ROI        | ₪52.5        | ₪31.5     |

---

# AI-Based KPI Calculation

The proposed solution automatically logs every customer inquiry in Google Sheets.

Using the collected data, AI can:

* Calculate KPI values automatically.
* Identify performance trends over time.
* Detect unusual changes.
* Generate weekly management summaries.

---

# KPI Visualization

The following visualizations are recommended:

**Average Response Time**

* Before vs. After Bar Chart

**Automatic Resolution Rate**

* Pie Chart

**Labor Cost per Inquiry**

* Before vs. After Bar Chart

The dashboard can be built using **Google Looker Studio** connected to Google Sheets.

---

# Monitoring

A Google Looker Studio dashboard will display the KPIs in near real time using data collected in Google Sheets.

### Monitoring Frequency

* Operational dashboard: Real-time
* Team review: Weekly
* Management review: Monthly

---

# Bonus – AI KPI Assistant (Gem)

A custom Gem can receive raw inquiry data from Google Sheets and automatically:

* Calculate all KPI values.
* Compare current performance against target values.
* Generate management summaries.
* Highlight unusual trends or declining performance.
