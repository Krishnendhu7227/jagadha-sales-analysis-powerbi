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






# jagadha-regional-sales-analysis-powerbi
Location-wise sales analysis and Power BI dashboard for Jagadha by Padanjali, continuing the sales analysis project.

## 📌 Project Overview

This part of the project extends the sales analysis by examining **where** Jagadha's orders and revenue come from. It uses the same dataset of **690 orders** and focuses on countries, states, and cities to identify high-performing locations, domestic versus international demand, and repeat-buying patterns.

The objective is to prepare the location data, calculate regional KPIs, and present findings through a dedicated **Jagadha Regional Sales Analysis** page in Power BI.

## 🧹 Data Cleaning & Preparation

Location preparation was performed in Power Query on the `Orders (2)` table, while preserving the original data for traceability.

- Used the standardized shipping fields: `Shipping_country_clean`, `Shipping_state_clean`, and `Shipping_city_clean`.
- Compared billing and shipping city, state, and country across all orders.
- Created a `Region Type` column to separate **India** orders from **International** orders.
- Preserved guest customer identifiers (`customer_id = 0`) and used identified customers only for repeat-customer analysis.

The `Region Type` column was created using:

`if [Shipping_country_clean] = "India" then "India" else "International"`

## 📈 Key Performance Indicators (KPIs)

| KPI | Current Value |
|---|---:|
| Total Countries | 24 |
| Total Shipping States / Regions | 73 |
| Total Cities | 269 |
| Top State | Kerala |
| Repeat Customers | 21 |

## 🧮 DAX Measures Used

| Measure | Purpose |
|---|---|
|Total  Orders | Counts distinct orders (`DISTINCTCOUNT` of `order_id`). |
| Total Revenue | Sums converted order value in INR (`order_subtotal_INR2`). |
| Total Countries / States / Cities | Count distinct, non-blank shipping countries, states, and cities. |
| Top State | Returns the state with the most orders using `TOPN`. |
| Repeat Customers | Counts identified customers with more than one order. |

## 📊 Charts & Their Uses

| Chart Name | Purpose |
|---|---|
| Top 10 Cities by Number of Orders | Shows which cities place the most orders. |
| Geographic Sales Distribution | Maps the countries that have received orders. |
| Total Orders by Region Type | Compares domestic (India) and international order volume. |
| Total Orders by Shipping State | Compares order volume across states and regions. |

## 💡 Insights from the Charts

### 1. Top 10 Cities by Number of Orders

Bengaluru leads with 57 orders (about 8% of all orders), ahead of Hyderabad (33) and Thiruvananthapuram (28). Four of the top 10 cities are in Kerala, and the top 10 cities together account for 256 of 690 orders (about 37%).

### 2. Geographic Sales Distribution

Orders reach 24 countries. India contributes about 53.5% of order value, and the United States is the largest overseas market at approximately ₹431K. Beyond the United States, Singapore, and the United Kingdom, each country contributes under ₹50K.

### 3. Total Orders by Region Type

India accounts for 609 orders (about 88.3%) and international destinations for 81 (about 11.7%). The international orders contribute about 46.5% of order value because the average international order is considerably larger (approximately ₹14.5K compared with ₹2.2K in India).

### 4. Total Orders by Shipping State

Kerala accounts for 235 of 690 orders (about 34%), more than Maharashtra, Tamil Nadu, and Karnataka combined. The top five states account for about 70% of orders, and 36 of the 73 regions placed only a single order.

## 🔍 Other Key Insights

- **Concentration:** The top five Indian states account for about 75% of INR order value, with Kerala alone at about 27%.
- **Value vs. Volume:** Hyderabad generates more order value than Bengaluru (approximately ₹147K vs ₹127K) from fewer orders, because its average order is about twice as large. Kerala has the lowest average order value among the major states.
- **Growth in 2026:** Kerala orders rose from 28 in 2026 Q1 to 89 in 2026 Q2 (about 64% of that quarter's orders), while the other main states remained broadly flat.
- **Products by Region:** Agnijith 90 gms leads in Karnataka, Maharashtra, Tamil Nadu, and Telangana, whereas Agnihari leads in Kerala.
- **Repeat Customers:** Only 21 of 323 identified customers (about 6.5%) ordered more than once, and 19 of them stayed within a single city.
- **Single-Order Cities:** 189 of 269 cities (about 70%) placed only one order.
- **Billing vs. Shipping:** Billing and shipping city, state, and country match on all 690 orders in the cleaned data, so orders shipped to a different address cannot be identified.
- **Guest Checkout:** About 49% of orders have no customer ID, limiting location-level repeat-customer analysis.


## ✅ Conclusion

This regional analysis shows that Jagadha's orders are concentrated in a small number of locations, led by Kerala, while international customers contribute a large share of order value from a small number of orders. Repeat purchasing and location-level customer tracking remain limited, highlighting areas for further growth and data improvement.
