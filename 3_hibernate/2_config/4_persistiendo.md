[00:00] Hola. En este punto ya nosotros hemos creado las características básicas de nuestro proyecto, agregamos a las dependencias la dependencia de Hibernate con JPA, agregamos de la dependencia de la base de datos h2, configuramos esta base datos con el archivo persistence.xml, donde configuramos las propiedades básicas de la base de datos, como son contraseña, usuario, los controladores.

[00:23] Y por último agregamos nuestra primera entidad para la tabla producto, donde colocamos los atributos básicos. Ahora nosotros vamos a hacer nuestro primer modelo de persistencia, que nos va a permitir guardar o registrar estos valores en la base de datos.

[00:43] Para eso nosotros vamos a las características básicas de JPA, vamos a crear un entityManager íbamos instanciar también nuestro primer producto. Vamos a comenzar en el panel de la izquierda, vamos a ir a la carpeta tienda, seleccionamos clic derecho, vamos a nuevo, nueva clase, y a esa clase le voy a poner RegistroDeProducto.

[01:07] El paquete no va a ser modelo sino prueba, es que aquí vamos a hacer todas las pruebas para nuestras transacciones y vamos a seleccionar la opción de clase main.

[01:18] Seleccionamos finalizar y ya con esto tenemos generada nuestra primera clase main, donde vamos a registrar toda las clases. Ahora falta instanciar nuestro primer producto. Para eso colocamos producto, indicar el tipo, vamos a colocar el nombre de esa instancia que va a ser celular y vamos a llamar la palabra clave nuevo producto.

[01:42] Ya con eso tenemos instanciado nuestro primer producto, importamos la clase y falta configurar las propiedades de los valores de esos atributos. Entonces para eso colocamos el nombre de la entidad que es celular, llamamos el setNombre y vamos a colocar aquí “Samsung”.

[02:06] La siguiente propiedad que tenemos que configurar es la descripción, vamos a suponer que esa tienda vende teléfonos usados. Entonces, vamos a colocar acá “teléfono usado”. Y por último está faltando el precio. Entonces, tenemos que colocar el setter para el precio: setPrecio.

[02:30] Como el precio tenía el tipo bigDecimal tenemos que instanciar un bigDecimal aquí adentro, bigDecimal. El valor para ese precio va a ser “1000”. Importamos y ya tenemos nuestro primer producto instanciado. Entonces ahora nosotros vamos a ir a la parte donde instanciamos el gerenciador de entidades que es el que nos va a permitir realizar todas las operaciones con la base de datos.

[03:06] Entonces recordando que en JDBC nosotros teníamos una clase. Era la clase connection que nos permitía conectar con la base de datos. Luego de eso nosotros hacíamos las consultas en el lenguaje SQL, lenguaje especial de consultas en base de datos y por último teníamos que cerrar la conexión.

[03:30] Nosotros con JPA tenemos algo bastante similar, que es el EntityManager. El EntityManager es el encargado de realizar todas esas operaciones. Entonces cada vez que nosotros queramos guardar, seleccionar algún elemento de la base de datos, nosotros lo vamos a hacer a través de esta interfase.

[03:52] Nosotros tenemos que colocarle un nombre a este interfase que va hacer em y generalmente nosotros instanciamos con la palabra clave new, pero como esta es una interfase, ella va a recibir valores de otras claves. Ninguna interfaz en Java se instancia a partir de la palabra clave new.

[04:11] Entonces pensando en esto se creó una otra clase, que es la clase EntityManagerFactory que nos permite crear una clase que va a ser guardada dentro de esa interfase. A este EntityManagerFactory le vamos a llamar Factory. Y este es parte de un patrón de diseño que nos permite crear valores o diferentes clases que pueden ser almacenadas dentro de esta interfase.

[04:52] Para esto, nosotros no vamos a usar la palabra clave new, sino vamos a utilizar un método estático que fue creado y que él utiliza el valor de la base de datos que fue colocada en nuestro archivo persistence.xml.

[05:09] Aquí en nosotros tenemos nuestra base de datos y el valor para esa base de datos es el nombre tienda, nosotros lo habíamos colocado. Nosotros vamos a utilizar ese valor. Para eso, nosotros vamos a usar la clase persistence y el método estático createEntityManagerFactory.

[05:28] Él nos está pidiendo el nombre de una entidad y el nombre de esa entidad, como habíamos mencionado, sería el valor de tienda. Y ya con esto importamos el entityManagerFactory de JPA colocamos punto y coma, y ya con esto tenemos nuestra clase creada, instanciada, que es con la que vamos a crear nuestro EntityManager.

[05:54] Entonces, a partir de ese factory vamos a llamar el método createEntityManager. Y este va a ser el que va a realmente instanciar una clase que es del tipo EntityManager. Vamos a importar aquí este EntityManager y todo este proceso se hacía antiguamente de forma manual.

[06:15] Ahora fueron creadas estas dos clases, el EntityManagerFactory y el createEntityManagerFactory que realiza estas operaciones por nosotros. Ahora, a partir del entityManager yo puedo comenzar a realizar mi primera persistencia. Entonces, esa persistencia me va a permitir guardar el valor de este producto en la base de datos para persistir.

[06:40] Aquí voy a colocar el valor de la entidad. Sería celular. Ya con esto puedo aceptar por primera vez la clase, a ver si está funcionando correctamente. Está generando un registro. El registro no genera ningún error, entonces aparentemente todo está funcionando correctamente.

[07:07] La siguiente parte, voy a ver cómo agregar en este registro más detalles de las operaciones que se están ejecutando, y voy a ver si en efecto ese valor de celular se está guardando en la base de datos.

