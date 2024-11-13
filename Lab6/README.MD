## 1. Revise la configuración simulada del pipeline de CI/CD:

***Etapa de construcción:***

	- Confirmación de código: los desarrolladores confirman el código en un sistema de control de versiones, lo que activa el proceso de CI.

	- Creación de imágenes de Docker: los Dockerfiles definen el entorno y las dependencias, y Docker crea una imagen que encapsula la aplicación y su tiempo de ejecución.

***Etapa de prueba:***

	- Pruebas automatizadas: las imágenes de Docker se utilizan para crear contenedores donde se realizan pruebas automatizadas, lo que garantiza que la aplicación se comporte como se espera en un entorno idéntico al de producción.

***Etapa de implementación:***

	- Registro de contenedores: las imágenes de Docker probadas con éxito se etiquetan y se envían a un registro de Docker.

	- Orquestación e implementación: herramientas como Kubernetes o Docker Swarm gestionan la implementación de estas imágenes en contenedores en diferentes entornos, manejando el escalamiento y el equilibrio de carga.

