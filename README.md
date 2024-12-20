# Car Sales Dashboard Project

## Overview
The Car Sales Dashboard is a dynamic and interactive solution developed using Power BI. It provides a comprehensive overview of car dealership sales performance, enabling stakeholders to track key performance indicators (KPIs), identify trends, and make data-driven decisions.

---

## Features
- **Real-Time KPI Tracking**: Displays Year-to-Date (YTD), Month-to-Date (MTD), and Year-over-Year (YOY) metrics for total sales, average prices, and cars sold.
- **Advanced Visualizations**:
  - Line chart for YTD sales weekly trends.
  - Pie charts for sales by body style and color.
  - Map chart for regional sales distribution.
  - Detailed and company-specific grids for sales trends and information.
- **Interactivity**: Includes filters for body style, dealer region, transmission, and engine, as well as page navigation.

---

## Key DAX Formulas
### Sales Overview
- **YTD Total Sale**:
  ```DAX
  TOTALYTD(SUM(car_data[Price ($)]), 'Calendar Table'[Date])
  ```
- **PYTD**:
  ```DAX
  CALCULATE(SUM(car_data[Price ($)]), SAMEPERIODLASTYEAR('Calendar Table'[Date]))
  ```
- **YOY Growth**:
  ```DAX
  ([YTD Total Sale] - [PYTD]) / [PYTD]
  ```

### Average Price Analysis
- **YTD Avg Price**:
  ```DAX
  TOTALYTD([Avg Price], 'Calendar Table'[Date])
  ```
- **Avg Price**:
  ```DAX
  SUM(car_data[Price ($)]) / COUNT(car_data[Car_id])
  ```

### Cars Sold Metrics
- **YTD Cars Sold**:
  ```DAX
  TOTALYTD(COUNT(car_data[Car_id]), 'Calendar Table'[Date])
  ```

### Highlighting Max Point
- **Max Point for YTD Sales Weekly Trend**:
  ```DAX
  IF(MAXX(ALLSELECTED('Calendar Table'[Week]), [Total Sale]) = [Total Sale], MAXX(ALLSELECTED('Calendar Table'[Week]), [Total Sale]), BLANK())
  ```

---

## Data Model
- Created relationships between the `Date Table` and `Calendar Table` for accurate time-based calculations.
- Utilized calendar functions like `TOTALYTD`, `TOTALMTD`, and `SAMEPERIODLASTYEAR` to facilitate time-series analysis.

---

## How to Use
1. Open the Power BI file (`Car_Sales_Dashboard.pbix`) in Power BI Desktop.
2. Use the filters (e.g., body style, dealer region) to customize views.
3. Navigate between pages for detailed sales trends and summary insights.
