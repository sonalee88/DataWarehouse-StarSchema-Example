# Data Warehousing Example with Star Schema

## Table of Contents
- [Introduction](#introduction)
- [Schema Design](#schema-design)
- [Python Code Explanation](#python-code-explanation)
  - [Library Imports](#library-imports)
  - [SQLite Database Creation](#sqlite-database-creation)
  - [Data Generation](#data-generation)
  - [Data Insertion](#data-insertion)
  - [Data Querying](#data-querying)
- [How to Run](#how-to-run)
- [Contact](#contact)

## Introduction
This repository contains an example of data warehousing using a star schema model. The implementation includes creating a SQLite database, populating it with sample data, and executing queries to retrieve meaningful insights. This project demonstrates the principles of data warehousing, schema design, and data manipulation using Python and SQLite.

## Schema Design
### Star Schema Design

**Fact Table:**
- **FactOrder:**
  - `OrderID` (Primary Key)
  - `CustomerID` (Foreign Key to DimCustomer)
  - `ProductID` (Foreign Key to DimProduct)
  - `VariantID` (Foreign Key to DimVariant)
  - `OrderDateID` (Foreign Key to DimDate)
  - `Quantity`
  - `Price`

**Dimension Tables:**
- **DimCustomer:**
  - `CustomerID` (Primary Key)
  - `Name`
  - `ContactNumber`
  - `ShippingAddress`
  - `Email`

- **DimProduct:**
  - `ProductID` (Primary Key)
  - `ProductName`
  - `Category`
  - `Description`

- **DimVariant:**
  - `VariantID` (Primary Key)
  - `ProductID` (Foreign Key to DimProduct)
  - `VariantName`
  - `LaunchDate`
  - `DiscontinueDate`

- **DimDate:**
  - `DateID` (Primary Key)
  - `Date`
  - `Year`
  - `Month`
  - `Day`

## Python Code Explanation
### Library Imports
The necessary libraries are imported, including `pandas` for data manipulation, `Faker` for generating fake data, and `sqlite3` for database operations.

```python
import pandas as pd
from faker import Faker
import random
import sqlite3
from datetime import datetime, timedelta



```
##SQLite Database Creation
An in-memory SQLite database is created, and the schema is defined using SQL commands. Tables for customers, products, variants, dates, and orders are set up.

