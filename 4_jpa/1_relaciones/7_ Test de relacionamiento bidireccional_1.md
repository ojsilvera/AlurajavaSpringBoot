[00:00] Hola. En esta parte ya vamos a comenzar a agregar nuestro primer pedido y así como el primer cliente. Este cliente realizó un pedido que tiene una lista de elementos que lo vamos a almacenar en una nueva entidad que se llama items_pedido,

[00:19] Dentro de esa entidad vamos a tener la cantidad de productos y el producto que fue solicitado. Para eso yo voy a copiar la clase main registro de producto, copiar y la voy a adicionar en el paquete de prueba. Son las pruebas que nosotros vamos a realizar. Vamos a colocar registro de pedido.

[00:41] Entonces ya tenemos nuestra clase creada, vamos a abrir, vamos a eliminar estos elementos de acá y vamos a comenzar a crear nuestro primer pedido. Lo primero que tenemos que hacer es instanciar un cliente. Si nosotros vemos acá en nuestro diagrama, nosotros tenemos el cliente, luego del cliente tenemos que crear instanciar un pedido y luego los items que van a estar dentro de ese pedido que nosotros los registramos a través del método agregarItems.

[01:17] El método agregarItems lo voy ya instanciar un nuevo itemsPedido donde voy a hacer la configuración bidireccional. Entonces ese itemsPedido va a recibir ese pedido que estamos instanciando y dentro del atributo de tipo lista vamos a agregar ese nuevo item. Entonces, de esa forma, tanto el itemsPedidos conoce el pedido, como el pedido conoce el itemsPedido.

[01:46] Entonces es un relacionamiento bidireccional. De vuelta en nuestra clase de registro pedido vamos a instanciar el cliente. Ese cliente se va a llamar “Juan”. Vamos a colocarle un DNI aleatorio, vamos a crear nuestro pedido, el valor de la variable se va a llamar pedido = new pedido. Tenemos que pasar dentro del constructor el cliente.

[02:27] Ahora vamos a importar esas clases. Importar. Dentro del pedido nosotros tenemos el método agregarItems. Ese método agregarItems nos está requiriendo una clase del tipo itemsPedido. Vamos a instanciarla, itemsPedido y vamos a pasar como constructor los siguientes elementos, la cantidad vamos a suponer que son cinco elementos de ese producto, el producto y el pedido.

[03:04] Tenemos que importar la plaza itemsPedido y solo nos está faltando llamar ese producto de la base de datos, nosotros ya lo habíamos registrado en la base de datos. Ahora con el DAO, instanciamos el DAO, productoDao. El área va a ser productoDap. Y vamos a pasarle el entityManager dentro del constructor.

[03:32] Para crear un constructor tenemos que llamar la clase utilitaria JPAUtils que fabrica con el EntityManager factory, una instancia del EntityManager. Ahora voy a usar el método de acceso consultar por id de mi clase Dao. Vamos a consultar. A ver cuáles métodos tiene acá, consultar por id. Como tenemos un único elemento, ese id va a ser el número 1 que fue el único elemento que tiene en la base de datos.

[04:17] Y ese producto lo vamos a guardar dentro de una variable del tipo producto. Ya con eso queda finalizado la creación de las entidades. Vamos a ejecutar nuestra clase registro de pedido y vamos a ver que sí los agregó, se agregó ese pedido de ese cliente. Creó las tablas, categoría, cliente, items_pedidos, pedidos, productos.

[04:49] Insertó los elementos dentro de la clase categoría. Insertó los de los productos. Realizó un select de ese nuevo producto cuando hicimos el Dao. Pero no realizó el insert del pedido, porque nosotros vamos a necesitar un Dao para ese pedido. Entonces tenemos que colocar acá PedidoDao y se va a llamar pedidoDao = new PedidoDao y pasamos el EntityManager como constructor.

[05:36] Entonces, como esa clase aún no existe, nosotros vamos a crearla. Vamos a copiar la clase producto. Y la vamos a copiar dentro de la clase Dao. La vamos a llamar PedidoDao. Vamos a corregirla, entonces tenemos la clase PedidoDao. Vamos a cambiar los elementos de producto por pedido, aquí puedo buscar producto. Reemplazar por pedido.

[06:15] Reemplazamos todo. Producto, pedido y reemplazamos. Cerramos acá, a ver nuestra clase RegistroDePedido, debería estar funcionando. Importamos la clase. Está funcionando correctamente. Ahora en nuestra clase pedidoDao como ya fue instanciada, nosotros vamos a colocar acá pedidoDao.guardar. Y tenemos que guardar ese pedido. Entonces guardamos el pedido.

[06:58] Vamos a ejecutar ahora. Y vemos que se crearon las tablas, realizó el insert de la categoría, el insert del producto y no realizó el insert del pedido. Vamos a ver por qué pasa eso. Entonces, nosotros no hemos iniciado la transacción. Me está faltando acá iniciar la transacción.

[07:27] Vamos a colocar acá. Iniciamos la transacción. Y realizamos un commit. Recordando que el commit nos permite sincronizar los valores con la base de datos. Vamos a ejecutar esta aplicación nuevamente. Vamos a ver. Entonces nos arroja un error. Ese error es el mismo error que habíamos tenido a la hora de intentar guardar un producto sin haber creado el Dao para la categoría.

[08:04] Entonces el error es un error que dice que estamos guardando un elemento que se encuentre como transient. Entonces, el elemento que se encuentra como transiente es el cliente, es decir, que en teoría nosotros tenemos que crear una clase Dao también para el elemento cliente. Eso lo vamos a hacer en la siguiente parte.

