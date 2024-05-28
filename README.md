# Lab5
  Implementing and Optimizing Database Queries
  
  Week 2: Code Management and Efficiency
  Implementing and Optimizing Database Queries
  
  Tasks:
  1. SQL Query Optimization
  Participants are given SQL queries and asked to improve them based on theoretical knowledge of database optimization.
  Provided SQL Queries for Optimization:
  Orders Query: Retrieve orders with many items and calculate the total price

    SELECT Orders.OrderID, SUM(OrderDetails.Quantity * OrderDetails.UnitPrice) AS TotalPrice
        FROM Orders
    JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID
    WHERE OrderDetails.Quantity > 10
    GROUP BY Orders.OrderID;

  Propuesta de Solución:
   Creo conveniente la creación de un Indice
    
       CREATE INDEX idx_orderid_ordersdetails ON OrderDetails(OrderID);

     SELECT OrderID , SUM(Quantity * UnitPrice) AS TotalPrice
        FROM OrderDetails 
        WHERE Quantity > 10;

  Dado que a simple vista no ve el porque ir a la otra tabla se optimiza Query
    Customer Query: Find all customers from London and sort by CustomerName.

      SELECT CustomerName FROM Customers WHERE City = 'London' ORDER BY CustomerName;
      
  Propuesta de Solución:
   Creo conveniente la creación de un Indice
      
      CREATE INDEX idx_city ON Customers(City);

2. NoSQL Query Implementation
Participants will optimize provided NoSQL queries theoretically, focusing on efficient data retrieval and minimized latency.
NoSQL Queries for Review:
User Posts Query: Retrieve the most popular active posts and display their title and like count.


2. NoSQL Query Implementation
Participants will optimize provided NoSQL queries theoretically, focusing on efficient data retrieval and minimized latency.
NoSQL Queries for Review:
User Posts Query: Retrieve the most popular active posts and display their title and like count.

        db.posts
          .find({ status: "active" }, { title: 1, likes: 1 })
          .sort({ likes: -1 });
   
     Propuesta de Solución:
   Creo conveniente la creación de un Indice

       db.posts.createIndex({ status: "active" })

   User Data Aggregation: Summarize the number of active users by location.



       db.users.aggregate([
       { $match: { status: "active" } },
       { $group: { _id: "$location", totalUsers: { $sum: 1 } } },
       ]);

    Propuesta de Solución:
   Creo conveniente la creación de un Indice
   
   db.users.createIndex({ status: "active" })
