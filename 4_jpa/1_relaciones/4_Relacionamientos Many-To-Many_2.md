[00:00] Hola. Continuamos con el desarrollo de nuestro nuevo modelo. En la parte anterior nosotros habíamos mapeado la relación entre la tabla pedidos y producto a través de una nueva tabla que se llamaba ítems_pedido utilizando la notación @JoinTable y el relacionamiento entre tablas ManyToMany.

[00:18] Ahora, nosotros vamos a agregar nuevos atributos dentro de esa tercera tabla que relacionaba los pedidos con los productos. Y para eso, nosotros tenemos que usar el modelo que nosotros veníamos usando de entidades, generar una clase, colocar las anotaciones de las entidades, colocar los constructores y los getters y setters.

[00:40] Nosotros necesitamos colocar esta nueva entidad porque de esta forma, nosotros vamos a tener un pedido con un único producto y como nosotros acá tenemos es un valor total, ese valor total va a ser el resultado entre el precio unitario del producto y la cantidad de elementos de ese producto, para eso nosotros tenemos que saber la cantidad.

[01:04] Adicionalmente, colocamos el precio unitario para saber el precio de venta para ese momento. Voy a tener un id que va a ser el identificador de ese item relacionado con el pedido y vamos a utilizar una nueva notación que no va a ser la notación ManyToMany.

[01:25] Entonces, por el momento vamos a colocar acá una notación incógnita y vamos a crear esa nueva entidad que se va a llamar iIemsPedido. El nombre de esa variable a a ser ítems y vamos a crear la clase con el padrón que veníamos usando.

[01:46] Vamos a colocar la notación @Entity, una notación @Table(names=”ítems_pedido”), vamos a colocar el @Id, vamos a traer de acá, vamos a colocarla en la entidad ItemsPedido. Vamos a importar las librerías de @Entity y de @Table y vamos a agregar los nuevos atributos que van a representar las columnas en la tabla.

[02:28] Va a ser del tipo private tipo int se va a llamar cantidad. La siguiente va a ser el tipo private, el tipo BigDecimal y va a ser el valor, el precio unitario: precioUnitario. Importamos la librería para BigDecimal y tenemos que colocar la relación a través del atributo de tipo clase producto y pedido, private Pedido pedido.

[03:21] Entonces lo siguiente que vamos a colocar acá, vamos a explicar un poco mejor esto, cada vez que nosotros instanciamos un ítem pedido, cuando nosotros instanciamos el item pedido 1 va a tener el producto 1 con el pedido 2. El item pedido 2 va a tener el producto 2 en el pedido 2.

[03:40] Entonces vemos que este pedido va a tener el mismo identificador pero diferentes productos. Entonces, vemos que tenemos un pedido con diferentes productos, eso nos recuerda a un cliente con muchos pedidos o un producto con una categoría que pertenece a muchos productos.

[04:05] Entonces aquí vamos a utilizar la notación @ManyToOne. De la misma forma, acá @ManyToOne. Ya con esto queda mapeada la relación. Entonces, vamos a ver acá. Y tenemos la notación @ManyToOne en el cliente, un cliente tiene múltiples pedidos.

[04:41] En ItemsPedido, un cliente tiene múltiples pedidos, múltiples ítems pedidos o un producto tiene múltiples ítems pedidos. Entonces vemos que la relación acá es ManyToOne. Otra forma de verlo es que nosotros estamos haciendo la relación ManyToMany, entonces, de un lado, tiene que existir la notación @ManyToOne mientras que en el pedido tiene que existir la notación OneToMany.

[05:16] Entonces, siempre que tengamos una lista es OneToMany o es un elemento que termina en ToMany. Si nosotros colocamos acá del otro lado colocamos ManyToOne y aquí colocamos OneToMany.

[05:35] Si vemos, eliminamos aquí el One del medio y queda ManyToMany. Entonces, nosotros ya tenemos una relación del tipo muchos a muchos. Vamos a importar esa librería y vamos a terminar la construcción de la entidad itemPedido agregando el constructor default, el consultor sin elementos.

[06:02] Y vamos a crear un constructor que va a tener los siguientes elementos: constructor, son de los campos, no va a tener el ID. Va a tener la cantidad, el producto y el pedido, y aquí el precio unitario lo podemos obtener del producto.

[06:26] Generamos del constructor. Eliminamos los elementos innecesarios y los getters y setters para esa entidad. Seleccionamos todos y borramos el setter para el ID. Ya con eso queda finalizada la construcción de nuestra entidad ItemsPedido. Vamos a ejecutar, a ver si está todo bien, guardamos.

[06:56] Aparentemente está todo bien, se crearon las tablas items_pedido, pedidos, pedidos_items_pedido, productos y la tabla categorías. Entonces esta tabla aquí extra pedidos_items_pedido. Nosotros vamos a hablar de eso en la siguiente parte y vamos a ver cómo hacemos para eliminarla, ya que nosotros vamos adicionando una nueva tabla aquí.

[07:30] Nosotros solamente tenemos la tabla items_pedido. Sería esta de acá, la primera que es items_pedido, pero acá está cargando la tabla pedidos_items_pedido, o sea, vamos a ver por qué pasa eso en la siguiente parte.