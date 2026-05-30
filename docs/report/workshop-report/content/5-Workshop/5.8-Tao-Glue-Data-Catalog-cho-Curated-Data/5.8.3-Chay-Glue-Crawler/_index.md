---

title: "5.8.3. Run Glue Crawler"
linkTitle: "5.8.3. Run Glue Crawler"
menuTitle: "5.8.3. Run Glue Crawler"
date: 2026-05-29
weight: 583
chapter: false
--------------

After the crawler is created successfully, select the crawler **crawler_ecommerce_curated**.

Click **Run crawler** to start crawling the Parquet data in the **curated/** folder.

The crawler will scan the subfolders inside `curated/`, automatically detect the schema, and create metadata tables in the Glue Data Catalog.

![](/images/5-Workshop/5.8.3-Chay-Glue-Crawler/image-006.png)

After the crawler runs successfully, the crawler status will show that the run has completed. The data has been crawled successfully into the **ecommerce_curated** database.

![](/images/5-Workshop/5.8.3-Chay-Glue-Crawler/image-007.png)

#### Check the tables in Glue Data Catalog

After the crawler finishes running, go to **AWS Glue** → **Data Catalog** → **Tables**.

In the **ecommerce_curated** database, check the tables that have been created.

The tables include:

* curated_fact_events

* curated_dim_products

* curated_fact_transactions

Select each table to check its schema.

![](/images/5-Workshop/5.8.3-Chay-Glue-Crawler/image-008.png)

#### Check the curated_fact_events table

Open the **curated_fact_events** table. Then check the main information:

* The data is stored in the `curated/fact_events/` folder

* The data format is Parquet

* It contains time-related columns such as `event_date`, `event_hour`, `year`, `month`, and `day`

* It contains the `ingestion_timestamp` column

* The table is partitioned by `year`, `month`, and `day`

![](/images/5-Workshop/5.8.3-Chay-Glue-Crawler/image-009.png)

#### Check the curated_dim_products table

Open the **curated_dim_products** table. Then check the main information:

* The data is stored in the `curated/dim_products/` folder

* The data format is Parquet

* It contains columns such as `product_id`, `category`, `brand`, `base_price`, `launch_date`, and `is_premium`

* The `is_premium` column has been converted to the boolean type

* It contains the `ingestion_timestamp` column

![](/images/5-Workshop/5.8.3-Chay-Glue-Crawler/image-010.png)

#### Check the curated_fact_transactions table

Open the **curated_fact_transactions** table. Then check the main information:

* The data is stored in the `curated/fact_transactions/` folder

* The data format is Parquet

* It contains time-related columns such as `transaction_date`, `transaction_hour`, `year`, `month`, and `day`

* It contains the `ingestion_timestamp` column

* The table is partitioned by `year`, `month`, and `day`

* It only contains valid transactions after the validation step in the Glue ETL Job

![](/images/5-Workshop/5.8.3-Chay-Glue-Crawler/image-011.png)
