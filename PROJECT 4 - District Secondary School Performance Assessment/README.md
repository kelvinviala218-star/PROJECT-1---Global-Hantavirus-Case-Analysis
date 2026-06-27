# 🎓 Ghana Education Service — District Secondary School Performance Assessment
## Academic Year 2023/2024

## Overview

This project is a three-page education analytics dashboard built to assess the academic and operational performance of 45 public secondary schools across all 16 regions of Ghana for the 2023/2024 academic year. The analysis was commissioned by the Ghana Education Service (GES) to support the Ministry of Education's budget allocation and intervention decisions ahead of the 2025/2026 academic year — identifying which schools need urgent intervention, which regions are most underserved, and where resources should be directed for maximum impact.

---

## Business Problem

Growing regional inequality in academic outcomes and declining national exam pass rates have placed pressure on the Ministry of Education to make data-driven resource allocation decisions. This dashboard was built to answer four key questions:

1. Which schools are consistently producing poor academic outcomes and need urgent intervention?
2. Do resource levels; teachers, funding, infrastructure, explain performance gaps, or are other factors at play?
3. Which schools should be prioritised for additional teachers, funding, and academic support in 2025/2026?
4. Do gender enrollment gaps exist, and do they correlate with weaker academic outcomes?

---

## Tools Used

- **Power BI Desktop** — Three-page dashboard design, scatter plot, and interactive cross-filtering
- **Power Query (M)** — Data cleaning, term sorting, and column type standardisation
- **DAX** — Custom measures including School Performance Indicator, Teacher Qualification Rate, Gender Enrollment Gap, Funding Per Student, and Student-to-Teacher Ratio
- **CSV** — Source dataset ingestion and initial profiling

---

## Key Findings

- **22 of 45 schools need urgent intervention** — nearly half the network is underperforming on exam pass rates, with Kintampo SHS (32.77%), Tamale Girls SHS (31.18%), and Juaben SHS (30.82%) recording the lowest average pass rates across the academic year
- **Labone Secondary School (90.16%), Mfantsipim School (89.36%), and Accra Academy (86.96%) are the top performers** — all located in Greater Accra and Ashanti, highlighting significant regional inequality
- **Schools with gender enrollment gaps above 0.2 have significantly lower pass rates** — suggesting that gender exclusion and academic underperformance are closely linked
- **Term 3 shows a steep decline in performance** — attendance drops and dropout rates rise in the final term, particularly in underserved regions
- **Oti is the most under-resourced region** — with only GHS 123 funding per student and an average infrastructure score of 3.2 out of 10, the lowest of all 16 regions
- **Schools without internet access show significantly lower pass rates** — averaging 40–55%, compared to approximately 80% for schools with internet access

---

## Dashboard Preview
<img width="1217" height="702" alt="dashboard_preview" src="https://github.com/user-attachments/assets/75ebe4fc-3626-457e-b0a3-dc317a4cbbd9" />
<img width="916" height="533" alt="dashboard_preview1" src="https://github.com/user-attachments/assets/f1354be7-0a20-4712-b0eb-8a607e60f4a1" />


> Please refer to `District Secondary School Performance Assessment.pdf` in this repository for the full three-page dashboard layout.

---

## Performance Indicator Framework

Each school was classified into one of three categories based on their average exam pass rate across all three terms:

| Indicator | Pass Rate Threshold |
|---|---|
| 🟢 Excellent | Average pass rate ≥ 70% |
| 🟡 Good | Average pass rate ≥ 50% |
| 🔴 Needs Intervention | Average pass rate < 50% |

---

## Dataset

The analysis uses a simulated but realistic dataset of 135 rows — 45 schools × 3 terms — covering Term 1, Term 2, and Term 3 of the 2023/2024 academic year. The dataset was designed to reflect real patterns in Ghanaian public secondary education including regional performance variation, gender enrollment gaps in northern regions, and infrastructure inequality across the 16 regions.

| Column | Description |
|---|---|
| school_id | Unique school identifier (e.g. GES-001) |
| school_name | School name |
| region | One of Ghana's 16 regions |
| district | District within the region |
| school_type | Day, Boarding, or Day/Boarding |
| term | Term 1, Term 2, or Term 3 |
| total_enrollment | Total number of students enrolled |
| male_enrollment | Number of male students |
| female_enrollment | Number of female students |
| total_teachers | Number of teachers on staff |
| qualified_teachers | Number of teachers with professional qualifications |
| avg_class_size | Average number of students per class |
| attendance_rate | Average student attendance rate (%) |
| exam_pass_rate | Percentage of students who passed end of term exams |
| top_grade_rate | Percentage of students achieving A or B grades |
| dropout_rate | Percentage of students who dropped out during the term |
| extracurricular_programs | Number of extracurricular programs offered |
| school_funding_ghs | Total funding received in the term (GHS) |
| infrastructure_score | School facilities rating out of 10 |
| internet_access | Whether the school has internet access (Yes/No) |

---

## DAX Measures

Key measures created for this analysis:

```dax
-- School Performance Indicator (Calculated Column)
School Performance Indicator = 
VAR AvgPassRate = 
    CALCULATE(
        AVERAGE('ges_school_performance_2023_24'[exam_pass_rate]),
        ALLEXCEPT(
            'ges_school_performance_2023_24',
            'ges_school_performance_2023_24'[school_name]
        )
    )
RETURN
SWITCH(
    TRUE(),
    AvgPassRate >= 0.70, "Excellent",
    AvgPassRate >= 0.50, "Good",
    "Needs Intervention"
)

-- Teacher Qualification Rate
Teacher Qualification Rate = 
DIVIDE(
    SUM('ges_school_performance_2023_24'[qualified_teachers]),
    SUM('ges_school_performance_2023_24'[total_teachers])
)

-- Gender Enrollment Gap
Gender Enrollment Gap = 
DIVIDE(
    SUM('ges_school_performance_2023_24'[male_enrollment]) - 
    SUM('ges_school_performance_2023_24'[female_enrollment]),
    SUM('ges_school_performance_2023_24'[total_enrollment])
)

-- Funding Per Student
Funding Per Student = 
DIVIDE(
    SUM('ges_school_performance_2023_24'[school_funding_ghs]),
    SUM('ges_school_performance_2023_24'[total_enrollment])
)

-- Student to Teacher Ratio
Student Teacher Ratio = 
DIVIDE(
    SUM('ges_school_performance_2023_24'[total_enrollment]),
    SUM('ges_school_performance_2023_24'[total_teachers])
)
```

---

## How to Use

1. Download the `.pbix` file and open in Power BI Desktop
2. Use the **Region**, **District**, and **Term** slicers to filter all visuals simultaneously
3. Navigate between the three pages using the sidebar buttons:
   - **Page 1 — School Performance Overview** — KPIs, scatter plot, performance table, and key insights
   - **Page 2 — Term Trends, Gender Equity and Access** — Term-by-term trends, gender breakdown, internet access analysis, and regional pass rates
   - **Page 3 — Resource Gaps and Investment Priorities** — Funding per student, infrastructure scores, and the bottom 24 schools by resource level

---

## Note on Dataset

This project uses a simulated dataset created to reflect realistic conditions in Ghana's public secondary education system. Real school names have been used for authenticity, but all performance figures are fictional and intended purely as a portfolio demonstration of education analytics and Power BI skills.

