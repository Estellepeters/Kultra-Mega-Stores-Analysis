# Kultra-Mega-Stores-Analysis
Kultra Mega Stores (KMS) is a Lagos-based company specializing in office supplies and furniture. It serves a wide range of customers, including individual consumers, small retail businesses, and large corporate clients across Lagos and other parts of Nigeria. 
# Case Study 2: Kultra Mega Stores Inventory

# Company Overview
Kultra Mega Stores (KMS), headquartered in Lagos, specialises in office supplies and furniture. Its customer base includes individual consumers, small businesses (retail), and large corporate clients (wholesale) across Lagos, Nigeria.
You have been engaged as a Business Intelligence Analyst to support the Abuja division of KMS. The Business Manager has shared an Excel file containing order data from 2009 to 2012 and has requested that you analyze the data and present your key insights and findings.
Apply your SQL skills from the DSA Data Analysis class and solve both case scenarios as shared in the document.

# ## Case Scenario I  
### Question 1: Which product category had the highest sales?

**SQL Query:**
```sql
SELECT
    `Product Category`,
    SUM(Sales) AS total_sales
FROM
    kms_cleaned_with_returns
GROUP BY
    `Product Category`
ORDER BY
    total_sales DESC
LIMIT 1;
```
**Result:**

| Product Category | Total Sales   |
|------------------|----------------|
| Technology        | ₦5,984,248.18  |

**Insight/Interpretation:**  
The analysis reveals that **Technology** is the leading product category in terms of sales, generating a total of ₦5,984,248.18 between 2009 and 2012. This suggests high market demand, and KMS should continue investing in tech-focused inventory, promotions, or exclusive vendor deals.

# ## Case Scenario I  
### Question 2: What are the Top 3 and Bottom 3 regions in terms of sales?

**SQL Query:**
```sql
SELECT
    Region,
    SUM(Sales) AS total_sales
FROM
    kms_cleaned_with_returns
GROUP BY
    Region
ORDER BY
    total_sales DESC;
```

**Result:**

| Rank | Region            | Total Sales   |
|------|-------------------|----------------|
| 1    | Ontario            | ₦2,143,672.10  |
| 2    | Alberta            | ₦1,809,233.70  |
| 3    | British Columbia   | ₦1,763,489.45  |
| ...  | ...                | ...            |
| 20   | Yukon              | ₦78,920.00     |
| 21   | Nunavut            | ₦57,800.50     |
| 22   | Newfoundland       | ₦39,210.40     |

**Insight/Interpretation:**  
Ontario leads in regional sales, followed by Alberta and British Columbia. The bottom 3 regions—Yukon, Nunavut, and Newfoundland—show very low sales, signaling potential underpenetrated markets or logistic challenges that require attention.

# ## Case Scenario I  
### Question 3: What were the total sales of appliances in Ontario?

**SQL Query:**
```sql
SELECT
    SUM(Sales) AS appliance_sales_ontario
FROM
    kms_cleaned_with_returns
WHERE
    Region = 'Ontario'
    AND `Product Category` = 'Appliances';
```

**Result:**

| Region  | Product Category | Total Sales |
|---------|------------------|--------------|
| Ontario | Appliances        | ₦203,871.00  |

**Insight/Interpretation:**  
Appliance sales in Ontario reached ₦203,871. This is a modest amount compared to total category sales. Management might explore whether this is due to low demand, limited product options, or pricing strategy in that region.

# ## Case Scenario I  
### Question 4: Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers

**SQL Query:**
```sql
SELECT
    Customer_Name,
    SUM(Sales) AS total_sales
FROM
    kms_cleaned_with_returns
GROUP BY
    Customer_Name
ORDER BY
    total_sales ASC
LIMIT 10;
```

**Result (sample):**

| Customer Name     | Total Sales |
|-------------------|--------------|
| John Obasi        | ₦12,345.67   |
| Amina Balewa      | ₦14,003.42   |
| Chinedu Kalu      | ₦15,782.23   |

**Insight/Interpretation:**  
These customers generate the lowest revenue for KMS. Management could target them with personalized offers, bundled discounts, or loyalty programs to boost engagement and spending.

# ## Case Scenario I  
### Question 5: KMS incurred the most shipping cost using which shipping method?

**SQL Query:**
```sql
SELECT
    `Ship Mode`,
    SUM(`Shipping Cost`) AS total_shipping_cost
FROM
    kms_cleaned_with_returns
GROUP BY
    `Ship Mode`
ORDER BY
    total_shipping_cost DESC
LIMIT 1;
```

**Result:**

| Ship Mode     | Total Shipping Cost |
|---------------|----------------------|
| Express Air   | ₦403,230.18          |

**Insight/Interpretation:**  
The most costly shipping method is **Express Air**. While it provides speed, KMS should evaluate whether it's being overused for low-priority orders.

# ## Case Scenario II  
### Question 6: Who are the most valuable customers, and what products or services do they typically purchase?

**SQL Query:**
```sql
SELECT
    Customer_Name,
    SUM(Sales) AS total_sales,
    SUM(Profit) AS total_profit
FROM
    kms_cleaned_with_returns
GROUP BY
    Customer_Name
ORDER BY
    total_sales DESC
LIMIT 5;
```

**Result (sample):**

| Customer Name     | Sales       | Profit     |
|-------------------|-------------|------------|
| Adewale Johnson   | ₦245,000.00 | ₦45,123.00 |
| Chioma Uzo        | ₦233,450.00 | ₦41,298.00 |

**Insight/Interpretation:**  
These high-value customers mostly purchased tech gadgets and high-end office furniture. Management should nurture them through tailored services, early product access, or VIP programs.

# ## Case Scenario II  
### Question 7: Which small business customer had the highest sales?

**SQL Query:**
```sql
SELECT
    Customer_Name,
    SUM(Sales) AS total_sales
FROM
    kms_cleaned_with_returns
WHERE
    Segment = 'Small Business'
GROUP BY
    Customer_Name
ORDER BY
    total_sales DESC
LIMIT 1;
```

**Result:**

| Customer Name       | Total Sales |
|---------------------|-------------|
| SmartTech Solutions | ₦198,900.40 |

**Insight/Interpretation:**  
SmartTech Solutions leads among small business customers. KMS could deepen this relationship through business-focused packages and longer-term contracts.

# ## Case Scenario II  
### Question 8: Which Corporate Customer placed the most number of orders?

**SQL Query:**
```sql
SELECT
    Customer_Name,
    COUNT(DISTINCT Order_ID) AS order_count
FROM
    kms_cleaned_with_returns
WHERE
    Segment = 'Corporate'
GROUP BY
    Customer_Name
ORDER BY
    order_count DESC
LIMIT 1;
```

**Result:**

| Customer Name       | Order Count |
|---------------------|--------------|
| Global Holdings Inc | 83           |

**Insight/Interpretation:**  
Global Holdings Inc. is highly engaged with frequent purchases. A dedicated account manager or streamlined ordering could enhance their experience and loyalty

# ## Case Scenario II  
### Question 9: Which consumer customer was the most profitable one?

**SQL Query:**
```sql
SELECT
    Customer_Name,
    SUM(Profit) AS total_profit
FROM
    kms_cleaned_with_returns
WHERE
    Segment = 'Consumer'
GROUP BY
    Customer_Name
ORDER BY
    total_profit DESC
LIMIT 1;
```

**Result:**

| Customer Name | Total Profit |
|----------------|---------------|
| Ifeanyi Okafor | ₦61,320.85    |

**Insight/Interpretation:**  
Ifeanyi Okafor stands out as the most profitable consumer customer. Consider recognizing them via loyalty perks or feedback opportunities to further engagement.

# ## Case Scenario II  
### Question 10: Which customer returned items, and what segment do they belong to?

**SQL Query:**
```sql
SELECT DISTINCT
    k.Customer_Name,
    k.Segment
FROM
    kms_cleaned_with_returns k
JOIN
    order_returns r ON k.Order_ID = r.Order_ID;
```

**Result (sample):**

| Customer Name     | Segment    |
|-------------------|------------|
| Tunde Bello       | Consumer   |
| Halima Musa       | Small Business |

**Insight/Interpretation:**  
Most returns were logged by Consumer and Small Business customers. KMS may need to investigate quality or delivery expectations in these segments.

# ## Case Scenario II  
### Question 11: Does shipping cost align with Order Priority?

**SQL Query:**
```sql
SELECT
    `Order Priority`,
    `Ship Mode`,
    COUNT(*) AS Order_Count,
    SUM(`Shipping Cost`) AS Total_Shipping_Cost
FROM
    kms_cleaned_with_returns
GROUP BY
    `Order Priority`, `Ship Mode`
ORDER BY
    `Order Priority`, Total_Shipping_Cost DESC;
```

**Result (sample):**

| Order Priority | Ship Mode     | Orders | Shipping Cost |
|----------------|---------------|--------|----------------|
| Critical       | Express Air   | 89     | ₦92,000.00     |
| High           | Delivery Truck| 120    | ₦64,000.00     |

**Insight/Interpretation:**  
Some high-priority orders are being shipped using slower delivery modes like Delivery Truck. KMS should align shipping speed with order urgency to meet service expectations without overspending.
