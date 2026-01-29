# LAB ON EXTRACT-TRANSFORM-LOAD PROCESS DESIGN FOR THE ACME-FLYING USE CASE

## Overview
This project involves creating an Extract-Transform-Load (ETL) process for the ACME-Flying use case. The goal is to extract data from AIMS and AMOS operational databases and additional provided sources, transform this data to conform to previously defined star schemas (from the Data Warehouse design lab), and load the data into these schemas. Additionally, the process focuses on improving the quality of the designed ETL workflow.

## Instructions

The designed ETL process must adhere to the following:

### Extraction
- Connect to the **AIMS** and **AMOS** operational databases to extract base operational data.
- Use additional data sources:
  - `aircraft-manufaturerinfo-lookup.csv`
  - `maintenance-personnel-airport-lookup.csv`

### Transformation
- **Integrate AIMS and AMOS Data:**
  - Common attribute: `flightID` (AIMS `Flights` <-> AMOS `OperationInterruption`)
  - Common attribute: `aircraftRegistration` (AIMS `Slots` <-> AMOS `MaintenanceEvents`, `WorkOrders`)
- **Complement Operational Data (Lookups):**
  - **Aircraft Manufacturer:** Use `aircraft-manufacturerinfo-lookup.csv` to map `aircraft registration code` to `manufacturer registration code`, `aircraft model`, and `manufacturer`.
  - **Maintenance Personnel:** Use `maintenance-personnel-airport-lookup.csv` to map maintenance personnel (e.g., `reporteurID` in `TechnicalLogBookOrders`) to their **working airport**.
- **Improve Data Quality:**
  - Remove duplicates/overlaps and incomplete records.
  - Correct attribute consistency problems to guarantee business rules.
  - *Note:* If removing records, make them available for offline analysis. If fixing values, justify the decision and assumptions.
- **Derive Additional Attributes:**
  - Calculate required KPIs (e.g., Value conversion, formula calculation).
  - *Example:* `Flight Hours (FH)` = `actualArrival` - `actualDeparture`.
  - *Example:* `Flight Cycles (TO)` = Count of non-cancelled flights in `Flights` table.

### Loading
- **Load Dimension Tables:**
  - Enable navigation through different aggregation levels (roll-up/drill-down).
  - *Example:* Aircraft dimension with model information.
- **Load Fact Tables:**
  - Enable calculation of all metrics needed for required KPIs.

### ETL Process Quality
Improve the following quality factors:
- **Performance:** Focus on execution time (e.g., parallelization, resource allocation).
- **Reliability:** Focus on robustness (handling unpredictable input) and recoverability (checkpoints, data recovery in case of failure).

## Approaches
You may choose one of the following approaches:
1.  **GUI-Based ETL Tool:** Use **Talend** to design and implement the process.
2.  **Programmatic (Hand-coded):** Use a programming language like **Python** or **Java**.

*Self-Evaluation:* Regardless of the approach, you must self-evaluate the ETL process against the eight dimensions of the ETL process quality rubric and justify how it fulfills each.

## Deliverables
1.  **Project Archive:** A single `.zip` file containing the Talend Open Studio project or Python/Java project (data and control flows).
2.  **Report (PDF):**
    - Max 3 A4 pages, 2.5cm margins, font size 12, inline space 1.15.
    - Content: Assumptions made, justification of decisions, and self-evaluation of the ETL process quality rubric.

## Evaluation Criteria
- **Conciseness of explanations**
- **Understandability**
- **Coherence**
- **Soundness**

### Grading
- **60%**: Deliverables
- **40%**: Exercises related to the project done individually in the classroom (Partial Exam day)
