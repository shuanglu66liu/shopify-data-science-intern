# shopify-data-science-intern

Question 1: Given some sample data, write a program to answer the following: click here to access the required data set

On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 

(1) Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. 

    There are some extreme values of order amount in the provided dataset, which makes the average value abnormally large. 
    Average value is prone to the impace of extreme values and outliers, while these extreme values have smaller impact on 
    median values. Hence, we could use median values instead to summarize the average order amount. 
    
(2) What metric would you report for this dataset?

    The distribution of order amount is right skewed with some extreme values. To avoid the impact of extreme values on 
    calculating mean, I would suggest use median to measure the average order value. 

(3) What is its value?

    the median of order value is $284.


Question 2: For this question you’ll need to use SQL. Follow this link to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

(1) How many orders were shipped by Speedy Express in total?

54.

SELECT count(*) as total FROM Orders where ShipperID in (select ShipperID from Shippers where ShipperName ="Speedy   Express")

(2) What is the last name of the employee with the most orders?

Peacock.

select LastName from Employees where EmployeeID in (SELECT EmployeeID FROM Orders group by EmployeeID order by count(OrderID) desc limit 1)

(3) What product was ordered the most by customers in Germany?

40. 

SELECT ProductID FROM OrderDetails od inner join orders o on od.orderID = o.orderID 
inner join customers c on o.customerID = c.customerID and c.Country ="Germany"
group by ProductID 
order by sum(od.Quantity) desc
limit 1

