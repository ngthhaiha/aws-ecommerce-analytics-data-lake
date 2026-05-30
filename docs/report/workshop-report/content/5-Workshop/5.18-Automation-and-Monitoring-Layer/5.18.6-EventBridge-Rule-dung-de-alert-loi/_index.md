---

title: "5.18.6. EventBridge Rule for Error Alerts"
linkTitle: "5.18.6. EventBridge Rule for Error Alerts"
menuTitle: "5.18.6. EventBridge Rule for Error Alerts"
date: 2026-05-29
weight: 686
chapter: false
--------------

# 5.18.6. EventBridge Rule for Error Alerts

We will use EventBridge to create rules that capture the following errors:

* Raw Crawler Failed

* Glue ETL Job FAILED / TIMEOUT / STOPPED

* Curated Crawler Failed

Then, the alerts will be sent to the email address registered in the SNS Email subscription.

#### Create EventBridge Rule

Access the AWS Management Console, search for and select the **Amazon EventBridge** service.

![](/images/5-Workshop/5.18.6-EventBridge-Rule-dung-de-alert-loi/image-001.png)

On the main screen, select **Create rule**.

![](/images/5-Workshop/5.18.6-EventBridge-Rule-dung-de-alert-loi/image-002.png)

#### Create an alert when the Raw Crawler or Curated Crawler fails

In the **Builder mode** section, select **Advanced builder**.

Then the configuration steps for the rule will be displayed. In the **Define rule detail** step, configure the following:

* Name: **alert-ecommerce-crawler-failed**

Click **Next**.

![](/images/5-Workshop/5.18.6-EventBridge-Rule-dung-de-alert-loi/image-003.png)

In the **Build event pattern** step, select **Custom pattern (JSON editor)** and paste the following JSON into the **Event pattern** box:

```json
{
  "source": ["aws.glue"],
  "detail-type": ["Glue Crawler State Change"],
  "detail": {
    "crawlerName": [
      "crawler_ecommerce_raw",
      "crawler_ecommerce_curated"
    ],
    "state": ["Failed"]
  }
}
```

Then click **Next**.

![](/images/5-Workshop/5.18.6-EventBridge-Rule-dung-de-alert-loi/image-004.png)

Next, in the **Select target(s)** step, configure the following:

* Target types: **AWS service**

```sql
Select a target: SNS Topic
```

* Target location: **Target in this account**

* Topic: **ecommerce-etl-alerts**

* Execution role: **Create a new role for this specific resource**

Then click **Next**.

![](/images/5-Workshop/5.18.6-EventBridge-Rule-dung-de-alert-loi/image-005.png)

Review the configuration, then click **Create rule**.

![](/images/5-Workshop/5.18.6-EventBridge-Rule-dung-de-alert-loi/image-006.png)

The EventBridge Rule for crawler failure alerts has been created successfully.

![](/images/5-Workshop/5.18.6-EventBridge-Rule-dung-de-alert-loi/image-007.png)

AWS Glue crawler state change events include states such as **Started**, **Succeeded**, and **Failed**, so this rule will send an SNS notification when either the raw crawler or curated crawler fails.

#### Create an alert when the Glue ETL Job fails

Create an alert rule for Glue ETL Job failures using the same steps as the crawler rule, with the following configuration:

* Name: **alert-ecommerce-glue-job-failed**

* JSON:

```json
{
  "source": ["aws.glue"],
  "detail-type": ["Glue Job State Change"],
  "detail": {
    "jobName": ["etl_ecommerce_raw_to_curated_1"],
    "state": ["FAILED", "TIMEOUT", "STOPPED"]
  }
}
```

![](/images/5-Workshop/5.18.6-EventBridge-Rule-dung-de-alert-loi/image-008.png)

The rule has been created successfully.

![](/images/5-Workshop/5.18.6-EventBridge-Rule-dung-de-alert-loi/image-009.png)

This is the most important rule because it captures errors from the main ETL process. When the Glue Job status becomes **FAILED**, **TIMEOUT**, or **STOPPED**, an email notification will be sent through SNS. AWS Glue job state change events are supported by EventBridge, allowing the system to react to job status changes.
