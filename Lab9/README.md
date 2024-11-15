## Diseño e implementación de una arquitectura de microservicios


***Dividiendo el Monolito en Microservicios***

***Usuarios***

 - Se encarga de toda la info de usuarios: perfiles, logins, y permisos.
 
 - Tiene su propia base de datos y una API para que otros servicios validen usuarios sin tener que saber todos los detalles.

***Catálogo de Productos***

 - Lleva el control de los productos: nombres, precios, descripciones, categorías y stock.

 - Cada vez que se haga un pedido, actualiza el inventario y permite que otros servicios consulten la disponibilidad.

***Pedidos***

 - Maneja todo el proceso de compra: desde agregar al carrito hasta el pago y seguimiento del pedido.

 - Coordina con el catálogo para confirmar existencias y el servicio de usuarios para verificar la identidad del comprador.

***Atención al Cliente***

 - Gestiona consultas, quejas y devoluciones a través de tickets.

 - Conecta con pedidos para obtener historial y con usuarios para saber quién es el cliente. También podría usar bots para respuestas rápidas.


***1. Análisis Inicial***

***Entender el monolito:*** 

Mapea las funcionalidades clave (usuarios, productos, pedidos, soporte, etc.).

***Identificar límites:*** 

Divide por dominios (lo que hace cada parte) y define qué microservicios serán independientes.

***Priorizar:*** 

Empieza con servicios que puedan ser separados sin afectar demasiado al resto.


***2. Crear una Base para Microservicios***

***Infraestructura:*** 

Configura contenedores (Docker) y orquestación (Kubernetes o similar).

***Comunicación:*** 

Define cómo hablarán los microservicios (REST o mensajería como RabbitMQ).

***Seguridad:***

Implementa autenticación compartida (JWT o OAuth).

***3. Descomponer el Monolito Paso a Paso***

***Gestión de Usuarios***

 - Separa todo lo relacionado con perfiles, autenticación y permisos.
 - Asegúrate de que otros servicios puedan consultar datos de usuarios sin problemas.

***Catálogo de Productos***

 - Migra todo lo de productos (detalles, inventario, búsqueda).
 - Haz que el monolito consulte este microservicio mientras se integra.

***Procesamiento de Pedidos***

 - Maneja carritos, pagos y estados de pedidos.
 - Coordina con el catálogo para actualizar inventarios.

***Atención al Cliente***

 - Mueve las consultas y devoluciones, y conéctalo con usuarios y pedidos.

***4. Migración de Datos***

 - Divide las bases: Cada microservicio necesita su base de datos.
 - Sincronización: Usa eventos para mantener datos actualizados mientras migras.

***5. Monitoreo y Optimización***
 
 - Monitoreo: Configura herramientas como Prometheus para vigilar cada microservicio.
 - Pruebas: Prueba cada servicio de forma aislada y en conjunto.

***6. Apagar el Monolito***

 - Cuando todo esté estable y bien integrado, desactiva las partes del monolito que ya no sean necesarias.


