# Hotel-Booking-Demand-Analysis

## Project Overview

This project analyzes hotel booking demand to identify the factors contributing to a decline in bookings during the second half of the year. Using SQL, Python, and Power BI, the analysis uncovers trends in customer behavior, cancellations, booking channels, and revenue to support data-driven business decisions.

## Problem Statement

A hotel chain has experienced a noticeable reduction in bookings over recent months, resulting in lower occupancy and decreased revenue. Management wants to understand the reasons behind the decline by analyzing historical booking data and identifying opportunities to improve booking performance, reduce cancellations, and increase customer retention.

## Objectives

- Analyze monthly booking trends.
- Identify factors contributing to declining bookings.
- Measure cancellation rates.
- Analyze booking channels and customer segments.
- Evaluate hotel performance and revenue.
- Study customer behavior and repeat guests.
- Provide actionable business recommendations.

## Data Set

Rows: 700

Columns: 20

Type: Simulated Hotel Booking Demand Dataset[link](C:\Users\91901\Downloads\hotel_booking_demand_700_rows.xlsx)

## Data Cleaning

- **Fixed Data Types** – Converted `Arrival_Date` from string to datetime and
  mapped `Is_Repeated_Guest` from Yes/No to True/False (boolean).
- **Validated Business Logic** – Removed invalid records with 0 total nights,
  zero/negative ADR, and 0 adults. Flagged revenue mismatches in canceled bookings.
- **Standardized Text** – Stripped whitespace and applied consistent casing across
  categorical columns like `Country`, `Hotel`, and `Market_Segment`.
- **Feature Engineering** – Created 6 new columns including `Total_Nights`,
  `Total_Guests`, `Is_Canceled`, and `Revenue_Per_Night` for deeper analysis.

  ## Data analysis

  ## 🗄️ Data Exploration – SQL Queries

This section documents the structured exploration of the Hotel Booking Demand dataset using SQL.
All queries were written and tested in **SQLite** and are compatible with PostgreSQL and MySQL.

---

### 📁 File
`hotel_sql_queries.sql`

---

### 🗃️ Table Structure

```sql
CREATE TABLE hotel_bookings (
  Booking_ID              TEXT,
  Hotel                   TEXT,
  Arrival_Date            TEXT,
  Arrival_Month           TEXT,
  Lead_Time               INTEGER,
  Stays_Weekend_Nights    INTEGER,
  Stays_Week_Nights       INTEGER,
  Adults                  INTEGER,
  Children                INTEGER,
  Country                 TEXT,
  Market_Segment          TEXT,
  Distribution_Channel    TEXT,
  Is_Repeated_Guest       TEXT,
  Previous_Cancellations  INTEGER,
  Reserved_Room_Type      TEXT,
  ADR                     REAL,
  Booking_Status          TEXT,
  Total_Special_Requests  INTEGER,
  Customer_Type           TEXT,
  Revenue                 REAL
);
```

---

### 🔍 Exploration Areas & Query Themes

#### 1. Monthly Booking Trends
- Total bookings per month with Check-Out, Canceled, and No-Show breakdown
- Month-over-month change in bookings using `LAG()` window function

#### 2. Cancellation Rate Analysis
- Overall cancellation and no-show rates
- Cancellation rate by hotel type (City Hotel vs Resort Hotel)
- Impact of prior cancellation history on current booking behaviour
- Cancellation rate by lead-time bucket (0–7 days → 180+ days)

#### 3. Booking Channels & Customer Segments
- Bookings, cancellation rate, and average revenue by Market Segment
- Revenue and ADR comparison across Distribution Channels
- Customer type breakdown (Transient, Contract, Group, Transient-Party)

#### 4. Hotel Performance & Revenue
- KPI summary per hotel — ADR, Revenue, Cancellation Rate, Avg Nights
- Revenue contribution by room type
- Top 5 countries by realised revenue

#### 5. Customer Behaviour & Repeat Guests
- New guest vs repeat guest — cancellation rate, ADR, and revenue
- Effect of special requests count on cancellation likelihood
- Guest profile segmentation: Solo, Couple/Group, Family (with children)

#### 6. Decline Diagnostics
- Months with both high cancellation rate (>30%) and low revenue
- Market segments driving the highest lost revenue from cancellations
- Long lead-time vs short lead-time cancellation rate comparison

---

### 🧠 SQL Concepts Used

| Concept | Applied In |
|--------|------------|
| `GROUP BY` + `COUNT`, `SUM`, `AVG` | Aggregations across all themes |
| `CASE WHEN` | Bucketing lead time, prior cancellations, guest profiles |
| `ROUND()` + `NULLIF()` | Safe percentage calculations |
| `LAG()` window function | Month-over-month booking change |
| `WITH` (CTE) | Month-over-month trend query |
| `HAVING` | Filtering aggregated cancellation rates |
| `ORDER BY` with `CASE` | Custom sort for calendar month order |
| `LIMIT` | Top-N country revenue ranking |

---

### 📊 Key Findings from SQL Analysis

| Metric | Value |
|--------|-------|
| Total Bookings | 700 |
| Overall Cancellation Rate | 26.9% |
| No-Show Rate | 6.1% |
| Highest Cancel Segment | Corporate (32.4%) |
| Lowest Cancel Segment | Offline (20.3%) |
| Repeat Guest Cancel Rate | 22.4% |
| New Guest Cancel Rate | 28.3% |
| Avg ADR | ₹141.28 |

> **Finding:** Guests with 3 or more prior cancellations cancel at nearly **2× the rate** of guests with no cancellation history.
> Bookings made more than 90 days in advance carry significantly higher cancellation risk than short lead-time bookings.

##  Recommendations

- Introduce flexible cancellation policies, booking reminders, and special offers to reduce cancellations.
- Launch loyalty programs and personalized discounts to increase repeat bookings and customer retention.
- Strengthen direct booking channels through the hotel website with exclusive deals and promotions.
- Increase marketing campaigns during low-demand seasons to improve occupancy rates.
- Use booking data regularly to monitor trends and optimize pricing and promotional strategies.




  
