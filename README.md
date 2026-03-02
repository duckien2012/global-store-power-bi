# 📊 Global Superstore Performance Analysis  
**Business Expansion & Profitability Optimization | Retail Industry | Power BI**

**Author:** Hoàng Đức Kiên  
**Date:** 2026-03-02  
**Tools Used:** Power BI, DAX  

---

## 📑 Table of Contents  
1. [📌 Background & Overview](#-background--overview)  
2. [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)  
3. [🧠 Design Thinking Process](#-design-thinking-process)  
4. [📊 Key Insights & Visualizations](#-key-insights--visualizations)  
5. [🔎 Final Conclusion & Recommendations](#-final-conclusion--recommendations)

---

## 📌 Background & Overview  

### 📖 What is this project about?  

**Global Superstore** is a multinational retail company operating across multiple markets and product categories.This project develops an interactive Power BI dashboard using the Global Superstore dataset (Orders, People, Returns) to transform transactional data into executive-level insights.

The dashboard enables leadership to:

- ✔️ Monitor revenue, profit, and margin performance
- ✔️ Ensure revenue growth translates into sustainable profitability
- ✔️ Identify truly profitable markets and high-impact product categories
- ✔️ Evaluate the impact of returns on overall business performance
- ✔️ Support market expansion and product growth strategy

Ultimately, the solution empowers data-driven decisions to improve long-term ROI and profitability.

### 👤 Who is this project for?  

This dashboard is designed for:

- ✔️ **Executive leadership team**   
- ✔️ **Marketing and sales teams**  
- ✔️ **Data analysts & business analysts** 

---

## 📂 Dataset Description & Data Structure
### 📌 Data Source  

- **Source:** Kaggle
- **Size:** ~50,000+ rows  
- **Format:** CSV 

#### **Table's used in Dataset:**  
The dataset consists of **three tables**:  
<details>
<summary> <strong>Table 1: Orders - detailed transaction and customer information</strong></summary>

| Column Name       | Data Type   | Description                              |
|------------------|------------|------------------------------------------|
| `Order ID`      | `VARCHAR`   | Unique identifier for each order.       |
| `Order Date`    | `DATE`      | Date when the order was placed.         |
| `Ship Date`     | `DATE`      | Date when the order was shipped.        |
| `Ship Mode`     | `VARCHAR`   | Shipping method used for delivery.      |
| `Customer ID`   | `VARCHAR`   | Unique identifier for each customer.    |
| `Customer Name` | `VARCHAR`   | Full name of the customer.              |
| `Segment`       | `VARCHAR`   | Customer segment (e.g., Consumer, Corporate). |
| `City`         | `VARCHAR`   | City where the order was placed.        |
| `State`        | `VARCHAR`   | State where the order was placed.       |
| `Country`      | `VARCHAR`   | Country where the order was placed.     |
| `Postal Code`  | `VARCHAR`   | Postal code of the shipping address.    |
| `Market`       | `VARCHAR`   | Market region (e.g., APAC, EMEA).       |
| `Region`       | `VARCHAR`   | Geographical region of the order.       |
| `Product ID`   | `VARCHAR`   | Unique identifier for each product.     |
| `Category`     | `VARCHAR`   | Product category (e.g., Furniture, Office Supplies). |
| `Sub-Category` | `VARCHAR`   | Sub-category of the product.            |
| `Product Name` | `VARCHAR`   | Name of the product ordered.            |
| `Sales`        | `DECIMAL`   | Revenue generated from the order.       |
| `Quantity`     | `INT`       | Number of items ordered.                |
| `Profit`       | `DECIMAL`   | Profit earned from the order.           |

</details>

<details>
<summary> <strong>Table 2: Returns - data on returned orders</strong></summary>

| Column Name  | Data Type | Description |
|--------------|-----------|-------------|
| `Returned`   | `VARCHAR` | Indicates whether the order was returned (e.g., 'Yes' or 'No'). |
| `Order ID`   | `VARCHAR` | Unique identifier for each order. |

</details>

<details>
<summary> <strong>Table 3: People - information about sales representatives</strong></summary>

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| `Person`    | `VARCHAR` | Name of the salesperson. |
| `Region`    | `VARCHAR` | Geographic region where the salesperson operates. |

</details>

### 📊 Data Structure & Relationships After Data Modeling

#### 1️⃣ Tables in Schema

The project uses a **star schema model** consisting of:

- **1 Fact Table:** Fact_Orders
- **5 Dimension Tables:** Dim_Customers, Dim_Products, Dim_Locations, Dim_SalesPeople, Dim_Date

---

#### 2️⃣ Table Schema & Data Snapshot  

<details>
<summary> <strong>🧾 Fact_Orders: transactional data about orders</strong></summary>


| Column Name | Data Type | Description |  
|------------|-----------|-------------|  
| Order_ID | Text | Unique order identifier |  
| Order_Date | Date | Transaction date |  
| Customer_ID | Text | Foreign key to Customers |  
| Product_ID | Text | Foreign key to Products |  
| Sales | Decimal | Revenue amount |  
| Quantity | Integer | Units sold |  
| Profit | Decimal | Profit per order |  
| Discount | Decimal | Applied discount |  
| Shipping_Cost | Decimal | Shipping expense | 
</details>


<details>
<summary> <strong>👥 Dim_Customers: customer information</strong></summary>

| Column Name | Description |  
|------------|-------------|  
| Customer_ID | Unique customer ID |  
| Customer_Name | Customer name |  
| Segment | Consumer / Corporate / Home Office |  

</details>

<details>
<summary> <strong>📦 Dim_Products: product information</strong></summary>

| Column Name | Description |  
|------------|-------------|  
| Product_ID | Unique product ID |  
| Product_Name | Product name |  
| Category | Main category |  
| Sub_Category | Sub-category |  

</details>

<details>
<summary> <strong>🌍 Dim_Locations: location information</strong></summary>

| Column Name | Description |  
|------------|-------------|  
| Country | Country |  
| City | City |  
| Market | Region grouping |  

</details>

<details>
<summary> <strong>🧑‍💼 Dim_SalesPeople: sales representative information</strong></summary>

| Column Name | Description |  
|------------|-------------|  
| Salesperson | Sales representative |  
| Region | Assigned region |  

</details>

<details>
<summary> <strong>📅 Dim_Date: date information for time intelligence</strong></summary>

| Column Name | Description |  
|------------|-------------|  
| Order_ID | Order reference |  
| Returned | Yes/No flag |  

</details>


---

#### 3️⃣ Data Relationships  

- **Fact_Orders → Dim_Customers** (Many-to-One)  
- **Fact_Orders → Dim_Products** (Many-to-One)  
- **Fact_Orders → Dim_Locations** (Many-to-One)  
- **Fact_Orders → Dim_SalesPeople** (Many-to-One)  
- **Fact_Orders → Dim_Date** (Many-to-One)  
- **Fact_Orders → Returns** (One-to-Many via Order_ID)  

**This structure ensures:**  

- ✔️ Clean filtering  
- ✔️ Strong time intelligence support  
- ✔️ Efficient market & product drill-down  

---

## 🧠 Design Thinking Process  

👉🏻 _Insert screenshot of your Design Thinking table here_  

---

### 1️⃣ Empathize  

**Leadership needs:**  

- Quick business health snapshot  
- Clear market comparison  
- Profitability visibility  
- Expansion decision support  

---

### 2️⃣ Define Point of View  

**The company must shift focus from revenue growth to profit-driven expansion.**

**Core problem:**  
_Not all revenue growth translates to sustainable profitability._

---

### 3️⃣ Ideate  

**Design 3 analytical layers:**  

1. **Business Overview** (Executive snapshot)  
2. **Product Performance** (Portfolio optimization)  
3. **Market Performance** (Expansion evaluation)  

**KPIs defined:**  

- Total Revenue  
- Total Profit  
- Profit Margin  
- Total Orders  
- Return Rate  
- YoY Growth  

---

### 4️⃣ Prototype & Review  

**Implementation steps:**  

- ✔️ Built interactive dashboard  
- ✔️ Applied KPI hierarchy  
- ✔️ Reduced visual clutter  
- ✔️ Enhanced cross-filtering  
- ✔️ Optimized layout for executive readability  

---

## 📊 Key Insights & Visualizations  

### 🔍 Dashboard 1: Business Overview  

👉🏻 _Insert screenshot of Business Overview page_  

---

#### 📌 Analysis 1  

**Observation:**  

- Revenue shows steady year-over-year growth  
- Profit growth fluctuates and does not always follow revenue trend  
- Profit margin varies across periods  
- Return rate impacts net performance  

**Recommendation:**  

- ✔️ Monitor **profit margin** alongside revenue growth  
- ✔️ Investigate cost and discount drivers affecting margin  
- ✔️ Improve return management process to protect profitability  

---

### 📦 Dashboard 2: Product Analysis  

👉🏻 _Insert screenshot of Product Analysis page_  

---

#### 📌 Analysis 2  

**Observation:**  

- **Technology category** generates highest revenue  
- Some sub-categories show high sales but **lower margin**  
- Profit contribution is concentrated among top-performing products  
- Certain products exhibit higher return rates  

**Recommendation:**  

- ✔️ Prioritize **high-margin product lines**  
- ✔️ Reevaluate low-margin or high-return products  
- ✔️ Apply portfolio optimization strategy to improve overall margin  

---

### 🌍 Dashboard 3: Market Analysis  

👉🏻 _Insert screenshot of Market Analysis page_  

---

#### 📌 Analysis 3  

**Observation:**  

- Revenue distribution varies significantly by market  
- **Not all high-revenue markets maintain strong profit margins**  
- Customer base differs widely between regions  
- Regional profitability efficiency is inconsistent  

**Recommendation:**  

- ✔️ Expand in markets with **strong margin performance**  
- ✔️ Reassess pricing and operational costs in low-margin markets  
- ✔️ Align regional strategies with profitability targets  

---

## 🔎 Final Conclusion & Recommendations  

👉🏻 Based on the insights above, we recommend the **Executive & Strategy Team** to consider the following:  

---

### 📌 Key Takeaways  

- ✔️ **Shift performance focus** from revenue-driven growth to **profit-driven growth**  
- ✔️ **Prioritize expansion** in high-margin markets rather than high-revenue markets  
- ✔️ **Optimize product portfolio** by reducing low-margin and high-return items  
- ✔️ **Monitor return rate** as a key operational risk indicator  

---

### 🚀 Business Impact  

This project demonstrates:  

- ✅ Strong **data modeling capability**  
- ✅ **Executive-focused** dashboard design  
- ✅ Strategic thinking beyond descriptive reporting  
- ✅ **Business-aligned** analytical storytelling  

---
