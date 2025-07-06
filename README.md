# Healthcare Readmission Analysis with Social Determinants of Health (SDoH)
## This project demonstrates a sophisticated BI analysis that goes beyond internal data to generate deeper insights. It simulates a scenario where a healthcare provider wants to understand the external factors affecting patient readmission rates. The project involves an ETL pipeline that integrates an internal patient data export with an external CSV.

**Live Demo:** [https://colab.research.google.com/drive/1eAGncBP_cxBoUllG9orF0GVncxV0Cin4?usp=sharing]

## Project Overview

This project demonstrates a sophisticated BI analysis that goes beyond internal data to generate deeper insights. It simulates a scenario where a healthcare provider wants to understand the external factors affecting patient readmission rates. The project involves an ETL pipeline that integrates an internal patient data export with an external, public CSV containing Social Determinants of Health (SDoH) data. The final output is an analytical dashboard that identifies correlations between socioeconomic factors and health outcomes, and pinpoints geographic areas that may require community-level interventions.

## Business Problem

A hospital network is being financially penalized for high 30-day patient readmission rates. While they have internal data on clinical factors, the leadership team hypothesizes that non-clinical, community-level factors are a major driver of readmissions. They need to answer:
*   Do patients from areas with higher poverty rates or lower income have higher readmission rates?
*   Can we identify geographic "hotspots" where readmissions are unusually high?
*   How can we use data to support resource allocation for community health programs?

To answer this, they need a data analyst to blend their internal patient data CSV with a public SDoH data CSV.

## Solution Architecture

The solution involves a Python pipeline to perform the data blending and analysis, creating an enriched dataset ready for a data warehouse and BI tools.


## Data Blending and Enrichment

The technical core of this project is the **data blending** step. This is a common and highly valuable skill for a Data/BI Analyst.

*   **Common Key:** The internal and external datasets did not share a common patient ID. However, both contained a geographic identifier (`hospital_zip_code` in the patient data and `zip_code` in the SDoH data). This was used as the **join key**.
*   **Enrichment:** By performing a `left join` from the patient data to the SDoH data, each patient encounter record was "enriched" with the socioeconomic context of the community where the hospital is located. This created a powerful new dataset that allows for a much richer analysis than either source could provide on its own.

## Key Skills & Technologies Demonstrated

*   **ETL and Data Blending:** Ingesting and cleaning data from different sources and joining them on a common key using **Pandas**.
*   **Data Aggregation:** Using `groupby` to transition from individual patient-level data to aggregated, community-level insights.
*   **Statistical Analysis:** Using a regression trendline (`OLS`) in **Plotly Express** to visually test the correlation between socioeconomic variables and health outcomes.
*   **Data Warehousing Concepts:** Staging the raw, cleaned, and aggregated data in a **SQLite** database, simulating a real-world BI architecture.
*   **Data Visualization for Insight:**
    *   Creating a **Scatter Plot** to explore complex relationships between multiple variables (poverty, readmissions, income, and encounter volume).
    *   Using a **Bar Chart** effectively to highlight geographic disparities and identify "hotspots."

## Key Insights & Visualizations

### SDoH Correlation Analysis

 <!-- Replace with a screenshot of your scatter plot -->

This scatter plot directly addresses the core business question. The upward-sloping trendline provides strong visual evidence of a positive correlation between community poverty rates and hospital readmission rates.

**Insights:**

*   **The Trend:** As the poverty rate in a hospital's community increases, the 30-day readmission rate also tends to increase.
*   **Actionable Intelligence:** This finding suggests that purely clinical, in-hospital interventions may not be enough. To truly reduce readmissions, the hospital network may need to invest in community-based programs, such as patient transport services, nutrition assistance, or partnerships with social workers.

### Geographic Hotspot Identification

 <!-- Replace with a screenshot of your bar chart -->

This chart translates the data into a simple operational view. It ranks hospital locations by their readmission rate, immediately showing leadership where the biggest problems are.

**Insights:**

*   **Prioritization:** The hospital network can now clearly see which communities (e.g., Miami-Dade and Harris County in the sample data) are "hotspots" and should be prioritized for intervention.
*   **Resource Allocation:** This provides a data-driven justification for allocating more resources, staff, or new programs to the highest-risk areas.

## How to Run the Project

1.  Clone this repository.
2.  Open the `healthcare_sdoh_analysis.ipynb` file in Google Colab or a local Jupyter environment.
3.  The notebook is self-contained. It downloads one public dataset and simulates the other, so no external file uploads are needed.
4.  Run all cells to execute the full data blending pipeline and generate the analytical visualizations.
