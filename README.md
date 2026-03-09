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

**Key Findings:**  

- **Overall KPIs:**
    - Revenue (**$12.64M**), Profit (**$1.47M**), and Orders (**25K**) all grew by about **51-52%**. 
    - The best point is the **Return Rate**, which dropped by **34.1%** to **4.68%**. This shows the company is increasing its sales volume while improving its service quality.

- **Revenue and Profit Over Time:**
    - Sales show a very strong **seasonal pattern** from **2011 to 2014**. Revenue always drops to its **lowest** point in **Q1** and always reaches its **highest** peak in **Q4**.
    - During these high sales periods, the **Profit Margin** stayed stable between **10.13% and 13.11%**. This means the company managed its costs well and did not cut prices just to get more sales.

- **Market Contribution vs. Growth:**
    - There is a clear divergence between scale and growth rate. **APAC** (**$3.59M**) and **EU** (**$2.94M**) brought in the most money, contributing **>51%** of total revenue. 
    - However, the future growth engines lie in **EMEA** (**+59.80%**) and **Africa** (**+56.52%**). Meanwhile, the **US market** shows signs of saturation, recording the lowest growth rate across all regions at **46.95%**.

- **Total Return and Orders Over Time:**
    - While transaction volume nearly doubled (from **4.4K in 2011** to **8.5K in 2014**), the number of returned orders only increased slightly (from **0.5K** to **1.0K**).
    - The growth rate of returns is much **slower** than sales growth, reinforcing the solid risk management capabilities of the Logistics and Customer Service operations.

- **Revenue by Market and Category:**
    - Consumer behavior shows distinct regional fragmentation. While most markets maintain a balanced proportion among categories (each **>25%**), **Canada** emerges as a unique niche market: 
        - **Office Supplies** overwhelmingly dominates at **44.88%**, whereas **Furniture** is underperforming at merely **15.83%**.


### 📦 Dashboard 2: Product Analysis  

![Image](https://github.com/user-attachments/assets/41174e5d-999c-436c-a73c-2e9a77dc0353)


#### 📌 Product Analysis 

**Key Findings:**  

- **Revenue Contribution by Category:** 
    - **Technology** is the core business driver, contributing the largest revenue share at $**4.74M** (**37.53%**). 
    - **Furniture** ($**4.11M**) and **Office Supplies** ($**3.79M**) follow closely, showing a relatively balanced product portfolio at the top category level.

- **Revenue and Profit by Sub-Category:**
    - **"Phones"** lead in total revenue ($**1.70M**), but **"Copiers"** are the true profit engine, generating the highest absolute profit of $**258K** with an outstanding **17.13%** margin. On the opposite end, **"Tables"** generate a substantial $**757K** in revenue but suffer from severe **negative profitability**.

- **Profit & Total Orders by Sub-Category:**
    - **High Profit, Low-to-Medium Orders:** **Copiers** lead this group. With only **~2,300 orders**, they generate the highest system profit (**>$250K**). They sell less but deliver excellent margins, meaning they require minimal operational effort for maximum financial return.
    - **High Profit, High Orders:** **Phones** (**~3,200 orders**, **>$200K profit**), **Chairs**, and **Accessories** drive the main cash flow. This means they are the core lifeline of the business, maintaining steady revenue and profitability.
    - **Low Profit, Very High Orders:** **Binders**, **Storage**, **Art**, and **Paper** have huge volumes (**Binders** hit **>5,000 orders**) but thin margins (**<$100K profit**). They cost a lot to pack and ship, meaning they drain logistics resources and human effort just to retain customers without bringing real financial gain.
    - **Near-Zero Profit, Low Orders:** **Envelopes**, **Fasteners**, **Labels**, and **Supplies** stay around **~2,000 orders** with almost **zero profit**. This means they are essentially dead inventory taking up valuable warehouse space without generating financial value.
    - **Negative Profit (The Loss-Maker):** **Tables** are the only product losing money (**~$60K loss**) despite nearly **1,000 orders**. This indicates a critical financial leak, likely because the high shipping and storage costs for these bulky items completely destroy their margins.
- **Top 10 Products by Revenue:** The best-selling individual items are overwhelmingly dominated by high-ticket smartphones from major brands like **Apple**, **Cisco**, **Motorola**, and **Nokia**. The **"Apple Smart Phone"** ranks first, bringing in $**87K** independently, confirming that premium tech devices are the biggest revenue pullers at the item level.

### 🌍 Dashboard 3: Market Analysis  

![Image](https://github.com/user-attachments/assets/91cacb29-8f55-4fd4-922f-239ad0ca263f)


#### 📌 Market Analysis

**Key Findings:**  

- **Revenue and Profit by Market:** 
    - **APAC** and **EU** lead in total revenue, but **Canada** stands out with the highest **profit margin** at **26.62%** despite having the lowest sales volume. 
    - This means **Canada** is a highly efficient premium market, while **EMEA** (with the lowest margin at **5.46%**) suffers from high operational costs that heavily reduce its actual earnings.

- **Revenue YoY% by Market:** 
    - **EMEA** and **Africa** record the highest year-over-year growth rates at **59.80%** and **56.52%**. Meanwhile, the **US market** shows the slowest growth at **46.95%**.
    - This indicates that **EMEA** and **Africa** are the new growth engines with high future potential, whereas the **US** has reached a saturation point with limited room for rapid expansion.

- **Total Customers by Market:** 
    - Major regions like **APAC**, **LATAM**, **US**, and **EU** maintain large and equal customer bases of around **800 customers** each. **Canada** has a very small customer pool of under **200**. 
    - This confirms **Canada** operates as a specialized niche market, depending on high-value individual sales rather than mass market volume.

- **Top 5 Sale Agents:** 
    - **Anna Andreadi** dominates the sales team by bringing in **$2.8M** in revenue, nearly double the second-place agent, **Chuck Magee** (**$1.6M**). 
    - This means the company's sales performance is highly unbalanced and overly dependent on a **single top performer**, creating a huge structural risk for the business.
---

## 🔎 Final Conclusion & Recommendations  

👉🏻 Based on the insights from Business, Product, and Market Analysis above, we recommend the Senior Management team to consider the following actions:

| **Strategy** | **Insight** | **Recommendation** |
|-------------|-------------|-------------------|
| 🌍 **1. Market & Sales Expansion Strategy** | - **APAC** & **EU** act as the primary cash cows stabilizing the business.<br>- **Canada** operates strictly as a highly efficient premium niche market.<br>- **EMEA** & **Africa** are the new growth engines, though **EMEA** struggles with profit-draining operational costs.<br>- The **US market** shows clear signs of saturation.<br>- Overall sales are heavily driven by end-of-year seasonality. | - Protect core revenue in **APAC** & **EU** with loyalty programs.<br>- Invest aggressively in **EMEA** & **Africa** to capture growth, but urgently optimize **EMEA's** operational costs to improve its margin.<br>- Treat **Canada** as a specialized premium market (focus on **Office Supplies**).<br>- Run **Q1** promotions to offset seasonal drops and prepare inventory early for **Q4**. |
| 🛒 **2. Product & Sales Portfolio Optimization** | - **Technology** is the ultimate profit driver for the company.<br>- High-margin items (**Copiers**) deliver maximum financial return with minimal operational effort, while **Phones** drive massive cash flow.<br>- High-volume items (**Binders**, **Paper**) drain logistics resources just to retain customers without bringing real financial gain.<br>- **Tables** represent a critical financial leak, destroying overall profitability. | - Push Sales KPIs toward high-margin **Copiers** and high-volume **Phones**.<br>- Bundle low-profit items (**Binders**, **Paper**) or set Minimum Order Values to cut packing/shipping costs.<br>- **Review or Drop Tables**: Urgently audit pricing and shipping costs for **Tables**; if unfixable, stop selling them immediately.<br>- Clear dead inventory (**Envelopes**, **Labels**) to save warehouse space. |
| 👥 **3. Sales Capability & Performance Gap** | - Sales performance is dangerously unbalanced and overly dependent on a **single top performer**.<br>- This extreme concentration creates a massive structural and dependency risk for the business if this individual leaves or underperforms. | - De-risk sales dependency by studying the top performer's winning techniques and creating a standardized training program for the rest of the team.<br>- Shift KPIs from purely closing volume to up-selling high-margin items (like **Copiers**) to boost overall profitability. |
| ⚙️ **4. Operational Efficiency & Risk Control** | - The company successfully scaled its order volume while sharply reducing the **return rate**.<br>- This divergence indicates excellent risk management, highly optimized logistics, and strong quality control during a period of rapid expansion. | - **Standardize current SOPs**: Document the successful logistics and customer service processes that kept return rates low, and enforce them in fast-growing regions (**EMEA**, **Africa**).<br>- Prioritize warehouse space for fast-moving, high-margin goods (**Phones**, **Chairs**) to ensure they are never out of stock. |

