# Movie Rental Data Warehouse Design

## Project Overview

This project presents a high-level Data Warehouse design for an OLTP Movie Rental System.

The original OLTP system is used for daily operational activities such as registering customers, managing films, storing inventory, recording rentals, processing payments, managing staff, and maintaining store and location information.

However, the OLTP system is not optimized for analytical reporting. Therefore, this project proposes a dimensional data warehouse model that supports business analysis and decision-making.

## Assignment Objective

The objective of this assignment is to transform the operational movie rental schema into a high-level dimensional model suitable for reporting and analysis.

The data warehouse is designed to help business managers analyze:

- Rental activity
- Revenue performance
- Film popularity
- Customer behavior
- Store performance
- Staff performance
- Location-based trends
- Time-based trends
- Inventory usage

## Data Warehouse Approach

This project uses a hybrid star schema design.

Most fact tables are directly connected to dimension tables, similar to a star schema. However, bridge tables are used to handle many-to-many relationships such as:

- Film and Category
- Film and Actor

## Main Business Processes

The main business processes identified from the OLTP system are:

1. Film rental transactions
2. Payment transactions
3. Inventory availability tracking

## Main Fact Tables

The proposed data warehouse contains the following fact tables:

### Fact_Rental

Stores rental transaction information.

Grain:

One row per rental transaction.

Main measures:

- Rental count
- Rental duration
- Late return flag
- Late days
- Open rental flag

### Fact_Payment

Stores payment and revenue transaction information.

Grain:

One row per payment transaction.

Main measures:

- Payment amount
- Payment count
- Revenue amount

### Fact_Inventory_Snapshot

Stores inventory availability information by film, store, and date.

Grain:

One row per film per store per date.

Main measures:

- Total copies
- Rented copies
- Available copies
- Inventory utilization rate

## Main Dimension Tables

The proposed dimension tables are:

- Dim_Date
- Dim_Customer
- Dim_Film
- Dim_Category
- Dim_Actor
- Dim_Store
- Dim_Staff
- Dim_Language
- Dim_Location

## ETL Process

The ETL process is divided into three main stages:

### Extract

Data is extracted from the OLTP source tables such as:

- rental
- payment
- customer
- film
- inventory
- store
- staff
- address
- city
- country
- category
- film_category
- actor
- film_actor
- language

### Transform

The transformation stage includes:

- Joining related OLTP tables
- Creating meaningful dimension tables
- Combining first name and last name into full name
- Creating surrogate keys
- Creating date keys
- Calculating rental duration
- Calculating revenue
- Detecting late returns
- Handling missing values
- Standardizing text values
- Handling many-to-many relationships

### Load

The loading stage inserts the transformed data into the data warehouse.

Dimension tables are loaded first, followed by bridge tables and fact tables.

Recommended loading order:

1. Dim_Date
2. Dim_Customer
3. Dim_Film
4. Dim_Category
5. Dim_Actor
6. Dim_Store
7. Dim_Staff
8. Bridge_Film_Category
9. Bridge_Film_Actor
10. Fact_Rental
11. Fact_Payment
12. Fact_Inventory_Snapshot

## Repository Structure

```text
movie-rental-data-warehouse/
│
├── README.md
│
├── report/
│   └── Movie_Rental_Data_Warehouse_Report.pdf
│
├── diagrams/
│   └── dimensional_model.png
│
├── sql/
│   ├── create_tables.sql
│   └── sample_queries.sql
│
└── docs/
    └── data_quality_rules.md
