---

title: "4.18.2. Create Glue Workflow"
linkTitle: "4.18.2. Create Glue Workflow"
menuTitle: "4.18.2. Create Glue Workflow"
date: 2026-05-29
weight: 582
chapter: false
--------------

# 4.18.2. Create Glue Workflow

A Glue Workflow is used to group pipeline steps into an ordered processing flow.

The workflow to be created:

```text
Start Workflow
      |
      v
crawler_ecommerce_raw
      |
      v
etl_ecommerce_raw_to_curated_1
      |
      v
crawler_ecommerce_curated
```

#### Create Workflow

Go to **AWS Glue** → **Workflows**, then click **Add workflow**.

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-001.png)

* Workflow name: **ecommerce-scheduled-etl-workflow**

Then click **Create workflow** to create the workflow.

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-002.png)

The workflow has been created successfully. Open the created workflow and proceed to create triggers.

Click **Add trigger** to create a trigger.

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-003.png)

#### Trigger 1: Start Raw Crawler

The first trigger is used to run the raw crawler when the workflow starts.

Configure the trigger as follows:

* Name: **trigger-start-raw-crawler**

* Description: **Start raw crawler when workflow starts**

* Trigger type: **On demand**

Then click **Add**.

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-004.png)

After creating the trigger, attach an action to it by clicking **Action**, then select **Add job/crawler to trigger**.

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-005.png)

In **Add job(s) and crawler(s) to trigger**:

* Select the **Crawler** tab

* Select the crawler **crawler_ecommerce_raw**

Then click **Add**.

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-006.png)

After completing Trigger 1, the graph will look as follows:

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-007.png)

#### Trigger 2: Run ETL Job After Raw Crawler Succeeds

The second trigger is used to run the Glue ETL Job after the raw crawler completes successfully.

After the Raw Crawler node is available, create the second trigger by selecting the **crawler_ecommerce_raw** node and clicking **Add trigger**.

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-008.png)

Next, attach an action to this trigger by clicking **Action**, then select **Add jobs/crawlers to watch**.

Then click **Add node** and configure the trigger as follows:

* Name: **trigger-after-raw-crawler-success**

* Description: **Start ETL job after raw crawler succeeds**

* Trigger type: **Event**

* Trigger logic: **Start after ANY watched event**

Then click **Add** to add the trigger.

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-009.png)

After the node is created successfully, click **Add node**. In **Add job(s) and crawler(s) to trigger**:

* Select the **Jobs** tab

* Select the Glue Job: **etl_ecommerce_raw_to_curated_1**

Then click **Add**.

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-010.png)

After the trigger is added successfully, the workflow graph will appear as shown below. At this step, the trigger watches the crawler, but the action is to run the job.

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-011.png)

#### Trigger 3: Run Curated Crawler After ETL Job Succeeds

The third trigger is used to run the curated crawler after the Glue ETL Job completes successfully.

From the **etl_ecommerce_raw_to_curated_1** node, click **Add trigger** and configure the trigger as follows:

* Name: **trigger-after-etl-success**

* Description: **Start curated crawler after ETL job succeeds**

* Trigger type: **Event**

* Trigger logic: **Start after ANY watched event**

Then click **Add**.

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-012.png)

Click **Add node**. In **Add job(s) and crawler(s) to trigger**:

* Select the **Crawler** tab

* Select the Crawler: **crawler_ecommerce_curated**

Click **Add**.

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-013.png)

After all 3 triggers are created, the workflow graph will look as follows:

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-014.png)

#### Run Glue Workflow

After creating the workflow, click **Run workflow**.

After the workflow finishes running and the status is **Completed**, the workflow has run successfully. Click the **History** tab to check the workflow.

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-015.png)

Select the latest workflow run, then click **View run details**.

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-016.png)

Check each node in the graph. You should see that:

* **crawler_ecommerce_raw** ran successfully

* **etl_ecommerce_raw_to_curated_1** ran successfully

* **crawler_ecommerce_curated** ran successfully

![](/images/4-Workshop/4.18.2-Tao-Glue-Workflow/image-017.png)
