Day 17
Build an AI Vehicle Cost & Fuel Analysis Dashboard

Fuel Economics Dashboard

Overview

Fuel Economics Dashboard is an AI-generated analytics application that transforms vehicle fuel consumption datasets into an interactive HTML dashboard.

The system analyzes fuel costs, emissions, maintenance expenses, vehicle aging effects, and fuel efficiency trade-offs, then generates a responsive glassmorphism-style dashboard using pure HTML, CSS, SVG, and JavaScript.

---

Features

Vehicle Profile Analysis

Supports:

- Vehicle model
- Fuel type (Petrol, Diesel, CNG, E85, EV)
- Monthly distance travelled
- Vehicle age
- Driving usage pattern

KPI Metrics

Automatically calculates:

- Fuel Cost per Kilometer
- Average CO₂ Emissions per Kilometer
- Maintenance Cost per Kilometer
- Refuel / Recharge Time
- Monthly Fuel Cost
- E85 Cost Premium vs Petrol
- E85 Break-even Fuel Price

Age-Based Analytics

Vehicle lifecycle buckets:

Bucket| Age
New| 0–2 years
Mid-life| 3–5 years
Aged| 6–9 years
Old| 10+ years

For each bucket:

- Average Cost/km
- Average Maintenance/km
- Current vehicle age highlighting

E85 Paradox Analysis

Specialized ethanol fuel evaluation:

- Pump Price Savings
- Real Running Cost Penalty
- Break-even Fuel Price
- Mileage Impact Analysis

Fuel Scoring System

Weighted score out of 10:

Metric| Weight
Cost| 4
CO₂ Emissions| 3
Refuel Time| 2
Maintenance| 1

Interactive Visualizations

Pure SVG charts:

- Cost/km Bar Chart
- CO₂ Doughnut Chart
- Fuel Cost vs Vehicle Age Line Chart
- Animated E85 Score Gauge

Fuel Comparison Cards

For every fuel type:

- Pros
- Cons
- Best Use Cases
- Visual Fuel Highlighting



Dashboard Design

Theme

- Dark Navy Background (#0a0f1e)
- Glassmorphism UI
- Responsive Layout

Fuel Color Mapping

Fuel| Color
E85| Amber
Petrol| Blue
Diesel| Grey
CNG| Green
EV| Purple

Technical Constraints

- No external libraries
- No CDN dependencies
- Pure HTML/CSS/JavaScript
- SVG-based charts
- Mobile responsive (375px–1440px)

---

Input Dataset

Expected CSV columns:

Fuel_Type,
Vehicle_Age,
Distance_km,
Fuel_Cost_INR,
CO2_emitted_kg,
Maintenance_Cost_INR,
Refuel_Recharge_time_min



Output

The AI generates:

- Single self-contained HTML file
- Embedded CSS
- Embedded JavaScript
- Interactive SVG visualizations
- Responsive dashboard layout

No additional setup or dependencies required.



Example Use Case

Analyze how different fuel types perform for a vehicle across:

- Running costs
- Maintenance expenses
- Environmental impact
- Aging effects
- Refueling convenience

The generated dashboard provides a comprehensive view of fuel economics and ownership efficiency.

HTML file:
https://github.com/reemaz01/60-day-claude-ai/blame/b3d9b2db6a61b4d648c776672ee2f8d7e1c42b5b/Corolla_E85_Fuel_Dashboard.html

Screenshot:

https://github.com/reemaz01/60-day-claude-ai/blob/b003fafd3c7b534c96efbc99f53f4beb90b042cb/IMG_20260617_155723.jpg
https://github.com/reemaz01/60-day-claude-ai/blob/b003fafd3c7b534c96efbc99f53f4beb90b042cb/IMG_20260617_155723.jpg 
https://github.com/reemaz01/60-day-claude-ai/blob/b003fafd3c7b534c96efbc99f53f4beb90b042cb/IMG_20260617_155710.jpg
