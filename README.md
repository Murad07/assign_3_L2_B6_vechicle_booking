# Vehicle Booking - SQL Queries

## ERD Diagram

![ERD Diagram](https://lucid.app/lucidchart/9c05ca75-9053-4665-8c71-387ee365c731/edit?invitationId=inv_ae9d1bb1-92df-46a9-bbf0-11541f8b0535)

## Video Link

[Video Link](https://drive.google.com/file/d/17NdhdOTPOqfIoHZHNVyy9YXslNtyBM_S/view?usp=sharing)

## Project Overview

This project consists of a set of SQL queries for vehicle booking management. Including joins, subqueries with `EXISTS`, filtering with `WHERE`, and aggregation with `GROUP BY` and `HAVING`. These queries will analyzing data of users, vehicles, and bookings.

## Queries

This section details the SQL queries included in the `queries.sql` file.

### Query 1: JOIN
Retrieve booking information along with:

- Customer name
- Vehicle name

```sql
select b.booking_id, u.name as customer_name, v.name, b.start_date, b.end_date, b.status
from
    bookings as b
    inner join users as u on u.user_id = b.user_id
    inner join vehicles as v on v.vehicle_id = b.vehicle_id;
```

### Query 2: EXISTS
Find all vehicles that have never been booked.

- Concepts used: NOT EXISTS

```sql
select v.*
from vehicles as v
where
    not exists (
        select 1
        from bookings as b
        where
            b.vehicle_id = v.vehicle_id
    );
```

### Query 3: WHERE
Retrieve all available vehicles of a specific type (e.g. cars).

- Concepts used: SELECT, WHERE

```sql
select * from vehicles where status = 'available' and type = 'car';
```

### Query 4: GROUP BY and HAVING
Find the total number of bookings for each vehicle and display only those vehicles that have more than 2 bookings.

- Concepts used: GROUP BY, HAVING, COUNT

```sql
select v.name, count(b.*) as total_bookings
from bookings as b
    join vehicles as v on v.vehicle_id = b.vehicle_id
group by
    v.vehicle_id,
    v.name
HAVING
    COUNT(b.booking_id) > 2;
```
