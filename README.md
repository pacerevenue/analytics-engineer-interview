# Pace Data Challenge
Welcome to the Pace Data Challenge. This exercise is designed to bring you closer to the type of data we interact with at Pace as well as putting your SQL skills to the test. 
In this exercise you will be required to: 

- Solve two individual SQL problems using BigQuery.
- Build out a data visualisation using the dataset from the second SQL problem (using Looker).

### IMPORTANT 
There are a total of 3 different exercises in this document. All 3 of these exercises will be completed during a live pair-programming session (1.5hr) with our Data/Analytics Engineers. Please feel free to explore the data we have provided as well as get familiar with the expected output of the final data visualisation exercise, but this is not a requirement. We will outline the expectations of the challenge during the pair programming session. First and foremost this data challenge is there to help us understand your approach to data. It should hopefully be fun and also give you a small insight into what type of data you will be dealing with! 

# Pair Programming Process
During the pair programming session we will give you access to Looker, specifically to use the SQL runner - a simple GUI that allows you to execute SQL queries against a dedicated BigQuery database.

In case you are new to Looker, here are some helpful resources to familiarise yourself with some key concepts & terminology: 
1. Understand the SQL Runner in Looker [here](https://cloud.google.com/looker/docs/sql-runner-basics).
2. Understand how to build visualizations and graphs [here](https://docs.looker.com/exploring-data/visualizing-query-results). 

In case you are new to BigQuery, please find some relevant documentation on the tooling [here](https://cloud.google.com/bigquery/docs). 

# Available tables in the data set

## Table for the reservations versions SQL challenge (exercise 1)

[reservations_history](https://github.com/pacerevenue/analytics-engineer-interview/blob/main/reservations_history.csv)

This table contains all versions of a booking which we ever received for the three demo properties with respect to the fields available in this table. 

## Tables for the reservation metrics SQL challenge (all remaining exercises)

[reservation_pickups](https://github.com/pacerevenue/analytics-engineer-interview/blob/main/reservation_pickups.csv.zip)

This table contains access to all booking data of three demo properties. The data is on a transactional level, i.e. for one `booking_id` you will find multiple rows. Additionally, this data set is already pre-transformed to deal with changes to reservations over time. E.g. when a booking is cancelled you will find the revenue and occupancy created (positive values) and deducted (negative values) - summing across these rows will yield the latest state of each reservation (ie 0 values for revenue and occupancy in this example).

[merchants](https://github.com/pacerevenue/analytics-engineer-interview/blob/main/merchants.csv) 

This table contains the information on the merchant (“merchant” is our terminology for Hotels/Hostels/Apartments). It can be joined to the reservations table by joining `merchant_id` on `id`. 

[hotelrooms](https://github.com/pacerevenue/analytics-engineer-interview/blob/main/hotelrooms.csv) 

This table contains the information on all hotel room types (name, how many of them etc). 

[rate_plans](https://github.com/pacerevenue/analytics-engineer-interview/blob/main/rate_plans.csv)

This table contains the information on all rate plans a reservation can be made on. Essentially, a rate plan describes what is included in your room booking and the corresponding cancellation policy (non-refundable vs flexible cancellation).

# Exercises 

## 1. Reservations Versions SQL challenge
Define a query that creates a view of the reservations_history table to provide you with the latest status received for each booking. To do so, utilise the `_version_received_at`, `status`, `external_id` and `property_id`.

## 2. Reservation Metrics SQL challenge
This challenge focuses on a collection of essential metrics that we calculate for our users. These metrics are a crucial part of our users everyday workflows, and are defined as the following:


- **Total net revenue:** The sum of the net revenue associated with each booking by consumption date. Be sure not sum up revenues across different currencies.
Test: The total net revenue on consumption date 01/01/2022 is 164,980 EUR across all properties.

- **Total units occupied:** The sum of occupancy per booking.
Test: The total units occupied on consumption date 01/01/2022 is 146 for Crown Hotel 1.

- **Average Daily Rate (ADR):** Total net revenue divided by total units occupied. Remember that we only want to calculate the ADR for confirmed bookings.
Test: The ADR on consumption date 01/01/2022 is 279 for Crown Apartments 3.

- **Lead time:** How many days before an actual consumption date was a booking created.

During the pair programming session, we will ask you to prepare a query to serve each of the above metrics by **consumption date**. We have provided some test cases to validate whether the query returns the expected output for the 01/01/2022.

## 3. Data Visualization 
During the pair programming session, we will ask you to build out the following data visualization in the SQL Runner feature of Looker.  

- Build out a revenue booking curve chart for the consumption date 31/12/2021. The revenue booking curve visualises at what point in time revenue was created for a particular night. It is displayed as a cumulative sum.

Tip: Make use of the lead time dimension and total units occupied metric you have calculated in the previous section.

An example of this visualisation can be found below.

![booking curve example](https://github.com/pacerevenue/analytics-engineer-interview/assets/62551475/20de0abe-5a77-49b5-b949-06fc8b6d6a1c)

