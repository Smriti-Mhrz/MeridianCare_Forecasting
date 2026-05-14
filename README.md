#Patient Visit Forecasting at MeridianCare
#Overview

This project presents a complete time-series forecasting analysis for MeridianCare, a regional urgent care network operating 31 clinics in the United States. The objective was to forecast patient visits for Q1 2025 (January–March 2025) using ten years of historical monthly data and recommend a statistically and operationally deployable forecasting model.

The analysis combines:

Exploratory Data Analysis (EDA)
Time-series forecasting
Dynamic regression modeling
ARIMA modeling
Model evaluation and diagnostics
Business-focused forecasting decisions
Operational forecasting constraints

The project was developed in R using the fpp3 forecasting framework.

#Business Problem

MeridianCare faces a major operational challenge:

Over-staffing increases labor costs and reduces margins.
Under-staffing causes long patient wait times, walk-outs, service quality issues, and potential regulatory complaints.

The COO required an accurate and defendable forecast to support:

Staffing decisions
Budget allocation
Operational planning
Resource management for Q1 2025
Dataset Description

The dataset contains 120 monthly observations from January 2015 to December 2024.

Variables
Variable	Description
Month	Observation month
Visits	Total patient visits across all clinics
StaffHours	Scheduled clinical staff-hours
Outreach	Community outreach spending
FluIndex	CDC regional influenza severity index
HolidayWeek	Indicator for major holiday periods
Project Objectives

The main goals of this project were to:

Forecast patient visits for Q1 2025.
Compare multiple forecasting approaches.
Select the best deployable forecasting model.
Evaluate forecasting accuracy using holdout validation.
Perform residual diagnostics and model validation.
Translate statistical findings into business recommendations.

#Technologies Used
R
fpp3
tidyverse
lubridate
patchwork
ggplot2
Forecasting Models Evaluated

The following forecasting models were developed and compared:

Model	Description
MEAN	Historical average baseline
SNAIVE	Seasonal naive benchmark
TSLM	Linear regression with trend and seasonality
Pure ARIMA	Automatic ARIMA without regressors
Dynamic Regression M1	Trend + Seasonality + StaffHours + Outreach + HolidayWeek
Dynamic Regression M2	M1 + FluIndex
Dynamic Regression M3	Trend + Seasonality + FluIndex
Exploratory Data Analysis (EDA)

Key findings from the exploratory analysis:

Patient visits showed a strong upward trend over the 10-year period.
Winter months consistently produced peak demand.
Summer months showed lower patient volume.
Holiday periods significantly impacted patient visits.
Flu activity demonstrated a strong relationship with visit demand.
Correlation Analysis
Regressor	Correlation with Visits
FluIndex	0.778
StaffHours	0.503
Outreach	0.105

The FluIndex variable showed the strongest relationship with patient visits.

Pure ARIMA Baseline

The automatic ARIMA model selected:

ARIMA(2,0,2)(1,1,1)[12] with drift

Performance
Metric	Value
RMSE	0.634
MAE	0.542
MASE	0.451
Key Insight

A MASE below 1 confirmed that the ARIMA model outperformed the seasonal naive benchmark.

Dynamic Regression Model Comparison
AICc Results
Model	AICc
M2	225.71
M3	272.87
M1	275.19
Best Statistical Model

M2 achieved the best statistical performance because it incorporated:

FluIndex
StaffHours
Outreach
HolidayWeek

However, operational constraints prevented deployment.

Final Deployment Decision

Although M2 produced the best AICc score, it required future FluIndex values that would not be available before Q1 2025.

Final Deployable Model: M1

The deployed model used:

StaffHours
Outreach
HolidayWeek
Trend and seasonality
Why M1 Was Selected
All regressors were available before forecasting.
The model remained operationally realistic.
MASE remained below 1.
The forecast could be defended in a business environment.

This project emphasizes an important forecasting principle:

The statistically best model is not always the best deployable business model.

Residual Diagnostics

Residual diagnostics were conducted using:

Residual plots
Ljung-Box test
Ljung-Box Test
Metric	Value
p-value	0.6998
Interpretation

The residuals behaved like white noise, indicating:

No significant autocorrelation remained
The model successfully captured systematic patterns
Prediction intervals were reliable
Accuracy Comparison
Holdout Forecast Performance
Model	RMSE	MASE
TSLM	0.6140	0.4344
ARIMA	0.6339	0.4510
DR_M1	0.7599	0.5704
SNAIVE	1.5022	1.0260
MEAN	5.0594	3.5810
Key Result

The deployed dynamic regression model reduced RMSE by:

49.4% compared to the seasonal naive benchmark

Business Insights
Major Operational Insights
Flu severity strongly drives urgent care demand.
Staffing plans are closely aligned with expected patient volume.
Forecast bias toward under-forecasting is operationally dangerous.
Deployability matters as much as statistical accuracy.
Code Review & Forecasting Best Practices

The project also included a review of flawed forecasting code and identified several common forecasting mistakes:

Incorrect time parsing
Improper lag handling inside ARIMA formulas
Incorrect residual diagnostics
Forecasting without future regressor values

This section demonstrates practical forecasting debugging and model validation skills.

Strategic Forecasting for New Markets

The project also evaluated why dynamic regression cannot forecast patient demand for newly opened clinics without historical data.

Recommended Alternatives
Analogue (reference-class) forecasting
Bottom-up market sizing and scenario analysis

This section highlights real-world forecasting limitations and strategic decision-making.

Key Skills Demonstrated
Time-series forecasting
ARIMA modeling
Dynamic regression
Forecast evaluation
Residual diagnostics
Business analytics
Operational forecasting
Data visualization
Statistical interpretation
Forecast deployment strategy

Future Improvements

Potential future enhancements include:

Incorporating real-time flu forecasts
Ensemble forecasting approaches
Machine learning forecasting models
Probabilistic forecasting
Clinic-level forecasting granularity
External economic and demographic variables
Conclusion

This project demonstrates how forecasting models must balance:

Statistical performance
Forecast accuracy
Operational feasibility
Business practicality

The final recommendation prioritized a model that could realistically be deployed in a real healthcare environment while still delivering strong forecasting performance.

Author
Smriti Maharjan

