# OTIF_ABC_Classification
This repository was created to demonstrate the Data Analytics project related to a possible request from a Supply Chain team to analyze the OTIF KPI and, at the same time, check this relevant indicator across Products and Customers classifications using an ABC Analysis.
____________________________________________

## The Challenge / Problem
We just began working in a Supply Chain Analytics team in a recently created company that's begining to see the impact of tracking important KPIs in the field, such as the OTIF indicator (on-time in-full), on service level, providing the best possible answer to customer demands. Also, the company, that has developed a large number of customers and has a great number of products in its portfolio, has just found out that we can segment (or classify) customers and products according to their impacts on delivery metrics with techniques such as ABC analysis. With this, the company wants to see how the OTIF KPI behaves across these classifications (of customers and products): 

### "Are we delivering the best service levels to the customers, and products, that drive our deliveries and revenues the most? Are we concentrating our efforts on the right customers and products?"

So, we receive this challenge: create a way to classify our customers and products using ABC analysis and a way to track the OTIF KPI in a single report/screen. We need to also see how is the OTIF KPI behaving across classifications and for each product and customer.

## The Data
For practical reasons, the data used was collected from Kaggle (https://www.kaggle.com/datasets/ashishyadav1993/atliq-marts-challenge). For the current challenge, we will be using these .csv files as if they were being accessed directly in the company's system (for example, if the company had a data warehouse or datalake) and we were building the ETL process through the use of python scripts.

Now, lets return to the understanding of the data avaliable. There are three datasets that can be accessed through the company's system: a fact table that brings the history of Orders delivered, and two other dimensional tables, one that brings information, such as name and type of product, for each product code and one that brings the names and locations for each customer code.
The Orders table can be joined with the Products table by using the product code as a key and joined with the Customers table by using the customer code as a key.
