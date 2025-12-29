
# Financial & Operational Performance Dashboard (Power BI)

This repository contains:
- **Power BI dashboard** for executive visibility into financial transactions, client metrics, and operational efficiency.
- **DAX measures** for advanced KPIs including margin analysis, SLA compliance, and risk scoring.
- **Screenshots and design notes** for layout and visualization best practices.

---

## Overview

The dashboard provides a **360° view** of:
- **Financial KPIs**: Total Amount, Net Revenue, Fees, Margin %, MoM trends.
- **Client Insights**: Active clients, risk rating levels, top clients by revenue.
- **Operational Metrics**: SLA compliance, resolution times, ticket status, and breach analysis.

### Key Use Cases
- Executive decision-making on revenue and margin performance.
- Monitoring SLA adherence and operational bottlenecks.
- Risk segmentation for client portfolios.
- Monthly trend analysis for transactions and support tickets.

---

## Dashboard Pages

### 1. **Executive Overview**
- **KPIs**:
  - Total Amount (€)
  - Net Revenue (€)
  - Total Fees (€)
  - MoM Amount % (Month-over-Month change)
  - Active Clients
  - SLA Compliance %
- **Visuals**:
  - Monthly Transaction Volume (line chart)
  - Top 10 Products by Net Revenue (bar chart)
  - Transaction Status (%) (donut chart)
  - Transaction Distribution by Country (map)
  - SLA Compliance Trend (line chart)

### 2. **Client & Product Analysis**
- **KPIs**:
  - Active Clients
  - Avg Margin %
  - Risk Rating Level (Low / Medium / High)
- **Visuals**:
  - Top 10 Clients by Net Revenue
  - Segment × Country × Avg Margin % (matrix)
  - Product Category: Volume vs Margin % (combo chart)
  - Client Scatter Plot: Avg Risk vs Net Revenue vs Total Amount

### 3. **Operational Efficiency**
- **KPIs**:
  - Tickets Count
  - SLA Compliance %
  - Avg Resolution Hours
  - Critical Tickets %
- **Visuals**:
  - Tickets Opened vs Closed (%)
  - Avg Resolution Time by Department vs SLA Target
  - SLA Compliance by Country

---

## Key DAX Measures

### Financial Metrics
- **Total Amount**  
  `SUM(Transactions[Amount])`
- **Net Revenue**  
  `SUM(Transactions[NetAmount])`
- **Net Revenue YTD**  
  `TOTALYTD([Net Revenue], 'Date'[Date])`
- **MoM Amount %**  
  Calculates month-over-month change using `DATESBETWEEN` and `EDATE`.

### Margin Analysis
- **Avg Margin % (Weighted)**  
  Weighted by transaction amount using `SUMX` and `LOOKUPVALUE`.

### Client Metrics
- **Active Clients**  
  `DISTINCTCOUNT(Clients[ClientID])` aligned with transactions.
- **Avg Risk Rating (numeric)**  
  Converts AAA–CCC to numeric scale (1–7) for aggregation.
- **Risk Rating Level**  
  Categorizes numeric risk into Low / Medium / High.

### Operational Metrics
- **Avg Resolution Hours**  
  Average of `ResolutionTimeHours` excluding blanks.
- **SLA Compliance %**  
  Ratio of tickets with `SLA_Breached = "No"`.
- **Within Target %**  
  Tickets resolved within SLA target hours.

### Other KPIs
- **Tickets Closed %**, **Critical Tickets %**, **SLA Breach %**, **Res vs Target Delta**.

---

## Data Model

- **Transactions**: Financial data (Amount, NetAmount, Fee, ProductID, ClientID).
- **Clients**: Client attributes (RiskRating, Segment, Country).
- **Products**: Product details (AvgMarginPct, Category).
- **Support_Tickets**: Operational data (Status, Priority, SLA_Breached, ResolutionTimeHours).
- **Date**: Calendar table for time intelligence (Year, Month, Quarter).

---

## Visual Design Highlights
- **Color Palette**: Purple for financial KPIs, orange for SLA targets, green for compliance.
- **KPI Cards**: Compact, with tooltips summarizing key metrics.
- **Maps**: Transaction distribution by country using Esri visuals.
- **Responsive Layout**: Optimized for executive screens (1366×768 and above).

---

## How to Use
1. Clone the repository:
   ```bash
   git clone https://github.com/your-org/financial-ops-performance-dashboard.git

Open the .pbix file in Power BI Desktop.
Connect to your data sources:

Transactions
Clients
Products
Support_Tickets
Date table


Refresh and publish to Power BI Service for sharing.

Requirements

Power BI Desktop (latest version)
Data sources in supported formats (SQL, Excel, CSV)
Proper relationships between tables (ClientID, ProductID, Date)

Future Enhancements

Add forecasting visuals for revenue and SLA trends.
Implement row-level security for client segmentation.
Integrate Power Automate alerts for SLA breaches.

License
MIT License — free to use, modify, and distribute with attribution.


