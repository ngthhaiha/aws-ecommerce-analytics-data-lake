---
title: "4.18. Automation & Monitoring Layer"
linkTitle: "4.18. Automation & Monitoring Layer"
menuTitle: "4.18. Automation & Monitoring Layer"
date: 2026-05-29
weight: 580
chapter: false
---

After the pipeline has successfully run manually, the next step is to automate and monitor the pipeline.

**Automation and monitoring architecture:**

![](/images/FlowChart/4.18.AutomationFlowDetai.png)

**Monitoring Layer Description**

The monitoring layer is used to track the pipeline execution and alert when errors occur.

**SNS Email Notification**

SNS is used to send alert emails when an alarm is triggered.

*Example:*

Glue Job Failed → EventBridge Rule → SNS → Email Notification
