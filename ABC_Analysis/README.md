# ABC Analysis of Inventory

## Table of Content
* [Introduction](#introduction)
* [Tools](#tools)
* [Approach](#approach)
* [Entity Relationship Diagram](#entity-relationship-diagram)
* [Step by Step ABC Analysis](#step-by-step-abc-analysis)
* [SQL Query & Microsoft Excel Workbook](#sql-query--microsoft-excel-workbook)
* [Results](#results)

## Introduction
ABC analysis is is a popular inventory management technique that categorizes inventory into three segments based on the value or importance of each stock-keeping unit (SKU). It is done to understand which segment of the inventory is most valuable or critical to the business. Through this analysis, organizations can rank their inventory and manage them efficiently.<br>
The value of each of the units or Stock keeping units (SKU) is analyzed and segmented into 3 buckets or segments — ``A``, ``B`` and ``C``.

* **A**: High-value items which represents a smaller portion of the entire inventory. This items being most valued and critical to the business, are closely tracked and managed.

* **B**: Medium-value items are not as critical as segment A items. But these are also tracked and manage.

* **C**: Low-value items which represents a large portion of the entire inventory. This items are not so closely tracked and are managed loosely.

## Tools 
* MySQL
* Microsoft Excel

## Approach
* Calculate the **revenue** of each product and sort it in the descending order.
* Calculate the **cummulative revenue**, **percentage of cummulative revenue** and **percentage of inventory** of each product.
* Based on the **percentage of cummulative revenue**, each product is given a segment - A,B,C.
* Calculate the **total inventory**, **percentage of inventory**, **total revenue**, and **percentage of revenue** of each of the segment.
* For graphical representation, plot **percentage of inventory** in **x-axis** and **percentage of cummulative revenue** in **y-axis**. 

## Entity Relationship Diagram
Two data tables are used:
```products``` and  ```order_details```

![image](https://i.imgur.com/nNRKfRW.png)


## Step by Step ABC Analysis
#  ABC Analysis Using Excel & SQL

ABC analysis is is a popular inventory management technique that categorizes inventory into three segments based on the value or importance of each stock-keeping unit (SKU). It is done to understand which segment of the inventory is most valuable or critical to the business. Through this analysis, organizations can rank their inventory and manage them efficiently.

The value of each of the units or Stock keeping units (SKU) is analyzed and segmented into 3 buckets or segments — A, B and C.

**_A:_** _High-value items which represents a smaller portion of the entire inventory. This items being most valued and critical to the business, are closely tracked and managed._

**_B:_** _Medium-value items are not as critical as segment A items. But these are also tracked and manage._

**_C:_** _Low-value items which represents a large portion of the entire inventory. This items are not so closely tracked and are managed loosely._
![](https://miro.medium.com/v2/resize:fit:700/1*xaUBE5cclaM3YFeEGrsOEA.png)
Image Source: [Oracle Netsuite](https://www.netsuite.com/portal/resource/articles/inventory-management/abc-inventory-analysis.shtml)

ABC Analysis is based on  [**Pareto Principle**](https://corporatefinanceinstitute.com/resources/economics/pareto-principle/). This principle states that 80% of the outcome comes from 20% of the input.

**For example**:

-   80% of revenues come from 20% of the customers
-   80% of the crashes come from 20% of the bugs
-   80% of the result come from 20% of the workers

Similarly, 80% of the revenue or value comes from 20% of the SKUs. So, businesses try to control and manage this 20% of the inventory efficiently to optimize their inventory management, reduce inventory costs, and increase profitability.

# Advantages of ABC Analysis

ABC Analysis allows:

-   To focus on the most valuable items in their storage, management and overall utilization.
-   To make the inventory management more efficient.
-   To save money and resources through proper inventory control.
-   To avoid stock-out or overstocks of the items.

# ABC Analysis using Excel

**Step 1:**  Open the data sets in the Excel. Select the entire data and convert it into a  **Table** from  **Insert > Table**.

![](https://miro.medium.com/v2/resize:fit:700/1*HaMh15han6P1fcRTysh2Ng.png)

**Step 2:** Name the tables as  **Products** and  **Orders**. Select the table > Design > Properties > Table Name.

![](https://miro.medium.com/v2/resize:fit:700/1*Ed77tbxhphhxNfN8sUmDyw.png)

**Step 3:** Use  **VLOOKUP** to get  **UnitPrice** and  **ProductName** column in the  **Orders** table.

> **_Formulas_**:
> 
    ProductName = VLOOKUP([@ProductID],Products, 2,FALSE)
         
    UnitPrice=VLOOKUP([@ProductID],Products,6,FALSE)

![](https://miro.medium.com/v2/resize:fit:700/1*-DDCjDi3VFNPPMC1fmAc0w.png)

**Step 4:**  Calculate  **Revenue.**

> **_Formula_**_:_

    Revenue =[@Quantity]*[@UnitPrice]

![](https://miro.medium.com/v2/resize:fit:700/1*xdwWJLJhnzMLOE76hhWqLg.png)

Step 5: In the  **Orders** table we will have data at a order line level, but we need the  **Revenue** of each product i.e., data at product level. For that copy the  **ProductID** and  **ProductName** columns and paste it in the same sheet after a few columns. Convert it as a table, rename if you want (I have renamed it as ABC_Analysis) and use  **Remove Duplicate** option to get distinct products.

![](https://miro.medium.com/v2/resize:fit:700/1*U97I-vpys0ujm8m3i_MVUw.png)

**Step 6:**  Calculate the total revenue at product level by adding new column to the product level table we created above.

> **_Formula:_**

    Revenue = SUMIF(Orders[ProductID],[@ProductID],Orders[Revenue])

![](https://miro.medium.com/v2/resize:fit:700/1*wL8UBJ3KCz25GAkIhsuElQ.png)

**Step 7:**  Sort the  **Revenue** in Descending order. Add a column  **Rank** and fill in starting from 1.

![](https://miro.medium.com/v2/resize:fit:534/1*vVHOw7JOGcpxtPBmbAXtgQ.png)

**Step 8:**  Calculate  **Cumulative Revenue, Total Revenue, Cumulative Percentage of Revenue**  for each product.

> **_Formulas_:**
> 

    CumRev =SUM($N$2:N2)
    
    TotalRev =SUM([Revenue])
     
    % of Cum Rev =[@CummRev]/[@TotalRev]
    
    % of Inventory =K2/COUNT($K$2:$K$78)

![](https://miro.medium.com/v2/resize:fit:700/1*gG4Z4uYKwSffNEBWQ-Ghnw.png)

**Step 9:**  Now we will decide the segment for each product based on the cumulative revenue.

> **_Formula:_**

    ABC =IF([@[% of Cum Rev]]<40%,”A”,IF([@[% of Cum Rev]]<70%,”B”,”C”))

> Here, we are giving condition as: Segment A if the  **% of Cum Rev**  is less than 40, Segment B if  **% of Cum Rev**  is less than 70 or else Segment C.

We can use  **Conditional Formatting** to fill color to cells according to the segment.

![](https://miro.medium.com/v2/resize:fit:700/1*PODXYnxIELXzD75mdtYHtA.png)

**Step 10:** After we have segmented the products or inventory, we will conclude our observation by calculating segment level revenue percentage and the percentage of inventory.

After a few blank rows, we will create a  **summary table** where we will calculate  **Count of Inventory, Total Inventory, Total Revenue, % of Inventory** and  **% of Revenue**.

> 

**Formulas:**

    Total Inventory =COUNTIF(Table2[ABC],[@[ABC Segment]])
     
    Total Revenue =SUMIF(Table2[ABC],[@[ABC Segment]],Table2[Revenue])
    
    % of Inventory =[@[Count of Inventory]]/COUNT($K$2:$K$78)
     
    % of Revenue =[@[Total Revenue]]/SUM(Table2[Revenue])

![](https://miro.medium.com/v2/resize:fit:699/1*XLPz6IaX5yP_4ztqSER7Pg.png)

**Step 11:**  Finally, we can create a graph. Plot  **% of Inventory in x-axis** and  **% of Cum Rev in y-axis** from product level table.

![](https://miro.medium.com/v2/resize:fit:700/1*UOQxRnbqdTLasHMbt-WkFQ.png)

![](https://miro.medium.com/v2/resize:fit:700/1*TL5j_0wSBvdaAcgKPE32sA.png)

**Final Analysis View**

![](https://miro.medium.com/v2/resize:fit:700/1*9jMV9tCJWeQBUE8jfEkU5Q.png)
![](https://miro.medium.com/v2/resize:fit:700/1*9jMV9tCJWeQBUE8jfEkU5Q.png)

# ABC Analysis using SQL

**Step 1:**  Analyze the data.

        -- Product and Orders 
    SELECT * FROM products;
    SELECT * FROM order_details;

![](https://miro.medium.com/v2/resize:fit:696/1*1F4cgiqozIWll3Dc88IZBQ.png)

![](https://miro.medium.com/v2/resize:fit:356/1*ITsCOPEoyBCxyCwIoU_nGQ.png)

**Step 2:** Calculate the revenue of each product and rank the products in descending order of revenue.

    -- Calculate the revenue of each product and rank the products in descending order of revenue
    
    SELECT
    
    DENSE_RANK() OVER(ORDER BY ROUND(SUM(od.Quantity*p.Price),2) DESC) AS Product_Rank_by_Revenue,
    
    p.ProductID, p.ProductName,
    
    ROUND(SUM(od.Quantity*p.Price),2) AS 'Revenue'
    
    FROM order_details od
    
    LEFT JOIN products p
    
    ON od.ProductID = p.ProductID
    
    GROUP BY p.ProductID, p.ProductName;
    

![](https://miro.medium.com/v2/resize:fit:560/1*ntVkgvC3tFp-JlJs4RwnNQ.png)

**Step 3:** Calculate Cumulative Revenue, Total Revenue, Cumulative Percentage of Revenue for each product.
-- Calculate Cumulative Revenue, Total Revenue, Cumulative Percentage of Revenue for each product

    WITH Cumulative AS
    
    (SELECT
    
    DENSE_RANK() OVER(ORDER BY ROUND(SUM(od.Quantity*p.Price),2) desc) AS Product_Rank_by_Revenue,
    
    p.ProductID, p.ProductName,
    
    ROUND(SUM(od.Quantity*p.Price),2) AS 'Revenue'
    
    FROM order_details od
    
    LEFT JOIN products p
    
    ON od.ProductID = p.ProductID
    
    GROUP BY p.ProductID, p.ProductName)
    
    SELECT Product_Rank_by_Revenue, ProductID, ProductName, Revenue,
    
    SUM(Revenue) OVER(ORDER BY Revenue DESC) AS Cumulative_Revenue,
    
    SUM(Revenue) OVER() AS Total_Revenue,
    
    ROUND(100*SUM(Revenue) OVER(ORDER BY Revenue DESC)/SUM(Revenue) OVER(),2) AS Cumulative_Percentage_of_Revenue,
    
    ROUND(100*Product_Rank_by_Revenue/(SELECT COUNT(*) FROM products),2) AS Cumulative_Percentage_of_Inventory
    
    FROM Cumulative;

![](https://miro.medium.com/v2/resize:fit:700/1*MtTwDnqXsVoZ7ivrK_SJ-A.png)

**Step 4:** Calculate the segment A,B,C based on the Cumulative Revenue.
-- Calculate the segment A,B,C based on the Cumulative Revenue

    WITH ABC_Analysis AS
    
    (WITH Cummulative AS
    
    (SELECT
    
    DENSE_RANK() OVER(ORDER BY ROUND(SUM(od.Quantity*p.Price),2) desc) AS Product_Rank_By_Revenue,
    
    p.ProductID, p.ProductName,
    
    ROUND(SUM(od.Quantity*p.Price),2) AS 'Revenue'
    
    FROM order_details od
    
    LEFT JOIN products p
    
    ON od.ProductID = p.ProductID
    
    GROUP BY p.ProductID, p.ProductName)
    
    SELECT Product_Rank_By_Revenue, ProductID, ProductName, Revenue,
    
    SUM(Revenue) OVER(ORDER BY Revenue DESC) AS Cumulative_Revenue,
    
    SUM(Revenue) OVER() AS Total_Revenue,
    
    ROUND(100*SUM(Revenue) OVER(ORDER BY Revenue DESC)/SUM(Revenue) OVER(),2) AS Cumulative_Percentage_of_Revenue,
    
    ROUND(100*Product_Rank_By_Revenue/(SELECT COUNT(*) FROM products),2) AS Cumulative_Percentage_of_Inventory
    
    FROM Cumulative)
    
    SELECT
    
    Product_Rank_By_Revenue, ProductID, ProductName, Revenue,
    
    Cumulative_Revenue, Total_Revenue, Cumulative_Percentage_of_Revenue, Cumulative_Percentage_of_Inventory,
    
    IF(Cumulative_Percentage_of_Revenue<40,'A',IF(Cumulative_Percentage_of_Revenue<70,'B','C')) AS ABC
    
    FROM ABC_Analysis;

![](https://miro.medium.com/v2/resize:fit:700/1*XNy_61M8zEzTFDoK3dzGSw.png)

**Step 5:** Calculate the Percentage of Revenue and Percentage of Inventory.

    -- Calculate the Percentage of Revenue and Percentage of Inventory
    
    WITH Count_of_Inventory AS (WITH ABC_Analysis AS
    
    (WITH Cumulative AS
    
    (SELECT
    
    DENSE_RANK() OVER(ORDER BY ROUND(SUM(od.Quantity*p.Price),2) desc) AS Product_Rank_By_Revenue,
    
    p.ProductID, p.ProductName,
    
    ROUND(SUM(od.Quantity*p.Price),2) AS 'Revenue'
    
    FROM order_details od
    
    LEFT JOIN products p
    
    ON od.ProductID = p.ProductID
    
    GROUP BY p.ProductID, p.ProductName)
    
    SELECT Product_Rank_By_Revenue, ProductID, ProductName, Revenue,
    
    SUM(Revenue) OVER(ORDER BY Revenue DESC) AS Cumulative_Revenue,
    
    SUM(Revenue) OVER() AS Total_Revenue,
    
    ROUND(100*SUM(Revenue) OVER(ORDER BY Revenue DESC)/SUM(Revenue) OVER(),2) AS Cumulative_Percentage_of_Revenue,
    
    ROUND(100*Product_Rank_By_Revenue/(SELECT COUNT(*) FROM products),2) AS Cumulative_Percentage_of_Inventory
    
    FROM Cumulative)
    
    SELECT
    
    Product_Rank_By_Revenue, ProductID, ProductName, Revenue,
    
    Cumulative_Revenue, Total_Revenue, Cumulative_Percentage_of_Revenue, Cumulative_Percentage_of_Inventory,
    
    IF(Cumulative_Percentage_of_Revenue<40,'A',IF(Cumulative_Percentage_of_Revenue<70,'B','C')) AS ABC_Segment
    
    FROM ABC_Analysis)
    
    SELECT
    
    ABC_Segment, COUNT(ProductID) AS Total_Inventory,
    
    ROUND(SUM(Revenue),2) AS Total_Revenue,
    
    ROUND(100*COUNT(ProductID)/(SELECT COUNT(*) FROM products),0) AS Percentage_of_Inventory,
    
    ROUND(100*SUM(Revenue)/(SELECT ROUND(SUM(od.Quantity*p.Price),2) FROM order_details od
    
    LEFT JOIN products p
    
    ON od.ProductID = p.ProductID),2) AS Percentage_of_Revenue
    
    FROM Count_of_Inventory
    
    GROUP BY ABC_Segment;

![](https://miro.medium.com/v2/resize:fit:700/1*N-AXrGGT8B2JnK9-v53jYg.png)

# Conclusion

Using both Excel and SQL we get similar result as the process we implemented is same.  **_We observe that around 37% of the revenue is generated from 8% of the inventory._**
# Dataset & GitHub Link

[https://github.com/mukulgehlot/SQL-Projects/tree/main/ABC_Analysis](https://github.com/ritusantra/SQL-Projects/tree/main/ABC_Analysis)

# Reference

-   [https://www.netsuite.com/portal/resource/articles/inventory-management/abc-inventory-analysis.shtml](https://www.netsuite.com/portal/resource/articles/inventory-management/abc-inventory-analysis.shtml)
-   [https://www.erp-information.com/abc-analysis.html#What_is_an_ABC_Analysis_in_Inventory_Management](https://www.erp-information.com/abc-analysis.html#What_is_an_ABC_Analysis_in_Inventory_Management)

## SQL Query & Microsoft Excel Workbook
* [SQL Query](https://github.com/ritusantra/SQL-Projects/blob/main/ABC_Analysis/ABC_2.sql)
* [Microsoft Excel Workbook](https://github.com/ritusantra/SQL-Projects/blob/main/ABC_Analysis/ABC%20Analysis%20Final.xlsx)

## Results
* ABC Analysis using SQL
  
  ![image](https://github.com/ritusantra/SQL-Projects/assets/75059347/eafb543b-92ee-4c88-b25d-6db0a8d990ce)

* ABC Analysis using Microsoft Excel
  
  ![image](https://github.com/ritusantra/SQL-Projects/assets/75059347/c1fa3f9d-06dd-4169-8cee-15e87212c9d3)
