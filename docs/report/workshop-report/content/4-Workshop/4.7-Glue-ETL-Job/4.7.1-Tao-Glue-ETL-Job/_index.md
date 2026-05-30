---

title: "4.7.1. Create Glue ETL Job"
linkTitle: "4.7.1. Create Glue ETL Job"
menuTitle: "4.7.1. Create Glue ETL Job"
date: 2026-05-29
weight: 471
chapter: false
--------------

Access the **AWS Management Console**, search for and select the **AWS Glue** service.

In the left menu, select **ETL jobs**. Then choose **Script editor**.

![](/images/4-Workshop/4.7-Glue-ETL-Job/4.7.1-Tao-Glue-ETL-Job/image-001.png)

#### Create a Spark script

In the job creation interface, configure the following:

* Engine: Select **Spark**

* Options: Select **Upload script**

Then click **Create script** to create the Glue Job script.

![](/images/4-Workshop/4.7-Glue-ETL-Job/4.7.1-Tao-Glue-ETL-Job/image-002.png)

After the script is created successfully, switch to the **Job details** tab to configure the job information.

In the **Basic properties** section, configure the following:

* Name: **etl_ecommerce_raw_to_curated**

* IAM Role: Select **AWSGlueServiceRoleDefault**

This role is the IAM Role created in the previous step. It grants Glue permission to read data from S3 and write output data back to S3.

![](/images/4-Workshop/4.7-Glue-ETL-Job/4.7.1-Tao-Glue-ETL-Job/image-003.png)

#### Add Job Parameter

In the **Advanced properties** section of the **Job details** tab, find **Job parameters**, click **Add new parameter**, and add the following parameter:

* Key: **--BUCKET_NAME**

* Value: **ecommerce-analytics-datalake-270642943130-ap-southeast-1-an**

![](/images/4-Workshop/4.7-Glue-ETL-Job/4.7.1-Tao-Glue-ETL-Job/image-004.png)

After completing the configuration, click **Save** to save the Glue Job.

The job has been updated successfully.

![](/images/4-Workshop/4.7-Glue-ETL-Job/4.7.1-Tao-Glue-ETL-Job/image-005.png)

#### Run Glue ETL Job

After the configuration is complete, click **Run** to start running the Glue ETL Job.

![](/images/4-Workshop/4.7-Glue-ETL-Job/4.7.1-Tao-Glue-ETL-Job/image-006.png)

Glue will perform the following steps:

* Read CSV data from the `raw/events/`, `raw/products/`, and `raw/transactions/` folders

* Clean the data and convert data types

* Create curated tables in Parquet format

* Separate invalid transaction records into the `error/transactions/` zone

* Write the output data to S3

#### Check the job run status

After clicking **Run**, switch to the **Runs** tab to monitor the job run status.

Here, check the following information:

* Run status

* Started on

* Duration

* DPU hours

* Error logs, if the job fails

If the job runs successfully, the status will be displayed as **Succeeded**.

![](/images/4-Workshop/4.7-Glue-ETL-Job/4.7.1-Tao-Glue-ETL-Job/image-007.png)

If the job fails, select that job run to view detailed logs and check the root cause in **CloudWatch Logs**.
