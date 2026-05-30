---
title: "4.18.5. Check the Schedule"
linkTitle: "4.18.5. Check the Schedule"
menuTitle: "4.18.5. Check the Schedule"
date: 2026-05-29
weight: 585
chapter: false
---

After EventBridge Scheduler runs according to the configured schedule, check the workflow at: **AWS Glue** → **Workflows** → **ecommerce-scheduled-etl-workflow** → **History** (section 4.18.2)

In addition, you can also check by accessing the AWS Glue service, then selecting **Job run monitoring** from the left-side menu to confirm that the Glue ETL Job **etl_ecommerce_raw_to_curated_1** has been automatically triggered every day at 9:00.

In the image, we can see that the jobs have been automatically run once per day according to the schedule at 9:00 since the Workflow was created (25/05/2026).

![](/images/4-Workshop/4.18.5-Kiem-tra-schedule/image-001.png)

