📊 Global Superstore Performance Analysis
Business Expansion & Profitability Optimization | Retail Industry | Power BI

Author: Hoàng Đức Kiên
Date: 2026-03-02
Tools Used: Power BI, DAX

📑 Table of Contents

📌 Background & Overview

📂 Dataset Description & Data Structure

🧠 Design Thinking Process

📊 Key Insights & Visualizations

🔎 Final Conclusion & Recommendations

📌 Background & Overview
📖 What is this project about?

Global Superstore is a multinational retail company operating across multiple markets and product categories.

This project analyzes company-wide performance to answer key business questions:

✔️ Is revenue growth supported by sustainable profit growth?
✔️ Which markets are truly profitable, not just high-revenue?
✔️ Which product categories drive margin performance?
✔️ Are returns significantly affecting profitability?
✔️ Where should expansion efforts focus?

The goal is to transform transactional sales data into clear, executive-level insights that support business expansion strategy.

👤 Who is this project for?

✔️ Executive leadership team
✔️ Regional managers
✔️ Product strategy team
✔️ Data analysts & business analysts

This dashboard supports strategic decision-making rather than operational reporting.

📂 Dataset Description & Data Structure
📌 Data Source

Source: Global Superstore Dataset

Size: ~50,000+ rows

Format: Excel (.xlsx)

Tables Used: Orders, Customers, Products, Locations, Salespeople, Returns

📊 Data Structure & Relationships
1️⃣ Tables Used

The project uses a star schema model consisting of:

1 Fact Table

5 Dimension Tables

1 Additional Returns Table

2️⃣ Table Schema & Data Snapshot
🧾 Fact_Orders
Column Name	Data Type	Description
Order_ID	Text	Unique order identifier
Order_Date	Date	Transaction date
Customer_ID	Text	Foreign key to Customers
Product_ID	Text	Foreign key to Products
Sales	Decimal	Revenue amount
Quantity	Integer	Units sold
Profit	Decimal	Profit per order
Discount	Decimal	Applied discount
Shipping_Cost	Decimal	Shipping expense

This table stores all transactional metrics.

👥 Dim_Customers
Column Name	Description
Customer_ID	Unique customer ID
Customer_Name	Customer name
Segment	Consumer / Corporate / Home Office
📦 Dim_Products
Column Name	Description
Product_ID	Unique product ID
Product_Name	Product name
Category	Main category
Sub_Category	Sub-category
🌍 Dim_Locations
Column Name	Description
Country	Country
City	City
Market	Region grouping
🧑‍💼 Dim_SalesPeople
Column Name	Description
Salesperson	Sales representative
Region	Assigned region
🔁 Returns
Column Name	Description
Order_ID	Order reference
Returned	Yes/No flag

Used to calculate Return Rate.

<details> <summary>Click to toggle: Data Model Screenshot</summary>

👉🏻 Insert screenshot of your Power BI data model here

</details>
3️⃣ Data Relationships

Fact_Orders → Dim_Customers (Many-to-One)

Fact_Orders → Dim_Products (Many-to-One)

Fact_Orders → Dim_Locations (Many-to-One)

Fact_Orders → Dim_SalesPeople (Many-to-One)

Fact_Orders → Dim_Date (Many-to-One)

Fact_Orders → Returns (One-to-Many via Order_ID)

This structure ensures:

✔️ Clean filtering
✔️ Strong time intelligence support
✔️ Efficient market & product drill-down

🧠 Design Thinking Process

👉🏻 Insert screenshot of your Design Thinking table here

1️⃣ Empathize

Leadership needs:

Quick business health snapshot

Clear market comparison

Profitability visibility

Expansion decision support

2️⃣ Define Point of View

The company must shift focus from revenue growth to profit-driven expansion.

Core problem:

Not all revenue growth translates to sustainable profitability.

3️⃣ Ideate

Design 3 analytical layers:

Business Overview (Executive snapshot)

Product Performance (Portfolio optimization)

Market Performance (Expansion evaluation)

KPIs defined:

Total Revenue

Total Profit

Profit Margin

Total Orders

Return Rate

YoY Growth

4️⃣ Prototype & Review

Built interactive dashboard

Applied KPI hierarchy

Reduced visual clutter

Enhanced cross-filtering

Optimized layout for executive readability

📊 Key Insights & Visualizations
🔍 Dashboard 1: Business Overview

👉🏻 Insert screenshot of Business Overview page

📌 Analysis 1

Observation:

Revenue shows steady year-over-year growth.

Profit growth fluctuates and does not always follow revenue trend.

Profit margin varies across periods.

Return rate impacts net performance.

Recommendation:

Monitor profit margin alongside revenue growth.

Investigate cost and discount drivers affecting margin.

Improve return management process to protect profitability.

📦 Dashboard 2: Product Analysis

👉🏻 Insert screenshot of Product Analysis page

📌 Analysis 2

Observation:

Technology category generates highest revenue.

Some sub-categories show high sales but lower margin.

Profit contribution is concentrated among top-performing products.

Certain products exhibit higher return rates.

Recommendation:

Prioritize high-margin product lines.

Reevaluate low-margin or high-return products.

Apply portfolio optimization strategy to improve overall margin.

🌍 Dashboard 3: Market Analysis

👉🏻 Insert screenshot of Market Analysis page

📌 Analysis 3

Observation:

Revenue distribution varies significantly by market.

Not all high-revenue markets maintain strong profit margins.

Customer base differs widely between regions.

Regional profitability efficiency is inconsistent.

Recommendation:

Expand in markets with strong margin performance.

Reassess pricing and operational costs in low-margin markets.

Align regional strategies with profitability targets.

🔎 Final Conclusion & Recommendations

👉🏻 Based on the insights above, we recommend the Executive & Strategy Team consider the following:

📌 Key Takeaways

✔️ Shift performance focus from revenue-driven growth to profit-driven growth

✔️ Prioritize expansion in high-margin markets rather than high-revenue markets

✔️ Optimize product portfolio by reducing low-margin and high-return items

✔️ Monitor return rate as a key operational risk indicator

🚀 Business Impact

This project demonstrates:

Strong data modeling capability

Executive-focused dashboard design

Strategic thinking beyond descriptive reporting

Business-aligned analytical storytelling
