[00:00] Hola. En la parte anterior nosotros comenzamos a hablar sobre mapeamientos bidireccionales y creamos la tabla o la entidad items_pedido que nos permite relacionar los pedidos con los productos.

[00:14] Entonces nosotros vimos que generamos la entidad items_pedido con los atributos productos y pedido, así como con los atributos, cantidad, cantidad de productos y el precio unitario que vamos a obtener ese valor del producto.

[00:32] Nosotros queríamos un modelo de este tipo donde se relacionase el pedido con los productos, pero tuvimos algo de este tipo, obtuvimos una sexta tabla que no queríamos llamada pedidos, items_pedido. Eso ocurrió porque JPA no supo cómo conectar este pedido con el item pedido.

[00:52] Para corregir eso, nosotros tenemos que indicarle que en el pedido esta lista con una notación @OneToMany se encuentra conectada a este item pedido en el atributo pedido. Entonces, vamos a ver, esa sexta tabla que se creó y vamos a ver cómo corregir ese error.

[01:14] Nosotros teníamos que se creó la tabla cliente, la tabla items_pedido, la tabla categoría, la tabla ítems_pedido es la que queremos obtener, que está correcto, la tabla pedidos y la tabla pedidos_items_pedido que tienen dos elementos: pedido_id e items_id.

[01:33] Entonces para corregir eso, tenemos que acá la tabla items_pedido tiene todos los elementos que deseamos, entonces este pertenece a la tabla items_pedido, entonces tenemos que eliminar esta nueva tabla, nosotros vamos a ir a la clase pedido y vamos a indicarle que la lista se encuentra mapeada por el elemento pedido existente en la entidad items_pedido.

[02:02] Entonces, de esta forma nosotros conectamos esta lista con la entidad items_pedido. Así vamos a eliminar esta sexta tabla, vamos a ver si eso es lo que está pasando. Ejecutamos la aplicación y tenemos que generar la tabla categoría, cliente, items_pedido, pedidos y producto, no tenemos la tabla pedidos_items_pedido.

[02:35] Entonces el error se corrigió. Lo siguiente que tenemos que hacer es esta lista se encuentra como nula, que es la lista que va a tener. Nosotros estamos relacionando los pedidos con la entidad items_pedido, que a su vez nos permite relacionarlo con los productos.

[02:55] Entonces, en la tabla pedido nosotros tenemos esta lista como nula, tenemos que inicializarla. Vamos a inicializarla new ArrayList; y ahora tenemos una lista vacía. Lo siguiente que tenemos que hacer es añadir los valores a esta lista, entonces vamos a añadir esos valores.

[03:16] Para añadir esos valores vamos a crear un método public void agregarItems(ItemsPedido ítem). Entonces, este método va a agregar nuevos items en esta lista. ¿Entonces, intuitivamente que tenemos que hacer? This.items. Agregamos, ¿y qué vamos a agregar? Ese item, ese item de acá.

[03:59] Pero ese item, ¿quién es ese item? Ese item de acá, necesita estar relacionado a su vez con este pedido, entonces nosotros tenemos que indicarle que ese ítem, en el pedido nosotros vamos a pasarle el valor de este pedido, nos está pidiendo un elemento del tipo pedido. ¿Y cuál va a ser el pedido? Este pedido de acá.

[04:29] Entonces, ya esta forma, nosotros configuramos el pedido de la clase item pedido y agregamos ese item pedido dentro de la lista que se encuentra en la clase pedido. Así, de esa forma, la clase items_pedido conoce a la clase pedido y la clase pedido conoce a la clase items_pedido, ya que nosotros acá tenemos un atributo de lista que conoce todos los elementos de items_pedido.

[05:04] Entonces a través de este elemento, yo puedo acceder, aquí voy a tener un itemsPedido, que nos va a permitir acceder a los productos de ese pedido. Ya tengo esa relación. Y lo último que está faltando es agregar en ItemsPedido el precio unitario que no fue configurado. El precio unitario lo puedo obtener del producto.

[05:32] Entonces sería this.precioUnitario=producto.getPrecio(); Entonces, ya de esta forma, quedan configurados todos los pequeños detalles. Vamos a ejecutar esto a ver si está corriendo todo perfecto. Está corriendo todo bien.

[05:57] Se crearon las tablas categorías, la tabla clientes, la tabla items_pedido, la tabla pedidos y la tabla productos. No tenemos una sexta tabla. Todas las tablas se conocen entre ellas. Y ahora sí tenemos algo de este tipo.

[06:18] Entonces, recapitulando nosotros hicimos la conexión entre la entidad items_pedido con la entidad pedido a través del mappadBy para realizar el mapeamiento bidireccional. Inicializamos la lista. Ya no es una lista nula, sino una lista vacía.

[06:38] Agregamos los items dentro de la lista de items_pedido e hicimos el mapeamiento bidireccional, tanto para la lista de items como para los pedidos que se encuentran en la entidad items_pedido. En la siguiente clase, vamos a crear nuestro primer cliente y nuestro primer pedido y vamos a crear un registro de pedidos y vamos a ver cómo se comportan todas estas clases, todas estas nuevas relaciones de clase.