[00:00] Hola a todos, continuamos con el curso de JPA y Hybernate. En esta segunda parte nosotros vamos a ampliar el modelo que iniciamos en la parte anterior.

[00:00] Entonces recordamos que nosotros teníamos un cliente, el cliente Alura que nos solicitó registrar diversos productos en la base de datos clasificados por categoría. Esos productos pueden ser cursos y esas categorías pueden ser lenguajes de programación o diversas otras categorías.

[00:27] Entonces, bueno, aquí en esta diapositiva. Nosotros íbamos a almacenar en la base de datos, una base de datos relacional, se caracteriza por tener un esquema. Íbamos a almacenar nuestros productos, ese producto iba a tener un ID, un hombre, una descripción, un precio, la fecha de registro de ese producto o de ese curso y un elemento que nos permitía relacionar ese producto con la categoría que iba a ser el ID.

[00:56] Entonces en la tabla categoría nosotros íbamos a tener el ID y el nombre. Ese atributo de la tabla categoría ID lo íbamos a insertar dentro de la tabla productos como categoría ID y de esta forma nosotros relacionábamos la tabla producto con la tabla categoría. Entonces vemos aquí que tenemos varias tablas productos relacionadas con un único elemento de categoría.

[01:23] Entonces, de esta forma nosotros expresamos many, de muchos, a una única categoría. Esa categoría vamos a decir que sea libros, entonces tenemos la categoría de libros relacionada a muchos, muchos libros que pueden ser libros de ciencia, libros del lenguaje, de portugués, libros de inglés, pero tenemos una única categoría y muchos productos.

[01:48] Ahora nosotros vamos a agregar dos nuevas tablas: la tabla cliente y la tabla pedidos. Entonces un cliente realiza múltiples pedidos. Esos múltiples pedidos a su vez van a tener productos, pero no vemos esos elementos acá, eso vamos a hablar más adelante.

[02:05] Lo importante es que esa tabla clientes también se encuentre relacionada con la tabla pedidos a través del ID. Entonces, recordando nuestro código anterior, nosotros habíamos creado un proyecto maven, donde agregamos las dependencias de nuestra aplicación, eran Hybernate con JPA y la base de datos H2.

[02:33] Configuramos la versión de Java que íbamos a utilizar en nuestra aplicación y la versión de Maven encargada de descargar las dependencias, que es 3.8. Aquí en las librerías nosotros vemos que descargamos correctamente la dependencia de Hybernate y otras dependencias necesarias, la dependencia de JPA y la dependencia de la base de datos H2.

[02:55] Posteriormente nosotros en la carpeta de recursos creamos la carpeta META-INF y el archivo persistence.xml. Este este archivo persistence tiene una única unidad de persistencia, ya que nosotros vamos a tener una única base de datos.

[03:09] Si tuviéramos más de una, nosotros tendríamos más de una unidad de persistencia. Configuramos la base de datos para la base de datos, H2 con el controlador, la ruta, el usuario y la contraseña, así como otras propiedades de Hybernate, como las consultas en consola, el formato de esas consultas y la construcción automática de esas tablas y bases de datos.

[03:35] En el curso anterior, nosotros aquí, habíamos colocado el valor update. Quiere decir que si no existían las tablas, él las creaba, y en caso de que existieran, él simplemente actualizaba los registros anteriores.

[03:50] Ahora nosotros vamos a utilizar el valor create and drop. Nosotros vamos a crear los valores y cada vez que nosotros realicemos una ejecución de nuestra aplicación vamos a primero eliminar los registros anteriores y los va a crear nuevamente.

[04:08] Luego de eso, nosotros comenzamos a construir el modelo para nuestra aplicación. Entonces recordamos que cada clase de nuestros modelos va a representar una tabla en la base de datos y eso los vamos a llamar entidades. Ya tenemos la entidad producto, que al igual que en la diapositiva, nosotros teníamos que él tenía una cierta cantidad de atributos, nombre y descripción.

[04:38] Y tenemos la entidad categoría únicamente con el nombre. Esa entidad producto se encontraba relacionada a través del atributo categoría que fue una clase que agregamos. Aquí, en la base, en la tabla, solamente estamos agregando el ID. Aquí en el código nosotros estamos agregando la clase entera.

[05:00] Entonces JPA se encarga de hacer ese procesamiento y de reconocer que el valor que tiene que agregar en la base de datos es el ID de la categoría. Luego para nosotros almacenar eso, teníamos que crear una clase utilitaria donde fabricamos o instanciamos el EntityManager a través de otra clase que era el EntityManagerFactory.

[05:24] El EntityManager es el que nos permite darle acceso a la base de datos. Ese EntityManager fue inyectado como atributo dentro de los DAO, DAO es para el producto y para la categoría, que como su nombre lo dice es Data Access Object. Con él nosotros vamos a tener acceso a la base de datos.

[05:44] Inyectábamos nuestro EntityManager como atributo y realizamos algunas de las operaciones de acceso a la base de datos como guardar, actualizar un registro, eliminar un registro existente o a consulta por nombre del producto. Nosotros podemos consultar, en este caso sería consulta por el nombre de la categoría.

[06:06] También podemos consultar todos los elementos. Aquí tenemos consultar todos los elementos, consultar por ID y otros tipos de consulta. En esta segunda parte del curso nosotros vamos a realizar algunas consultas más un poco más avanzadas y también vamos a ver cómo mejorar el performance o el desempeño en esta aplicación, ya que a medida que crece la aplicación van a haber más cantidades de registro ocupando más memoria y la velocidad de búsqueda se va viendo reducida.

[06:42] Entonces, es importante tener una buena estrategia a la hora de desarrollar nuestra aplicación, para tener una buena aplicación con buen performance. Nos vemos en la siguiente clase.