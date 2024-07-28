-- Challenge --
-- Step 1: Creating a Customer Summary Report --
CREATE VIEW sakila.customer_rental_summary AS
SELECT
    c.customer_id,
    CONCAT(c.first_name, ' ', c.last_name) AS customer_name,
    c.email,
    COUNT(r.rental_id) AS rental_count
FROM
    sakila.customer AS c
LEFT JOIN sakila.rental AS r ON c.customer_id = r.customer_id
GROUP BY
    c.customer_id, c.first_name, c.last_name, c.email;

SELECT * FROM customer_rental_summary;
-- Step 2: Create a Temporary Table --

CREATE TEMPORARY TABLE customer_payment_summary AS
SELECT
    crs.customer_id,
    SUM(p.amount) AS total_paid
FROM
    customer_rental_summary crs
LEFT JOIN payment p ON crs.customer_id = p.customer_id
GROUP BY
    crs.customer_id;
SELECT * FROM  customer_payment_summary;
Next, create a Temporary Table that calculates the total amount paid by each customer (total_paid). The Temporary Table should use the rental summary view created in Step 1 to join with the payment table and calculate the total amount paid by each customer.

- Step 3: Create a CTE and the Customer Summary Report

Create a CTE that joins the rental summary View with the customer payment summary Temporary Table created in Step 2. The CTE should include the customer's name, email address, rental count, and total amount paid. 

Next, using the CTE, create the query to generate the final customer summary report, which should include: customer name, email, rental_count, total_paid and average_payment_per_rental, this last column is a derived column from total_paid and rental_count.

## Requirements

- Fork this repo
- Clone it to your machine


## Getting Started

Complete the challenge in this readme in a `.sql` file.

## Submission

- Upon completion, run the following commands:



```bash
git add .
git commit -m "Solved lab"
git push origin master
```






