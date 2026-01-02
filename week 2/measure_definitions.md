# PulseFit Measure Definitions (KPIs)

This document defines the core Business Intelligence measures for the PulseFit ecosystem. These measures use the **Star Schema** to provide insights into gym performance.

## 1. Financial Measures (Revenue)

| Measure Name | Formula | Business Purpose |
| :--- | :--- | :--- |
| **Total Revenue** | `SUM(FactPayments[amount])` | Total gross income generated. |
| **Avg Revenue per Member**| `Total Revenue / [Active Members Count]`| Measures financial efficiency per client. |
| **MOM Revenue Growth %** | `([Current Month Rev] - [Prev Month Rev]) / [Prev Month Rev]` | Tracks financial expansion month-over-month. |

## 2. Engagement Measures (Activity)

| Measure Name | Formula | Business Purpose |
| :--- | :--- | :--- |
| **Avg Visits per Member**| `COUNT(FactVisits) / [Total Members]` | Measures how often the average member uses the gym. |
| **Avg Visit Duration** | `AVERAGE(FactVisits[DurationMinutes])` | Analyzes gym-floor engagement. |
| **Class Occupancy Rate %**| `COUNT(FactBookings) / SUM(DimClasses[max_capacity])` | Identifies if group classes are under or overbooked. |

## 3. Retention Measures (Churn)

| Measure Name | Formula | Business Purpose |
| :--- | :--- | :--- |
| **Active Members Count** | `COUNTROWS(FILTER(DimMembers, status = "Active"))` | The core "Health" metric of the subscription business. |
| **Churn Rate %** | `[Members Cancelled this Month] / [Active Members Start of Month]`| Measures the percentage of lost customers. |
| **Retention Rate %** | `1 - [Churn Rate %]` | Measures the percentage of kept customers. |

## 4. Operational Measures (Efficiency)

| Measure Name | Formula | Business Purpose |
| :--- | :--- | :--- |
| **Trainer Utilization** | `Number of Classes Taught / Available Working Slots` | Identifies staff efficiency and potential burnout. |
| **Branch Index** | `Weighted average of Revenue and Visits per Branch` | Compares performance across Tunisia branches. |

---

> [!TIP]
> **Implementation Note**: These measures are designed for **DAX (Power BI)** or **SQL-based** calculation. By using the `DimDate` table as a shared axis, all these measures can be compared Year-Over-Year (YOY) accurately.
