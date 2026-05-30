---
title: "4.4.2. Tạo Glue Database"
linkTitle: "4.4.2. Tạo Glue Database"
menuTitle: "4.4.2. Tạo Glue Database"
date: 2026-05-29
weight: 442
chapter: false
---

**Glue Database** được dùng để nhóm các bảng metadata trong Glue Data Catalog. Ở bước này, tạo một database riêng để lưu metadata của dữ liệu raw.

#### Truy cập Glue Data Catalog

Truy cập **AWS Management Console**, tìm kiếm và chọn dịch vụ **AWS Glue**.

![](/images/4-Workshop/4.4.2-Tao-Glue-Database/image-001.png)

#### Tạo database mới

Trong menu bên trái, chọn **Data Catalog** → **Databases**

Nhấn **Add database**.

![](/images/4-Workshop/4.4.2-Tao-Glue-Database/image-002.png)

#### Tại màn hình tạo database, cấu hình như sau:

- Database type: Chọn **Glue Database**

- Name: **ecommerce_raw**

- Description: **Raw zone metadata database for ecommerce dataset stored in Amazon S3**.

Sau đó nhấn **Create database**.

![](/images/4-Workshop/4.4.2-Tao-Glue-Database/image-003.png)

Glue Database **ecommerce_raw** đã được tạo thành công.
