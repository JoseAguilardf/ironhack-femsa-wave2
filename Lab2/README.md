## Existen varias violaciones a los principios SOLID.

**Single Responsibility Principle (SRP):**

En el caso de SystemManager, la clase tiene múltiples responsabilidades:
    
  1. Verificar inventario.
  2. Procesar pagos (estándar y exprés).
  3. Actualizar el estado de la orden en la base de datos.
  4. Notificar al cliente.

Estas responsabilidades podrían dividirse en clases separadas (InventoryService, PaymentService, OrderService, NotificationService) para que cada una tenga un único propósito.


**Open/Closed Principle (OCP):**

Este principio sugiere que una clase debe estar abierta para extensión pero cerrada para modificación. SystemManager tiene lógica condicional (if-else) basada en el tipo de pedido (order.type), lo cual implica que si se agrega un nuevo tipo de pedido (por ejemplo, "priority"), se tendría que modificar la clase para manejar ese nuevo tipo.

Para cumplir con OCP, podríamos crear una interfaz o una clase base para el procesamiento de pedidos (OrderProcessor).


***Interface Segregation Principle (ISP):***

Este principio establece que las clases no deben depender de interfaces que no utilizan. Aunque en este ejemplo no se ven interfaces directamente, SystemManager depende de múltiples servicios (paymentService, expressPaymentService, database, emailService) que podrían tener interfaces más específicas y separadas.

Dividir estas responsabilidades en diferentes clases y servicios ayudaría a que SystemManager solo dependa de los métodos necesarios para cada función, evitando dependencias innecesarias.

***Dependency Inversion Principle (DIP):***

El principio de inversión de dependencias sugiere que las clases de alto nivel no deben depender de clases de bajo nivel, sino de abstracciones. SystemManager hace uso directo de instancias específicas como paymentService, expressPaymentService, database, y emailService. Esto crea una dependencia directa en clases concretas, lo que dificulta cambiar las implementaciones de estos servicios.

Para cumplir con DIP, podríamos inyectar interfaces de servicios a través del constructor o mediante inyección de dependencias, permitiendo que SystemManager dependa de abstracciones en lugar de implementaciones concretas.


***Liskov Substitution Principle (LSP):*** 

Este principio se aplica implícitamente ya que cualquier clase que implemente la interfaz OrderProcessor puede ser sustituida sin cambiar la corrección del programa
