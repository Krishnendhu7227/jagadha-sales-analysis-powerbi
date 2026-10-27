# jagadha-sales-analysis-powerbi
Exploratory sales analysis and Power BI dashboard for Jagadha by Padanjali.

## 📌 Project Overview

This project analyzes WooCommerce sales data for Jagadha by Padanjali to identify sales trends, product performance, revenue patterns, and business insights.

The dataset contains **690 orders and 72 columns**. The objective is to clean and prepare the data, calculate key sales KPIs, and present findings through an interactive Power BI dashboard.

## 🧹 Data Cleaning & Preparation

Data preparation was performed using Power Query while preserving the original data for traceability.

- Reviewed data types, missing values, errors, and column quality.
- Separated order and payment date/time information where required.
- Standardized billing and shipping location details.
- Examined INR and USD transactions and historical exchange-rate requirements.
- Preserved meaningful nulls, zero tax and discount values, and guest customer identifiers.
- Reviewed product line-item data for product-level analysis.

The cleaned order table used in Power BI is named `Orders (2)`.

## 📈 Key Performance Indicators (KPIs)

| KPI | Current Value |
|---|---:|
| Total Orders | 690 |
| Total Order Value | ≈ ₹2.52M |
| INR Order Value | ≈ ₹1.35M |
| USD Orders | ≈ $13K |
| Average Order Value | ≈ ₹3.66K |
| Products Sold | ≈ 1K |


## 📊 Charts & Their Uses

| Chart Name | Purpose |
|---|---|
| Quarterly Revenue & Order Volume | Compares revenue performance with order activity across quarters. |
| Top Products by Revenue | Highlights products contributing the most to displayed revenue. |
| Revenue by Shipping State Location | Compares sales value across geographic markets. |
| Sales by Order Currency | Shows the displayed contribution of INR and USD orders. |

## 💡 Insights from the Charts

### 1. Quarterly Revenue & Order Volume

Revenue and order volume do not always move together. Higher revenue can result from larger orders even when order counts are lower.

### 2. Top Products by Revenue

Agnijith 90 gms and its multipack variants feature among the leading products in the displayed revenue ranking.

### 3. Revenue by Shipping State Location

Kerala leads the displayed geographic ranking, with approximately ₹363K across 235 orders. Singapore shows approximately ₹211K across only four orders, highlighting the importance of considering order volume alongside revenue.

### 4. Sales by Order Currency

The displayed currency mix is approximately 53.5% INR and 46.5% USD by value. This comparison requires a consistent and validated currency-conversion method.

## 🔍 Other Key Insights

- **Order Status:** 405 orders (58.7%) are completed, while 285 (41.3%) are processing.
- **Payment Methods:** Razorpay appears on 684 orders (approximately 99.1%), while COD appears on 6 (approximately 0.9%).
- **Guest Checkout:** 340 orders (approximately 49.3%) have `customer_id = 0`, limiting customer-level repeat-purchase analysis.
- **Revenue Validation:** The selected converted value is approximately ₹2.52M, compared with approximately ₹1.36M in the original order subtotals. This difference requires reconciliation.


## 🛠️ Tools & Technologies

- Microsoft Power BI
- Power Query
- DAX
- Microsoft Excel
- WooCommerce


## ✅ Conclusion

This project demonstrates how data cleaning, KPI analysis, and Power BI visualization can be used to explore e-commerce sales performance, identify important business patterns, and highlight areas requiring further investigation.


---
# Jagadha Regional Sales Analysis | Power BI

Location-wise sales analysis and interactive Power BI dashboard for **Jagadha by Padanjali**, extending the original sales analysis project to explore geographic performance, regional demand, and customer purchasing patterns.

## 📌 Project Overview

This project extends the Jagadha Sales Analysis project by examining **where orders are placed, where products are delivered, and which regions contribute most to sales**.

Using a WooCommerce dataset containing **690 orders**, the analysis explores countries, shipping states, cities, domestic versus international demand, regional revenue distribution, and repeat-customer behaviour.

The objective is to clean and standardize location data, develop regional KPIs, and build an interactive **Jagadha Regional Sales Analysis** dashboard in Power BI to identify high-performing markets and potential business opportunities.

## 🎯 Project Objectives

- Analyse order distribution across countries, states, and cities.
- Identify the highest-performing regions by order volume and revenue.
- Compare domestic and international sales performance.
- Visualize geographic sales distribution.
- Analyse repeat purchasing among identified customers.
- Compare billing and shipping locations.
- Identify regional concentration and opportunities for customer retention.

## 🧹 Data Cleaning & Preparation

Location data was cleaned and prepared using **Power Query** in Power BI while preserving the original dataset for traceability.

Key preparation steps included:

- Used the cleaned columns `Shipping_country_clean`, `Shipping_state_clean`, and `Shipping_city_clean` for geographic analysis.
- Compared billing and shipping city, state, and country information.
- Created a `Region Type` column to classify orders as domestic or international.
- Preserved guest customer identifiers (`customer_id = 0`) while excluding them from registered-customer repeat-purchase calculations.
- Checked distinct countries, states, cities, and order distribution across regions.

The `Region Type` column was created using the following Power Query custom column formula:

```powerquery
if [Shipping_country_clean] = "India"
then "India"
else "International"
```

## 📊 Dashboard Overview

The Power BI dashboard presents regional performance through five KPI cards and six visualizations.

### Key Performance Indicators (KPIs)

| KPI | Current Value | Description |
|---|---:|---|
| Total Countries | 24 | Number of distinct shipping countries |
| Total Shipping States / Regions | 73 | Number of distinct shipping states and regions |
| Total Cities | 269 | Number of distinct shipping cities |
| Top State | Kerala | State with the highest order count |
| Repeated Registered Customers | 6.50% | Percentage of identified customers who placed more than one order |

**Repeat customer calculation:** 21 of 323 identified customers placed more than one order. Guest checkouts (`customer_id = 0`) are excluded from this calculation.

## 🧮 DAX Measures

The following DAX measures were used to calculate the regional KPIs and customer metrics.

### 1. Total Orders

Counts distinct orders in the dataset.

```dax
Total Orders =
DISTINCTCOUNT ( 'Orders (2)'[order_id] )
```

### 2. Total Revenue

Calculates the total order value using the INR-converted order subtotal.

```dax
Total Revenue =
SUM ( 'Orders (2)'[order_subtotal_INR2] )
```

### 3. Total Countries

Counts distinct, non-blank shipping countries.

```dax
Total Countries =
DISTINCTCOUNTNOBLANK ( 'Orders (2)'[Shipping_country_clean] )
```

### 4. Total Shipping States

Counts distinct, non-blank shipping states and regions.

```dax
Total Shipping States =
DISTINCTCOUNTNOBLANK ( 'Orders (2)'[Shipping_state_clean] )
```

### 5. Total Cities

Counts distinct, non-blank shipping cities.

```dax
Total Cities =
DISTINCTCOUNTNOBLANK ( 'Orders (2)'[Shipping_city_clean] )
```

### 6. Top State

Returns the state with the highest number of orders.

```dax
Top State =
MAXX (
    TOPN (
        1,
        VALUES ( 'Orders (2)'[Shipping_state_clean] ),
        [Total Orders],
        DESC
    ),
    'Orders (2)'[Shipping_state_clean]
)
```

### 7. Registered Customers

Counts unique identified customers, excluding guest checkouts.

```dax
Registered Customers =
CALCULATE (
    DISTINCTCOUNT ( 'Orders (2)'[customer_id] ),
    'Orders (2)'[customer_id] <> 0
)
```

### 8. Repeated Registered Customers

Counts identified customers who have placed more than one order.

```dax
Repeated Registered Customers =
COUNTROWS (
    FILTER (
        VALUES ( 'Orders (2)'[customer_id] ),
        'Orders (2)'[customer_id] <> 0
            && CALCULATE ( [Total Orders] ) > 1
    )
)
```

### 9. Repeated Registered Customers %

Calculates the percentage of identified customers who have placed multiple orders.

```dax
Repeated Registered Customers % =
DIVIDE (
    [Repeated Registered Customers],
    [Registered Customers]
)
```

**Current result:** 21 repeat registered customers out of 323 identified customers, giving a repeat-customer percentage of approximately **6.5%**.

The measure is formatted as a percentage with one decimal place in Power BI.

## 📈 Charts & Visualizations

The regional dashboard includes six visualizations.

| Chart | Visual Type | Purpose |
|---|---|---|
| Top 10 Cities by Number of Orders | Horizontal Bar Chart | Identifies cities with the highest order volume |
| Geographic Sales Distribution | Map | Visualizes the geographic reach of orders |
| Total Orders by Region Type | Pie Chart | Compares domestic and international order volume |
| Total Orders in India | Treemap | Compares order volume across Indian states |
| Top 10 Indian States by Revenue | Horizontal Bar Chart | Ranks Indian states by INR-converted order value |
| Billing vs Shipping City | Donut Chart | Compares the number of orders with matching and differing billing and shipping cities |

### 1. Top 10 Cities by Number of Orders

The horizontal bar chart ranks the ten cities with the highest order counts.

**Key insights:**
- Bengaluru leads with **57 orders**, representing approximately 8% of all orders.
- Hyderabad follows with 33 orders, while Thiruvananthapuram records 28 orders.
- Four of the top ten cities are in Kerala: Thiruvananthapuram, Thrissur, Kozhikode, and Ernakulam.
- Together, the top ten cities account for 256 of 690 orders, or approximately **37% of total orders**.

These findings help identify key urban markets for regional marketing and inventory planning.

### 2. Geographic Sales Distribution

The map visualizes the countries receiving orders and helps assess Jagadha's geographic reach.

**Key insights:**
- Orders are distributed across **24 countries**.
- India contributes approximately **53.5% of total order value**, equivalent to around ₹1.35 million.
- The United States is the largest overseas market, contributing approximately ₹431K, or 17% of total order value.
- Singapore and the United Kingdom are also notable overseas markets.

The map helps identify the geographic markets contributing to revenue and where international sales are concentrated.

### 3. Total Orders by Region Type

The pie chart compares orders shipped within India with those shipped internationally.

**Key insights:**
- India accounts for **609 orders (88.3%)**.
- International destinations account for **81 orders (11.7%)**.
- Despite representing a smaller share of order volume, international orders contribute approximately 46.5% of total order value.
- The average international order value is approximately ₹14.5K, compared with ₹2.2K for domestic orders.

This highlights the difference between order volume and order value across domestic and international markets.

### 4. Total Orders in India

The treemap compares order volume across Indian states, making it easy to identify regions with concentrated demand.

**Key insights:**
- Kerala leads with **235 orders**, accounting for approximately 34% of all 690 orders in the dataset.
- Kerala records more orders than Maharashtra, Tamil Nadu, and Karnataka combined, which together account for 211 orders.
- The top five states account for 485 orders, or approximately **70% of all orders**.
- Order activity is concentrated in a relatively small number of regions.

This analysis can help prioritize regional marketing, distribution, and inventory planning.

### 5. Top 10 Indian States by Revenue

The horizontal bar chart ranks Indian states according to their INR-converted order value.

**Key insights:**
- Kerala leads with approximately **₹363K**, representing about 26.9% of Indian-order value.
- Kerala generates more than twice the order value of Maharashtra.
- The top five states—Kerala, Maharashtra, Tamil Nadu, Telangana, and Karnataka—contribute approximately 75% of Indian-order value.

These findings show that a small group of Indian states accounts for a substantial proportion of domestic sales value.

### 6. Billing vs Shipping City

The donut chart compares orders where the corrected billing and shipping city values match with those where they differ.

The comparison uses the following calculated column in the `padanjaly_cleaned` table:

```dax
City Match =
IF (
    padanjaly_cleaned[Billing City (corrected)]
        = padanjaly_cleaned[Shipping city (corrected)],
    "Same",
    "Different"
)
```

**Key insights:**
- Billing and shipping cities match for **682 orders (98.84%)**.
- Eight orders (1.16%) are classified as having different billing and shipping cities.
- Most orders therefore have matching billing and shipping city values in the cleaned data.

The eight differing records can be investigated to understand whether they represent deliveries to alternative addresses or data-quality inconsistencies. Blank city values should also be reviewed to ensure they are classified appropriately.

## 🔍 Additional Regional Findings

### Regional Concentration

The top five Indian states contribute approximately 75% of Indian-order value. Kerala alone contributes around 27%, highlighting its importance to domestic sales.

### Revenue Versus Order Volume

Hyderabad generates approximately ₹147K compared with Bengaluru's ₹127K, despite receiving fewer orders. Its higher average order value illustrates why regional performance should be assessed using both order volume and revenue.

### Regional Growth in 2026

Kerala's order count increased from 28 in Q1 2026 to 89 in Q2 2026, accounting for approximately 64% of the quarter's 139 orders. This indicates a substantial concentration of recent order activity in Kerala.

### Product Preferences by Region

Agnijith 90 gms performs strongly in Karnataka, Maharashtra, Tamil Nadu, and Telangana. Kerala differs from these states, with Agnihari leading in the reported product-unit comparison.

### Repeat Customer Behaviour

Only **21 of 323 identified customers (6.5%)** placed more than one order. Nineteen of these repeat customers remained within a single city.

This suggests an opportunity to improve customer retention and encourage repeat purchases.

### Single-Order Cities

A total of 189 out of 269 cities, or approximately 70%, recorded only one order. Converting first-time buyers in these cities into repeat customers may offer a growth opportunity.

### Guest Checkout

Approximately 49% of orders have no identified customer ID. This limits the ability to track repeat purchases and customer behaviour across locations.


## 🛠️ Tools & Technologies

- **Power BI Desktop** — Dashboard development and visualization
- **Power Query** — Data cleaning and transformation
- **DAX** — KPI calculations and customer metrics
- **WooCommerce Sales Data** — Order, customer, product, and location analysis

## ✅ Conclusion

The regional analysis shows that Jagadha's order volume is concentrated in Kerala and a small group of other Indian states, while international orders contribute a disproportionately large share of order value.

Bengaluru leads the city ranking by order count, while Hyderabad illustrates how fewer orders can still generate higher revenue when average order value is larger.

The repeat registered customer rate is approximately **6.5%**, and many cities have recorded only one order. These findings highlight opportunities to strengthen established markets, develop higher-value locations, encourage repeat purchasing, and improve customer identification.

Overall, the **Jagadha Regional Sales Analysis dashboard** provides a geographic view of sales performance that complements the original sales analysis dashboard and supports more informed regional business decisions.





