# Kultra-Mega-Stores-Analysis
Kultra Mega Stores (KMS) is a Lagos-based company specializing in office supplies and furniture. It serves a wide range of customers, including individual consumers, small retail businesses, and large corporate clients across Lagos and other parts of Nigeria. 
# Case Study 2: Kultra Mega Stores Inventory

# Company Overview
Kultra Mega Stores (KMS), headquartered in Lagos, specialises in office supplies and furniture. Its customer base includes individual consumers, small businesses (retail), and large corporate clients (wholesale) across Lagos, Nigeria.
You have been engaged as a Business Intelligence Analyst to support the Abuja division of KMS. The Business Manager has shared an Excel file containing order data from 2009 to 2012 and has requested that you analyze the data and present your key insights and findings.
Apply your SQL skills from the DSA Data Analysis class and solve both case scenarios as shared in the document.

Tools Used
- **SQL (MySQL):** For querying and aggregating insights
- **Excel Pivot Table:** For summarizing sales by categories, regions, and customer segments
- **Power BI:** To build interactive dashboards and data visuals

---
## Case Scenario I

### Q1: Which product category had the highest sales?

```sql
SELECT product_category, SUM(sales) AS total_sales
FROM public.orders
GROUP BY product_category
ORDER BY total_sales DESC
LIMIT 1;
```
**Answer:**  
| Product Category | Total Sales      |
|------------------|------------------|
| Technology       | ₦5,984,248.18 ✅ |

 **Insight:** Technology is the most profitable category, representing the best-performing product line. This suggests high demand, and KMS should double down on inventory expansion and targeted marketing for tech.

---
### Q2: Top 3 and Bottom 3 Regions by Sales

```sql
SELECT region, SUM(sales) AS total_sales
FROM public.orders
GROUP BY region
ORDER BY total_sales DESC;
```

**Top 3:**
| Region  | Sales         |
|---------|---------------|
| West    | ₦3,597,549.17 |
| Ontario | ₦3,063,212.30 |
| Prarie  | ₦2,837,305.45 |

**Bottom 3:**
| Region               | Sales         |
|----------------------|---------------|
| Yukon                | ₦975,867.12   |
| Northwest Territories| ₦800,847.06   |
| Nunavut              | ₦116,376.16   |

 **Insight:** Marketing efforts and pricing strategies can be optimized for underperforming regions like Nunavut and Yukon.

---
### Q3: Total Sales of Appliances in Ontario

```sql
SELECT SUM(sales)
FROM public.orders
WHERE product_category = 'Appliances' AND province = 'Ontario';
```

**Answer:** ₦0.00

⚠ **Insight:** No appliance sales were recorded in Ontario. This may point to stock availability issues or unmet demand.

---
### Q4: 4.	Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers

```sql
SELECT customer_name, SUM(sales) AS total_sales
FROM public.orders
GROUP BY customer_name
ORDER BY total_sales ASC
LIMIT 10;
```
**Answer:**
| Customer Name      | Sales   |
|--------------------|---------|
| Jeremy Farry       | ₦85.72  |
| Natalie DeCherney  | ₦125.90 |
| Nicole Fjeld       | ₦153.03 |
| Katrina Edelman    | ₦180.76 |
| Dorothy Dickinson  | ₦198.08 |
|Christine Kargatis  | 293.22  |
|Eric Murdock        | 343.328 |
|Chris McAfee        | 350.18  |
|Rick Huthwaite      | 415.82  |
|Mark Hamilton       | 450.99  |

** Advise: Improve engagement, promos, or exit non-profitable customers.
Consider personalized offers like Improve engagement, promos, or exit non-profitable customers.
--

###  Q5: 5.	KMS incurred the most shipping cost using which shipping method?

```sql
SELECT ship_mode, SUM(shipping_cost) AS total_cost
FROM public.orders
GROUP BY ship_mode
ORDER BY total_cost DESC;
```

**Answer:**
| Ship Mode       | Total Shipping Cost |
|------------------|---------------------|
| Delivery Truck   | ₦51,971.94         |

**Insight:** Delivery Truck, despite being the slowest, is the most expensive overall. Explore cost-effective alternatives for low-priority orders.

---

## Case Scenario II

###  Q6: Most Valuable Customers (by Sales & Profit)

```sql
SELECT customer_name, SUM(sales) AS total_sales, SUM(profit) AS total_profit
FROM public.orders
GROUP BY customer_name
ORDER BY total_sales DESC
LIMIT 5;
```

**Top Customers:**
| Name             | Sales         | Profit      |
|------------------|---------------|-------------|
| Emily Phan       | ₦117,124.44   | ₦34,005.44  |
| Deborah Brumfield| ₦97,433.14    | ₦31,121.22  |

 **Insight:** Emily Phan and Deborah Brumfield are high-value and high-profit customers — ideal for loyalty programs.

---

###  Q7: Small Business Customer with Highest Sales

```sql
SELECT customer_name, SUM(sales) AS total_sales
FROM public.orders
WHERE customer_segment = 'Small Business'
GROUP BY customer_name
ORDER BY total_sales DESC
LIMIT 1;
```

**Answer:**  
Dennis Kane – ₦75,967.59 

---

###  Q8: Corporate Customer with Most Orders

```sql
SELECT customer_name, COUNT(DISTINCT order_id) AS total_orders
FROM public.orders
WHERE customer_segment = 'Corporate'
GROUP BY customer_name
ORDER BY total_orders DESC
LIMIT 1;
```

**Answer:**  
Roy Skaria – 18 Orders 

---

### 🔹 Q9: Most Profitable Consumer Customer

```sql
SELECT customer_name, SUM(profit) AS total_profit
FROM public.orders
WHERE customer_segment = 'Consumer'
GROUP BY customer_name
ORDER BY total_profit DESC
LIMIT 1;
```

**Answer:**  
Emily Phan – ₦34,005.44 

---

###  Q10: Returned Customers and Segment

```sql
SELECT customer_name, customer_segment, COUNT(*) AS return_count
FROM public.orders
WHERE status = 'Returned'
GROUP BY customer_name, customer_segment
ORDER BY return_count DESC;
```

**Top Returned:**
| Name            | Segment     | Returns |
|-----------------|-------------|---------|
| Erin Creighton  | Corporate   | 10      |
| Darren Budd     | Consumer    | 10      |

---

###  Q11: Is Shipping Cost Aligned with Priority?

```sql
SELECT order_priority, ship_mode, AVG(shipping_cost) AS avg_cost
FROM public.orders
GROUP BY order_priority, ship_mode
ORDER BY order_priority, avg_cost DESC;
```

**Insight:**  
Delivery Truck has the **highest average cost across all order priorities**, including Critical. Express Air (fastest) is **underutilized**.

 **Recommendation:** Revisit shipping policies. Assign faster methods to critical orders and balance cost for low-priority ones.

---



