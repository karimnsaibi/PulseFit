# PulseFit Data Modeling Plan (Weeks 2-3)

## Goal
Transform the 6 processed datasets into a **Dimensional Star Schema** and define the logic for BI measures (KPIs) to answer analytical questions about churn, revenue, and attendance.

## Star Schema Architecture

### Fact Tables (Events)
- **`FactPayments`**: Transactions for memberships.
- **`FactVisits`**: Physical attendance at gym branches.
- **`FactBookings`**: Class registration events.

### Dimension Tables (Filters/Attributes)
- **`DimMembers`**: Demographic and membership profile info.
- **`DimTrainers`**: Staff profiles and expertise.
- **`DimClasses`**: Schedule and metadata about group fitness.
- **`DimDate` [NEW]**: A dedicated calendar table for time-intelligence (YOY, MOM).

## Key Measures To Define
1. **Financial**: Total Revenue, Average Revenue per Member, MoM Revenue Growth.
2. **Behavioral**: Churn Rate, Retention Rate, Average Visit Duration.
3. **Operational**: Trainer Utilization, Class Occupancy %, Branch Performance Index.