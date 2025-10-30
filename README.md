<img width="977" height="546" alt="Screenshot 2025-10-30 213122" src="https://github.com/user-attachments/assets/799c98de-e95e-4524-b4d9-d53677e63071" />
📊 Insurance Policy Analytics Dashboard — End-to-End (Power BI)
✅ Objective

This project builds a complete Insurance Policy Performance Dashboard using Power BI.
The dashboard tracks key metrics such as active policies, closed policies, claims, premium collection, claim ratios, and vehicle-wise performance.

🏗️ Data Model
Table	Description
policies	Contains policy-level insurance data (premium, claim paid, start & end dates, vehicle type)
calendar	Date table used for time intelligence & period-based reporting

Relationship between calendar[Date] and policies[INSR_END] is inactive and activated using USERELATIONSHIP() for closed-policy calculations.

📐 DAX Measures Used
Policy Metrics
Police Count = COUNTROWS(policies)

Polices Opend = [Police Count]

Polices Closed =
CALCULATE(
    [Police Count],
    USERELATIONSHIP('calendar'[Date], policies[INSR_END])
)

Financial Metrics
Total Premium = SUM(policies[PREMIUM])

Total Claim = SUM(policies[CLAIM_PAID])

Avg. Premium = AVERAGE(policies[PREMIUM])

Avg. Claim = AVERAGE(policies[CLAIM_PAID])

Avg. Claim2 = DIVIDE([Total Claim], [Polices Opend])

Premium to Claim Ratio = DIVIDE([Total Premium], [Total Claim])

Claim Count
Claim Count =
CALCULATE(
    [Police Count],
    policies[CLAIM_PAID] > 0
)


Using condition because some claim values may be blank
(Alternative: COUNTROWS( FILTER(policies, policies[CLAIM_PAID] > 0 ) ))

Dynamic Bar Chart Labels
Barchart Lables =
VAR v_t = SELECTEDVALUE(policies[TYPE_VEHICLE])
VAR Polices = FORMAT([Polices Opend], "#,##0,.0k")
VAR pr = IF([Premium to Claim Ratio] < 1, "x", "y")
RETURN
v_t & " " & Polices & " " & pr

📸 Dashboard Highlights

🚦 KPI Cards: Open Policies, Closed Policies, Total Premium, Total Claims

📈 Trend Line: Premium vs Claims over time

🚘 Vehicle-wise Policy & Claim analysis

⚖️ Claim Ratios & Loss Ratios

🧠 Advanced DAX with USERELATIONSHIP() for closed policy tracking

🎛️ Custom Tooltip & Narrative insights

🎯 Outcome

This dashboard helps insurance stakeholders:

Monitor business performance in real time

Analyze claim behavior & financial health

Compare premium vs claim for profitability

Track policy lifecycle metrics

🔑 Key DAX Concepts Applied

COUNTROWS, SUM, AVERAGE

USERELATIONSHIP() for inactive relationship activation

DIVIDE() for safe ratio calculation

SELECTEDVALUE() for context-aware labels

FORMAT() for display enhancement

📎 Next Enhancements

Add Time Intelligence (YTD, MOM, YOY)

Implement Forecasting (Premium & Claims)

RLS for branch/agent-level access

AI insights integration

🏁 Conclusion

This project showcases a complete professional Power BI workflow:
Data Prep → Modeling → DAX → Visualization → Insights
