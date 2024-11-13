## Análisis de la integración de Docker en CI/CD

***Revise la configuración simulada del pipeline de CI/CD:***

***Etapa de construcción:***

- Confirmación de código: los desarrolladores confirman el código en un sistema de control de versiones, lo que activa el proceso de CI.
- Creación de imágenes de Docker: los Dockerfiles definen el entorno y las dependencias, y Docker crea una imagen que encapsula la aplicación y su tiempo de ejecución.

***Etapa de prueba:***

- Pruebas automatizadas: las imágenes de Docker se utilizan para crear contenedores donde se realizan pruebas automatizadas, lo que garantiza que la aplicación se comporte como se espera en un entorno idéntico al de producción.

***Etapa de implementación:***

- Registro de contenedores: las imágenes de Docker probadas con éxito se etiquetan y se envían a un registro de Docker.
- Orquestación e implementación: herramientas como Kubernetes o Docker Swarm gestionan la implementación de estas imágenes en contenedores en diferentes entornos, manejando el escalamiento y el equilibrio de carga.

## Mejoras

***Etapa de Construcción***

- Consistencia total: Docker elimina "funciona en mi máquina" porque todos usamos el mismo entorno.
- Arranque rápido: Con Dockerfiles listos, levantar el entorno no toma nada, lo que nos ahorra tiempo en configuración.

***Etapa de Pruebas***

- Pruebas idénticas a producción: Corremos las pruebas en contenedores que son iguales a producción, así encontramos problemas antes de que lleguen allá.
- Aislamiento de tests: Cada prueba corre en su propio contenedor, así que si una falla, no afecta a las demás y es fácil ubicar el problema.

***Etapa de Implementación***
- Escalar fácil: Con Kubernetes o Swarm, solo lanzamos más contenedores y listo, ya está escalado.
- Despliegue seguro y rápido: Solo subimos imágenes probadas y etiquetadas al registro, así el despliegue a producción es controlado y sin sorpresas.

## Posibles Problemas

- Las imágenes pueden traer vulnerabilidades ocultas en las librerías base, así que necesitamos escanearlas constantemente para evitar sorpresas feas.

- Aunque ayuda a orquestar los contenedores, Kubernetes no es nada simple; tiene su propia curva de aprendizaje y, si no se configura bien, puede darnos más trabajo que soluciones.

- Si lanzamos muchos contenedores para pruebas y despliegues, el servidor se puede saturar y hacernos sufrir con el rendimiento. Hay que configurar bien el uso de CPU y memoria.

- Las imágenes de Docker se quedan viejas rápido, y hay que estar actualizando dependencias y el sistema base todo el tiempo, si no queremos problemas de compatibilidad.

