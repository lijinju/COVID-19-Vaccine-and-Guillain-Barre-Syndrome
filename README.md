
## 📖 Overview
This repository contains the data processing pipeline and analytic code for a large-scale retrospective cohort study emulating to evaluate the incidence of **Guillain-Barré Syndrome (GBS)** following **COVID-19 vaccination**. 

The pipeline is built on the **OMOP Common Data Model (CDM)** and utilizes advanced epidemiological safeguards to handle immortal time bias, competing risks, and surveillance bias.

## Study Design: Target Trial Emulation
The study emulates a target trial with a primary **30-day risk window** (with sensitivity analyses at 60 and 90 days) starting from `Time_Zero`.


### Cohort Allocation
Study participants were assigned to mutually exclusive exposure groups according to the first qualifying event occurring on or after December 11, 2020.

**Vaccination-First Cohort**: Index date defined by the first (or second, for dose-specific analyses) COVID-19 vaccine administration.

**Infection-First Cohort**: Index date defined by the first documented SARS-CoV-2 infection.

**Visit-First Control Cohort**: Index date defined by the routine medical visit / well-check, serving as a contemporary control group to account for healthcare-seeking behavior.


<img width="1003" height="578" alt="image" src="https://github.com/user-attachments/assets/73c458a3-81e4-4c72-84b8-caa26c56957e" />

We additionally evaluated a sequential exposure cohort consisting of individuals who received COVID-19 vaccination and subsequently developed SARS-CoV-2 infection.

### Epidemiological Surveillance Measures
* **Prevalent Case Exclusion:** 365-day lookback to exclude patients with prior GBS diagnoses.
* **Competing Risks:** Survival time is censored at the date of death if the patient dies before developing GBS.
* **Surveillance Bias Adjustment:** Baseline healthcare utilization (Outpatient, ER, Inpatient visit counts) is calculated and adjusted for.


