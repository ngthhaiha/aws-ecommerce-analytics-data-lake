---

title: "4.12. Dashboard 1: Executive Overview"
linkTitle: "4.12. Dashboard 1: Executive Overview"
menuTitle: "4.12. Dashboard 1: Executive Overview"
date: 2026-05-29
weight: 520
chapter: false
--------------

The goal of this dashboard is to help viewers understand the overall business performance within about 10 seconds.

**The dashboard should answer the following key questions:**

* Is revenue increasing or decreasing?

* Is the number of orders increasing?

* What is the Average Order Value?

* Is the refund rate abnormal?

* Are there any days or months when revenue dropped significantly?

Dataset used: **vw_executive_overview**

### I. CREATE CALCULATED FIELDS FOR TIME FILTERS

To create filters by year, quarter, and month, create **calculated fields** from the **transaction_date** column.

In QuickSight, select **Add calculated field**.

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-001.png)

#### 1. Create transaction_year

* Calculated field name: **transaction_year**

* Formula: `extract('YYYY', {transaction_date})`

Then click **Save**.

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-002.png)

#### 2. Create transaction_month

* Calculated field name: **transaction_month**

* Formula: `extract('MM', {transaction_date})`

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-003.png)

#### 3. Create transaction_quarter

* Calculated field name: **transaction_quarter**

* Formula: `floor((extract('MM', {transaction_date}) - 1) / 3) + 1`

This formula is used to identify the quarter from the month:

* Months 1, 2, 3 → Quarter 1

* Months 4, 5, 6 → Quarter 2

* Months 7, 8, 9 → Quarter 3

* Months 10, 11, 12 → Quarter 4

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-004.png)

### II. CREATE FILTER CONTROLS

After creating the calculated fields, proceed to create filters for the dashboard.

In the QuickSight Analysis interface:

* Click the **Filter** icon

* Select **Add**

* Select the fields to filter:

  * transaction_year

  * transaction_quarter

  * transaction_month

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-005.png)

Then click the three-dot icon for each filter and select **Add control**. Set the display position to **Top of this sheet**.

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-006.png)

Enter the display name for the filter field, select the **Dropdown** filter type, and click **Add**.

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-007.png)

For the **transaction_quarter** and **transaction_month** filters, enable **Show relevant values only**. This option allows the filters to work in a hierarchy. For example, when a specific year is selected, the quarter and month filters will only show values relevant to that year.

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-008.png)

Select **Quarter** to create the hierarchy Year → Quarter. Click **Update**.

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-009.png)

The relevant hierarchy values have been added successfully. Click **Add** to add the filter.

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-010.png)

The filter has been added successfully.

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-011.png)

### Configure the filter scope

After creating the filter controls, configure the scope in which each filter is applied to visuals.

In QuickSight, each filter can be applied in one of the following three scopes:

| Scope            | Meaning                                                      |
| ---------------- | ------------------------------------------------------------ |
| Only this visual | The filter applies only to the selected visual               |
| This sheet       | The filter applies to all visuals in the current sheet       |
| Cross-sheet      | The filter applies to multiple sheets using the same dataset |

Click each filter and select the **This sheet** icon to apply it to all visuals on the same sheet. Since hierarchy filters are used, Cross-sheet cannot be used.

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-012.png)

Check the filters after creation:

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-013.png)

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-014.png)

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-015.png)

### III. Create KPI Cards

The Executive Overview dashboard has **4 main KPI Cards**:

* TOTAL REVENUE

* TOTAL ORDERS

* AVG ORDER VALUE

* REFUND RATE

#### Create a KPI Card

Create a new visual and select Visual type: **KPI**.

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-016.png)

Configuration:

* Value: **total_revenue(Sum)**

* Show as: **Currency**

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-017.png)

#### Customize KPI Cards

To customize the KPI Card interface:

* Select the KPI Card to edit

* Open the **Properties** panel on the right

* Select **KPI options**

* Customize information such as font size, title, value format, trend display, color, layout, and more.

To rename a visual, **double-click the Card title** and enter a new name. Click **Save** to save the changes.

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-018.png)

Repeat the same process to create the following KPI Cards:

#### KPI 1: TOTAL REVENUE

Create the Total Revenue KPI Card with the following configuration:

* Visual type: **KPI**

* Value: **sum(total_revenue)**

* Trend group: **transaction_date**

* Format: **Currency**

* Title: **TOTAL REVENUE**

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-019.png)

#### KPI 2: TOTAL ORDERS

Create the Total Orders KPI Card with the following configuration:

* Value: **sum(total_orders)**

* Trend group: **transaction_date**

* Format: **Number**

* Title: **TOTAL ORDERS**

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-020.png)

#### KPI 3: AVG ORDER VALUE

Create the Avg Order Value KPI Card with the following configuration:

* Value: **avg(avg_order_value)**

* Trend group: **transaction_date**

* Format: **Currency**

* Title: **AVG ORDER VALUE**

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-021.png)

#### KPI 4: REFUND RATE

Create the Refund Rate KPI Card with the following configuration:

* Value: **avg(refund_rate)**

* Trend group: **transaction_date**

* Format: **Percent**

* Title: **REFUND RATE**

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-022.png)

#### I. CREATE REVENUE TREND LINE CHART

This visual is used to monitor revenue trends over time.

Click **Add** to create a new visual and select **Line chart**.

Configuration:

Create the Revenue Trend chart with the following configuration:

* X-axis: **transaction_date**

* Value: **total_revenue(Sum)**

* Title: **REVENUE TREND**

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-023.png)

**This chart helps answer:**

* Is revenue increasing or decreasing?

* Is there any seasonality by month or quarter?

* Which quarter has the highest revenue?

* Are there any days or months when revenue dropped abnormally?

#### II. CREATE ORDERS TREND BAR CHART

This visual is used to monitor the number of orders over time.

Create the Orders Trend chart with the following configuration:

* Visual type: **Bar chart**

* X-axis: **transaction_date**

* Value: **total_orders(Sum)**

* Title: **ORDERS TREND**

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-024.png)

**This chart helps answer:**

* Is order volume increasing?

* Does the number of orders follow the same trend as revenue?

* Which period shows a clear increase or decrease in order volume?

#### III. CREATE ORDERS TREND CLUSTERED BAR COMBO CHART

A combo chart helps compare the number of orders and revenue over time at the same time.

Create the Orders Trend chart with the following configuration:

* Visual type: **Clustered bar combo chart**

* X-axis: **transaction_date**

* Value: **total_orders(Sum)**

* Title: **ORDERS TREND**

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-025.png)

**This chart helps check:**

* Is revenue increasing because the number of orders is increasing or because the order value is increasing?

* Are there any periods where orders increase but revenue does not increase accordingly?

* Is the business growing by volume or by order value?

#### IV. CREATE REFUND RATE TREND LINE CHART

This visual is used to monitor the refund rate over time.

Create the Refund Rate Trend chart with the following configuration:

* Visual type: **Line chart**

* X-axis: **transaction_date**

* Value: **refund_rate(Average)**

* Title: **REFUND RATE TREND**

![](/images/4-Workshop/4.12-Dashboard-1-Executive-Overview/image-026.png)

This chart shows how the refund rate changes over time.

If the refund rate increases after a specific period, the cause may be related to:

* Product quality

* Customer expectation mismatch

* Shipping issues

* Sales campaigns targeting the wrong audience

* A specific category or brand having problems

This dashboard helps viewers quickly evaluate the overall status of the ecommerce business, including revenue, number of orders, average order value, and refund rate.

#### VIII. Completed dashboard filtered by April 2023

<iframe 
  src="/files/Dashboard_1.pdf" 
  width="100%" 
  height="700px"
  style="border: 1px solid #ccc;">
</iframe>

Or download the file here: [Download PDF](/files/Dashboard_1.pdf)
