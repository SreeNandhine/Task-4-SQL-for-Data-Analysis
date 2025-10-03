-- 1. Select all data
SELECT * FROM ecommerce;

-- 2. Customers who bought Electronics
SELECT customer_id, product, price
FROM ecommerce
WHERE category = 'Electronics';

-- 3. Total revenue per customer
SELECT customer_id, SUM(price * quantity) AS total_spent
FROM ecommerce
GROUP BY customer_id
ORDER BY total_spent DESC;

-- 4. Average order value
SELECT AVG(price * quantity) AS avg_order_value
FROM ecommerce;

-- 5. Join Example (Orders with Customers - assume a customer table exists)
-- Dummy customer table for example:
-- customer_id | customer_name
-- 101 | John
-- 102 | Alice
-- 103 | David
-- 104 | Maria
-- 105 | Sam

SELECT c.customer_name, e.product, e.price, e.order_date
FROM ecommerce e
INNER JOIN customers c ON e.customer_id = c.customer_id;

-- 6. Subquery: Customers who spent more than avg spending
SELECT customer_id, SUM(price * quantity) AS total_spent
FROM ecommerce
GROUP BY customer_id
HAVING total_spent > (SELECT AVG(price * quantity) FROM ecommerce);

-- 7. Create a View
CREATE VIEW high_value_orders AS
SELECT * FROM ecommerce WHERE price > 500;

-- 8. Query optimization (add index on customer_id)
CREATE INDEX idx_customer ON ecommerce(customer_id);
