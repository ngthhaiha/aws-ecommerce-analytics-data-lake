---
title: "4.18. Automation & Monitoring Layer"
linkTitle: "4.18. Automation & Monitoring Layer"
menuTitle: "4.18. Automation & Monitoring Layer"
date: 2026-05-29
weight: 580
chapter: false
---

Sau khi pipeline đã chạy thủ công thành công, bước tiếp theo là tự động hóa và giám sát pipeline.

**Kiến trúc automation và monitoring:**

![](/images/FlowChart/4.18.AutomationFlowDetai.png)

**Mô tả Monitoring Layer**

Monitoring layer dùng để theo dõi quá trình chạy pipeline và cảnh báo khi có lỗi.

**SNS Email Notification**

SNS dùng để gửi email cảnh báo khi alarm được kích hoạt.

*Ví dụ:*

Glue Job Failed → EventBridge Rule → SNS → Email Notification
