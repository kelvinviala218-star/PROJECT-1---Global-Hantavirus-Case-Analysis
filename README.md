## Global Hantavirus Epidemiological Analysis Dashboard

### Overview
This project presents an interactive public health intelligence dashboard built to analyze global Hantavirus outbreak trends, transmission dynamics, and clinical severity metric. Tracking 2,000 active cases across 10 countries between January 2025 and May 2026, the analysis translates complex zoonotic and epidemiological data into high-impact visual narratives. The dashboard provides health agencies, clinical researchers, and environmental management teams with actionable insights to allocate medical resources, optimize localized containment strategies, and mitigate cross-border viral transmission.

### Problem
Epidemiological anomalies and complex viral mutations make tracking infectious diseases exceptionally challenging for international health bodies. Without integrated, localized data, public health resource distribution is frequently reactive rather than preventative. This dashboard was built to support critical, data-backed interventions, specifically answering:
1. Which regional hotspots exhibit significantly higher Case Fatality Rates (CFR) requiring targeted deployment of therapeutics and critical care resources?
2. Which virus strains and specific environmental exposure sources represent the most severe vectors of community transmission?
3. What patient demographic cohorts suffer from disproportionate clinical severity, necessitating tailored clinical protocols and public awareness campaigns?

### Tools Used
*   Power BI Desktop: Core dashboard architecture, interactive cross-filtering interfaces, and data storytelling.
*   Power Query (M): Data ingestion, field schema cleaning, structural standardization, and multi-field conditional formatting.
*   DAX (Data Analysis Expressions): Custom epidemiological metrics including dynamic Case Fatality Rates (CFR %), Hospitalization Rates %, and rolling case volume totals.
*   Excel: Initial data profiling and quality screening of the core epidemiological dataset.

### Key Findings
*   Regional Hotspots & High-Risk Zones: While cases are spread across 10 countries, Argentina and Chile exhibit the highest clinical severity, recording     alarming Case Fatality Rates of 10.9% and 10.0% respectively. 
*   Strain-Specific Lethality: Outbreak analysis revealed that the **Seoul** strain (8.70% CFR) and **Dobrava** strain (8.53% CFR) are the most lethal variants globally, despite **Sin Nombre exhibiting the highest overall raw case count at 21.55% of total infections.
*   Demographic Vulnerabilities: A distinct age-skewed mortality gap was identified; middle-aged adults between 36–50 comprise the highest-risk group with a   9.19% fatality rate, notably outpacing older cohorts and youth. 
*   Socio-Environmental Drivers: Transmission vectors are split nearly equally between *Human-to-Human* (50.05%) and *Rodent-to-Human* (49.95%) paths. Commercial/travel environments like Cruise Exposures (354 cases) and Warehouse Exposures (346 cases) represent the most frequent sources of viral acquisition.


### Dataset
The project utilizes the `Global Hantavirus Dataset.csv`, a comprehensive collection of 2,000 detailed epidemiological records mapping real-time infectious disease tracking. Key attributes modeled include:
*   Patient Profiles: Unique case identifiers (`case_id`), Age, Gender, and presenting Clinical Symptoms (e.g., Fever, Muscle Pain, Cough).
*   **Epidemiological Vectors:** Specific `virus_strain`, `transmission_type` (Zoonotic vs. Community Transmission), and localized `exposure_source`.
*   **Clinical & Environmental Metrics:** Hospitalization records, clinical mortality markers (`fatality`), recovery durations, alongside regional climate indices such as localized temperature, humidity levels, and rodent presence indicators.
