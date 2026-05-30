---

title: "4.16. Dashboard 5: A/B Testing"
linkTitle: "4.16. Dashboard 5: A/B Testing"
menuTitle: "4.16. Dashboard 5: A/B Testing"
date: 2026-05-29
weight: 560
chapter: false
--------------

The **A/B Testing** dashboard is used to compare the performance of experiment groups, such as Group A and Group B.

**This dashboard helps answer the following questions:**

* Which experiment group has a higher conversion rate?

* Which group has a better add-to-cart rate?

* Which group has a lower bounce rate?

* Which group has a higher session duration?

* Is the difference between groups stable over time?

View used: **vw_ab_testing_summary**

### I. CREATE TIME FILTERS

Create **calculated fields** from **event_date**:

* **event_year** = `extract('YYYY', {event_date})`

* **event_quarter** = `floor((extract('MM', {event_date}) - 1) / 3) + 1`

* **event_month** = `extract('MM', {event_date})`

Then create **filter controls** for Year, Quarter, and Month.

### II. CREATE KPI CARDS

#### KPI 1: TOTAL EVENTS

Create the Total Events KPI Card with the following configuration:

* View: **vw_ab_testing_summary**
* Visual type: **KPI**
* Value: **total_events(Sum)**
* Title: **TOTAL EVENTS**

![](/images/4-Workshop/4.16-Dashboard-5-AB-Testing/image-001.png)

**Insight**:

Shows the total number of events recorded in the A/B test. This metric helps evaluate the data scale and whether the sample size is large enough before comparing performance between experiment groups.

#### KPI 2: TOTAL VIEWS

Create the Total Views KPI Card with the following configuration:

* View: **vw_ab_testing_summary**
* Visual type: **KPI**
* Value: **views(Sum)**
* Title: **TOTAL VIEWS**

![](/images/4-Workshop/4.16-Dashboard-5-AB-Testing/image-002.png)

**Insight**:

Shows the total input sample size of the A/B test. If the number of views is too low, it is not recommended to conclude which group performs better.

#### KPI 3: TOTAL PURCHASES

Create the Total Purchases KPI Card with the following configuration:

* View: **vw_ab_testing_summary**
* Visual type: **KPI**
* Value: **purchases(Sum)**
* Title: **TOTAL PURCHASES**

![](/images/4-Workshop/4.16-Dashboard-5-AB-Testing/image-003.png)

**Insight**:

Shows the total number of purchases in the A/B test. This is the most important business outcome metric.

#### KPI 4: CONVERSION RATE

Create the Conversion Rate KPI Card with the following configuration:

* View: **vw_ab_testing_summary**
* Visual type: **KPI**
* Value: **conversion_rate(Average)**
* Format: **Percentage**
* Title: **CONVERSION RATE**

![](/images/4-Workshop/4.16-Dashboard-5-AB-Testing/image-004.png)

**Insight**:

Shows the average conversion rate. This is the main metric used to evaluate which group performs better.

#### KPI 5: ADD TO CART RATE

Create the Add to Cart Rate KPI Card with the following configuration:

* View: **vw_ab_testing_summary**
* Visual type: **KPI**
* Value: **add_to_cart_rate(Average)**
* Format: **Percentage**
* Title: **ADD TO CART RATE**

![](/images/4-Workshop/4.16-Dashboard-5-AB-Testing/image-005.png)

**Insight**:

Shows which group creates stronger purchase intent among users.

#### KPI 6: BOUNCE RATE

Create the Bounce Rate KPI Card with the following configuration:

* View: **vw_ab_testing_summary**
* Visual type: **KPI**
* Value: **bounce_rate(Average)**
* Format: **Percentage**
* Title: **BOUNCE RATE**

![](/images/4-Workshop/4.16-Dashboard-5-AB-Testing/image-006.png)

**Insight**:

Shows which group retains users better. A better-performing group usually has a lower bounce rate.

#### I. CREATE EXPERIMENT FUNNEL VOLUME BY GROUP BAR CHART

Create the Experiment Funnel Volume by Group chart with the following configuration:

* View: **vw_ab_testing_summary**
* Visual type: **Bar chart**
* X-axis: **experiment_group**
* Value:

  * **views(Sum)**
  * **clicks(Sum)**
  * **add_to_carts(Sum)**
  * **purchases(Sum)**
* Title: **EXPERIMENT FUNNEL VOLUME BY GROUP**

![](/images/4-Workshop/4.16-Dashboard-5-AB-Testing/image-007.png)

**Insight**:

Shows the volume of each group at every funnel step. If Group B has a similar number of views as Group A but higher purchases, Group B may be more effective.

#### II. CREATE EXPERIMENT RATE COMPARISON BAR CHART

Create the Experiment Rate Comparison chart with the following configuration:

* View: **vw_ab_testing_summary**
* Visual type: **Bar chart**
* X-axis: **experiment_group**
* Value:

  * **conversion_rate(Average)**
  * **add_to_cart_rate(Average)**
  * **bounce_rate(Average)**
* Format: **Percentage**
* Title: **EXPERIMENT RATE COMPARISON**

![](/images/4-Workshop/4.16-Dashboard-5-AB-Testing/image-008.png)

**Insight**:

This is the most important chart in the dashboard. It shows which group has:

* higher conversion_rate
* higher add_to_cart_rate
* lower bounce_rate

If a group has a high conversion rate but also a high bounce rate, it needs to be reviewed because the result may not be stable.

#### III. CREATE CONVERSION RATE TREND BY EXPERIMENT GROUP LINE CHART

Create the Conversion Rate Trend by Experiment Group chart with the following configuration:

* View: **vw_ab_testing_summary**
* Visual type: **Line chart**
* X-axis: **event_date**
* Value: **conversion_rate(Average)**
* Color/Group: **experiment_group**
* Format: **Percentage**
* Title: **CONVERSION RATE TREND BY EXPERIMENT GROUP**

![](/images/4-Workshop/4.16-Dashboard-5-AB-Testing/image-009.png)

**Insight**:

Shows whether the A/B test result is stable over time. If one group consistently performs higher over multiple days, the result is more reliable than if it only performs higher on a single day.

#### IV. CREATE PURCHASE AND CONVERSION TREND BY EXPERIMENT GROUP BAR CHART

Create the Purchase and Conversion Trend by Experiment Group chart with the following configuration:

* View: **vw_ab_testing_summary**
* Visual type: **Bar chart**
* X-axis: **event_date**
* Value: **purchases(Sum)**
* Group/Color: **experiment_group**
* Title: **PURCHASE AND CONVERSION TREND BY EXPERIMENT GROUP**

![](/images/4-Workshop/4.16-Dashboard-5-AB-Testing/image-010.png)

**Insight**:

This chart shows how the number of purchases for each experiment group changes over time. It helps identify which group generates more purchases and whether the result is stable across multiple days or only spikes during a short period. If one experiment group consistently has higher purchases, that group may deliver better business performance. On the other hand, if purchases fluctuate strongly or increase only on a few days, conversion rate, traffic volume, and sample size should be checked before concluding which group performs best.

#### V. CREATE A/B TESTING PERFORMANCE DETAIL PIVOT TABLE

Create the A/B Testing Performance Detail table with the following configuration:

* View: **vw_ab_testing_summary**
* Visual type: **Pivot table**
* Rows: **event_date**
* Columns: **experiment_group**
* Values:

  * **views(Sum)**
  * **clicks(Sum)**
  * **add_to_carts(Sum)**
  * **purchases(Sum)**
  * **conversion_rate(Average)**
  * **add_to_cart_rate(Average)**
  * **bounce_rate(Average)**
* Format:

  * **conversion_rate: Percentage**
  * **add_to_cart_rate: Percentage**
  * **bounce_rate: Percentage**
* Title: **A/B TESTING PERFORMANCE DETAIL**

![](/images/4-Workshop/4.16-Dashboard-5-AB-Testing/image-011.png)

**Insight**:

This table is used to check details by day and experiment group. When the charts above show an abnormal point, the table helps identify which date or group caused the change.

#### VIII. Completed dashboard filtered by 2023

{{< pdf src="/files/Dashboard_5.pdf" >}}

Or download the file here: [Download PDF](/files/Dashboard_5.pdf)
