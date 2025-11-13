# 🚲 Bike Rental Shop — Bash + PostgreSQL CLI System

A command-line bike rental management system built using **Bash** and **PostgreSQL**.  
This project lets users rent and return bikes through a simple terminal interface, storing all information in a database.

---

## 🧠 Overview

The **Bike Rental Shop** script allows you to:

- View all available bikes for rent  
- Register new customers by phone number  
- Rent available bikes and mark them as unavailable  
- Return rented bikes and update their availability  
- Store all data (customers, bikes, rentals) in a PostgreSQL database  

This project was developed as part of the FreeCodeCamp Relational Database certification.

---

## ⚙️ Prerequisites

Before running the script, make sure you have:

- **Bash** (v4.0 or later)
- **PostgreSQL** (v12 or later)
- A PostgreSQL user named `freecodecamp`
- A database named `bikes`

---

## 🗃️ Database Setup

Run the following SQL commands inside `psql` to create the database and required tables:

```sql
CREATE DATABASE bikes;

\c bikes

CREATE TABLE customers(
  customer_id SERIAL PRIMARY KEY,
  phone VARCHAR(20) UNIQUE NOT NULL,
  name VARCHAR(50) NOT NULL
);

CREATE TABLE bikes(
  bike_id SERIAL PRIMARY KEY,
  type VARCHAR(50) NOT NULL,
  size INT NOT NULL,
  available BOOLEAN DEFAULT TRUE
);

CREATE TABLE rentals(
  rental_id SERIAL PRIMARY KEY,
  customer_id INT REFERENCES customers(customer_id),
  bike_id INT REFERENCES bikes(bike_id),
  date_rented TIMESTAMP DEFAULT NOW(),
  date_returned TIMESTAMP
);

INSERT INTO bikes(type, size) VALUES
('Mountain', 26),
('Road', 28),
('Hybrid', 27),
('Electric', 29),
('BMX', 24);
```

## 🚀 Usage

1. Clone or download the project.
2. Make the script executable:

```bash
chmod +x bike_shop.sh
```

3. Run the script:

```bash
./bike-shop.sh
```
4. Follow the interactive menu:
- Rent a bike
- Return a bike
- Exit the program

## 💾 Example Interaction

```txt
~~~~~ Bike Rental Shop ~~~~~

How may I help you?

1. Rent a bike
2. Return a bike
3. Exit
1

Here are the bikes we have available:
1) 26" Mountain Bike
2) 28" Road Bike
3) 27" Hybrid Bike

Which one would you like to rent?
2
What's your phone number?
555-1234
What's your name?
Alice
I have put you down for the 28" Road Bike, Alice.

```

## 🧩 Script Structure

- **`PSQL` variable** — defines the PostgreSQL command used throughout  
- **`MAIN_MENU()`** — displays main options (rent, return, exit)  
- **`RENT_MENU()`** — handles bike selection, customer registration, and rental updates  
- **`RETURN_MENU()`** — processes bike returns and updates database availability  
- **`EXIT()`** — cleanly exits the program  

### Input Validation Ensures:
- Only valid bike IDs are accepted  
- Customers are checked or created automatically  
- Bike availability is updated on rent/return  

## 👨‍💻 Author

Created by: Hugo Rocha
