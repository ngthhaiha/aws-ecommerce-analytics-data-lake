---
title: "4.18.1. Tạo SNS Email Notification"
linkTitle: "4.18.1. Tạo SNS Email Notification"
menuTitle: "4.18.1. Tạo SNS Email Notification"
date: 2026-05-29
weight: 581
chapter: false
---

#### Tuy cập Amazon SNS

Truy cập AWS Management Console, tìm kiếm và chọn dịch vụ **Simple Notification Service**.

![](/images/4-Workshop/4.18.1-Tao-SNS-Email-Notification/image-001.png)

Trong menu bên trái chọn **Topics**, sau đó nhấn **Create topic**.

![](/images/4-Workshop/4.18.1-Tao-SNS-Email-Notification/image-002.png)

#### Tạo SNS Topic

Trong phần **Details** cấu hình như sau:

- Type: **Standard**

- Name: **ecommerce-etl-alerts**

Sau đó nhấn **Create topic**.

![](/images/4-Workshop/4.18.1-Tao-SNS-Email-Notification/image-003.png)

SNS Topic đã được tạo thành công.

Sau khi tạo topic, nhấn **Create subscription** để tạo email subscription.

![](/images/4-Workshop/4.18.1-Tao-SNS-Email-Notification/image-004.png)

Trong phần **Details** của Create subscription, cấu hình:

- Protocol: **Email**

- Endpoint: email muốn nhận Notification (nguyenthihaiha8124@gmail.com)

Sau đó nhấn **Create subscription**.

![](/images/4-Workshop/4.18.1-Tao-SNS-Email-Notification/image-005.png)

Sau khi tạo subscription thành công, trạng thái subscription ban đầu sẽ là **pending confirmation**.

![](/images/4-Workshop/4.18.1-Tao-SNS-Email-Notification/image-006.png)

#### Confirm email subscription

Truy cập vào email đã đăng ký, tìm email từ AWS Notifications ta sẽ thấy email như hình dưới đây, nhấn **Confirm subscription**.

![](/images/4-Workshop/4.18.1-Tao-SNS-Email-Notification/image-007.png)

Subscription confirm thành công.

![](/images/4-Workshop/4.18.1-Tao-SNS-Email-Notification/image-008.png)

Sau khi xác nhận thành công, quay lại SNS để kiểm tra trạng thái subscription. Trạng thái cần hiển thị: **Confirmed**.

![](/images/4-Workshop/4.18.1-Tao-SNS-Email-Notification/image-009.png)
