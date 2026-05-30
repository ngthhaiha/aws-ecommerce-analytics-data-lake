---

title: "5.7.2. Check Output on Amazon S3"
linkTitle: "5.7.2. Check Output on Amazon S3"
menuTitle: "5.7.2. Check Output on Amazon S3"
date: 2026-05-29
weight: 573
chapter: false
--------------

After the Glue Job runs successfully, return to the Amazon S3 service.

Access the project bucket **ecommerce-analytics-datalake-270642943130-ap-southeast-1-an**.

Then check the **curated/** folder.

The data structure after ETL will be as follows:

```
curated/
├── dim_products/
├── fact_events/
└── fact_transactions/
```

The data structure after ETL:

```
curated/
├── dim_products/
│   └── part-xxxxx.snappy.parquet
│
├── fact_events/
│   └── year=2021/
│       └── month=1/
│           └── day=1/
│               └── part-xxxxx.snappy.parquet
│
└── fact_transactions/
    └── year=2021/
        └── month=1/
            └── day=1/
                └── part-xxxxx.snappy.parquet
```

#### Check the dim_products table

* Go to **curated/dim_products/**.

* This folder contains product data that has been cleaned and written in Parquet format.

* The data in this folder is not partitioned by date because it is a product dimension table.

![](/images/5-Workshop/5.7.3-Kiem-tra-output-tren-Amazon-S3/image-001.png)

#### Check the fact_events table

* Go to **curated/fact_events/**.

* The **fact_events** table is partitioned by year, month, and day. Therefore, the folder structure will be similar to the following:

```
curated/fact_events/
└── year=YYYY/
    └── month=MM/
        └── day=DD/
            └── part-xxxxx.parquet
```

This partition structure helps Athena and other analytics tools query data more efficiently when filtering by day, month, or year.

![](/images/5-Workshop/5.7.3-Kiem-tra-output-tren-Amazon-S3/image-002.png)

#### Check the fact_transactions table

* Go to **curated/fact_transactions/**.

* The **fact_transactions** table is also partitioned by year, month, and day.

* The folder structure will be similar to the following:

```
curated/fact_transactions/
└── year=YYYY/
    └── month=MM/
        └── day=DD/
            └── part-xxxxx.parquet
```

This folder only contains valid transactions after validation.

![](/images/5-Workshop/5.7.3-Kiem-tra-output-tren-Amazon-S3/image-003.png)

#### Check error data

* Continue checking the **error/transactions/** folder.

* This folder contains invalid transactions, for example:

  * Missing `product_id`

  * Missing `gross_revenue`

  * Invalid `transaction_timestamp` format

  * `gross_revenue < 0` but not marked as a refund

![](/images/5-Workshop/5.7.3-Kiem-tra-output-tren-Amazon-S3/image-004.png)

This is the result after completing the Glue ETL Job. After this step, curated data in Parquet format is available in Amazon S3.

**Expected results:**

* Raw CSV data has been processed using AWS Glue ETL

* Data has been cleaned and cast to the correct data types

* Events and transactions data have been partitioned by year/month/day

* Products data has been stored as a dimension table

* Invalid transactions have been separated into the `error/transactions/` zone

* Curated data is ready for creating a Glue Crawler and querying with Athena

The next step is to create a Glue Data Catalog for the curated data so that Athena can query the Parquet tables after ETL.
