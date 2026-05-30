---

title: "4.13. Dashboard 2: Funnel Analytics"
linkTitle: "4.13. Dashboard 2: Funnel Analytics"
menuTitle: "4.13. Dashboard 2: Funnel Analytics"
date: 2026-05-29
weight: 530
chapter: false
--------------

The **Funnel Analytics Dashboard** is used to track the customer purchase journey from product views to successful purchases.

**This dashboard helps answer the following questions:**

* At which step do users drop off the most in the funnel?

* How do views, clicks, add-to-carts, and purchases change over time?

* Does the conversion rate decrease at any stage?

* Which source/device has the best conversion?

* Which source/device has a high bounce rate?

**Views used:**

* vw_daily_event_funnel

* vw_funnel_summary

* vw_daily_funnel_by_source_device

### I. CREATE TIME FILTERS

Because the dashboard uses views that contain the `event_date` column, calculated fields need to be created to filter by year, quarter, and month. In each dataset used for the dashboard, create the following calculated fields.

* **event_year**: `extract('YYYY', {event_date})`

![](/images/4-Workshop/4.13-Dashboard-2-Funnel-Analytics/image-001.png)

* **event_quarter**: `floor((extract('MM', {event_date}) - 1) / 3) + 1`

* **event_month**: `extract('MM', {event_date})`

For **event_quarter** and **event_month**, enable **Show relevant values only** so that the filters work as a hierarchy: Year → Quarter → Month.

Then create filter controls for:

* event_year

* event_quarter

* event_month

The steps above are performed in the same way as **Create calculated fields for time filters** and **Create filter controls**.

### II. KPI CARDS

#### 1. KPI 1: TOTAL EVENTS

* View: **vw_daily_event_funnel**

* Visual type: **KPI**

* Value: **total_events(Sum)**

* Title: **TOTAL EVENTS**

![](/images/4-Workshop/4.13-Dashboard-2-Funnel-Analytics/image-002.png)

**Insight:** Shows the total number of events across the entire funnel.

#### 2. KPI 2: TOTAL VIEWS

* View: **vw_daily_event_funnel**

* Visual type: **KPI**

* Value: **views(Sum)**

* Title: **TOTAL VIEWS**

![](/images/4-Workshop/4.13-Dashboard-2-Funnel-Analytics/image-003.png)

**Insight:** Shows the total number of product views.

#### 3. KPI 3: TOTAL CLICKS

* View: **vw_daily_event_funnel**

* Visual type: **KPI**

* Value: **clicks(Sum)**

* Title: **TOTAL CLICKS**

![](/images/4-Workshop/4.13-Dashboard-2-Funnel-Analytics/image-004.png)

**Insight:** Shows the level of interaction after users view products.

#### 4. KPI 4: TOTAL ADD TO CARTS

* View: **vw_daily_event_funnel**

* Visual type: **KPI**

* Value: **add_to_carts(Sum)**

* Title: **TOTAL ADD TO CARTS**

![](/images/4-Workshop/4.13-Dashboard-2-Funnel-Analytics/image-005.png)

**Insight:** Shows the total number of add-to-cart actions.

#### 5. KPI 5: TOTAL PURCHASES

* View: **vw_daily_event_funnel**

* Visual type: **KPI**

* Value: **purchases(Sum)**

* Title: **TOTAL PURCHASES**

![](/images/4-Workshop/4.13-Dashboard-2-Funnel-Analytics/image-006.png)

**Insight:** Shows the total number of successful purchases in the event funnel.

#### 6. KPI 6: BOUNCE RATE

* View: **vw_daily_event_funnel**

* Visual type: **KPI**

* Value: **bounce_rate(Average)**

* Format: **Percentage**

* Title: **BOUNCE RATE**

![](/images/4-Workshop/4.13-Dashboard-2-Funnel-Analytics/image-007.png)

**Insight:** Shows the overall quality of traffic. The higher the bounce rate, the more it is necessary to review the traffic source or landing page.

#### I. CREATE CONVERSION FUNNEL CHART

Create the Conversion Funnel chart with the following configuration.

This visual is used to show the overall number of events at each funnel stage.

Configuration:

* View: **vw_funnel_summary**

* Visual type: **Funnel chart**

* Category: **funnel_stage**

* Value: **funnel_count(Sum)**

* Sort: funnel_stage **Descending**

* Title: **CONVERSION FUNNEL**

![](/images/4-Workshop/4.13-Dashboard-2-Funnel-Analytics/image-008.png)

**Insight:** This chart shows where customers drop off in the journey: **Views → Clicks → Add to Cart → Purchases**.

If Views are high but Clicks are low, the displayed content, banner, or product may not be attractive enough. If Add to Cart is high but Purchases are low, the issue may be related to checkout, shipping fees, or payment methods.

#### II. CREATE DAILY FUNNEL VOLUME TREND LINE CHART

Create the Daily Funnel Volume Trend chart with the following configuration.

This visual is used to track the volume of each funnel step by day.

Configuration:

* View: **vw_daily_event_funnel**

* Visual type: **Line chart**

* X-axis: **event_date**

* Value:

  * **views(Sum)**

  * **clicks(Sum)**

  * **add_to_carts(Sum)**

  * **purchases(Sum)**

* Title: **DAILY FUNNEL VOLUME TREND**

![](/images/4-Workshop/4.13-Dashboard-2-Funnel-Analytics/image-009.png)

This chart shows how the number of events at each funnel step changes over time. It can be used to detect days when traffic increases or decreases, days when purchases increase abnormally, or whether the funnel steps increase or decrease together.

#### III. CREATE FUNNEL CONVERSION RATE TREND LINE CHART

Create the Funnel Conversion Rate Trend chart with the following configuration.

This visual is used to track the conversion rate between funnel steps.

Configuration:

* View: **vw_daily_event_funnel**

* Visual type: **Line chart**

* X-axis: **event_date**

* Value:

  * **view_to_click_rate(Average)**

  * **click_to_cart_rate(Average)**

  * **cart_to_purchase_rate(Average)**

  * **view_to_purchase_rate(Average)**

* Format: **Percentage**

* Title: **FUNNEL CONVERSION RATE TREND**

![](/images/4-Workshop/4.13-Dashboard-2-Funnel-Analytics/image-010.png)

**Insight:** This chart helps identify which funnel step has a low conversion rate or drops sharply over time.

**Meaning of each metric:**

* **View to Click Rate**: Shows whether users click after viewing. If it is low, the content or product may not be attractive enough.

* **Click to Cart Rate**: Shows whether users add products to cart after clicking. If it is low, the product page, price, description, or CTA may not be convincing enough.

* **Cart to Purchase Rate**: Shows whether users complete the purchase after adding items to cart. If it is low, the issue may be related to checkout, shipping fees, or payment methods.

* **View to Purchase Rate**: The overall conversion rate from view to purchase. This is an important metric for evaluating the effectiveness of the entire funnel.

#### IV. CREATE PURCHASES BY SOURCE AND DEVICE STACKED BAR CHART

Create the Purchases by Source and Device chart with the following configuration.

This visual is used to see which traffic sources and devices generate purchases.

Configuration:

* View: **vw_daily_funnel_by_source_device**

* Visual type: **Stacked bar chart**

* X-axis: **traffic_source**

* Value: **purchases(Sum)**

* Group/Color: **device_type**

* Sort: purchases **Descending**

* Title: **PURCHASES BY SOURCE AND DEVICE**

![](/images/4-Workshop/4.13-Dashboard-2-Funnel-Analytics/image-011.png)

**Insight:** This chart shows which traffic sources and devices generate purchases. By looking at the chart, you can identify which channel generates the most orders and whether purchases mainly come from mobile, desktop, or tablet.

#### V. CREATE CONVERSION RATE BY SOURCE AND DEVICE HEAT MAP

Create the Conversion Rate by Source and Device chart with the following configuration.

This visual is used to compare conversion rates by traffic source and device.

Configuration:

* View: **vw_daily_funnel_by_source_device**

* Visual type: **Heat map**

* Rows: **traffic_source**

* Columns: **device_type**

* Value: **conversion_rate(Average)**

* Format: **Percentage**

* Title: **CONVERSION RATE BY SOURCE AND DEVICE**

![](/images/4-Workshop/4.13-Dashboard-2-Funnel-Analytics/image-012.png)

**Insight:** This chart shows which source/device combination converts best, for example:

* Email + Desktop

* Social + Mobile

* Organic + Tablet

If a combination has a high conversion rate, marketing optimization or budget allocation can be prioritized for that combination.

#### VI. CREATE BOUNCE RATE BY SOURCE AND DEVICE HEAT MAP

Create the Bounce Rate by Source and Device chart with the following configuration.

This visual is used to detect low-quality traffic by source and device.

Configuration:

* View: **vw_daily_funnel_by_source_device**

* Visual type: **Heat map**

* Rows: **traffic_source**

* Columns: **device_type**

* Value: **bounce_rate(Average)**

* Format: **Percentage**

* Title: **BOUNCE RATE BY SOURCE AND DEVICE**

![](/images/4-Workshop/4.13-Dashboard-2-Funnel-Analytics/image-013.png)

This chart helps detect which source/device combination has a high bounce rate. For example, if Social + Mobile has a high bounce rate, social traffic may not be targeting the right audience, or the landing page on mobile may load slowly, causing users to leave quickly.

### IX. FUNNEL ANALYTICS DASHBOARD AFTER FILTERING BY APRIL 2023

<iframe 
  src="/files/Dashboard_2.pdf" 
  width="100%" 
  height="700px"
  style="border: 1px solid #ccc;">
</iframe>

Or download the file here: [Download PDF](/files/Dashboard_2.pdf)
