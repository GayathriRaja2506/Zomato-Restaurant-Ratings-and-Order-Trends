# 🍽️ Zomato Restaurant Ratings & Order Trends Analysis

## Industry

Food Delivery / Restaurant Analytics / Customer Behaviour / Business Intelligence

---

## Project Overview

Zomato Restaurant Ratings & Order Trends Analysis is an end-to-end Business Intelligence project that analyzes food-delivery orders, customers, restaurants, ratings, reviews, and delivery performance through a five-page interactive Power BI dashboard.

The CSV datasets are stored in MySQL for SQL-based cleaning and analysis. Power Query is used for data preparation, and DAX with Microsoft Power BI is used to build KPIs, visualizations, and interactive reports.

> **Important Project Note:** This is an educational analytics project. The dashboard figures are preliminary observations from the project dataset and should not be treated as verified live data from Zomato. The project has no official affiliation with Zomato.

## Project Workflow

CSV Datasets → MySQL Database → SQL Cleaning & Analysis → Power Query → Data Modeling → DAX Measures → Power BI Dashboards → Insights & Recommendations

---

## Project Objectives

- Build a structured MySQL database for food-delivery data.
- Analyze order volume, order value, order status, and order timing.
- Explore customer segments and their distribution across cities.
- Examine restaurant ratings, reviews, cuisines, and online-delivery availability.
- Compare delivery time and order activity across cities.
- Visualize restaurant locations and ratings across India.
- Convert analytical results into business insights and recommendations.

---

## Problem Statement

Food-delivery platforms generate data about orders, customers, restaurants, ratings, reviews, and delivery performance. Analyzing these separately makes it hard to compare order status, customer segments, restaurant ratings, and city-level patterns.

This project brings the data together to answer questions such as:

- How many orders are delivered, cancelled, or returned?
- Which cities generate the most orders and order value?
- Which payment methods and customer segments contribute most to order value?
- How are customers split between new, regular, and repeat segments?
- Which restaurants and cuisines are rated and ordered the most?
- How widely is online delivery available among restaurants?
- Where might delivery performance or customer experience need further investigation?

The dashboards are descriptive and do not by themselves establish the causes of observed patterns.

---

## Tools & Technologies

| Tool / Technology | Purpose |
|---|---|
| MySQL | Database creation and data storage |
| SQL | Data cleaning, joins, aggregations, and analysis |
| Power Query | Data transformation and preparation |
| Microsoft Power BI Desktop | Interactive dashboards |
| DAX | KPI calculations and measures |
| CSV | Source dataset format |
| GitHub | Version control and portfolio publishing |

---

## Dataset Description

The dataset contains four CSV files: customers, orders, restaurants, and reviews.

| Table | Purpose | Key Fields |
|---|---|---|
| `customers` | Customer segments and locations | `customer_id`, `customer_segment`, `customer_city` |
| `orders` | Order activity, value, status, and delivery | `order_id`, `order_date`, `order_time`, `order_status`, `order_amount`, `payment_method`, `delivery_time_mins`, `customer_id`, `restaurant_id` |
| `restaurants` | Restaurant attributes and ratings | `restaurant_id`, `restaurant_name`, `city`, `primary_cuisine`, `restaurant_rating`, `rating_count`, `online_delivery` |
| `reviews` | Ratings and written feedback | `rating`, `review_text`, `review_id` and related identifiers |

> **To complete before publishing:** dataset source/attribution, exact MySQL database and table names, and verified row and column counts.

---

## Database Design

**Database Name:** *(add your MySQL database name)*

```
     customers                restaurants
   (customer_id)            (restaurant_id)
         |                        |
         +-----------+------------+
                     |
                     v
                  orders  <------ reviews
                     |
                     v
             Power BI Reporting
```

This is a conceptual illustration. The actual relationships should match the keys in your tables and the Power BI model, including the date table relationship.

---

## SQL Analysis

SQL is used to clean, validate, aggregate, and analyze the data. The scripts are in the `SQL` folder.

**Key activities:** database and table creation, import validation, row count checks, missing-value and duplicate checks, joins between orders, customers, and restaurants, and KPI aggregations.

**Example — Orders by status**

```sql
SELECT order_status, COUNT(*) AS total_orders
FROM orders
GROUP BY order_status
ORDER BY total_orders DESC;
```

**Example — Average delivery time by city**

```sql
SELECT c.customer_city, AVG(o.delivery_time_mins) AS avg_delivery_time
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
GROUP BY c.customer_city
ORDER BY avg_delivery_time DESC;
```

> These are illustrative. Replace them with the exact queries from the SQL script in the `SQL` folder.

---

## ETL & Data Cleaning

1. **Extract** — CSV files are imported into MySQL and connected to Power BI.
2. **Transform** — Review column names, fix data types, check missing values and duplicates, standardize categories, prepare date and time fields, and validate numeric fields.
3. **Load** — Load the prepared tables into the Power BI model, then create relationships, DAX measures, and visuals.

---

## DAX Measures

| Area | Measures |
|---|---|
| Orders & Revenue | Total Orders, Total Order Value, Average Order Value, Delivered Orders, Cancelled Orders, Cancellation Rate % |
| Delivery & Ratings | Average Delivery Time, Average Review Rating |
| Customers | Total Customers, Repeat Customers, New Customers, Regular Customers, Customer Retention %, Average Spend per Customer |

---

## Power BI Dashboard Architecture

**Page 1 → Overview → Page 2 → Restaurants → Page 3 → Customers → Page 4 → Ratings & Orders → Page 5 → Map**

### Page 1 — Zomato Restaurant Ratings & Order Trends Analysis

**KPI cards:** 12.00K Total Orders · 3.95 Average Review Rating · 6.29M Total Order Value · 35.92 Average Delivery Time

**Visuals:**
- Orders by Hour
- Total Order Value, Total Orders, and Average Order Value by customer city (area chart)
- Total Orders by order status (donut chart)
- Order Value Breakdown (decomposition tree: order status → payment method → customer segment)
- Total Orders by customer city (bar chart)

### Page 2 — Zomato Restaurant Analysis

**Visuals:**
- Highest-Rated Restaurants
- Total Restaurants by online delivery (pie chart)
- Total Reviews by review text
- Restaurant Rating Distribution
- Total Orders by restaurant name and order status (100% stacked bar)
- Total Reviews and Total Restaurants by city (donut chart)

### Page 3 — Customer Behaviour & Insights

**KPI cards:** 900 Total Customers · 229 Repeat Customers · 232 New Customers · 439 Regular Customers · 0.25 Customer Retention %

**Visuals:**
- Order Status by Customer Segment
- Customer by Segment (donut chart)
- Customer Distribution by City
- Total Orders by Year Month and customer segment
- Average Spend by Segment
- City vs Customer Segment (matrix)

### Page 4 — Zomato Ratings & Orders Analysis

**KPI cards:** 11K Delivered Orders · 865 Cancelled Orders · 0.07 Cancellation Rate % · 524.05 Average Order Value

**Visuals:**
- Average Delivery Time by city
- Order Amount Distribution
- Restaurant count and average review rating by restaurant rating (histogram)
- Order Status Breakdown
- Total Orders by primary cuisine and restaurant name (treemap)
- Top 10 Restaurants by Revenue

### Page 5 — Restaurant Locations and Ratings Across India

A bubble map showing restaurant locations across India. Bubbles appear over Delhi, Jaipur, Ahmedabad, Mumbai, Pune, Hyderabad, Bengaluru, Chennai, Coimbatore, and Kolkata, with tooltips for city, reviews, restaurant name, average restaurant rating, and total orders.

---

## Key Business Insights

The following observations are read from the dashboard screenshots. Validate them against the source tables and DAX definitions before formal use.

**Orders & Revenue**
- The dataset shows **12.00K orders** with a total order value of **6.29M** (average order value **524.05**; currency not confirmed).
- **Delivered** orders make up about **90.96%** of orders (about 11K), with **865 cancelled** orders and a small share of returned orders.
- By value, delivered orders account for about **57.26 lakh** of the **62.89 lakh** total, cancelled orders about **4.50 lakh**, and returned orders about **1.12 lakh**.
- Within the delivered, credit-card path selected in the breakdown tree, **UPI** has the largest order value of the payment methods shown (about 26.93 lakh), ahead of credit card (about 10.21 lakh) and debit card (about 8.51 lakh).

**Cities**
- **Chennai** has the most orders (about 1.4K) and the highest order value; **Kolkata** has the fewest orders (about 0.9K) and the lowest order value.
- Mumbai and Bengaluru follow Chennai at about 1.3K orders each.
- Average delivery time looks similar across cities (roughly in the mid-30s).

**Customers**
- Of **900 customers**, **439 (48.78%)** are regular, **232 (25.78%)** new, and **229 (25.44%)** repeat/frequent.
- **Chennai** (105 customers) and **Mumbai** (103) have the largest customer bases.
- Average spend per customer is similar across segments, with the new segment slightly highest.

**Restaurants & Ratings**
- About **84.94% (203)** of restaurants offer online delivery; **15.06% (36)** do not.
- Restaurant ratings are concentrated around **4**, and the average review rating is **3.95**.
- Review text is spread fairly evenly across categories such as "Great taste", "Late delivery", "Food was cold on arrival", and "Packaging could be better".
- Top restaurants by order value include Grill Garden 101, Pizza Station, Cafe Mosaic 128, and Noodle Hub 043.

---

## Recommendations

Depending on the validated results, the analysis can support actions such as:

- Investigate the cancelled orders (865) by city, restaurant, and customer segment.
- Review delivery-time differences across cities and investigate cities with longer times.
- Look at negative review themes (late delivery, cold food, packaging) to see which restaurants are affected.
- Study the 15% of restaurants without online delivery and compare their ratings and orders.
- Design retention efforts for new customers, since new customers are about a quarter of the base.
- Explore why Kolkata has the fewest orders compared with other cities.
- Keep a close watch on UPI, the largest payment channel in the displayed breakdown.

These are example actions; final recommendations should rest on validated findings.

---

## Dashboard Screenshots

### 1. Overview Dashboard
![Zomato Restaurant Ratings and Order Trends Analysis](./Dashboard%20Screenshots/zomato%20Restaurant%20Ratings%20%26%20Order%20Trend%20Analysis.png)

### 2. Restaurant Analysis
![Zomato Restaurant Analysis](./Dashboard%20Screenshots/zomato%20restaurant%20analysis.png)

### 3. Customer Behaviour & Insights
![Customer Behaviour and Insights](./Dashboard%20Screenshots/customer%20behaviour%20%26%20insights.png)

### 4. Ratings & Orders Analysis
![Zomato Ratings and Orders Analysis](./Dashboard%20Screenshots/zomato%20ratings%20%26%20orders%20analysis.png)

### 5. Restaurant Locations and Ratings Across India
![Restaurant Locations and Ratings Across India](./Dashboard%20Screenshots/restaurants%20loactions%20and%20ratings%20across%20india.png)

> The image paths point to the `Dashboard Screenshots` folder. Each filename must match the file in that folder exactly (including capitals and underscores).

---

## Repository Structure

```text
Zomato-Restaurant-Ratings-and-Order-Trends/
│
├── README.md
│
├── Raw Dataset/
├── Cleaned dataset/
├── SQL/
├── PowerBI/
├── Documentation/
│
└── Dashboard Screenshots/
    ├── zomato Restaurant Ratings & Order Trend Analysis.png
    ├── zomato restaurant analysis.png
    ├── customer behaviour & insights.png
    ├── zomato ratings & orders analysis.png
    └── restaurants loactions and ratings across india.png
```

---

## How to Run the Project

1. **Prepare the datasets** — verify filenames, columns, data types, and record counts, and make sure key columns have no blanks.
2. **Create the MySQL database** in MySQL Workbench.
3. **Create the tables** matching the CSV columns and data types.
4. **Import the CSV files** and verify the import.
5. **Validate the data** — row counts, missing values, duplicates, and key consistency.
6. **Run the SQL script in the `SQL` folder** and review the results.
7. **Open the `.pbix` file in the `PowerBI` folder** in Power BI Desktop.
8. **Connect to MySQL** (install the MySQL connector if needed).
9. **Refresh the data** after verifying the model.
10. **Explore the five dashboard pages** using slicers, filters, and visuals.

---

## Limitations & Validation Notes

- Add the dataset source URL and licensing details.
- Confirm the MySQL database and table names, row counts, currency, and units.
- **Year Month shows `(Blank)`** on the customer page, so monthly trends are not reliable yet. Check missing order dates, date data types, the date table range, and the date–orders relationship.
- **A `(Blank)` city** appears in Average Delivery Time by city. Check for restaurants or orders with missing city values.
- **Cancellation Rate % (0.07) and Customer Retention % (0.25)** display as decimals. Format them as percentages and confirm the formulas (865 cancelled out of about 12K orders is roughly 7%).
- The **Order Amount Distribution pie chart** has too many distinct values to read; use numeric bins or a histogram instead.
- **Review text categories** are numerous; consider grouping them or doing text analysis.
- The **Top 10 Restaurants by Revenue** visual shows only 4 restaurants in view; resize it or add scrolling.
- Results depend on filters, relationships, and measure definitions in the PBIX file.
- Do not publish passwords, database credentials, or private customer information.

---

## Project Outcome

This project demonstrates an end-to-end Business Intelligence workflow:

**MySQL + SQL + Power Query + DAX + Power BI**

It shows how food-delivery data can be turned into interactive dashboards for monitoring orders, comparing customer segments, analyzing restaurant ratings, exploring city-level performance, and communicating findings visually.

---

## Author

**Name:** Gayathri R

**Student ID:** AF05321013

**Organization:** Anudip Foundation

**Course:** DBA_AI

**Batch Code:** ANP-D7635

**Technologies:** MySQL | SQL | Power Query | DAX | Microsoft Power BI | GitHub

---

## License

This project is created for educational, portfolio, and data analytics demonstration purposes. It is an independent analytics project and is not an official Zomato product or a source of verified live data.

⭐ If you find this project useful, feel free to explore the repository and its documentation.
