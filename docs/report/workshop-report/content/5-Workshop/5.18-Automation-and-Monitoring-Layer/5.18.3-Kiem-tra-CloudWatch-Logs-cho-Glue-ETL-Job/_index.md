---

title: "5.18.3. Check CloudWatch Logs for Glue ETL Job"
linkTitle: "5.18.3. Check CloudWatch Logs for Glue ETL Job"
menuTitle: "5.18.3. Check CloudWatch Logs for Glue ETL Job"
date: 2026-05-29
weight: 683
chapter: false
--------------

# 5.18.3. Check CloudWatch Logs for Glue ETL Job

Access the **AWS Management Console**, search for and select the **CloudWatch** service.

![](/images/5-Workshop/5.18.3-Kiem-tra-CloudWatch-Logs-cho-Glue-ETL-Job/image-001.png)

After the Glue Workflow runs, check the Glue ETL Job logs in **CloudWatch** → **Logs** → **Log groups**.

Commonly used log groups:

* `/aws-glue/jobs/output`
* `/aws-glue/jobs/error`

![](/images/5-Workshop/5.18.3-Kiem-tra-CloudWatch-Logs-cho-Glue-ETL-Job/image-002.png)

Purpose:

* Monitor the ETL job execution process.

* Check errors when the job fails.

* Debug data read/write errors, schema errors, or PySpark errors.
