# Power BI Report Usage Metrics

An enhanced Power BI usage analytics dashboard that extends the default Usage Metrics report with actionable measures for report adoption, repeat usage, user engagement, meaningful adoption, usage trends, and report performance.


# Project Background

Power BI provides a built-in Usage Metrics report for monitoring report views and users. While useful for basic activity tracking, the default report does not provide enough information to determine whether users return consistently, which reports have become part of their regular workflows, or whether adoption initiatives are producing meaningful results.

This limitation made it difficult for the data analytics team to monitor adoption-related OKRs and identify reports or users requiring further investigation. To address this, I developed an enhanced Power BI Report Usage Metrics dashboard focused on making report adoption, user engagement, and performance more actionable.

The analysis is organized into three key areas:

- **Report Usage and Adoption:** Monitors report and page views, viewing trends, report coverage, and the most frequently accessed content.
- **User Engagement and Retention:** Evaluates adoption, repeat usage, meaningful engagement, active days, reports viewed per user, and user-engagement distribution.
- **Report Performance:** Assesses report load times using average, P50, P75, and P90 measures to identify comparatively slower reports.

The dashboard was designed to answer the following questions:

- Which reports are viewed most frequently?
- How many users return after their first visit?
- How actively and consistently do users engage with reports?
- Which reports demonstrate meaningful adoption?
- Which reports may have performance or adoption issues?
- When was each user last active?

> **Data limitation:** The underlying Power BI Usage Metrics data currently provides approximately one month of historical activity. This limits long-term retention, quarterly adoption, and historical trend analysis.


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

### Why the Default Usage Metrics Report Was Not Sufficient

Microsoft's default Power BI Usage Metrics report provides a useful starting point for understanding report activity. It shows basic indicators such as report views, unique viewers, viewing trends, and usage by user or report page.

<img width="540" height="288" alt="image" src="https://github.com/user-attachments/assets/034cac2e-7264-455a-a759-801526641ab0" />

However, these metrics primarily answer **how much a report was viewed**. They do not sufficiently explain whether users return consistently, how deeply they engage, whether reports are becoming part of their regular workflows, or which reports and users require attention.

This creates a monitoring gap for a data analytics team that needs to track report adoption and support adoption-related OKRs. Important measures such as repeat-user behavior, active days, breadth of report usage, inactive users, meaningful adoption, and detailed report performance are not readily available in the default view.

### Enhanced Usage Monitoring

To address these limitations, I developed an enhanced Usage Metrics dashboard with two analytical perspectives:

- **Report Usage** evaluates report and page consumption, usage trends, report coverage, frequently viewed content, and report-loading performance using average and percentile measures.
- **User Engagement** evaluates adoption rate, repeat-user rate, meaningful adoption, active days, reports viewed per user, engagement distribution, and inactive or one-time users.

<img width="1456" height="825" alt="image" src="https://github.com/user-attachments/assets/15e2168e-e6db-4ed6-9ee2-552548ee734f" />

<img width="1388" height="780" alt="image" src="https://github.com/user-attachments/assets/334992dd-3e68-406c-b1bb-ffa30b90d084" />

### Business Value

The enhanced dashboard changes Usage Metrics from a basic activity report into an actionable monitoring tool. It helps the data analytics team determine whether report usage represents sustained adoption, identify underused or slow-performing reports, understand differences in user engagement, and prioritize follow-up actions with report owners and users.



# Insights Deep Dive

### Category 1: Report Usage and Adoption

The selected reporting period runs from **7 August to 18 August 2026**, with usage data available through **17 August 2026**.

* **All monitored reports received usage during the selected period.** Seven out of seven reports were viewed, resulting in 100% report coverage. However, full coverage only confirms that each report was accessed—it does not demonstrate frequent or sustained adoption.

* **Users interacted with multiple pages after opening the reports.** The dashboard recorded 152 page views from 20 report views, equivalent to approximately 7.6 page-view events per report view. This suggests that users generally navigated through report content rather than leaving immediately after opening it.

* **Overall report activity declined during the comparison period.** The dashboard recorded a negative view trend of 36.4%. This decline should be monitored across subsequent periods to determine whether it represents temporary fluctuation or an ongoing reduction in report usage.

* **Usage was concentrated among several leading reports.** Customer Support Dashboard, IT Operations, Finance Summary, and HR Analytics generated 15 of the 20 report views, representing 75% of selected-report activity. Customer Support Dashboard was the most viewed report, with five views from five users.

<img width="1456" height="825" alt="image" src="https://github.com/user-attachments/assets/39f80110-66ad-41ba-bf43-f666edf6d036" />


### Category 2: User Engagement and Retention

The engagement analysis covers activity from **7 August to 24 August 2026** in the dummy portfolio dataset.

* **Report adoption remained below half of the eligible user population.** The dashboard identified 17 active users, producing an adoption rate of 39.53%. This means that approximately 60.47% of the eligible users did not access any monitored report during the selected period.

* **Most active users did not return on multiple days.** Twelve of the 17 active users were active on only one day, while five users returned on at least two separate days. This produces a Repeat User Rate of 29.41%, showing that initial access was considerably higher than recurring engagement.

* **Cross-report adoption was limited.** Twelve users, or 70.59% of active users, accessed only one report. Four users viewed three to four reports, one user viewed at least five reports, and no users viewed exactly two reports. Although the average was two reports per user, the distribution shows that the majority remained concentrated on a single report.

* **Meaningful engagement was concentrated within a small group of users.** Meaningful Adoption was 29.41%, while users averaged two active days during the selected period. The most engaged user was active on eight days, generated nine report views, and accessed five reports, demonstrating a substantial difference between the most engaged users and the broader user population.

<img width="1388" height="780" alt="image" src="https://github.com/user-attachments/assets/2d4d0d12-2b61-4e1d-ab8c-476a5a092f89" />


### Category 3: Report Performance

The selected reporting period runs from **7 August to 18 August 2026**, with performance data available through **17 August 2026**.

* **The monitored reports recorded an overall average load time of 10.12 seconds.** Individual averages ranged from 7.40 seconds for HR Analytics to 12.75 seconds for Sales Overview, resulting in a 5.35-second difference between the fastest and slowest reports.

* **Sales Overview showed the most consistently elevated load times.** It recorded the highest average load time at 12.75 seconds, the highest median at 16.00 seconds, a P75 of 17.25 seconds, and the highest P90 at 18.30 seconds. Based on its performance across all four measures, it is the strongest candidate for further investigation.

* **Percentile measures revealed intermittent performance issues that averages did not fully capture.** Marketing Dashboard recorded a relatively low average of 9.64 seconds and a median of 7.50 seconds, but its P90 increased to 17.10 seconds. Operations Report showed a similar pattern, increasing from a 10.90-second average to an 18.10-second P90.

* **The performance results provide relative prioritization rather than a formal pass-or-fail assessment.** P90 load times ranged from 13.00 to 18.30 seconds across the monitored reports. Without an agreed performance target, the dashboard can identify comparatively slower reports but cannot determine whether a specific load time breaches an acceptable standard.

<img width="657" height="279" alt="image" src="https://github.com/user-attachments/assets/f5936a31-1512-4cf5-acf8-0c5b3d3d2f27" />

<img width="644" height="479" alt="image" src="https://github.com/user-attachments/assets/a973689e-45c8-40e3-8ee7-e6c246e95c8f" />


# Recommendations

Based on the illustrative findings, the data analytics team and report owners should consider the following actions:

* Report views declined by 36.4% during the comparison period, but the available history is too short to establish whether this represents a sustained decline. **Monitor the trend across several comparable periods and investigate only when the decline persists or affects a business-critical report.**

* The adoption rate was 39.53%, while only 29.41% of active users returned on multiple days. **Define separate targets for initial adoption, repeat usage, and meaningful adoption so that high view volume is not incorrectly treated as sustained engagement.**

* Approximately 70.59% of active users accessed only one report. **Use targeted communication, training, and report recommendations to introduce users to other relevant reports based on their roles and analytical needs.**

* Four reports generated 75% of selected-report activity, while the remaining reports received relatively limited usage. **Prioritize maintenance of high-usage reports and review lower-usage reports for discoverability, relevance, duplication, or possible retirement.**

* Sales Overview showed the highest and most consistently elevated load times, while Marketing Dashboard and Operations Report showed slower P90 experiences. **Investigate these reports first and establish agreed performance thresholds using average, P50, P75, and P90 load times.**

* Power BI Usage Metrics provides only a limited historical window. **Evaluate an independent extraction or snapshot process to preserve usage history and support monthly, quarterly, and long-term adoption analysis.**
  


# Assumptions and Caveats

The analysis and dashboard should be interpreted with the following assumptions and limitations:

* **Synthetic data:** This public portfolio version uses dummy data to protect confidential business and user information. The semantic-model structure, DAX logic, dashboard design, and analytical use cases reflect the original solution, but the displayed values do not represent actual business performance.

* **Limited historical coverage:** The underlying Power BI Usage Metrics source provides approximately one month of historical activity. This limits monthly comparisons, quarterly trend analysis, retention tracking, and evaluation of long-term adoption.

* **Refresh latency:** The latest available usage date may be earlier than the end date selected in the report. Metrics are calculated only from data available at the most recent dataset refresh.

* **User definitions:** An active user is a user with at least one recorded report view during the selected period. A repeat user is an active user who accessed a report on at least two distinct dates.

* **Adoption as a behavioral proxy:** Report views, repeat usage, active days, and reports viewed are used as indicators of adoption. These metrics show interaction with reports but do not prove that the information was understood, acted upon, or produced a measurable business outcome.

* **Report-load interpretation:** Load times may be affected by report design, dataset size, capacity utilization, network conditions, user location, and device performance. A slow observation cannot automatically be attributed to the report itself.

* **No formal performance threshold:** Performance results are evaluated comparatively using average, P50, P75, and P90 load times. Without an agreed target or service-level threshold, the analysis identifies relatively slower reports rather than formally classifying performance as acceptable or unacceptable.
