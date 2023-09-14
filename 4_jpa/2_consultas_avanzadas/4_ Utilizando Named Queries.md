[00:00] Hola, en esta parte vamos a hablar sobre otro recurso de JPA, que son las namedQuery que son consultas que se encuentran dentro de la entidad, entonces nosotros tenemos la entidad producto y dentro de nuestra misma entidad, nosotros vamos a crear las consultas que estábamos realizando en la clase Dao.

[00:17] Por lo general, nosotros colocamos todos los accesos a la base de datos dentro del Dao. En este caso particular nosotros podemos colocarlas dentro de la entidad. Entonces vemos las consultas como selectPorId, consultarPorId, consultarTodos, consultarPorNombre, consultarPorNombreDeCategoría y consultarPrecioPorNombreDeProducto.

[00:39] El último método que nosotros utilizamos en la clase de registroDeProducto fue consultarPrecioPorNombreDeProducto, o sea, vamos a trabajar con ese método. En la clase productoDao nosotros vamos a copiar esta consulta, y vamos a ir a la clase de producto. Acá vamos a colocar la notación namedQuery, y vamos a colocarle un sobrenombre a esa consulta.

[01:12] Ese va a ser el sobrenombre con el que JPA va a identificar la consulta. Aquí como es consulta. ¿Cómo se llama el método? Consultar precio por nombre del producto. Vamos a colocar simplemente “consultaDePrecio”. Y el segundo parámetro sería la query o la consulta.

[01:36] Esa query va a ser la consulta que nosotros estamos realizando en el Dao. Entonces, ya esa forma tenemos los dos parámetros de la anotación. Ahora podemos remover esa consulta y vamos a reemplazar el método createQuery por el método createNameQuery.

[02:03] Nos está solicitando dos parámetros, el primero, que es el sobrenombre con el que podemos identificarla, sería consultaDePrecio. Vamos a colocar el sobrenombre y el segundo parámetro es el retorno de esa consulta. En este caso es BigDecimal.class.

[02:24] “ConsultaDePrecio”. Entonces, ya tenemos nuestro método de nuevo funcionando, solo falta hacer la mencionar que generalmente es como un estándar identificar de dónde estaba proviniendo ese sobrenombre o esa consulta, vamos a namedQuery, colocando el nombre de la entidad, antes del sobrenombre.

[02:59] Entonces vamos a colocar “Producto.consultaDePrecio”, de la misma forma en la consulta. Aquí sería “Producto.consultaDePrecio”. Entonces, está funcionando igual de los dos lados.

[03:20] Creamos la consulta, vamos a la clase de registroDeProducto, vamos a ver si esto continúa funcionando. Guardamos los cambios. Y vemos que el método está funcionando correctamente. Entonces es otro recurso de JPA las namedQuery.

[03:40] En la siguiente, en la siguiente parte vamos a ver cómo mejorar el performance o el desempeño de nuestra aplicación. Y eso fue todo por la parte de consultas.