##
# Amazing Superstore Analysis

![](Home-Electronics.jpg)
<br><br>
## Introduction

**Type of Data Set:**  Sales Dataset 

**Stakeholder Requirement / Problem Statement:** The analysis aims to identify areas where the company can improve its performance and productivity, also draw out insight for Improved Decision-Making, Sales and Profitability. 
1. Create a dashboard, do a Show and Tell at the end of the Sprint
2. Create a power point presentation to present the insight and recommendation.
3. Document the insights

**Data Structure:** There are 2 tables in the dataset, which are named <kbd> Listoforders </kbd> and <kbd> Orderbreakdown </kbd>.

**Relationship between the Stakeholder Requirement and the Dataset:** There is a strong relationship between the stakeholder requirement and the dataset considering column like Discount, sales, Profit and category. The dataset is super rich and it’s capable of providing relevant insights.
<br><br>
## Analysis Pipe Line

**Data Source:** SharePoint

**Data Transformation/Cleaning:** Data cleaning and transformation was carried out using Power Query. After scrutinizing all the columns, they were found to be valid and devoid of empty cells and errors. However, it was highly important that I transformed the Discount column to percentage for calculation purposes.

Hence new column and Tables were created, which are listed below
- A calendar table was created, this was achieved by using the <kbd> Min </kbd> and <kbd> Max </kbd> dax function on the <kbd> order date</kbd> from the <kbd>Orderbreakdown Table</kbd>.
- The <kbd>Month and Year columns </kbd> were also created on the <kbd>calendar table </kbd> which were extract of the <kbd>date column </kbd> on the <kbd>calendar table</kbd>.
- A new column was created for <kbd>Cost of Sale</kbd> on the <kbd>Orderbreakdown Table</kbd> by using the formula below
  
   Cost of Sales = Orderbreakdown[Sales] - Orderbreakdown[Profit]

   The formula above is simply “Cost of sales = Sales – profit”

   How the formula is derived is explained below
  
   Sales = Revenue

   Cost of Sales = Selling Price

   Profit = Revenue – Selling price

   **∴ Selling Price = Revenue - Profit**

- Another column was created named <kbd>SP_before_Dis</kbd> which stand for Selling Price Before Discount

   - The formula below is used if the <kbd>discount column</kbd> is in decimals
     
     SP_before_Dis = ( 1 * Orderbreakdown[Sales] ) / ( 1 - Orderbreakdown[Discount] )

   - This formula below is used if the <kbd>discount column</kbd> is in percentage 

     SP_before_Dis = (100 * Orderbreakdown[Sales] ) / ( 100 - Orderbreakdown[Discount] )
     <br><br>
   The above financial formula shows the original selling price before discount is applied, let me break it down to show how we arrived at the above.
   <br><br>
     ![](Formula2.png)

- A column was created for **profit without discount** (<kbd>Profit_B4_Dis </kbd>), this column shows the profitability of the company without applying any discount on sales.

      Cost of sale is Unique and Universal
  
      Profit = Revenue - Selling Price without Discount
  
      Revenue is also knows as sales
  
      Selling Price is also known as cost of sales.
  
      The Formula used is shown below
  
      <kbd> Profit_B4_Dis = Orderbreakdown[SP_before_Dis] - Orderbreakdown[Cost of Sales] </kbd>

 - A column named <kbd>Yes&No</kbd> was created, which state If Discount = 0 return No and If Discount > 0 is to return Yes
 - A Measure Table was created to house the Dax Functions

   ![](Table.png)
   <br><br>
## Data Modelling 

The data provided for this analysis are located on two tables and new a new Calendar table was also created. 
Therefore, an appropriate modelling is required. A Snowflake model is designed with the <kbd>Orderbreakdown Table</kbd> representing the Fact table containing all the day to day activities of the business, the dimension tables are the <kbd>Listoforders Table</kbd> and <kbd>Calendar Table</kbd>

You must understand the snowflake model which will enable you know how to carry out your filters and direction of filter.

   - 	For <kbd>Orderbreakdown Table</kbd> and <kbd>Listoforders Table</kbd> is <kbd>Order ID</kbd>
   - 	For <kbd>Listoforders Table</kbd>  and <kbd>Calendar Table</kbd> is <kbd>Order Date</kbd> and <kbd>Date</kbd> Respectively.
<br><br>
![](Snowflake.png)
<br><br>
## Analysis

Complex Dax functions were employed to solve business problem.

   1. Year on Year Growth is abbreviated as <kbd>YoY_Growth</kbd>
   
      <kbd>YoY_Growth</kbd> = (Current year Profit – Previous Year Profit) divide by Previous Year Profit
      
      The Dax function used to achieve this data manipulation was the <kbd>Divide function</kbd>
      
       <kbd>YoY_Growth</kbd> = <kbd>DIVIDE</kbd> ( (<kbd>[Total Profit] </kbd> - <kbd> [PY_Prof] </kbd>), <kbd> [PY_Prof]</kbd> )
      
  2. **Previous Year profit** was calculated by using **complex Dax function**. A complex dax function is the combination of more than one dax function.
     
     Previous year profit was manipulated using a <kbd>calculate function</kbd>, <kbd>sum function</kbd> and <kbd>dateadd function</kbd> were used as shown below

     <kbd>PY_Prof = CALCULATE([Total Profit], DATEADD('Dimcalendar'[Date],"-1",YEAR))</kbd>

     <kbd>Calculate function</kbd> is a **filter function**, the sum of **Total Profit** is filter by <kbd>date add function</kbd>.

<br><br>
## Visualization, Trends, Patterns & Insight.  

 For Live Visualiztion click here <kbd>[Live-Visualization](https://app.powerbi.com/view?r=eyJrIjoiMzczYjA0YzItYTgzZi00MTk0LTk4ZTYtN2U4MDdjYzk2ZjQ3IiwidCI6IjU0OGU5MDRlLTY2MDEtNGQ0My1iZmY3LTYzZGRlZTRjOWVlNiJ9 )</kbd>
<br><br>
**Home Page**

    

    

