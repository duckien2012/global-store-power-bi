# 📊 Global Superstore Performance Analysis | Power BI

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



#### 3️⃣ Data Relationships  
![Image](https://github.com/user-attachments/assets/8745648b-c585-4d48-9456-32587bd00425)
| **From Table (Fact)** | **To Table (Dimension)** | **Join Key**          | **Relationship Type** | **Description**                                                     |
| --------------------- | ------------------------ | --------------------- | --------------------- | ------------------------------------------------------------------- |
| `Fact_Orders`         | `Dim_Customers`          | `Customer ID`         | Many-to-One (*:1)     | Multiple orders belong to one customer                              |
| `Fact_Orders`         | `Dim_SalePeople`         | `Person ID`           | Many-to-One (*:1)     | Multiple orders handled by one salesperson                          |
| `Fact_Orders`         | `Dim_Products`           | `Product Key`         | Many-to-One (*:1)     | Multiple orders for one product                                     |
| `Fact_Orders`         | `Dim_Locations`          | `Location ID`         | Many-to-One (*:1)     | Multiple orders belong to one location                              |
| `Fact_Orders`         | `Dim_Date`               | `Order Date` → `Date` (active) | Many-to-One (*:1)     | Multiple orders occur on one date  
| `Fact_Orders`         | `Dim_Date`               | `Ship Date` → `Date` (inactive) | Many-to-One (*:1)     | Multiple shipped orders occur on one date                                     |
| `Fact_Orders`         | `Returns`                | `Order ID`            | Many-to-One (*:1)     | Multiple orders may appear in Returns table (not all orders are returned) |

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

![Image](https://github.com/user-attachments/assets/270e5fdb-d93f-4bf2-8daf-ecc81a07493f)


#### 📌 Overall Business Performance

**Observation:**  

- Revenue increases steadily from 2011 to 2014, showing strong business growth.

- Profit also rises, but not always at the same speed as revenue, which may indicate pressure on profit margin.

- Profit margin reaches its highest point around 2013 and then decreases slightly, possibly due to higher costs or more discounting.

- Total orders grow every year, showing increasing customer demand.

- The number of returns also increases over time, which can reduce overall profit if not managed well.

- Revenue comes from multiple markets (APAC, EU, US, LATAM, EMEA), helping the company avoid relying too much on one region.

**Recommendation:**  

- ✔️ Focus not only on revenue growth but also on maintaining healthy profit margins.

- ✔️ Review costs and discount policies to understand what is affecting margin performance.

- ✔️ Improve product strategy by promoting higher-margin products where possible.

- ✔️ Improve return management processes to reduce losses and protect profitability.

- ✔️ Expand more in markets that show both strong growth and good profit margins to improve long-term results.


### 📦 Dashboard 2: Product Analysis  

![Image](https://github.com/user-attachments/assets/41174e5d-999c-436c-a73c-2e9a77dc0353)


#### 📌 Product Analysis 

**Observation:**  

- Phones and Copiers generate the highest revenue and profit, making them the key revenue drivers. Copiers show a particularly strong profit margin (around 17%), indicating good pricing power.

- Chairs and Bookcases generate high revenue but lower margin compared to Copiers, suggesting higher costs or heavier discounting.

- Some sub-categories such as Tables and Accessories show relatively weaker profit performance, even though revenue is moderate. This may indicate inefficient cost control.

- The Top 10 products are dominated by smartphones and technology-related items, confirming that Technology is a strategic category.

- The scatter plot shows that most markets generate positive profit, but at least one market has negative profit despite having orders, which is a warning sign.

- Return rate is relatively high in some sub-categories (over 30–50%), which can significantly reduce net profit if not managed carefully.

**Recommendation:**  

- ✔️ Prioritize high-margin sub-categories like Copiers and Phones in marketing and expansion strategies.

- ✔️ Review pricing and cost structure of low-margin products (e.g., Tables, Accessories) to improve profitability.

- ✔️ Strengthen inventory and demand planning for top-performing products to avoid stock shortages.

- ✔️ Carefully analyze markets with negative or low profit despite strong order volume to identify pricing or operational issues.

- ✔️ Implement stricter return policies or improve product quality and descriptions to reduce high return rates.

- ✔️ Focus future product strategy on Technology-related items, as they show strong revenue contribution and competitive margins.

### 🌍 Dashboard 3: Market Analysis  

![Image](https://github.com/user-attachments/assets/91cacb29-8f55-4fd4-922f-239ad0ca263f)


#### 📌 Market Analysis

**Observation:**  

- APAC and EU generate the highest revenue, making them the main contributors to overall sales performance.

- EMEA shows strong Year-over-Year growth, even though its total revenue is lower than APAC and EU. This indicates high growth potential.

- Africa has a high profit margin compared to some larger markets, suggesting efficient cost control or strong pricing strategy.

- Canada has very low revenue and customer volume, contributing minimally to overall performance.

- The number of customers is relatively stable across major markets (APAC, EU, LATAM, US), showing balanced market coverage.

- Revenue growth rate varies by region, meaning expansion performance is not equally distributed.

- Top sales agents contribute significantly to revenue, indicating that sales performance is partly driven by key individuals.

**Recommendation:**  

- ✔️ Maintain strong investment and customer retention strategies in APAC and EU, as they are core revenue markets.

- ✔️ Prioritize expansion in EMEA, where growth rate is high and future potential looks promising.

- ✔️ Study the Africa market model to understand how it maintains higher profit margin and apply best practices to other regions.

- ✔️ Re-evaluate strategy in Canada, considering whether to restructure, reposition, or limit investment.

- ✔️ Develop training and incentive programs to scale the performance of top sales agents across other teams.

- ✔️ Allocate resources based on both revenue size and profit margin, not revenue alone, to maximize long-term ROI.

---

## 🔎 Final Conclusion & Recommendations  

👉🏻 Based on the insights from Business, Product, and Market Analysis above, we recommend the Senior Management team to consider the following actions:

### 📌 Key Takeaways  

- ✔️ Focus on sustainable growth by balancing revenue expansion with stable profit margins, rather than pursuing revenue alone.

- ✔️ Prioritize high-margin products and high-growth markets (such as Technology category and EMEA market) to maximize long-term profitability.

- ✔️ Improve cost control and return management to reduce margin pressure and protect overall business performance.

- ✔️ Allocate resources strategically by investing more in profitable markets (APAC, EU, EMEA) while reviewing underperforming markets like Canada.

- ✔️ Strengthen product and sales strategy by scaling best-performing products and applying top sales practices across regions.
