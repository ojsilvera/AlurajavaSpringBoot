[00:00] Hola. Continuando con el desarrollo del curso de JPA y Hybernate, nosotros ya creamos la tabla de clientes y de pedidos, y la tabla de productos y categorías. Ahora queremos ver cómo éstas se relacionan entre sí.

[00:15] Entonces vamos a ver, aquí en nuestras diapositivas, nosotros tenemos la tabla productos relacionada con categoría a través de la notación ManyToOne, la tabla clientes relacionado con el pedido a través de la notación ManyToOne y ahora nosotros vamos a relacionar un pedido con los productos y vemos que todos estos elementos se encuentran relacionados.

[00:36] Un cliente realiza un pedido y ese pedido puede tener múltiples productos. Ahora, para realizar ese modelo, nosotros tenemos que agregar un nuevo atributo dentro del pedido. Un atributo private. Y como vamos a tener múltiples productos, tenemos que realizar una lista que almacene elementos del tipo producto.

[01:01] Valor de esa variable se va a llamar productos y la relación seria: un pedido puede tener múltiples productos y esos múltiples productos pueden encontrarse en muchos pedidos. Es decir, una primera persona realizó el pedido de un libro, de un libro de ciencia y una segunda persona también realizó un pedido de un libro de ciencia.

[01:28] Adicional, esa primera persona, puede realizar un pedido de un libro de ciencia y un libro de matemáticas, entonces va a tener múltiples productos. Entonces, aquí la relación sería del tipo ManyToMany. De esta forma, nosotros le indicamos a JPA cuál va a ser el tipo de relación existente entre ellos.

[01:51] Para nosotros no crear una nueva entidad JPA genera de forma automática esa nueva tabla a través de la notación @JoinTable. Esta nueva tabla que permite relacionar los productos con los pedidos, es creada a través de la notación @JoinTable.

[02:14] Sin embargo aquí nosotros no tenemos sino simplemente dos atributos, dos columnas, que es la que nos permite tener el identificador del producto y el identificador del pedido.

[02:26] Si nosotros queremos agregar nuevos elementos, ya que por lo menos acá el pedido, nosotros tenemos el valor total, ese valor total es el resultado del precio del producto por un valor que sería la cantidad de elementos de ese producto.

[02:44] Nosotros podemos pedir tres libros o tres pen drive o 5 laptops y una diversidad de variaciones. Entonces, si nosotros creamos un modelo simple, como este, donde solamente tenemos un pedido relacionado con un único producto, nosotros podemos utilizar la anotación ManyToMany.

[03:11] Vamos a ejecutar esto para ver cómo se crean esas tablas. Vemos que realicé un drop de la anotación persistence. Nosotros ya habíamos modificado de update a drop. Vamos a ejecutarlo de nuevo. Y aquí vemos la creación de las tablas.

[03:36] Creó la tabla categoría, la tabla cliente, la tabla pedidos. Categoría, clientes, pedidos, la tabla producto y una nueva tabla que sería la tabla pedidos_productos. Entonces nosotros tenemos la relación pedidos_productos. Vamos a aquí colocar la tabla pedido, el atributo name, que se vea similar a “ítems_pedidos”.

[04:05] Entonces nosotros vamos a tener aquí también un conjunto de atributos que podemos anexarle a la notación @JoinTable. Vamos a ejecutar. Y vemos que creó la tabla clientes, la tabla pedidos, la tabla productos y la tabla ítems_pedido. Nosotros podemos colocar ítem_pedidox, ejecutamos y vamos a tener ese valor.

[04:41] Ya de esta forma, queda mapeada la relación simple entre producto y pedido, sin embargo, nosotros no vamos a tener una relación tan simple. Es que ese pedido puede tener múltiples elementos de un único producto. Para eso en la siguiente parte nosotros vamos a ver cómo anexarle nuevos atributos y modificar, pasar de esta tabla simple a una tabla donde tenemos el precio unitario y la cantidad.

[05:13] Porque vamos a colocar el precio unitario, ya que nosotros no tenemos que tener un histórico, un registro donde se mantenga el precio para el momento de esa venta, de que este precio del producto pueda modificar con el tiempo. Entonces nosotros vamos a agregar nuevos elementos y para eso vamos a agregar una nueva entidad.

