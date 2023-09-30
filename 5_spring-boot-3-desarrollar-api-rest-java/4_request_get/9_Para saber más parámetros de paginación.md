Como aprendimos en videos anteriores, por defecto, los parámetros utilizados para realizar la paginación y el ordenamiento deben llamarse page, size y order. Sin embargo, Spring Boot permite modificar los nombres de dichos parámetros a través de la configuración en el archivo application.properties.

Por ejemplo, podríamos traducir al español los nombres de estos parámetros con las siguientes propiedades:

spring.data.web.pageable.page-parameter=pagina
spring.data.web.pageable.size-parameter=tamano
spring.data.web.sort.sort-parameter=ordenCOPIA EL CÓDIGO
Por lo tanto, en solicitudes que usen paginación, debemos usar estos nombres que fueron definidos. Por ejemplo, para listar los médicos de nuestra API trayendo solo 5 registros de la página 2, ordenados por email y en orden descendente, la URL de solicitud debe ser:

http://localhost:8080/medicos?tamano=5&pagina=1&orden=email,desc