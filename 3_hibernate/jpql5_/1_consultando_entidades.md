[00:00] Hola. Y ya llegando al final de nuestro curso en esta parte, nosotros vamos a hablar sobre consultas con JPA. Y en este video nosotros hablar de consultas por id y consultas de todos los elementos en la tabla producto.

[00:14] Para eso vamos a utilizar el EntityManager, vamos a utilizar el DAO para la clase producto y a lo largo de estos últimos videos nosotros vamos a ir agregando los métodos de consulta en el DAO de la clase producto.

[00:27] Recordando que los métodos de consulta sirven tanto para producto como para la categoría o cualquier otra entidad que ustedes estén usando en su proyecto. Volviendo a nuestra clase RegistroDeProducto, voy a eliminar esta parte del código que yo utilicé para explicar los ciclos de vida y las transiciones entre estados y voy a copiar el código donde yo instancié una categoría y el producto para guardar un elemento en la base datos.

[00:55] Entonces aquí voy a importar el producto, voy a importar los DAO y la CategoriaDao. Entonces, si recuerdan yo ya he realizado este código, algunos videos atrás, me importa el BigDecimal, con eso tenemos todo funcionando donde yo guardé un elemento del tipo producto en la base de datos, así como un elemento del tipo categoría.

[01:27] Nosotros instanciamos el producto, instanciamos el EntityManager, instanciamos los DAO para ambos utilizando el método guardar y realizamos la persistencia y con el commit del EntityManager sincronizamos los valores en la base de datos.

[01:41] Realizamos el close y fue cerrado el EntityManager. Ahora yo voy a copiar este código, voy a extraer ese método abstracto y le voy a colocar ese método abstracto registrarProducto. Con eso, yo voy a tener un elemento guardado en la base de datos.

[02:01] Lo siguiente que tengo que hacer instanciar el EntityManager y voy instanciar también el productoDao que lo voy a estar utilizando partir de este momento. Entonces nosotros vamos a estar trabajando con la clase productoDao. El primer método de consulta que vamos a realizar, sería método tipo público, que nos va a retornar una entidad producto y se va a llamar consultaPorId.

[02:32] Normalmente estos métodos son escritos en inglés y nosotros lo vamos a colocar acá en español y tenemos que enviar un parámetro. Ese parámetro tiene que ser un elemento del tipo Long y lo vamos a llamar id.

[02:47] El retorno de este método va a ser un elemento de tipo producto. Para eso, otro a colocar la palabra return, utilizamos el EntityManager, vamos a utilizar el método find que nos está solicitando dos parámetros. El primer parámetro es la entidad a la que vamos a solicitar, ya que existen diversas entidades con las que podemos estar trabajando. En este caso tenemos dos, que es la categoría y el producto.

[03:12] Nosotros tenemos que indicarle que queremos hacer una consulta de la entidad producto, indicando que es una clase y vamos a estar solicitando cuál es la llave primaria o sea, cuál va a ser el código, la posición en la tabla en la que se encuentra este elemento que queremos buscar.

[03:31] Entonces para eso podemos utilizar el id que pasamos como parámetro. Ahora de vuelta en nuestra clase RegistroDeProducto, vamos a usar ese Dao para la clase producto, productoDao y vamos a llamar el método consultaPorId. El id va a ser 1 ya que como nosotros tenemos guardado un único elemento y ese id es auto generado por la base de datos, el primer valor que es generado en la base de datos es el número 1.

[04:03] Entonces vamos a llamar al elemento en la posición 1, eso nos va a retornar un elemento del tipo producto, que lo vamos a llamar producto. Entonces, ya tengo mi consulta guardada en una variable. Vamos a imprimir ese valor utilizando system.out, vamos a colocar aquí system.out, vamos a llamar a ese producto, instancia, y vamos a imprimir el nombre en la consola.

[04:35] Vamos ejecutar la aplicación para ver si está funcionando correctamente, guardamos las alteraciones y efectivamente creamos las tablas, realizo el inserte de ese producto que colocamos en el método estático. Hicimos un select con el id que fue pasado como parámetro, imprimimos en la consola el nombre que sería Xiaomi.

[05:01] Entonces, si vemos acá, este es el nombre correcto. El siguiente método que vamos a aplicar sería buscar todos los elementos en la tabla producto, en este caso. Entonces, para eso vamos a crear un método, que también va a ser público y nos va a retornar una lista de producto. Entonces a ese método lo vamos a llamar consultarTodos.

[05:28] Entonces vamos a consultar todos, como son todos los elementos no necesitamos indicar algún parámetro y para esto, lo primero que tenemos que hacer es importar la lista y tenemos que establecer cómo va ser realizada esa consulta. Esa consulta la vamos a realizar a través del lenguaje JPQL, que es un lenguaje similar a SQL, pero utilizado para Java.

[05:52] Entonces, el significado sería Java Persistence Query Language, que es un lenguaje de consulta y lo primero que tenemos que hacer es establecer nuestra query o nuestra consulta. Esa consulta va a ser un string, que lo vamos a llamar en este caso JPQL, y string va ser un “SELECT”.

[06:15] Vamos a realizar un “SELECT”. Así como nosotros estábamos viendo en la consola, generalmente se coloca un asterisco en las consultas SQL, aquí vamos a ver la diferencia y colocamos la entidad que aquí sería producto, un alias que sería AS e indicamos que lo vamos a representar esa entidad con la letra P.

[06:38] En JPQL nosotros no utilizamos un asterisco, sino que tenemos que utilizar un token. Ese token va a ser la letra P que estamos pasando como alias.

[06:47] Cerramos nuestra consulta y ahora sí vamos a realizar el retorno. Ese retorno va a ser em.createQuery. Entonces, aquí tenemos que pasar dos parámetros también. Podemos pasar el parámetro jpql y el parámetro de la entidad, que sería Producto.class. Aquí me faltó un elemento que sería “SELECT P FROM Producto”.

[07:21] Entonces, hago el retorno que sería el EntityManager, creo la consulta con elementos jpql. Y lo siguiente que tengo que hacer es obtener la lista de resultados. Entonces, para eso yo voy a colocar acá getResultList(); entonces con eso establecido mi segundo método para este video, que sería consultar todos los elementos en la tabla producto.

[07:53] Entonces, vamos a probarlo a ver si está funcionando. Lo primero que vamos a hacer es llamar a productoDao y vamos a llamar al método consultarTodos. Acá está funcionando y vamos a guardar el resultado en una variable que va a ser del tipo lista de producto, lo vamos a llamar productos.

[08:17] Entonces, tenemos nuestro resultado guardado en una variable. Importamos la lista y ahora vamos a imprimir para ver si está todo correcto. Entonces sería productos. Como hago una lista podemos utilizar el forEach, y va a ser producto y aquí sería producto, vamos a imprimir la descripción System.out.println.

[08:55] Y vamos a colocar producto y vamos a tener la descripción. Vamos a ejecutar la aplicación. Efectivamente nosotros imprimimos el nombre para la entidad producto, imprimimos la descripción de la lista de productos. Entonces, como nosotros tenemos un único elemento en la tabla, nosotros obtuvimos solamente un resultado.

[09:19] Si tuviésemos múltiples elementos, podríamos obtener diversos resultados. Entonces en esta parte nosotros realizamos las consultas por id y la consulta de todos los elementos. En la siguiente parte nosotros vamos a ver un las consultas filtradas. Entonces vamos a ver cómo hacer cuando nosotros queremos obtener elementos específicos dentro de la tabla.