# PulseFit Data Model Diagram

This Mermaid diagram illustrates the **Star Schema** architecture designed for the PulseFit BI project.

```mermaid
erDiagram
    DimMembers ||--o{ FactPayments : "1:N (member_id)"
    DimMembers ||--o{ FactVisits : "1:N (member_id)"
    DimMembers ||--o{ FactBookings : "1:N (member_id)"
    
    DimTrainers ||--o{ DimClasses : "1:N (trainer_id)"
    DimClasses ||--o{ FactBookings : "1:N (class_id)"
    
    DimDate ||--o{ FactPayments : "1:N (DateKey)"
    DimDate ||--o{ FactVisits : "1:N (DateKey)"
    DimDate ||--o{ FactBookings : "1:N (DateKey)"

    FactPayments {
        string payment_id PK
        string member_id FK
        date payment_date FK
        decimal amount
        string payment_method
    }

    FactVisits {
        string visit_id PK
        string member_id FK
        string branch
        datetime check_in
        date DateKey FK
    }

    FactBookings {
        string booking_id PK
        string member_id FK
        string class_id FK
        date booking_date FK
        string status
    }

    DimMembers {
        string member_id PK
        string full_name
        string gender
        string home_branch
        date join_date
    }

    DimTrainers {
        string trainer_id PK
        string full_name
        string specialization
        string branch
    }

    DimClasses {
        string class_id PK
        string class_name
        string trainer_id FK
        string day_of_week
        int max_capacity
    }

    DimDate {
        date DateKey PK
        int Year
        int Month
        int Quarter
        string MonthName
        int WeekNumber
    }
```

> [!IMPORTANT]
> **Why we use a `DimDate` table**:
> 1. **Time Intelligence**: Essential for calculating Year-over-Year (YOY) and Month-over-Month (MOM) growth. Standard date columns from raw data can have "gaps" (days with no transactions), which break these complex formulas.
> 2. **Unified Filtering**: Allows a single "Month" or "Year" slicer to control every chart in the dashboard simultaneously (Revenue, Visits, and Bookings).
> 3. **Extended Metadata**: Automatically provides attributes like "IsWeekend", "Quarter", or "Public Holiday" without manual coding.
