# power-bi-report-usage-metrics
An enhanced Power BI usage analytics dashboard that extends the default Usage Metrics report with actionable measures for report adoption, repeat usage, user engagement, meaningful adoption, usage trends, and report performance.


# Project Background

Power BI provides a built-in Usage Metrics report for monitoring report views and users. While useful for basic activity tracking, the default report does not provide enough information to determine whether users return consistently, which reports have become part of their regular workflows, or whether adoption initiatives are producing meaningful results.

This limitation made it difficult for the data analytics team to monitor adoption-related OKRs and identify reports or users requiring further investigation. To address this, I developed an enhanced Power BI Report Usage Metrics dashboard focused on making report adoption, user engagement, and performance more actionable.

The analysis is organized into four key areas:

- **Report Usage and Adoption:** Monitors total views, unique users, average views per user, viewing trends, and the most frequently accessed reports.
- **User Engagement and Retention:** Evaluates repeat usage, meaningful adoption, active days, and each user’s most recent activity.
- **Usage Distribution:** Groups users by activity level to distinguish one-time, occasional, and more engaged users.
- **Report Performance:** Assesses report load times using percentile-based performance metrics to identify potentially slow reports.

The dashboard was designed to answer the following questions:

- Which reports are viewed most frequently?
- How many users return after their first visit?
- How actively and consistently do users engage with reports?
- Which reports demonstrate meaningful adoption?
- Which reports may have performance or adoption issues?
- When was each user last active?

> **Data limitation:** The underlying Power BI Usage Metrics data currently provides approximately one month of historical activity. This limits long-term retention, quarterly adoption, and historical trend analysis.

The DAX measures used to calculate the enhanced usage, engagement, adoption, and performance metrics can be found [here](link).

Definitions of the dashboard metrics and their underlying business logic can be found [here](link).

Dashboard screenshots and a walkthrough of the Power BI report can be found [here](link).


# Data Structure & Initial Checks

The Power BI semantic model contains 14 tables organized into dimension, activity, summary, bridge, and calculation tables. The model separates report-level activity, page-level activity, user engagement, and performance data to prevent metrics with different granularities from being combined incorrectly.

- **Synthetic data:** This public portfolio version uses dummy data to protect confidential business and user information. The semantic-model structure, DAX logic, dashboard design, and analytical use cases reflect the original solution, but the displayed values do not represent actual business performance.
## Model Structure

| Table group | Tables | Purpose |
|---|---|---|
| Dimensions | `Dates`, `Users`, `Reports`, `Report pages` | Provide descriptive attributes and filtering for dates, users, reports, and report pages. |
| Activity tables | `Report views`, `Report page views`, `Report load times`, `Workspace views` | Store usage and performance activity at different levels of detail. |
| Summary tables | `Workspace reports`, `User Engagement Summary` | Provide report-level and user-level aggregations used by the dashboard. |
| Bridge/helper tables | `Users_ReportPageView`, `Report rank`, `Refresh Stats` | Support relationships, report ranking, refresh monitoring, and specialized calculations. |
| Measure table | `Model measures` | Stores the DAX measures used throughout the report. |

## Primary Table Granularity

- **`Report views`:** Report-view activity by date, report, and user.
- **`Report page views`:** Page-view activity by date, report page, and user.
- **`Report load times`:** Individual report-opening and load-time observations.
- **`Workspace views`:** Usage activity across reports in the monitored workspace.
- **`Workspace reports`:** Report-level summary information, including days with usage and usage trends.
- **`User Engagement Summary`:** User-level engagement attributes, including active days and engagement segments.
- **`Users_ReportPageView`:** Supports analysis between users and report-page activity.
- **`Model measures`:** A dedicated table containing reusable DAX calculations rather than transactional records.

## Initial Data and Model Checks

Initial validation of the model focused on the following areas:

- Confirming the available date range and latest refresh time.
- Checking for missing or duplicate user, report, and report-page identifiers.
- Reviewing relationship paths between reports, pages, users, and activity tables to prevent duplicated counts.
- Keeping report views, page views, and load-time observations separate because they have different granularities.
- Comparing summary-table results with the underlying activity tables.
- Reviewing blank, zero, and unusually high load-time values before evaluating report performance.
- Using percentile measures alongside averages because extreme load times can distort the mean.

<img width="1430" height="1375" alt="image" src="https://github.com/user-attachments/assets/aad6cc83-852f-4344-a50d-75680e0425b6" />


# Executive Summary

### Overview of Findings

The analysis demonstrates that report-view volume alone is not sufficient to measure meaningful adoption. Combining views with repeat usage, active days, engagement segments, and reports viewed per user provides stronger evidence of whether reports are becoming part of users’ regular workflows.

Three key takeaways emerge from the enhanced monitoring approach:

- **Adoption requires more than total views.** Repeat User Rate, Meaningful Adoption, and Active Days help distinguish sustained engagement from one-time activity.
- **User-level monitoring makes usage data actionable.** Engagement segments and last-active information help identify highly engaged, occasional, and potentially inactive users.
- **Performance should not rely only on averages.** Percentile measures such as P50, P75, and P90 provide a clearer view of the typical and slower report-loading experiences.

Together, these metrics provide the data analytics team with a more actionable framework for monitoring adoption-related OKRs, prioritizing report improvements, investigating performance issues, and identifying where additional user engagement may be required.

<img width="1456" height="825" alt="image" src="https://github.com/user-attachments/assets/15e2168e-e6db-4ed6-9ee2-552548ee734f" />

<img width="1454" height="818" alt="image" src="https://github.com/user-attachments/assets/c8ed051f-dba5-4578-9045-803cc459c33a" />




# Insights Deep Dive
### Category 1:

* **Main insight 1.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 2.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 3.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 4.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.

[Visualization specific to category 1]


### Category 2:

* **Main insight 1.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 2.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 3.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 4.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.

[Visualization specific to category 2]


### Category 3:

* **Main insight 1.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 2.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 3.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 4.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.

[Visualization specific to category 3]


### Category 4:

* **Main insight 1.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 2.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 3.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 4.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.

[Visualization specific to category 4]



# Recommendations:

Based on the insights and findings above, we would recommend the [stakeholder team] to consider the following: 

* Specific observation that is related to a recommended action. **Recommendation or general guidance based on this observation.**
  
* Specific observation that is related to a recommended action. **Recommendation or general guidance based on this observation.**
  
* Specific observation that is related to a recommended action. **Recommendation or general guidance based on this observation.**
  
* Specific observation that is related to a recommended action. **Recommendation or general guidance based on this observation.**
  
* Specific observation that is related to a recommended action. **Recommendation or general guidance based on this observation.**
  


# Assumptions and Caveats:

Throughout the analysis, multiple assumptions were made to manage challenges with the data. These assumptions and caveats are noted below:

* Assumption 1 (ex: missing country records were for customers based in the US, and were re-coded to be US citizens)
  
* Assumption 1 (ex: data for December 2021 was missing - this was imputed using a combination of historical trends and December 2020 data)
  
* Assumption 1 (ex: because 3% of the refund date column contained non-sensical dates, these were excluded from the analysis)
