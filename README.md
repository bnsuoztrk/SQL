-- 1. Tüm müşterileri listeleyin.
SELECT * FROM customers;

-- 2. Tüm çalışanların adlarını ve soyadlarını listeleyin.
SELECT first_name, last_name FROM employees;

-- 3. Şehirleri tekrarsız (DISTINCT) olarak getirin.
SELECT DISTINCT city FROM customers;

-- 4. Şirket ismi "Around the Horn" olan müşterinin bilgilerini getirin.
SELECT * FROM customers WHERE company_name = 'Around the Horn';

-- 5. 10’dan fazla stoğu olan ürünleri listeleyin.
SELECT * FROM products WHERE units_in_stock > 10;

-- 6. Ürün ismi "Chai" olan ürünün fiyatını bulun.
SELECT unit_price FROM products WHERE product_name = 'Chai';

-- 7. Çalışanların tam adını (FirstName + LastName) "Full Name" olarak listeleyin.
SELECT CONCAT(first_name, ' ', last_name) AS "Full Name" FROM employees;

-- 8. En pahalı ürünü getirin.
SELECT * FROM products ORDER BY unit_price DESC LIMIT 1;

-- 9. En pahalı 5 ürünü listeleyin.
SELECT * FROM products ORDER BY unit_price DESC LIMIT 5;

-- 10. Çalışanların doğum tarihlerini yıl bazında sıralayın.
SELECT * FROM employees ORDER BY birth_date;

-- 11. İsmi "Maria" olan çalışanları listeleyin.
SELECT * FROM employees WHERE first_name = 'Maria';

-- 12. Adresinde "Street" geçen müşterileri bulun.
SELECT * FROM customers WHERE address LIKE '%Street%';

-- 13. Fiyatı 20 ile 50 arasında olan ürünleri listeleyin.
SELECT * FROM products WHERE unit_price BETWEEN 20 AND 50;

-- 14. "London" şehrinde bulunan müşterileri bulun.
SELECT * FROM customers WHERE city = 'London';

-- 15. "L" harfiyle başlayan ürünleri listeleyin.
SELECT * FROM products WHERE product_name LIKE 'L%';

-- 16. 1997 yılında işe alınan çalışanları listeleyin.
SELECT * FROM employees WHERE EXTRACT(YEAR FROM hire_date) = 1997;

-- 17. Ürün ismi içinde "cheese" geçenleri bulun.
SELECT * FROM products WHERE product_name ILIKE '%cheese%';

-- 18. 1996 yılında sipariş veren müşterileri bulun.
SELECT DISTINCT customers.* 
FROM customers 
JOIN orders ON customers.customer_id = orders.customer_id 
WHERE EXTRACT(YEAR FROM orders.order_date) = 1996;

-- 19. İsmi "E" harfi ile biten çalışanları listeleyin.
SELECT * FROM employees WHERE first_name LIKE '%E';

-- 20. Müşterilerin faks numarası olmayanları listeleyin.
SELECT * FROM customers WHERE fax IS NULL;

-- 21. Ürünleri fiyatlarına göre artan şekilde sıralayın.
SELECT * FROM products ORDER BY unit_price ASC;

-- 22. Çalışanları soyadına göre azalan sıralayın.
SELECT * FROM employees ORDER BY last_name DESC;

-- 23. Çalışanları en eski işe alınandan en yeniye sıralayın.
SELECT * FROM employees ORDER BY hire_date ASC;

-- 24. Siparişleri sipariş tarihine göre sıralayın.
SELECT * FROM orders ORDER BY order_date ASC;

-- 25. En fazla sipariş veren müşterileri sıralayın.
SELECT customers.customer_id, customers.company_name, COUNT(orders.order_id) AS total_orders
FROM customers
JOIN orders ON customers.customer_id = orders.customer_id
GROUP BY customers.customer_id, customers.company_name
ORDER BY total_orders DESC;

-- 26. Ürünleri stok miktarına göre sıralayın.
SELECT * FROM products ORDER BY units_in_stock DESC;

-- 27. En son alınan siparişin detaylarını getirin.
SELECT * FROM orders ORDER BY order_date DESC LIMIT 1;

-- 28. En ucuz 3 ürünü listeleyin.
SELECT * FROM products ORDER BY unit_price ASC LIMIT 3;

-- 29. Çalışanları yaşlarına göre sıralayın.
SELECT *, AGE(birth_date) AS age FROM employees ORDER BY birth_date ASC;

-- 30. Ürünleri kategoriye göre sıralayın.
SELECT * FROM products ORDER BY category_id;

-- 31. Müşterilerin yaptığı siparişleri listeleyin.
SELECT customers.customer_id, customers.company_name, orders.*
FROM customers
JOIN orders ON customers.customer_id = orders.customer_id;

-- 32. Çalışanların gerçekleştirdiği siparişleri listeleyin.
SELECT employees.employee_id, employees.first_name, employees.last_name, orders.*
FROM employees
JOIN orders ON employees.employee_id = orders.employee_id;

-- 33. "USA" ülkesindeki müşterilerin siparişlerini getirin.
SELECT customers.customer_id, customers.company_name, orders.*
FROM customers
JOIN orders ON customers.customer_id = orders.customer_id
WHERE customers.country = 'USA';

-- 34. En fazla sipariş veren müşteriyi bulun.
SELECT customer_id, COUNT(order_id) AS total_orders
FROM orders
GROUP BY customer_id
ORDER BY total_orders DESC
LIMIT 1;

-- 35. Her siparişin hangi çalışana ait olduğunu getirin.
SELECT order_id, employee_id FROM orders;

-- 36. Hangi tedarikçinin hangi ürünü sağladığını listeleyin.
SELECT suppliers.supplier_id, suppliers.company_name, products.product_name 
FROM suppliers
JOIN products ON suppliers.supplier_id = products.supplier_id;

-- 37. Çalışanların bağlı olduğu yöneticileri bulun.
SELECT e.employee_id, e.first_name, e.last_name, e.reports_to AS manager_id 
FROM employees e;

-- 38. Çalışanların yaşını hesaplayın.
SELECT employee_id, first_name, last_name, AGE(birth_date) AS age FROM employees;

-- 39. Her çalışanın kaç sipariş aldığını listeleyin.
SELECT employee_id, COUNT(order_id) AS total_orders 
FROM orders
GROUP BY employee_id
ORDER BY total_orders DESC;

-- 40. Her kategoride kaç ürün bulunduğunu hesaplayın.
SELECT category_id, COUNT(product_id) AS total_products 
FROM products
GROUP BY category_id;

-- 41. Her kategorideki ortalama ürün fiyatlarını listeleyin.
SELECT category_id, AVG(unit_price) AS average_price 
FROM products
GROUP BY category_id;

-- 42. Çalışanların toplam kaç sipariş işlediğini hesaplayın.
SELECT employee_id, COUNT(order_id) AS total_orders 
FROM orders
GROUP BY employee_id;

-- 43. En fazla sipariş alan ilk 5 müşteriyi listeleyin.
SELECT customer_id, COUNT(order_id) AS total_orders 
FROM orders
GROUP BY customer_id
ORDER BY total_orders DESC
LIMIT 5;

-- 44. Ortalama fiyatı 30’dan fazla olan kategorileri listeleyin.
SELECT category_id, AVG(unit_price) AS avg_price 
FROM products
GROUP BY category_id
HAVING AVG(unit_price) > 30;

-- 45. 10’dan fazla sipariş veren müşterileri listeleyin.
SELECT customer_id, COUNT(order_id) AS total_orders 
FROM orders
GROUP BY customer_id
HAVING COUNT(order_id) > 10;

-- 46. Ülkeye göre müşteri sayısını listeleyin.
SELECT country, COUNT(customer_id) AS total_customers 
FROM customers
GROUP BY country;

-- 47. Ürünleri tedarikçiye göre gruplayın.
SELECT supplier_id, COUNT(product_id) AS total_products 
FROM products
GROUP BY supplier_id;

-- 48. 100’den fazla siparişi olan çalışanları listeleyin.
SELECT employee_id, COUNT(order_id) AS total_orders 
FROM orders
GROUP BY employee_id
HAVING COUNT(order_id) > 100;

-- 49. Ortalama sipariş miktarı 10’dan fazla olan siparişleri listeleyin.
SELECT order_id, AVG(quantity) AS avg_quantity 
FROM order_details
GROUP BY order_id
HAVING AVG(quantity) > 10;

-- 50. Çalışan bazında toplam satış miktarlarını hesaplayın.
SELECT o.employee_id, SUM(od.unit_price * od.quantity) AS total_sales
FROM orders o
JOIN order_details od ON o.order_id = od.order_id
GROUP BY o.employee_id
ORDER BY total_sales DESC;

-- 51. En pahalı ürünün fiyatını döndürün.
SELECT MAX(unit_price) FROM products;

-- 52. En yüksek fiyatlı ürünün bilgilerini getirin.
SELECT * FROM products 
ORDER BY unit_price DESC 
LIMIT 1;

-- 53. En az sipariş alan ürünü listeleyin.
SELECT product_id, COUNT(order_id) AS total_orders 
FROM order_details
GROUP BY product_id
ORDER BY total_orders ASC
LIMIT 1;

-- 54. 1997 yılında en fazla sipariş veren müşteriyi getirin.
SELECT customer_id, COUNT(order_id) AS total_orders 
FROM orders
WHERE EXTRACT(YEAR FROM order_date) = 1997
GROUP BY customer_id
ORDER BY total_orders DESC
LIMIT 1;

-- 55. En fazla sipariş alan çalışanı bulun.
SELECT employee_id, COUNT(order_id) AS total_orders 
FROM orders
GROUP BY employee_id
ORDER BY total_orders DESC
LIMIT 1;

-- 56. En fazla satış yapan çalışanın ismini bulun.
SELECT e.first_name, e.last_name, SUM(od.unit_price * od.quantity) AS total_sales
FROM employees e
JOIN orders o ON e.employee_id = o.employee_id
JOIN order_details od ON o.order_id = od.order_id
GROUP BY e.employee_id
ORDER BY total_sales DESC
LIMIT 1;

-- 57. En çok sipariş alan müşteriyi listeleyin.
SELECT customer_id, COUNT(order_id) AS total_orders 
FROM orders
GROUP BY customer_id
ORDER BY total_orders DESC
LIMIT 1;

-- 58. Ortalama fiyatın üzerindeki ürünleri bulun.
SELECT * FROM products 
WHERE unit_price > (SELECT AVG(unit_price) FROM products);

-- 59. Ortalama sipariş tutarını hesaplayın.
SELECT AVG(od.unit_price * od.quantity) AS avg_order_value
FROM order_details od;

-- 60. En pahalı ürünün tedarikçisinin bilgilerini getirin.
SELECT s.* FROM suppliers s
JOIN products p ON s.supplier_id = p.supplier_id
ORDER BY p.unit_price DESC
LIMIT 1;

-- 61. Yeni bir müşteri ekleyin.
INSERT INTO customers (customer_id, company_name, contact_name, city, country)
VALUES ('NEW01', 'New Company', 'John Doe', 'New York', 'USA');

-- 62. Yeni bir ürün ekleyin.
INSERT INTO products (product_name, supplier_id, category_id, unit_price, units_in_stock)
VALUES ('New Product', 1, 2, 15.99, 50);

-- 63. "Berlin" şehrinde bulunan müşterilerin şehir adını "New Berlin" olarak güncelleyin.
UPDATE customers 
SET city = 'New Berlin' 
WHERE city = 'Berlin';

-- 64. "Beverages" kategorisindeki ürünlerin fiyatlarını %10 artırın.
UPDATE products 
SET unit_price = unit_price * 1.10 
WHERE category_id = (SELECT category_id FROM categories WHERE category_name = 'Beverages');

-- 65. 50’den az stoğu olan ürünlerin stoğunu 100 olarak güncelleyin.
UPDATE products 
SET units_in_stock = 100 
WHERE units_in_stock < 50;

-- 66. En pahalı ürünü silin.
DELETE FROM products 
WHERE unit_price = (SELECT MAX(unit_price) FROM products);

-- 67. 1996'dan önce işe alınan çalışanları silin.
DELETE FROM employees 
WHERE EXTRACT(YEAR FROM hire_date) < 1996;
-- 68. Şirketi olmayan müşterileri silin.
DELETE FROM customers 
WHERE company_name IS NULL OR company_name = '';

-- 69. En az sipariş veren müşteriyi silin.
DELETE FROM customers 
WHERE customer_id = (
    SELECT customer_id FROM orders
    GROUP BY customer_id
    ORDER BY COUNT(order_id) ASC
    LIMIT 1
);

-- 70. En az stoğu olan ürünü silin.
DELETE FROM products 
WHERE units_in_stock = (SELECT MIN(units_in_stock) FROM products);

-- 71. Her kategorideki en pahalı ürünü bulun.
SELECT category_id, product_name, unit_price 
FROM products p
WHERE unit_price = (
    SELECT MAX(unit_price) FROM products WHERE category_id = p.category_id
);

-- 72. En çok sipariş edilen ürünü bulun.
SELECT product_id, SUM(quantity) AS total_quantity
FROM order_details
GROUP BY product_id
ORDER BY total_quantity DESC
LIMIT 1;

-- 73. Çalışanların sipariş ortalamasını hesaplayın.
SELECT employee_id, AVG(order_count) AS avg_orders
FROM (
    SELECT employee_id, COUNT(order_id) AS order_count
    FROM orders
    GROUP BY employee_id
) AS employee_orders
GROUP BY employee_id;

-- 74. Müşterilerin sipariş miktarlarını yüzde bazında gösterin.
SELECT customer_id, 
       COUNT(order_id) AS total_orders, 
       COUNT(order_id) * 100.0 / (SELECT COUNT(*) FROM orders) AS percentage
FROM orders
GROUP BY customer_id;

-- 75. Müşterilerin en çok sipariş verdiği şehirleri bulun.
SELECT city, COUNT(order_id) AS total_orders
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY city
ORDER BY total_orders DESC
LIMIT 1;

-- 76. Ürünlerin fiyatlarını ortalama fiyatla karşılaştırarak yüzdelik farkını bulun.
SELECT product_name, unit_price, 
       (unit_price - (SELECT AVG(unit_price) FROM products)) / (SELECT AVG(unit_price) FROM products) * 100 AS price_difference_percent
FROM products;

-- 77. Çalışanların her yıl kaç sipariş aldığını hesaplayın.
SELECT employee_id, EXTRACT(YEAR FROM order_date) AS year, COUNT(order_id) AS total_orders
FROM orders
GROUP BY employee_id, year
ORDER BY year DESC;

-- 78. Müşterileri sipariş sayısına göre "Düşük", "Orta", "Yüksek" olarak etiketleyin.
SELECT customer_id, COUNT(order_id) AS total_orders,
       CASE 
           WHEN COUNT(order_id) < 5 THEN 'Düşük'
           WHEN COUNT(order_id) BETWEEN 5 AND 15 THEN 'Orta'
           ELSE 'Yüksek'
       END AS order_category
FROM orders
GROUP BY customer_id;

-- 79. En yüksek ciro yapan ilk 3 tedarikçiyi bulun.
SELECT p.supplier_id, s.company_name, SUM(od.unit_price * od.quantity) AS total_revenue
FROM products p
JOIN suppliers s ON p.supplier_id = s.supplier_id
JOIN order_details od ON p.product_id = od.product_id
GROUP BY p.supplier_id, s.company_name
ORDER BY total_revenue DESC
LIMIT 3;

-- 80. En az 3 sipariş veren müşterileri listeleyin.
SELECT customer_id, COUNT(order_id) AS total_orders
FROM orders
GROUP BY customer_id
HAVING COUNT(order_id) >= 3;

-- 81. Sipariş veren müşterileri ve sipariş sayılarını gösterin.
SELECT customer_id, COUNT(order_id) AS total_orders
FROM orders
GROUP BY customer_id;

-- 82. En çok sipariş verilen ürünleri ve sipariş sayılarını listeleyin.
SELECT product_id, COUNT(order_id) AS total_orders
FROM order_details
GROUP BY product_id
ORDER BY total_orders DESC;

-- 83. En yüksek toplam satış yapan çalışanları gösterin.
SELECT o.employee_id, SUM(od.unit_price * od.quantity) AS total_sales
FROM orders o
JOIN order_details od ON o.order_id = od.order_id
GROUP BY o.employee_id
ORDER BY total_sales DESC;

-- 84. En fazla sipariş veren müşterinin bilgilerini getirin.
SELECT * FROM customers 
WHERE customer_id = (
    SELECT customer_id FROM orders
    GROUP BY customer_id
    ORDER BY COUNT(order_id) DESC
    LIMIT 1
);

-- 85. Her siparişte sipariş verilen ürünleri listeleyin.
SELECT o.order_id, p.product_name, od.quantity
FROM orders o
JOIN order_details od ON o.order_id = od.order_id
JOIN products p ON od.product_id = p.product_id;

-- 86. Müşterinin yaptığı siparişlerde hangi çalışanın ilgilendiğini gösterin.
SELECT o.customer_id, o.order_id, e.first_name, e.last_name
FROM orders o
JOIN employees e ON o.employee_id = e.employee_id;

-- 87. Çalışanların sattığı toplam ürün miktarını getirin.
SELECT o.employee_id, SUM(od.quantity) AS total_products_sold
FROM orders o
JOIN order_details od ON o.order_id = od.order_id
GROUP BY o.employee_id;

-- 88. Siparişlerde en çok kullanılan nakliye şirketlerini listeleyin.
SELECT ship_via, COUNT(order_id) AS total_orders
FROM orders
GROUP BY ship_via
ORDER BY total_orders DESC;

-- 89. Çalışanların kaç farklı müşteriyle çalıştığını listeleyin.
SELECT employee_id, COUNT(DISTINCT customer_id) AS unique_customers
FROM orders
GROUP BY employee_id;

-- 90. En çok sipariş verilen kategorileri listeleyin.
SELECT p.category_id, c.category_name, COUNT(od.order_id) AS total_orders
FROM products p
JOIN categories c ON p.category_id = c.category_id
JOIN order_details od ON p.product_id = od.product_id
GROUP BY p.category_id, c.category_name
ORDER BY total_orders DESC;

-- 91. Müşterilerden en çok sipariş alan tedarikçileri bulun.
SELECT p.supplier_id, s.company_name, COUNT(od.order_id) AS total_orders
FROM products p
JOIN suppliers s ON p.supplier_id = s.supplier_id
JOIN order_details od ON p.product_id = od.product_id
GROUP BY p.supplier_id, s.company_name
ORDER BY total_orders DESC;

-- 92. Müşteri bazında toplam sipariş tutarlarını listeleyin.
SELECT o.customer_id, SUM(od.unit_price * od.quantity) AS total_spent
FROM orders o
JOIN order_details od ON o.order_id = od.order_id
GROUP BY o.customer_id;

-- 93. Çalışan bazında ortalama sipariş tutarlarını listeleyin.
SELECT o.employee_id, AVG(od.unit_price * od.quantity) AS avg_order_value
FROM orders o
JOIN order_details od ON o.order_id = od.order_id
GROUP BY o.employee_id;

-- 94. En uzun sürede teslim edilen siparişi getirin.
SELECT * FROM orders
ORDER BY (shipped_date - order_date) DESC
LIMIT 1;

-- 95. En hızlı teslim edilen siparişi getirin.
SELECT * FROM orders
ORDER BY (shipped_date - order_date) ASC
LIMIT 1;

-- 96. 1000 dolardan fazla sipariş veren müşterileri bulun.
SELECT customer_id, SUM(od.unit_price * od.quantity) AS total_spent
FROM orders o
JOIN order_details od ON o.order_id = od.order_id
GROUP BY customer_id
HAVING SUM(od.unit_price * od.quantity) > 1000;

-- 97. Ortalama sipariş değerini geçen siparişleri listeleyin.
SELECT order_id, SUM(od.unit_price * od.quantity) AS order_total
FROM order_details od
GROUP BY order_id
HAVING SUM(od.unit_price * od.quantity) > (SELECT AVG(od.unit_price * od.quantity) FROM order_details od);

-- 98. Ülkeye göre en çok sipariş veren müşterileri bulun.
SELECT country, customer_id, COUNT(order_id) AS total_orders
FROM customers
JOIN orders USING(customer_id)
GROUP BY country, customer_id
ORDER BY total_orders DESC;

-- 99. En çok satış yapılan ayları bulun.
SELECT EXTRACT(MONTH FROM order_date) AS month, COUNT(order_id) AS total_orders
FROM orders
GROUP BY month
ORDER BY total_orders DESC;

-- 100. Çalışanların toplam sattığı ürün miktarını listeleyin.
SELECT employee_id, SUM(od.quantity) AS total_products_sold
FROM orders o
JOIN order_details od ON o.order_id = od.order_id
GROUP BY employee_id;

