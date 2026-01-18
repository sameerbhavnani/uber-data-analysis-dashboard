# Uber Data Analysis Dashboard
This project presents an interactive Uber Data Analysis Dashboard developed using Microsoft Power BI, designed to uncover key insights from ride-sharing data. The dashboard focuses on understanding operational performance, demand patterns, and revenue trends to support data-driven decision-making.

## Key Features

Analysis of ride demand across time periods and locations

Trip distribution and usage trends

Revenue and performance KPIs

Interactive filters and drill-down capabilities

Clean and intuitive dashboard design for business insights

## Tools & Technologies

Microsoft Power BI

Data modeling and DAX measures

Interactive visual analytics

## Objective

The goal of this project is to demonstrate how business intelligence tools can be used to transform raw ride data into actionable insights, helping stakeholders optimize operations, improve customer experience, and identify growth opportunities.

```python
# Extracting specific numbers for detailed insights

# 1. Ride Status Counts
status_counts = df['Booking Status'].value_counts()

# 2. Vehicle Type Popularity (Counts)
vehicle_counts = df['Vehicle Type'].value_counts()

# 3. Monthly Trends
monthly_rides = df.groupby(['Month_Num', 'Month']).size().reset_index(name='Counts').sort_values('Month_Num')
peak_month = monthly_rides.loc[monthly_rides['Counts'].idxmax()]
low_month = monthly_rides.loc[monthly_rides['Counts'].idxmin()]

# 4. Revenue by Vehicle Type (Completed only)
revenue_by_vehicle = df[df['Booking Status'] == 'Completed'].groupby('Vehicle Type')['Booking Value'].sum().sort_values(ascending=False)

# 5. Customer Cancellation Reasons (Percentages)
cancel_reasons = df['Reason for cancelling by Customer'].value_counts()
cancel_total = cancel_reasons.sum()
cancel_percents = (cancel_reasons / cancel_total * 100).round(2)

print("--- Status Counts ---")
print(status_counts)
print("\n--- Vehicle Counts ---")
print(vehicle_counts)
print("\n--- Monthly Peak ---")
print(peak_month)
print("\n--- Revenue ---")
print(revenue_by_vehicle)
print("\n--- Cancellation Reasons (%) ---")
print(cancel_percents)



```

```text
--- Status Counts ---
Booking Status
Completed                93000
Cancelled by Driver      27000
No Driver Found          10500
Cancelled by Customer    10500
Incomplete                9000
Name: count, dtype: int64

--- Vehicle Counts ---
Vehicle Type
Auto             37419
Go Mini          29806
Go Sedan         27141
Bike             22517
Premier Sedan    18111
eBike            10557
Uber XL           4449
Name: count, dtype: int64

--- Monthly Peak ---
Month_Num        7
Month          Jul
Counts       12897
Name: 6, dtype: object

--- Revenue ---
Vehicle Type
Auto             11727615.0
Go Mini           9411418.0
Go Sedan          8538560.0
Bike              7144913.0
Premier Sedan     5733655.0
eBike             3298157.0
Uber XL           1406256.0
Name: Booking Value, dtype: float64

--- Cancellation Reasons (%) ---
Reason for cancelling by Customer
Wrong Address                                   22.50
Change of plans                                 22.41
Driver is not moving towards pickup location    22.24
Driver asked to cancel                          21.86
AC is not working                               11.00
Name: count, dtype: float64


```

### **Detailed Insights from the Uber Analytics**

* **Ride Success & Reliability (Ride Status Distribution)**
Out of the **150,000** total ride requests, **93,000** were successfully completed, representing a **62% fulfillment rate**. However, the data highlights a significant supply gap, with **27,000** rides cancelled by drivers and **10,500** requests failing because "No Driver Found." This indicates that approximately **25%** of potential rides are lost due to driver-side cancellations or lack of availability, pointing to a need for better driver retention or higher incentives during peak hours.
* **Dominance of Low-Cost Transit (Vehicle Type Popularity)**
The **Auto** category is the most popular choice for commuters in NCR, accounting for **37,419** bookings, followed by **Go Mini** with **29,806** bookings. Together, these two vehicle types represent nearly **45%** of all booking requests. The preference for Autos and Mini cars suggests that users in the region prioritize affordability and the ability to navigate through heavy traffic over luxury or larger vehicle capacities like the **Uber XL**, which saw only **4,449** bookings.
* **Peak Demand Trends (Monthly Ride Bookings)**
Ride demand showed a steady fluctuation throughout the year, reaching its absolute peak in **July** with **12,897** bookings. This surge may be attributed to seasonal factors such as the monsoon season in NCR, where commuters often shift from walking or public transport to ride-hailing services for door-to-door comfort. Conversely, demand was relatively lower in other months, suggesting that marketing campaigns should be intensified during off-peak periods to maintain steady ride volumes.
* **Revenue Contribution (Revenue by Vehicle Type)**
Despite being a lower-cost option per kilometer, the **Auto** category generated the highest total revenue for the period, contributing **₹11,727,615** (roughly 22.6% of total revenue). This is followed by **Go Mini** at **₹9,411,418**. This highlights a "volume-over-value" strategy where the sheer number of short, affordable trips significantly outweighs the revenue generated by premium services like **Premier Sedan** (**₹5.73M**) or **Uber XL** (**₹1.4M**).
* **Customer Friction Points (Cancellation Reasons)**
A deep dive into customer cancellations reveals that **"Wrong Address" (22.5%)** and **"Change of Plans" (22.4%)** are the leading causes, closely followed by frustration with the driver's progress, as **22.2%** of customers cancelled because the **"Driver is not moving towards pickup location."** Interestingly, nearly **21.9%** of customers cancelled because the **"Driver asked to cancel,"** suggesting that some drivers may be avoiding certain routes or payment methods, which negatively impacts the user experience.
