# If you want to see the Queries you can get access to this link below
[Link to SQL Fiddle](http://sqlfiddle.com/#!9/ce3dc3e/170)

#This project utilizes the follow Superstore data: 

CREATE TABLE superstore (
    item_id INTEGER PRIMARY KEY,
    item_name TEXT,
    category TEXT,
    price DECIMAL(10, 2),
    stock_quantity INTEGER,
    average_rating DECIMAL(3, 2)
);

INSERT INTO superstore (item_id, item_name, category, price, stock_quantity, average_rating)
VALUES
    (1, 'Stainless Steel Cookware Set', 'Kitchen Supplies', 89.99, 50, 4.6),
    (2, 'Memory Foam Mattress', 'Furnishings', 499.99, 30, 4.8),
    (3, 'Smart LED TV', 'Electronics', 549.00, 20, 4.5),
    (4, 'Robot Vacuum Cleaner', 'Appliances', 199.50, 40, 4.3),
    (5, 'Wireless Bluetooth Speaker', 'Electronics', 39.99, 60, 4.2),
    (6, 'Non-Stick Baking Set', 'Kitchen Supplies', 29.95, 80, 4.4),
    (7, 'Cotton Bedding Set', 'Furnishings', 89.00, 25, 4.7),
    (8, 'Smart Home Security Camera', 'Electronics', 79.95, 15, 4.1),
    (9, 'Air Purifier', 'Appliances', 129.50, 35, 4.6),
    (10, 'Premium Coffee Maker', 'Kitchen Supplies', 79.99, 50, 4.9),
    (11, 'Ergonomic Office Chair', 'Furnishings', 189.00, 20, 4.5),
    (12, 'Wireless Earbuds', 'Electronics', 49.99, 75, 4.3),
    (13, 'Slow Cooker', 'Appliances', 49.95, 30, 4.7),
    (14, 'Cutlery Set', 'Kitchen Supplies', 34.50, 40, 4.4),
    (15, 'Cozy Throw Blanket', 'Furnishings', 24.99, 100, 4.2);



  #Use a SELECT statement to order the items by price.
SELECT *
FROM superstore
ORDER BY price DESC;
#Implementing SQL query that will show a statistic about the item prices, like a sum, average, minimum, maximum, or count.
SELECT
  item_id,
  item_name,
  SUM(price) AS total_price,
  AVG(price) AS average_price,
  MIN(price) AS min_price,
  MAX(price) AS max_price,
  COUNT(*) AS item_count
FROM superstore
GROUP BY item_id, item_name;
#Writing a SQL query that will show a statistic about the price for items in the category of "Kitchen Supplies". The values in the categories column are called text strings, and text strings are case sensitive. That means if you want to select "Kitchen Supplies".

SELECT
  SUM(price) AS total_price,
  AVG(price) AS average_price,
  MIN(price) AS min_price,
  MAX(price) AS max_price,
  COUNT(*) AS item_count
FROM superstore
WHERE category = 'Kitchen Supplies';

#1.How many air purifiers are in stock? 
SELECT SUM(stock_quantity) AS air_purifier_stock
FROM superstore
WHERE category = 'Air Purifiers';

#2. What is the total inventory value of the store?
SELECT SUM(stock_quantity * price) AS total_inventory_value
FROM superstore;

#3. Which category has the highest average rating?
SELECT category, AVG(average_rating) AS avg_rating
FROM superstore
GROUP BY category
ORDER BY avg_rating DESC
LIMIT 1;

#4.What is the most expensive item in stock?
SELECT item_name, price
FROM superstore
ORDER BY price DESC
LIMIT 1;

#5.How many items are there in each category?
SELECT category, COUNT(*) AS item_count
FROM superstore
GROUP BY category;

#6. Which item has the lowest stock quantity?
SELECT item_name, stock_quantity
FROM superstore
ORDER BY stock_quantity ASC
LIMIT 1;

#7.What is the total stock quantity for all items in the "Kitchen Supplies" category?
SELECT SUM(stock_quantity) AS total_stock_quantity
FROM superstore
WHERE category = 'Kitchen Supplies';

#8. What is the average price of items with an average rating above 4.5?
SELECT AVG(price) AS avg_price_high_rating
FROM superstore
WHERE average_rating > 4.5;

#9. Which category has the highest total inventory value?
SELECT category, SUM(stock_quantity * price) AS total_inventory_value
FROM superstore
GROUP BY category
ORDER BY total_inventory_value DESC
LIMIT 1;

#10. What is the total number of items in stock and their average price?
SELECT SUM(stock_quantity) AS total_stock_quantity, AVG(price) AS average_price
FROM superstore;

#11.Which items have an average rating above 4.5 and are priced below $50?
SELECT item_name, average_rating, price
FROM superstore
WHERE average_rating > 4.5 AND price < 50;



