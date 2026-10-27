# Urban Mobility & Transportation Intelligence Dashboard
### Power BI • DAX • Power Query • Data Modeling • Data Quality

An interactive five-page Power BI portfolio project designed to explore urban taxi-trip demand, fare patterns, geographic activity, and data-quality exceptions using a large trip-level dataset.

> **Dataset disclosure:** The bundled practice dataset contains **1,000,000 synthetically generated taxi-trip records**. It is not official NYC Taxi and Limousine Commission (TLC) data. Dashboard results describe this synthetic dataset only and must not be presented as real-world findings.

## Table of Contents

- [Project Overview](#project-overview)
- [Business Problem](#business-problem)
- [Project Objectives](#project-objectives)
- [Tools and Technologies](#tools-and-technologies)
- [Dataset Description](#dataset-description)
- [Data Model](#data-model)
- [Dashboard Pages](#dashboard-pages)
- [Key Metrics and DAX](#key-metrics-and-dax)
- [Power Query and Data Quality](#power-query-and-data-quality)
- [How to Run the Project](#how-to-run-the-project)
- [Validation and Testing](#validation-and-testing)
- [Key Analytical Questions](#key-analytical-questions)
- [Known Limitations](#known-limitations)
- [Future Improvements](#future-improvements)
- [Repository Structure](#repository-structure)
- [Resume Description](#resume-description)
- [License and Attribution](#license-and-attribution)

---

## Project Overview

The **Urban Mobility & Transportation Intelligence Dashboard** is a business-intelligence project built in Power BI. It transforms trip-level data into an interactive report for examining demand over time, fare and trip characteristics, pickup/drop-off locations, and data-quality exceptions.

The project emphasizes a reusable semantic model, DAX measures, Power Query transformations, interactive filtering, and clear executive-facing visual design.

| Item | Description |
|---|---|
| Project type | Business Intelligence / Data Analytics |
| Primary tool | Microsoft Power BI Desktop |
| Dataset size | 1,000,000 synthetic trip records |
| Reporting period | 2024, as generated in the practice dataset |
| Fact-table grain | One row per generated taxi trip |
| Main techniques | Power Query, star schema, DAX, time intelligence, exception flags |
| Report pages | 5 |
| Intended audience | Analysts, operations teams, business stakeholders |

## Business Problem

Urban transportation operations generate large volumes of trip records. Decision-makers may need to understand when demand peaks, which pickup areas generate the most trips, how recorded fares vary with trip characteristics, and whether the underlying data contains suspicious or incomplete records.

This project demonstrates how a BI analyst could bring those questions together in one report. Because the supplied dataset is synthetic, the report demonstrates analytical methods rather than assessing actual taxi operations.

## Project Objectives

- Summarize trip volume and recorded charges using executive KPIs.
- Identify demand patterns by month, hour, weekday, borough, and pickup zone.
- Explore fare components, distance, duration, tips, and payment types.
- Compare pickup and drop-off locations and rank frequent routes.
- Flag selected data-quality anomalies for investigation.
- Build a consistent, interactive five-page Power BI report.
- Demonstrate reusable DAX measures and a dimensional data model.

## Tools and Technologies

- **Power BI Desktop** — report pages, visuals, semantic model, slicers, drill-through, and interactions.
- **Power Query (M)** — data import, type conversion, date/time derivation, and data preparation.
- **DAX** — KPIs, time intelligence, percentage change, ranking, rolling calculations, and data-quality measures.
- **CSV** — source tables.
- **GitHub** — project documentation, versioning, and portfolio presentation.

---

## Dataset Description

The generated dataset is distributed as separate CSV files. The principal table contains one million trip records; the remaining files provide lookup attributes.

| File | Approx. rows | Purpose |
|---|---:|---|
| `fact_taxi_trips.csv` | 1,000,000 | Trip-level fact table |
| `dim_location.csv` | 265 | Location ID, zone name, borough, and service-area code |
| `dim_vendor.csv` | 4 | Vendor lookup |
| `dim_payment_type.csv` | 6 | Payment type descriptions |
| `dim_rate_code.csv` | 7 | Rate-code descriptions |

### Main fact-table fields

The fact table includes fields such as:

- `trip_id` — generated unique trip identifier
- `VendorID` — vendor key
- `tpep_pickup_datetime` and `tpep_dropoff_datetime` — trip timestamps
- `passenger_count` — generated passenger count
- `trip_distance` — generated trip distance
- `PULocationID` and `DOLocationID` — pickup and drop-off location keys
- `RatecodeID` and `payment_type` — lookup keys
- `fare_amount`, `tip_amount`, `tolls_amount`, `extra`, and surcharge fields
- `total_amount` — generated total charge for the trip

Check the exact column names and types against the CSV files before recreating the report.

### Intentional test anomalies

A small proportion of generated records intentionally contain cases such as:

- Zero trip distance
- Drop-off timestamp earlier than pickup timestamp
- Missing pickup location ID

These are **synthetic test cases** included to demonstrate validation logic. Their frequency must not be interpreted as real-world anomaly prevalence.

### Metric interpretation

`total_amount` is a generated trip-charge field. It is **not profit**. The dataset does not provide a verified operating-cost model, so the dashboard should not claim profit, margin, or profitability.

---

## Data Model

The report uses a dimensional model centered on `FactTaxiTrips`.

### Fact table

`FactTaxiTrips` contains one row per generated trip. Measures such as trip count, recorded charges, fare, tips, distance, and duration are calculated from this table.

### Dimension tables

- `DimVendor`
- `DimPaymentType`
- `DimRateCode`
- `DimPickupLocation`
- `DimDropoffLocation`
- `DimDate`

The pickup and drop-off location tables are role-playing copies of the location dimension. This allows the model to analyze trip origins and destinations independently.

### Recommended relationships

| One-side table and key | Many-side table and key | Cardinality |
|---|---|---|
| `DimVendor[VendorID]` | `FactTaxiTrips[VendorID]` | One-to-many |
| `DimPaymentType[payment_type]` | `FactTaxiTrips[payment_type]` | One-to-many |
| `DimRateCode[RatecodeID]` | `FactTaxiTrips[RatecodeID]` | One-to-many |
| `DimPickupLocation[LocationID]` | `FactTaxiTrips[PULocationID]` | One-to-many |
| `DimDropoffLocation[LocationID]` | `FactTaxiTrips[DOLocationID]` | One-to-many |
| `DimDate[Date]` | `FactTaxiTrips[PickupDate]` | One-to-many |

Use single-direction filtering from dimensions to the fact table unless a specific, justified requirement calls for another approach. Confirm dimension keys are unique before creating relationships.

### Date modeling

Create a calendar table with year, quarter, month, year-month, weekday, and weekday-number attributes. Mark it as the date table and sort month labels chronologically. Use the pickup-date relationship as the primary active date relationship. For drop-off-date analysis, use a separate role-playing date dimension or a deliberately inactive relationship.

---

## Dashboard Pages

The report is designed with a shared **Midnight Navy + Teal** theme on a 1920 × 1080 Full HD canvas.

### 1. Executive Overview

**Purpose:** Provide a high-level view of trip activity and recorded charges.

**Suggested KPIs**
- Total Trips
- Total Recorded Charges
- Average Fare per Trip
- Average Trip Duration

**Visuals**
- Trips by Pickup Borough
- Trips by Pickup Hour
- Monthly Trip Trend
- Payment Type Distribution

**Interactions:** Date, pickup borough, and payment type slicers; chart tooltips; cross-filtering between visuals.

### 2. Demand & Time Intelligence

**Purpose:** Understand when trip demand is highest and how it changes over time.

**Suggested KPIs**
- Peak Pickup Hour
- Busiest Weekday
- Month-over-Month Trip Growth

**Visuals**
- Monthly demand trend
- Trips by pickup hour
- Demand by weekday
- Daily trips with a rolling-average comparison

**Techniques:** Calendar table, previous-period measures, month-over-month comparisons, and rolling-window calculations.

### 3. Fare & Trip Economics

**Purpose:** Explore how trip characteristics relate to generated fare amounts.

**Suggested KPIs**
- Total Fare Amount
- Total Tips
- Average Fare per Trip
- Average Trip Distance

**Visuals**
- Average fare by distance band
- Fare-component breakdown
- Trip distance versus fare scatter plot
- Recorded charges by payment type

**Important:** These are fare and charge analyses, not profit analyses. No operating-cost data is supplied.

### 4. Geographic Intelligence

**Purpose:** Compare activity by pickup and drop-off locations.

**Suggested KPIs**
- Top Pickup Borough
- Top Pickup Zone
- Top Drop-off Zone
- Most Frequent Route

**Visuals**
- Trips by pickup zone
- Top 10 pickup zones
- Trips by borough
- Pickup-to-drop-off route matrix
- Map, only when validated geographic coordinates or boundary data are available

**Geographic caveat:** The generated location lookup is for modeling practice and is not a verified geographic boundary dataset. Validate location metadata before presenting a geographically accurate map or making geographic claims.

### 5. Data Quality & Audit

**Purpose:** Surface records that need investigation before the data is trusted.

**Suggested KPIs**
- Zero Distance Trips
- Invalid Duration Trips
- Missing Pickup Location Trips
- Distinct Trips with Exceptions

**Visuals**
- Exceptions by type
- Valid versus flagged records
- Exceptions by hour or location
- Trip-level exception table

**Counting rule:** A trip can trigger more than one issue. Clearly distinguish *issue instances* from *distinct trips with at least one issue*.

---

## Key Metrics and DAX

The following examples assume the model uses the table and column names shown above. Adapt names to the final model as needed.

### Core measures

```dax
Total Trips =
COUNTROWS ( FactTaxiTrips )

Total Recorded Charges =
SUM ( FactTaxiTrips[total_amount] )

Total Fare Amount =
SUM ( FactTaxiTrips[fare_amount] )

Average Fare per Trip =
DIVIDE ( [Total Fare Amount], [Total Trips] )

Total Tips =
SUM ( FactTaxiTrips[tip_amount] )

Average Trip Distance =
AVERAGE ( FactTaxiTrips[trip_distance] )

Average Trip Duration =
AVERAGE ( FactTaxiTrips[TripDurationMinutes] )


## Power Query and Data Quality

The Power Query workflow should be repeatable and documented.

1. Import the CSV tables using **Get Data → Text/CSV**.
2. Set timestamps to Date/Time, dates to Date, IDs to appropriate whole-number types, and monetary fields to numeric types.
3. Derive `PickupDate`, `DropoffDate`, `PickupHour`, `PickupDayName`, and `TripDurationMinutes`.
4. Inspect nulls, duplicate `trip_id` values, invalid timestamps, non-positive distances, and unmatched location keys.
5. Preserve raw source values where possible; use explicit flags or a separate exception table rather than silently deleting suspicious records.
6. Confirm dimension keys are unique and fact-table keys have expected behavior.
7. Load the model and validate measures against source-table totals.

Example Power Query duration expression:

```powerquery
Duration.TotalMinutes(
    [tpep_dropoff_datetime] - [tpep_pickup_datetime]
)
```

---

## How to Run the Project

### Requirements

- Power BI Desktop
- The CSV dataset files
- Sufficient memory and storage for a one-million-row fact table

### Setup

1. Download or clone this repository.
2. Extract the dataset archive, if supplied separately.
3. Open Power BI Desktop.
4. Select **Get Data → Text/CSV** and import the fact table and lookup tables.
5. Open **Transform Data** and verify data types and transformation steps.
6. Create the dimension tables and relationships described in [Data Model](#data-model).
7. Create the date table and measures.
8. Build the five report pages using the design guide.
9. Validate filters, relationships, totals, and anomaly measures.
10. Save the report as a `.pbix` file.

If the PBIX uses local file paths, update the data-source paths in Power Query when opening it on another machine.

---

## Validation and Testing

Before treating the report as complete, verify:

- The fact table has the expected row count of 1,000,000.
- `trip_id` uniqueness is tested.
- Numeric measures match source-table aggregations under the same filters.
- Location dimension keys are unique.
- Pickup and drop-off relationships return the intended labels.
- Month labels sort chronologically.
- Date slicers filter all intended visuals.
- Zero-distance, invalid-duration, and missing-pickup checks detect the generated test cases.
- Exception totals are clearly defined as either issue instances or distinct affected trips.
- Rankings and percentage measures behave correctly under slicers.
- Generated metrics are not described as real-world operational findings.

---

## Key Analytical Questions

1. How does trip volume change by month?
2. Which pickup hours have the highest generated trip counts?
3. How does demand vary by weekday?
4. Which boroughs and pickup zones have the most trips?
5. How do average fare and recorded charges vary by distance?
6. How are trips distributed across payment types?
7. Which routes appear most frequently in the generated data?
8. How many records have zero distance, invalid duration, or missing pickup locations?
9. Do trends and rankings change when date, borough, or payment filters are applied?

Answers should be calculated from the final loaded dataset and documented with applicable filters and definitions.

## Known Limitations

- All supplied trip records are synthetic; they do not represent official NYC TLC records.
- The generated location lookup is not a verified geographic boundary dataset.
- `total_amount` is a generated charge field, not profit or verified company revenue.
- Intentional anomalies were inserted for demonstration and do not establish real-world data-quality rates.
- Dashboard values, screenshots, and insights should be identified as illustrative or synthetic unless independently validated against a real source.

## Future Improvements

- Replace or supplement the practice dataset with a properly cited official transportation dataset.
- Add validated geographic coordinates or boundary files for mapping.
- Add a dedicated trip-level drill-through page.
- Implement dynamic metric selection using a disconnected table and `SWITCH`.
- Add carefully defined rolling averages and period comparisons.
- Optimize model size and visual performance.
- Add automated reconciliation tests and a documented data dictionary.
- Publish a report walkthrough with screenshots and a short explanation of the main findings.

---
## License and Attribution

The generated practice dataset is synthetic. If you incorporate third-party datasets, map boundaries, icons, or other assets in future versions, review their license and attribution requirements and document the sources here.

This README describes the intended project design. Update it to match the final PBIX, actual measures, screenshots, data sources, and validations before publishing the repository.
