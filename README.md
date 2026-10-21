# Zomato-Restaurant-Ratings-and-Order-Trends

## Industry

Food Delivery / Restaurant Analytics / Customer Behaviour / Business Intelligence

---

## Project Overview

Zomato Restaurant Ratings & Order Trends Analysis is an end-to-end Business Intelligence project that demonstrates how food-delivery data covering orders, customers, restaurants, ratings, reviews, and delivery performance can be analyzed through interactive Power BI dashboards.

The project stores the CSV datasets in MySQL for centralized storage and SQL-based analysis. Power Query is used for data preparation, while DAX and Microsoft Power BI are used to build analytical measures, interactive visualizations, and a five-page dashboard.

The platform brings together several business areas to help users explore order activity, compare customer segments, review restaurant ratings, and identify areas that may need further investigation.

> **Important Project Note:** This is an educational analytics project. The dashboard figures should be treated as preliminary observations from the project dataset and should not be interpreted as verified live data from Zomato. The project does not imply any official affiliation with Zomato.

## Project Workflow

CSV Datasets → MySQL Database → SQL Cleaning & Analysis → Power Query → Data Modeling → DAX Measures → Power BI Dashboards → Insights & Recommendations

---

## Business Areas Covered

- Order volume, order value, and order status analysis
- Customer segment and customer retention analysis
- Restaurant rating and review analysis
- Cuisine-wise and city-wise performance comparison
- Online-delivery availability analysis
- Delivery-time analysis across cities
- Payment-method and order-value breakdowns
- Geographic view of restaurant locations and ratings across India
- Identification of areas needing further investigation (cancellations, delivery times, low ratings)

---

## Project Objectives

- Build a structured MySQL database for food-delivery data.
- Analyze order volume, order value, and order status.
- Explore customer segments and their distribution by city.
- Examine restaurant ratings, reviews, cuisine categories, and online-delivery availability.
- Compare delivery-time indicators across cities.
- Perform SQL-based data cleaning, aggregation, and analysis.
- Apply Power Query for data preparation.
- Develop DAX measures for analytical KPIs.
- Build an interactive five-page Power BI dashboard.
- Convert analytical results into meaningful business insights.
- Demonstrate an end-to-end Data Analyst workflow.

---

## Problem Statement

Food-delivery platforms generate data about orders, customers, restaurants, ratings, reviews, and delivery performance. When these areas are analyzed separately, it is difficult to compare order status, customer segments, restaurant ratings, and city-level patterns.

This project brings the data together and presents key indicators in interactive Power BI dashboards to answer questions such as:

- Which order statuses are most common?
- How do customer segments differ in spend and order status?
- Which restaurants have the highest ratings or order value?
- How do ratings and orders vary by city and cuisine?
- How does average delivery time vary across cities?
- How many customers are new, regular, or repeat customers?
- Where may delivery performance or customer experience need further investigation?

The dashboards are descriptive and do not independently establish the causes of the observed patterns.

---

## Tools & Technologies

| Tool / Technology | Purpose |
|---|---|
| MySQL | Database creation, data storage, and table management |
| SQL | Data cleaning, joins, aggregations, and analysis |
| Power Query | Data transformation and preparation |
| Microsoft Power BI Desktop | Interactive dashboards and business intelligence |
| DAX | KPI calculations and analytical measures |
| CSV | Source dataset format |
| GitHub | Version control, documentation, and portfolio publishing |

---

## Dataset Description

The project dataset consists of four CSV files covering customers, orders, restaurants, and reviews.

> **Dataset Source:** *Add the original dataset URL or attribution here before publishing.*
> **Row and column counts:** *Add the verified counts from the actual CSV files or MySQL tables.*

### 1. `customers.csv`

Customer segments and locations.

- Key fields: `customer_id`, `customer_segment`, `customer_city`
- Applications: segment distribution, city-wise customer analysis, retention analysis

### 2. `orders.csv`

Order activity, value, status, and delivery information.

- Key fields: `order_id`, `order_date`, `order_status`, `order_amount`, `delivery_time_mins`, `customer_id`, `restaurant_id`
- Applications: order counts, order value, status breakdown, delivery-time and monthly trend analysis

### 3. `restaurants.csv`

Restaurant attributes and ratings.

- Key fields: `restaurant_id`, `restaurant_name`, `city`, `primary_cuisine`, `restaurant_rating`, `rating_count`, `online_delivery`
- Applications: top-rated restaurants, cuisine comparison, online-delivery availability, map analysis

### 4. `reviews.csv`

Ratings and written feedback.

- Key fields: `rating`, `review_text`, and associated identifiers where available
- Applications: review counts, rating analysis, feedback review

---

## Database Design

**Database Name:** *Confirm the exact name from MySQL Workbench* (e.g. `zomato_analytics`)

The project uses a relational structure in which customers and restaurants act as descriptive tables and orders and reviews hold the transactional records.

### Example Data Model

```
        customers                    restaurants
      (customer_id)                (restaurant_id)
            |                             |
            +-------------+---------------+
                          |
                          v
                       orders
                          |
                          v
                Power BI Reporting
                          ^
                          |
                       reviews
```

> This is a conceptual illustration. The actual relationships should match the keys present in your tables (`customer_id`, `restaurant_id`) and the Power BI model, including the date table relationship.

---

## SQL Analysis

SQL is used to clean, retrieve, validate, aggregate, and analyze the data stored in MySQL. The SQL script in this repository is `zomato sql.sql`.

### Key SQL Activities

- Database and table creation
- CSV data import validation
- Row count verification
- Missing-value and duplicate checks
- Joins between orders, customers, and restaurants
- Aggregation and grouping
- KPI preparation

### Example 1 — Orders by Status

```sql
SELECT
    order_status,
    COUNT(*) AS total_orders
FROM orders
GROUP BY order_status
ORDER BY total_orders DESC;
```

### Example 2 — Total and Average Order Value

```sql
SELECT
    SUM(order_amount) AS total_order_value,
    AVG(order_amount) AS avg_order_value
FROM orders;
```

### Example 3 — Average Delivery Time by City

```sql
SELECT
    c.customer_city,
    AVG(o.delivery_time_mins) AS avg_delivery_time
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
GROUP BY c.customer_city
ORDER BY avg_delivery_time DESC;
```

### Example 4 — Top Rated Restaurants

```sql
SELECT
    restaurant_name,
    city,
    primary_cuisine,
    restaurant_rating
FROM restaurants
ORDER BY restaurant_rating DESC
LIMIT 10;
```

> The examples above are illustrative. Replace them with the exact queries from `zomato sql.sql` and use your actual table and column names.

---

## ETL & Data Cleaning

**1. Extract** — CSV files are imported into MySQL, and Power BI connects to the data for reporting.

**2. Transform** — Reviewing column names, correcting data types, checking missing values, identifying duplicates, standardizing categorical values, preparing date fields, and validating numeric measurements.

**3. Load** — The prepared tables are loaded into the Power BI model, where relationships, DAX measures, and visuals are created.

---

## DAX Measures

Key measures used in the report:

**Orders & Revenue**
- Total Orders
- Total Order Value
- Average Order Value
- Delivered Orders
- Cancelled Orders
- Cancellation Rate

**Delivery & Ratings**
- Average Delivery Time
- Average Review Rating

**Customers**
- Total Customers
- Repeat / Frequent Customers
- Regular Customers
- New Customers
- Customer Retention %

> Confirm each measure's formula, formatting (for example, whether cancellation rate and retention should display as percentages), and units against the PBIX file.

---

## Power BI Dashboard Architecture

The report contains five pages, progressing from a high-level overview to detailed restaurant, customer, and geographic analysis.

**Page 1 → Overview → Page 2 → Restaurants → Page 3 → Customers → Page 4 → Ratings & Orders → Page 5 → Map**

### Page 1 — Zomato Restaurant Ratings & Order Trends Analysis

**KPIs:** Total Orders, Average Review Rating, Total Order Value, Average Delivery Time

**Visuals:** Orders by Hour, order-status breakdown, total orders by customer city, and order-value breakdown by status, payment method, and customer segment.

### Page 2 — Zomato Restaurant Analysis

Highest-rated restaurants, online-delivery availability, review counts by review text, restaurant rating distribution, orders by restaurant and order status, and reviews/restaurants by city.

### Page 3 — Customer Behaviour & Insights

**KPIs:** Total Customers, Repeat Customers, New Customers, Regular Customers, Customer Retention %

**Visuals:** Order status by customer segment, segment distribution, customers by city, orders by year-month and segment, average spend by segment, and a city-versus-segment matrix.

### Page 4 — Zomato Ratings & Orders Analysis

Average delivery time by city, order amount distribution, restaurant count by rating, order-status breakdown, orders by primary cuisine and restaurant, and Top 10 restaurants by order value.

### Page 5 — Restaurant Locations and Ratings Across India

A map of restaurant locations across India with tooltips showing city, reviews, restaurant name, average restaurant rating, and total orders.

---

## Key Business Insights

The values below are taken from dashboard screenshots. Treat them as **preliminary observations**, not audited results.

- The overview displays approximately **12.00K total orders**.
- Total order value is displayed as **6.29M** (currency/unit to be confirmed).
- Average review rating is displayed as **3.95**.
- Average delivery time is displayed as **35.92** (verify unit and filters).
- The customer page shows **900 total customers**: 229 repeat/frequent, 232 new, and 439 regular.
- The customer-retention card shows **0.25** (confirm formula and percentage formatting).
- **Delivered** is the largest order-status category in the displayed data.

> Validate these figures against the source tables and DAX definitions before using them in a presentation. Do not infer causes from charts alone.

---

## Recommendations

Depending on the validated results, the analysis can support actions such as:

- Investigate cities with higher average delivery times.
- Review cancelled orders by city, restaurant, and customer segment.
- Examine low-rated restaurants with high order volume.
- Compare spend across customer segments to identify retention opportunities.
- Compare ratings and orders across cuisines.
- Check the impact of online-delivery availability on ratings and orders.
- Group review-text categories to make feedback easier to interpret.

These are example analytical actions; final recommendations should rest on validated dashboard findings.

---

## Dashboard Screenshots

### 1. Overview Dashboard
![Zomato Restaurant Ratings and Order Trends Analysis](./zomato%20Restaurant%20Ratings%20%26%20Order%20Trend%20Analysis.jpg)

### 2. Restaurant Analysis
![Zomato Restaurant Analysis](./zomato%20restaurant%20analysis.jpg)

### 3. Customer Behaviour & Insights
![Customer Behaviour and Insights](./customer%20behaviour%20%26%20insights.jpg)

### 4. Ratings & Orders Analysis
![Zomato Ratings and Orders Analysis](./zomato%20ratings%20%26%20orders%20analysis.jpg)

### 5. Restaurant Locations and Ratings Across India
![Restaurant Locations and Ratings Across India](./restaurants%20locations%20and%20ratings%20across%20india.jpg)

---

## Repository Structure

```text
Zomato-PowerBI-SQL-Project/
│
├── README.md
├── zomato sql.sql
├── zomato powerbi.pbix
│
├── Dataset/                      (optional, if you upload the CSV files)
│   ├── customers.csv
│   ├── orders.csv
│   ├── restaurants.csv
│   └── reviews.csv
│
└── Screenshots/
    ├── zomato Restaurant Ratings & Order Trend Analysis.jpg
    ├── zomato restaurant analysis.jpg
    ├── customer behaviour & insights.jpg
    ├── zomato ratings & orders analysis.jpg
    └── restaurants locations and ratings across india.jpg
```

> Update the structure to match the files actually uploaded to your repository. If you move the screenshots into a folder, update the image paths above.

---

## How to Run the Project

1. **Prepare the datasets** — Locate the CSV files and verify filenames, columns, data types, and record counts (make sure there are no blank values in key columns before import).
2. **Create the MySQL database** — Open MySQL Workbench and create your database.
3. **Create the tables** — Define tables that match the CSV column names and data types.
4. **Import the data** — Import the CSV files into their corresponding tables and verify the import.
5. **Validate the database** — Check row counts, missing values, duplicates, and key consistency.
6. **Run the SQL analysis** — Execute the queries in `zomato sql.sql` and review the results.
7. **Open the Power BI report** — Open `zomato powerbi.pbix` in Power BI Desktop.
8. **Connect to MySQL** — Configure the connection to your database (install the MySQL connector if required).
9. **Refresh the data** — Refresh the report after verifying the model.
10. **Explore the dashboard** — Navigate the five pages using slicers, filters, and visuals.

---

## Limitations & Validation Notes

- Add the exact dataset source URL and licensing details.
- Confirm the MySQL database name and exact table names.
- Confirm row counts, column counts, currency, and units from the source data.
- A `(Blank)` Year Month category appeared on the customer page; check missing order dates, date data types, the date-table range, and the date–orders relationship before relying on monthly trends.
- Validate the cancellation-rate and customer-retention formulas and their formatting.
- A pie chart with many distinct order amounts is hard to read; consider numeric bins or a histogram.
- Review-text categories may be too numerous for a readable axis; consider grouping.
- Results depend on filters, relationships, and measure definitions in the PBIX file.
- Do not publish passwords, database credentials, or private customer information.

---

## Project Outcome

This project demonstrates an end-to-end Business Intelligence workflow:

**MySQL + SQL + Power Query + DAX + Power BI**

It shows how food-delivery data can be transformed into interactive dashboards that help users monitor orders, compare customer segments, analyze restaurant ratings, explore city-level delivery performance, and communicate findings visually. It reflects practical skills in database management, SQL querying, data preparation, data modeling, DAX calculations, and dashboard development.

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
