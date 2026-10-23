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

## 💼 Business Recommendations

- Validate currency conversion and revenue calculations before financial reporting.
- Investigate the high-value order affecting the October 2025 revenue peak.
- Monitor leading products and compare revenue with units sold.
- Evaluate geographic markets using both order count and revenue.
- Review processing orders and improve customer-level reporting where possible.

## 🛠️ Tools & Technologies

- Microsoft Power BI
- Power Query
- DAX
- Microsoft Excel
- WooCommerce


## ✅ Conclusion

This project demonstrates how data cleaning, KPI analysis, and Power BI visualization can be used to explore e-commerce sales performance, identify important business patterns, and highlight areas requiring further investigation.
