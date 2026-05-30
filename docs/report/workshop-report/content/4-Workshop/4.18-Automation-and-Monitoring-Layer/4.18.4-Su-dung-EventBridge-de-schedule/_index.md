---

title: "4.18.4. Use EventBridge for Scheduling"
linkTitle: "4.18.4. Use EventBridge for Scheduling"
menuTitle: "4.18.4. Use EventBridge for Scheduling"
date: 2026-05-29
weight: 584
chapter: false
---

EventBridge Scheduler is responsible for running the workflow on a schedule, while Glue Workflow is responsible for orchestrating the execution order: Raw Crawler → ETL Job → Curated Crawler.

#### Create IAM Policy

Go to **IAM** → **Policies** → **Create policy**.

![](/images/4-Workshop/4.18.4-Su-dung-EventBridge-de-schedule/image-001.png)

* Select the **JSON** tab

* Paste the following policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowStartGlueWorkflow",
      "Effect": "Allow",
      "Action": "glue:StartWorkflowRun",
      "Resource": "arn:aws:glue:ap-southeast-1:270642943130:workflow/ecommerce-scheduled-etl-workflow"
    }
  ]
}
```

Click **Next**.

![](/images/4-Workshop/4.18.4-Su-dung-EventBridge-de-schedule/image-002.png)

* Policy name: **AllowStartGlueWorkflow**

Then click **Create policy**.

![](/images/4-Workshop/4.18.4-Su-dung-EventBridge-de-schedule/image-003.png)

#### Create an IAM Role for EventBridge Scheduler

##### CREATE ROLE:

Go to **IAM** → **Roles** → **Create role**.

![](/images/4-Workshop/4.18.4-Su-dung-EventBridge-de-schedule/image-004.png)

For **Trusted entity type**, select **Custom trust policy**, then paste the policy below:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "scheduler.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

EventBridge Scheduler needs an execution role to assume the role and call the target service on behalf of the user. Therefore, the trust principal must be `scheduler.amazonaws.com`.

Then click **Next**.

![](/images/4-Workshop/4.18.4-Su-dung-EventBridge-de-schedule/image-005.png)

##### ATTACH POLICY

In the **Add permissions** step, search for and select the policy **AllowStartGlueWorkflow**.

Then click **Next**.

![](/images/4-Workshop/4.18.4-Su-dung-EventBridge-de-schedule/image-006.png)

* Set the role name to **EventBridgeSchedulerStartGlueWorkflowRole**

Review the information, then click **Create role**.

![](/images/4-Workshop/4.18.4-Su-dung-EventBridge-de-schedule/image-007.png)

#### Create EventBridge Schedule

Access the **AWS Management Console**, search for and select the **Amazon EventBridge** service.

![](/images/4-Workshop/4.18.4-Su-dung-EventBridge-de-schedule/image-008.png)

In the left menu, select **Schedules**, then click **Create schedule**.

![](/images/4-Workshop/4.18.4-Su-dung-EventBridge-de-schedule/image-009.png)

In the **Specify schedule detail** step, configure the following:

* Schedule name: **schedule-ecommerce-glue-workflow**

* Schedule pattern: **Recurring schedule**

* Time zone: **Asia/Saigon**

![](/images/4-Workshop/4.18.4-Su-dung-EventBridge-de-schedule/image-010.png)

* Schedule type: **Cron-based schedule**

* Cron expression: `cron(0 09 * * ? *)`

* Flexible time window: **OFF**

![](/images/4-Workshop/4.18.4-Su-dung-EventBridge-de-schedule/image-011.png)

EventBridge Scheduler supports recurring schedules using cron/rate expressions and also supports time zones in schedules.

#### Select target

In the **Select target** step, configure the following:

* Target API: **All APIs**

* Select service: **AWS Glue**

* Select API: **StartWorkflowRun**

* In the input field, paste the following JSON script:

```json
{
  "Name": "ecommerce-scheduled-etl-workflow"
}
```

Then click **Next**.

![](/images/4-Workshop/4.18.4-Su-dung-EventBridge-de-schedule/image-012.png)

#### Settings

* Enable schedule: **Enable**

* Action after schedule completion: **NONE**

* Execution role: **Use existing role**

* Select an existing role: **EventBridgeSchedulerStartGlueWorkflowRole**

Then click **Next**.

![](/images/4-Workshop/4.18.4-Su-dung-EventBridge-de-schedule/image-013.png)

Review the configuration, then click **Create schedule**. The schedule has been created successfully.

![](/images/4-Workshop/4.18.4-Su-dung-EventBridge-de-schedule/image-014.png)
