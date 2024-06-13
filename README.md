Data Warehousing Example with Star Schema

Table of Contents

Introduction
Schema Design
Python Code Explanation
Library Imports
SQLite Database Creation
Data Generation
Data Insertion
Data Querying
How to Run
Contact
Introduction
This repository contains an example of data warehousing using a star schema model. The implementation includes creating a SQLite database, populating it with sample data, and executing queries to retrieve meaningful insights. This project demonstrates the principles of data warehousing, schema design, and data manipulation using Python and SQLite.

Schema Design
Star Schema Design
Fact Table:

FactOrder:
OrderID (Primary Key)
CustomerID (Foreign Key to DimCustomer)
ProductID (Foreign Key to DimProduct)
VariantID (Foreign Key to DimVariant)
OrderDateID (Foreign Key to DimDate)
Quantity
Price
Dimension Tables:

DimCustomer:

CustomerID (Primary Key)
Name
ContactNumber
ShippingAddress
Email
DimProduct:

ProductID (Primary Key)
ProductName
Category
Description
DimVariant:

VariantID (Primary Key)
ProductID (Foreign Key to DimProduct)
VariantName
LaunchDate
DiscontinueDate
DimDate:

DateID (Primary Key)
Date
Year
Month
Day
Python Code Explanation
Library Imports
The necessary libraries are imported, including pandas for data manipulation, Faker for generating fake data, and sqlite3 for database operations.

python
Copy code
import pandas as pd
from faker import Faker
import random
import sqlite3
from datetime import datetime, timedelta
SQLite Database Creation
An in-memory SQLite database is created, and the schema is defined using SQL commands. Tables for customers, products, variants, dates, and orders are set up.

python
Copy code
# Initialize faker
fake = Faker()

# Create a SQLite database
conn = sqlite3.connect(':memory:')
cursor = conn.cursor()

# Create dimension tables
cursor.execute('CREATE TABLE DimCustomer ...')
cursor.execute('CREATE TABLE DimProduct ...')
cursor.execute('CREATE TABLE DimVariant ...')
cursor.execute('CREATE TABLE DimDate ...')
cursor.execute('CREATE TABLE FactOrder ...')
Data Generation
Sample data is generated using the Faker library for customers, products, and variants. Dates are generated programmatically, and orders are created using random values.

python
Copy code
# Generate sample data for DimCustomer
for _ in range(10):
    cursor.execute('INSERT INTO DimCustomer ...', (fake.name(), fake.phone_number(), fake.address(), fake.email()))

# Generate sample data for DimProduct
product_names = ['Laptop', 'Smartphone', 'Tablet', ...]
categories = ['Electronics', 'Peripherals', 'Accessories']
for name in product_names:
    cursor.execute('INSERT INTO DimProduct ...', (name, random.choice(categories), fake.text(max_nb_chars=100)))

# Generate sample data for DimVariant
variant_names = ['Basic', 'Pro', 'Advanced']
for product_id in range(1, 11):
    for name in variant_names:
        launch_date = fake.date_between(start_date='-2y', end_date='today')
        discontinue_date = fake.date_between(start_date=launch_date, end_date='today')
        cursor.execute('INSERT INTO DimVariant ...', (product_id, name, launch_date, discontinue_date))

# Generate sample data for DimDate
start_date = datetime.strptime('2022-01-01', '%Y-%m-%d')
end_date = datetime.strptime('2024-01-01', '%Y-%m-%d')
current_date = start_date
while current_date <= end_date:
    cursor.execute('INSERT INTO DimDate ...', (current_date, current_date.year, current_date.month, current_date.day))
    current_date += timedelta(days=1)
Data Insertion
The generated data is inserted into the respective tables.

python
Copy code
# Generate sample data for FactOrder
for _ in range(100):
    cursor.execute('INSERT INTO FactOrder ...', (
        random.randint(1, 10), # CustomerID
        random.randint(1, 10), # ProductID
        random.randint(1, 30), # VariantID
        random.randint(1, 731), # OrderDateID
        random.randint(1, 5), # Quantity
        round(random.uniform(10, 1000), 2) # Price
    ))

conn.commit()
Data Querying
Data is queried from the database to verify the content and structure.

python
Copy code
# Query the data to verify
df_customers = pd.read_sql_query('SELECT * FROM DimCustomer', conn)
df_products = pd.read_sql_query('SELECT * FROM DimProduct', conn)
df_variants = pd.read_sql_query('SELECT * FROM DimVariant', conn)
df_dates = pd.read_sql_query('SELECT * FROM DimDate', conn)
df_orders = pd.read_sql_query('SELECT * FROM FactOrder', conn)

# Display some sample data
print(df_customers.head())
print(df_products.head())
print(df_variants.head())
print(df_dates.head())
print(df_orders.head())

conn.close()


How to Run




Clone the repository to your local machine.

Ensure you have Python and the necessary libraries (pandas, Faker, sqlite3) installed.

Run the Python script to create the database, generate data, and execute queries.

Modify the SQL queries to suit your analysis needs.




Contact
For any questions or feedback, please reach out:
guptasonalee88@gmail.com
https://www.linkedin.com/in/sonali-kumari21/
https://github.com/sonalee88
