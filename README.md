# OTIF_ABC_Classification
This repository was created to demonstrate the Data Analytics project related to a possible request from a Supply Chain team to analyze the OTIF KPI and, at the same time, check this relevant indicator across Products and Customers classifications using an ABC Analysis.
____________________________________________

## The Challenge / Problem
We just began working in a Supply Chain Analytics team in a recently created company that's begining to see the impact of tracking important KPIs in the field, such as the OTIF indicator (on-time in-full), on service level, providing the best possible answer to customer demands. Also, the company, that has developed a large number of customers and has a great number of products in its portfolio, has just found out that we can segment (or classify) customers and products according to their impacts on delivery metrics with techniques such as ABC analysis. With this, the company wants to see how the OTIF KPI behaves across these classifications (of customers and products): 

### "Are we delivering the best service levels to the customers, and products, that drive our deliveries and revenues the most? Are we concentrating our efforts on the right customers and products?"

So, we receive this challenge: create a way to classify our customers and products using ABC analysis and a way to track the OTIF KPI in a single report/screen. We need to also see how is the OTIF KPI behaving across classifications and for each product and customer.

## The Data
For practical reasons, the data used was collected from Kaggle (https://www.kaggle.com/datasets/ashishyadav1993/atliq-marts-challenge). For the current challenge, we will be using these .csv files as if they were being accessed directly in the company's system (for example, if the company had a data warehouse or datalake) and we were building the ETL process through the use of python scripts.

Now, lets return to the understanding of the data avaliable. There are three datasets that can be accessed through the company's system: a fact table that brings the history of Orders delivered, and two other dimensional tables, one that brings information, such as name and type of product, for each product code and one that brings the names and locations for each customer code. They will be consumed and converted to pandas DataFrame for data manipulation. The Orders table can be joined with the Products table by using the product code as a key and joined with the Customers table by using the customer code as a key.

In the Orders table we have the main information needed to build the OTIF KPI and the ABC Classifications, such as delivered and ordered quantities of the products and delivery and order dates for each Order ID.

## Data Preparation and Modeling
The code bulit is attached to this repository, but we will comment its main steps. Also, here we are commenting the logic behind the ABC classification and the OTIF calculation. The ABC classifiation segments ou products, or customers also in this case, in 3 groups:

A - A small part of our products or customers (usually 20%) that drive the majority of sales (lets say 80% of the volume sold);
B - A intermediary part of our products or customers that drive an intermediary amount of sales (lets say 15% of the volume sold);
C - A large part (the majority) of our products or customers that drive the smallest amount of sales (lets say 5% of the volume sold).

This calculation was inputed in the folowing function:

![image](https://github.com/T1burski/OTIF_ABC_Classification/assets/100734219/58226de2-49ea-494a-b526-751e779ac08f)


So, with this logic, we can see that we can concentrate the most of our efforts in controlling and improving the service level of a small group which has the most impact: group A. This makes management easier the orients better improvement actions in the business.

At the same time, the OTIF KPI, which stands for On-Time In-Full, was calculated firstly by defining a column that compares the quantity delivered with the quantity ordered of the product (if Qty Delivered >= Qty Ordered, then In-Full) and also a column that compares the delivery date with the requested date of delivery (if Delivery Date >= Requested Date, then On-Time).

So, with these columns calculated, we can define e Measure inside Power BI that adjusts the results according to the context and filters applied efficiently. The equations to reach the desired results are as follows:

### In-Full = [Number of Orders In-Full] / [Total Number of Orders]

### On-Time = [Number of Orders On-Time] / [Total Number of Orders]

So,

### OTIF = [On-Time] * [In-Full]

After the data processing in Python, four datasets were produced and imported into Power BI: orders_final (fact table tht brings the orders history), dim_products (dimension table that brings information about the products, joined with the fact table using the product ID), dim_customers (dimension table that brings information about the customers, joined with the fact table using the customer ID), abc_cust (dimension table that brings the customers' ABC classifications, joined with the fact table using the customer ID) and abc_prod (dimension table that brings the products' ABC classifications, joined with the fact table using the product ID). In Power BI, they were conected using star schema logic, which can be viewed in the image below:

![image](https://github.com/T1burski/OTIF_ABC_Classification/assets/100734219/05ea9a40-d6b5-40ca-8167-62fbf5963a2d)



