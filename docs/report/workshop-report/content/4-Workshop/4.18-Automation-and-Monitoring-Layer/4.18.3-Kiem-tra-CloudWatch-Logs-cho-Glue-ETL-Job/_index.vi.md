---
title: "4.18.3. Kiểm tra CloudWatch Logs cho Glue ETL Job"
linkTitle: "4.18.3. Kiểm tra CloudWatch Logs cho Glue ETL Job"
menuTitle: "4.18.3. Kiểm tra CloudWatch Logs cho Glue ETL Job"
date: 2026-05-29
weight: 583
chapter: false
---

Truy cập **AWS Management Console**, tìm kiếm và chọn dịch vụ **CloudWatch**.

![](/images/4-Workshop/4.18.3-Kiem-tra-CloudWatch-Logs-cho-Glue-ETL-Job/image-001.png)

Sau khi Glue Workflow chạy, kiểm tra log của Glue ETL Job tại **CloudWatch** → **Logs** → **Log groups
**
Các log group thường dùng:
- /aws-glue/jobs/output
- /aws-glue/jobs/error

![](/images/4-Workshop/4.18.3-Kiem-tra-CloudWatch-Logs-cho-Glue-ETL-Job/image-002.png)

**Mục đích**:

- Theo dõi quá trình chạy ETL job.

- Kiểm tra lỗi khi job failed.

- Debug lỗi đọc/ghi dữ liệu, lỗi schema hoặc lỗi PySpark.
