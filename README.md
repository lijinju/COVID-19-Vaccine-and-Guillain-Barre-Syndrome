
## 📖 Overview
This repository contains the reproducible data pipeline and analysis code for a large-scale retrospective cohort study emulating a **Target Trial** to evaluate the incidence, risk factors, and severe outcomes of **Guillain-Barré Syndrome (GBS)** following **COVID-19 vaccination** and/or **SARS-CoV-2 infection**. 

The pipeline is built on the **OMOP Common Data Model (CDM)** and utilizes advanced epidemiological safeguards to handle immortal time bias, competing risks, and surveillance bias. It is designed to be executed on any OHDSI-compliant database (e.g., PostgreSQL, BigQuery, Snowflake, Databricks, Spark SQL).

## 🎯 Study Design: Target Trial Emulation
The study emulates a target trial with a primary **30-day risk window** (with sensitivity analyses at 60 and 90 days) starting from `Time_Zero`.

### Cohort Allocation
To prevent **immortal time bias**, patients are assigned to mutually exclusive groups based on their *first* occurring event after the pandemic/vaccine onset (`2020-12-11`):
1. **Vaccine First:** Index date = 1st (or 2nd) COVID-19 vaccine dose.
2. **Infection First:** Index date = 1st confirmed SARS-CoV-2 infection.
3. **Visit First (Negative Control):** Index date = Routine medical visit / Well-check (Controls for healthcare-seeking behavior and surveillance bias).
4. **Sequential:** Vaccinated, then subsequently infected.

### Epidemiological Surveillance Measures
* **Prevalent Case Exclusion:** 365-day lookback to exclude patients with prior GBS diagnoses.
* **Competing Risks:** Survival time is censored at the date of death if the patient dies before developing GBS.
* **Surveillance Bias Adjustment:** Baseline healthcare utilization (Outpatient, ER, Inpatient visit counts) is calculated and adjusted for.

## 🔬 Statistical Analysis Features

- **Primary Analysis**: Incidence rates and risk differences in 30-day window
- **Censoring**: Right-censoring at death or end of risk window
- **Sensitivity Analyses**:
  - 60-day and 90-day risk windows
  - Second-dose cohort
  - COVID-19 vaccine only for excluding the other co-administarion of vaccines
  - Variant-period stratification
- **Baseline Balance**: Standardized mean differences via Table 1
- **Time-to-Event**: Kaplan-Meier, Cox regression
