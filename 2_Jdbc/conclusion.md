[00:00] Hola. Llegamos al final del curso y aprendimos un montón en el camino, más allá del JDBC para conectar a una base de datos, aprendimos cómo crear un proyecto con el Maven para manejar a sus dependencias. También conocimos algunas librerías que ayudan de forma transparente a realizar operaciones más complejas, como tomar la conexión con la base de datos.

[00:21] ¿Eso lo aprendimos con qué? Con el driver de MySQL y también con el JDBC. Aplicamos buenas prácticas de desarrollo también, y aprendimos algunos patrones de diseño para optimizar la reutilización de nuestro código, como por ejemplo el patrón factory que utilizamos acá en la connectionFactory para tomar conexiones con la base de datos.

[00:40] También aprendimos el patrón DAO, que centraliza las operaciones de acceso a un recurso específico. En nuestro caso, tenemos el recurso de categoría, las tablas de la base de datos, que son la categoría y el producto. Y las clases DAO hacen justamente todo ese manejo de las conexiones de acceso a las fuentes de datos.

[01:03] También aprendimos el modelo de arquitectura MVC, de Model View Controller, que divide las responsabilidades de las aplicaciones en capas específicas para la vista, el modelo y las reglas de negocio.

[01:17] Más allá de los patrones de diseño, aprendimos cómo mantener una buena performance y optimización de recursos de nuestra aplicación a través de la configuración de un pool de conexiones utilizando el C3P0 acá, y lo utilizamos acá en la connectionFactory para crear un dataSource que tiene un pool de conexiones.

[01:39] Aprendimos también el recurso de try with resources, para que no tengamos más que preocuparnos con el manejo de los recursos que abrimos. Entonces el try with resurces utiliza recursos que son de autoClausable que se cierran solos.

[01:53] Entonces este propio try with resources ya lo maneja para nosotros y no tenemos que preocuparnos con estar cerrando las conexiones, los statements, los resultSets. Y por fin aprendimos cómo proteger nuestra aplicación de posibles ataques de SQL injection utilizando los PreparedStatements.

[02:10] Así, nosotros pasamos la responsabilidad para el JDBC manejar todo el contenido de las queries. Aprendimos también cómo evitar el problema de queries N + 1 cuando queremos relacionar más de una tabla para crear un reporte, por ejemplo.

[02:23] Aprendimos acá haciendo un JOIN para no tener que realizar más de una conexión a la base de datos para buscar a todos los recursos que tienen relación entre categoría y producto. Todo eso lo hicimos de una aplicación que fue disponibilizada para agregar acá las funcionalidades y tuvimos un resultado muy bueno.

[02:42] Espero que hayan disfrutado de todo lo que vimos en este curso y puedan seguir aprendiendo aún más con los demás cursos que tenemos aquí a la plataforma. Aprovechen bastante el foro para sacar dudas y compartir conocimientos con los demás también. Muchas gracias por la compañía y nos vemos en la próxima.