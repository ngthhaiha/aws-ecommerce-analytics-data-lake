---

title: "5.8.2. Create Glue Crawler for Curated Parquet Data"
linkTitle: "5.8.2. Create Glue Crawler for Curated Parquet Data"
menuTitle: "5.8.2. Create Glue Crawler for Curated Parquet Data"
date: 2026-05-29
weight: 582
chapter: false
--------------

After creating the database, continue creating a Glue Crawler to scan the Parquet data in the **curated/** folder.

* In **AWS Glue**, select **Data Catalog** → **Crawlers**.

* Then click **Create crawler**.

![](/images/5-Workshop/5.8.2-Tao-Glue-Crawler-cho-du-lieu-Curated-Parquet/image-001.png)

#### Configure crawler information

On the **Set crawler properties** screen, enter:

* Name: **crawler_ecommerce_curated**

Then click **Next**.

![](/images/5-Workshop/5.8.2-Tao-Glue-Crawler-cho-du-lieu-Curated-Parquet/image-002.png)

#### Add a data source for the crawler

At the data source selection step, click **Add a data source**.

![](/images/5-Workshop/5.8.2-Tao-Glue-Crawler-cho-du-lieu-Curated-Parquet/image-003.png)

In the **Add a data source** interface, configure the following:

* Data source: Select **S3**

* Enter the S3 path: **s3://ecommerce-analytics-datalake-270642943130-ap-southeast-1-an/curated/**

After selecting the correct S3 path, click **Add an S3 data source**.

![](/images/5-Workshop/5.8.2-Tao-Glue-Crawler-cho-du-lieu-Curated-Parquet/image-004.png)

The data source has been added to the crawler. Click **Next** to continue.

![](/images/5-Workshop/5.8.2-Tao-Glue-Crawler-cho-du-lieu-Curated-Parquet/image-005.png)

#### Select an IAM Role for the crawler

On the **Configure security settings** screen, select the IAM Role created for AWS Glue: **AWSGlueServiceRoleDefault**.

Then click **Next**.

This IAM Role allows the Glue Crawler to read data from S3 and write metadata to the Glue Data Catalog.

![](/images/5-Workshop/5.8.2-Tao-Glue-Crawler-cho-du-lieu-Curated-Parquet/image-006.png)

#### Configure crawler output

On the **Set output and scheduling** screen, configure the following:

* Target database: **ecommerce_curated**

* Table name prefix: **curated_**

* Crawl schedule: **On demand**

In this step, select **On demand** because the crawler will be run manually. Later, the crawler can be added to a Glue Workflow or scheduled automatically using EventBridge.

After completing the configuration, click **Next**.

![](/images/5-Workshop/5.8.2-Tao-Glue-Crawler-cho-du-lieu-Curated-Parquet/image-007.png)

#### Review and create the crawler

On the **Review and create** screen, review the following information:

* Name: **crawler_ecommerce_curated**

* Data source: the **curated/** folder in S3

* IAM Role: **AWSGlueServiceRoleDefault**

* Target database: **ecommerce_curated**

* Table name prefix: **curated_**

* Schedule: **On demand**

If all information is correct, click **Create crawler**.

![](/images/5-Workshop/5.8.2-Tao-Glue-Crawler-cho-du-lieu-Curated-Parquet/image-008.png)

The crawler **crawler_ecommerce_curated** has been created successfully.
