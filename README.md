# OLA Ride Performance Analytics
![Ola_logo](http://github.com/akashpanchale24-hub/OLA-Ride-Performance-Analytics/blob/main/pngegg.png)

## Overview
This project analyzes ride booking data from OLA to understand business performance, ride trends, customer behavior, and revenue generation.
The objective is to transform raw ride data into meaningful business insights using SQL and Power BI.

## Objectives
- Analyze total bookings and total revenue
- Identify ride cancellation patterns
- Track ride completion rate
- Monitor average ride distance
- Evaluate customer and driver ratings
- Identify peak booking hours

### Dataset Description
1. Date
2. Time
3. Booking_ID
4. Booking_Status
5. Customer_ID
6. Vehicle_Type
7. Pickup_Location
8. Drop_Location
9. V_TAT
10. C_TAT
11. cancelled_Rides_by_Customer
12. cancelled_Rides_by_Driver
13. Incomplete_Rides
14. Incomplete_Rides_Reason
15. Booking_Value
16. Payment_Method
17. Ride_Distance
18. Driver_Ratings
19. Customer_Rating

## Business Problems and Solutions

### 1. Retrieve all successful bookings:
```sql
Create View Successful_Bookings As
SELECT * FROM bookings
WHERE Booking_Status = 'Success';
```
### 2. Find the average ride distance for each vehicle type:
```sql
Create View ride_distance_for_each_vehicle As
SELECT Vehicle_Type, AVG(Ride_Distance) as avg_distance 
FROM bookings
GROUP BY Vehicle_Type;
```
### 3.  Get the total number of cancelled rides by customers:
```sql
Create View cancelled_rides_by_customers As
SELECT COUNT(*) FROM bookings
WHERE Booking_Status = 'cancelled by Customer'
```
### 4.  List the top 5 customers who booked the highest number of rides:
```sql
Create View Top_5_Customers As
SELECT Customer_ID, COUNT(Booking_ID) as total_rides
FROM bookings
GROUP BY Customer_ID
ORDER BY total_rides DESC LIMIT 5;
```
### 5. Get the number of rides cancelled by drivers due to personal and car-related issues:
```sql
Create View Rides_cancelled_by_Drivers_P_C_Issues As
SELECT COUNT(*) FROM bookings
WHERE cancelled_Rides_by_Driver = 'Personal & Car related issue';;
```
### 6. Find the maximum and minimum driver ratings for Prime Sedan bookings:
```sql
Create View Max_Min_Driver_Rating As
SELECT MAX(Driver_Ratings) as max_rating,
MIN(Driver_Ratings) as min_rating
FROM bookings WHERE Vehicle_Type = 'Prime Sedan'
```
### 7. Retrieve all rides where payment was made using UPI:
```sql
Create View UPI_Payment As
SELECT * FROM bookings
WHERE Payment_Method = 'UPI';
```
### 8. Find the average customer rating per vehicle type:
```sql
Create View AVG_Cust_Rating As
SELECT Vehicle_Type, AVG(Customer_Rating) as avg_customer_rating
FROM bookings
GROUP BY Vehicle_Type;
```
### 9. Calculate the total booking value of rides completed successfully:
```sql
Create View total_successful_ride_value As
SELECT SUM(Booking_Value) as total_successful_ride_value
FROM bookings
WHERE Booking_Status = 'Success';
```
### 10. List all incomplete rides along with the reason
```sql
Create View Incomplete_Rides_Reason As
SELECT Booking_ID, Incomplete_Rides_Reason
FROM bookings
WHERE Incomplete_Rides = 'Yes';
```
## Dashboard Features
  1️.Overall Performance
- Ride Volume Over Time (Time Series)
- Booking Status Breakdown
- Interactive Date Slicer
- Dynamic KPI Cards

  2️. Revenue Analysis
- Revenue by Payment Method
- Top 5 Customers by Booking Value
- Daily Ride Distance Distribution

  3️. Vehicle Performance
- Top 5 Vehicle Types by Ride Distance
- Average Ride Distance per Vehicle Type

  4️.Cancellation Analysis
- Customer Cancellation Rate
- Driver Cancellation Rate
- Cancellation Reasons Breakdown

  5️.Ratings Analysis
- Driver Ratings Distribution
- Customer Ratings Distribution
- Customer vs Driver Rating Comparison

## Dashboard Preview
![OLA Dashboard](https://github.com/akashpanchale24-hub/OLA-Ride-Performance-Analytics/blob/main/ola_dashboard_1.PNG)
![OLA Dashboard]()
