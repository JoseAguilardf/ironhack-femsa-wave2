## 1. Optimización de consultas SQL
A los participantes se les dan consultas SQL y se les pide que las mejoren basándose en conocimientos teóricos de optimización de bases de datos.

Consultas SQL proporcionadas para optimización:

Consulta de pedidos: recupera pedidos con muchos artículos y calcula el precio total.

      SELECT Orders.OrderID, SUM(OrderDetails.Quantity * OrderDetails.UnitPrice) AS TotalPrice
      FROM Orders
      JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID
      WHERE OrderDetails.Quantity > 10
      GROUP BY Orders.OrderID;

### SOLUCION:

En la tabla Orders, se creará un índice en la columna OrderID para mejorar el rendimiento de la unión con OrderDetails.

***CREATE INDEX idx_orders_orderid ON Orders (OrderID);***

Utilizare un indice compuesto en la tabla OrderDetails para que busque rapidamente en nuestra base de datos, para los registros que coincidan con OrderID.
Este índice permite que la base de datos realice la operación de JOIN con mayor rapidez al unir Orders y OrderDetails con OrderID.

***CREATE INDEX idx_orderdetails_orderid_quantity_unitprice ON OrderDetails (OrderID, Quantity, UnitPrice);***

## 2. Consulta de cliente: encuentre todos los clientes de Londres y ordene por nombre de cliente.

      SELECT CustomerName FROM Customers WHERE City = 'London' ORDER BY CustomerName;

### SOLUCION:
Crear un indice para la columna City y otro para la columna CustomerName, para que la consulta busque rápidamente los registros que coinciden.


***CREATE INDEX idx_customers_city ON Customers(City);
CREATE INDEX idx_customers_customername ON Customers(CustomerName);***

## 3. Los participantes optimizarán teóricamente las consultas NoSQL proporcionadas, centrándose en la recuperación eficiente de datos y la latencia minimizada.

Consultas NoSQL para revisión:

Consulta de publicaciones de usuario: recupera las publicaciones activas más populares y muestra su título y número de “Me gusta”.

      db.posts
      .find({ status: "active" }, { title: 1, likes: 1 })
      .sort({ likes: -1 });

### SOLUCION:

Un indice compuesto ayudará tanto la condición de busqueda tanto el ordenación 

***db.posts.createIndex({ status: 1 });
db.posts.createIndex({ likes: -1 });***

## 4. Agregación de datos de usuario: resuma la cantidad de usuarios activos por ubicación.

      db.users.aggregate([
      { $match: { status: "active" } },
      { $group: { _id: "$location", totalUsers: { $sum: 1 } } },
      ]);


### SOLUCION:

***db.users.createIndex({ status: 1 });***
