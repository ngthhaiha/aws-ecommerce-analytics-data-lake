---

title: "5.18.1. Create SNS Email Notification"
linkTitle: "5.18.1. Create SNS Email Notification"
menuTitle: "5.18.1. Create SNS Email Notification"
date: 2026-05-29
weight: 681
chapter: false
--------------

# 5.18.1. Create SNS Email Notification

#### Access Amazon SNS

Access the AWS Management Console, search for and select the **Simple Notification Service**.

![](/images/5-Workshop/5.18.1-Tao-SNS-Email-Notification/image-001.png)

In the left menu, select **Topics**, then click **Create topic**.

![](/images/5-Workshop/5.18.1-Tao-SNS-Email-Notification/image-002.png)

#### Create SNS Topic

In the **Details** section, configure the following:

* Type: **Standard**

* Name: **ecommerce-etl-alerts**

Then click **Create topic**.

![](/images/5-Workshop/5.18.1-Tao-SNS-Email-Notification/image-003.png)

The SNS Topic has been created successfully.

After creating the topic, click **Create subscription** to create an email subscription.

![](/images/5-Workshop/5.18.1-Tao-SNS-Email-Notification/image-004.png)

In the **Details** section of **Create subscription**, configure the following:

* Protocol: **Email**

* Endpoint: the email address that will receive notifications (**[nguyenthihaiha8124@gmail.com](mailto:nguyenthihaiha8124@gmail.com)**)

Then click **Create subscription**.

![](/images/5-Workshop/5.18.1-Tao-SNS-Email-Notification/image-005.png)

After the subscription is created successfully, the initial subscription status will be **Pending confirmation**.

![](/images/5-Workshop/5.18.1-Tao-SNS-Email-Notification/image-006.png)

#### Confirm email subscription

Access the registered email inbox and find the email from **AWS Notifications**. You will see an email similar to the image below. Click **Confirm subscription**.

![](/images/5-Workshop/5.18.1-Tao-SNS-Email-Notification/image-007.png)

The subscription has been confirmed successfully.

![](/images/5-Workshop/5.18.1-Tao-SNS-Email-Notification/image-008.png)

After the confirmation is successful, return to SNS to check the subscription status. The status should display: **Confirmed**.

![](/images/5-Workshop/5.18.1-Tao-SNS-Email-Notification/image-009.png)
