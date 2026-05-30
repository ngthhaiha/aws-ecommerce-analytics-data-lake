---

title: "4.8.4. Query Curated Tables in Athena"
linkTitle: "4.8.4. Query Curated Tables in Athena"
menuTitle: "4.8.4. Query Curated Tables in Athena"
date: 2026-05-29
weight: 484
chapter: false
--------------

After the Glue Crawler has created metadata for the curated data, you can verify the data using **Amazon Athena**.

Access **Amazon Athena**. In the **Query editor**, select:

* Data source: **AwsDataCatalog**

* Database: **ecommerce_curated**

#### Query the curated_fact_events table

* Check the total number of rows in the `curated_fact_events` table:

```sql
SELECT COUNT(*) AS total_events
FROM ecommerce_curated.curated_fact_events;
```

![](/images/4-Workshop/4.8.4-Query-Curated-Tables-trong-Athena/image-001.png)

* Check the number of events by each `year`, `month`, and `day` partition:

```sql
SELECT year, month, day, COUNT(*) AS total_events
FROM ecommerce_curated.curated_fact_events
GROUP BY year, month, day
ORDER BY year, month, day
LIMIT 20;
```

![](/images/4-Workshop/4.8.4-Query-Curated-Tables-trong-Athena/image-002.png)

This query helps verify whether the `fact_events` data has been correctly partitioned by date.

#### Query the curated_fact_transactions table

* Check the total number of rows in the `curated_fact_transactions` table:

```sql
SELECT COUNT(*) AS total_transactions
FROM ecommerce_curated.curated_fact_transactions;
```

![](/images/4-Workshop/4.8.4-Query-Curated-Tables-trong-Athena/image-003.png)

* Check the number of transactions by each `year`, `month`, and `day` partition:

```sql
SELECT year, month, day, COUNT(*) AS total_transactions
FROM ecommerce_curated.curated_fact_transactions
GROUP BY year, month, day
ORDER BY year, month, day
LIMIT 20;
```

![](/images/4-Workshop/4.8.4-Query-Curated-Tables-trong-Athena/image-004.png)

This query helps verify whether valid transaction data has been written correctly to the curated layer and partitioned properly by date.

#### Query the curated_dim_products table

* Check the total number of products in the `curated_dim_products` table:

```sql
SELECT COUNT(*) AS total_products
FROM ecommerce_curated.curated_dim_products;
```

![](/images/4-Workshop/4.8.4-Query-Curated-Tables-trong-Athena/image-005.png)

* Check the number of products by category:

```sql
SELECT
category,
COUNT(*) AS product_count
FROM ecommerce_curated.curated_dim_products
GROUP BY category
ORDER BY product_count DESC;
```

![](/images/4-Workshop/4.8.4-Query-Curated-Tables-trong-Athena/image-006.png)

This query helps verify whether the product data has been crawled correctly and categorized properly by category.
