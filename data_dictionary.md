# PulseFit Data Dictionary (Final)

This document describes the attributes of the PulseFit clean datasets after ETL processing.

## 1. Members Dataset (`members_clean.csv`)
| Column Name | Description | Data Type | Notes |
| :--- | :--- | :--- | :--- |
| `member_id` | Unique ID | String | Primary Key |
| `full_name` | Member Name | String | - |
| `email` | Contact email | String | Standardized format |
| `phone_number` | Phone number | String | Normalized |
| `gender` | Gender | String | [M, F, U] (U = Unknown) |
| `join_date` | Joining Date | Date | YYYY-MM-DD |
| `membership_type`| Level | String | Standardized case |
| `status` | Current state | String | [Active, Cancelled, Expired] |
| `home_branch` | Primary branch | String | Cleaned names (e.g. Tunis Lake) |
| `birth_year` | Birth Year | Integer | Used for age categorization |

## 2. Visits Dataset (`visits_clean.csv`)
| Column Name | Description | Data Type | Notes |
| :--- | :--- | :--- | :--- |
| `visit_id` | Visit ID | String | Unique |
| `member_id` | Member ID | String | Links to Members table |
| `branch` | Gym branch | String | Normalized |
| `check_in_time` | Arrival | Timestamp | YYYY-MM-DD HH:MM:SS |
| `check_out_time`| Departure | Timestamp | Imputed if missing (1hr duration) |

## 3. Payments Dataset (`payments_clean.csv`)
| Column Name | Description | Data Type | Notes |
| :--- | :--- | :--- | :--- |
| `payment_id` | Trans. ID | String | Unique |
| `member_id` | Payer ID | String | Links to Members table |
| `date` | Trans. Date | Date | YYYY-MM-DD |
| `amount` | Amount (TND) | Decimal | Outliers corrected (10x errors fixed) |
| `payment_method`| Method | String | [Cash, Credit Card, Bank Transfer] |
| `membership_type`| Plan paid for | String | Standardized case |
