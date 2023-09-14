[00:00] Hola. En la parte anterior, nosotros intentamos guardar un pedido y nos encontramos con el siguiente error. El pedido, el objeto pedido hace referencia a un objeto que no ha sido salvado y que tiene un estado transiente. Entonces, recordando del primer curso, cuando nosotros intentamos guardar un producto que tenía dentro de sus atributos la entidad categoría, y esa categoría no había sido guardada en la base de datos anteriormente, no nos arrojaba el error de estado transiente.

[00:30] Entonces nosotros tuvimos que crear un Dao para la categoría, para poder corregir ese error. Entonces, en teoría nosotros tenemos que crear un Dao para todos los elementos que sean guardados en las bases de datos. Y cuando nosotros tenemos un elemento que recibe otro como atributo, él nos arroja ese error del estado transiente.

[00:55] Recordando del primer curso, los estados son transientes cuando es instanciado, manage cuando persistimos o cuando usamos el método guardar del EntityManager. Cuando realizamos el commit sincronizamos y cuando realizamos el close de ese EntityManager, nosotros pasamos a ese estado, un estado detached o separado, que es similar al estado transiente.

[01:22] Ahora tenemos que construir el cliente Dao, para eso vamos a copiar el pedido Dao, vamos a pegarlo en el paquete Dao. Vamos a eliminar acá, aquí es cliente Dao. Vamos a abrir la clase ClienteDao. Vamos a reemplazar cliente pedido por cliente y todos los pedidos los vamos a reemplazar por cliente. Cerramos.

[02:01] Otro error que me había faltado mencionar, es que acá el directorio que yo coloqué en la base de datos, yo no coloqué el nombre del archivo. El nombre de mi archivo es database. En la ruta o en la URL, todos los archivos antes del último nombre son los directorios. Entonces este de aquí, el nombre database va a ser el nombre del archivo que va a ser generado por JPA de forma automática.

[02:31] Usuarios público Alura y JPA ellos van a ser los directorios o carpetas que ustedes deben crear donde van a almacenar el archivo de base de datos. Ahora vamos a ir a la clase de RegistroDePedido. Vamos a instanciar el clienteDao que nos va a dar acceso a la base de datos para almacenar ese cliente, nuevo ClienteDao y vamos a pasar como atributo el EntityManager.

[03:05] Importamos la librería, x sería clienteDao.guardar(cliente). Entonces, de esa forma, ya tenemos nuestro Dao, ya le dimos acceso al cliente en la base de datos y deberíamos corregir el error de propiedad transiente. Se corrigió el error. Agregamos la categoría, el producto, seleccionamos el producto con ID1, insertamos el cliente y el pedido. No nos mencionó nada de itemPedido, vamos a abrir la consola.

[03:43] En la consola nosotros vemos que tenemos la ruta con el archivo al final database, el nombre de usuario ustedes lo pueden alterar a la hora que crean la base de datos y la contraseña, que colocaron. En caso yo coloqué esta contraseña. Vamos a revisar que hay en las categorías. Celulares, correcto.

[04:05] En productos, Xiaomi, correcto. Ahora vamos a ver si agregó el cliente, el cliente, Juan, el id, identidad el DNI. Perfecto. Vamos a ver los pedidos. En pedido agregó el ID, la fecha y el cliente ID número 1, que es el cliente Juan. El valor total está como nulo. Vamos a tener que corregir ese error, pues no puede aparecer nulo.

[04:33] V vamos a limpiar acá y vamos a ver qué apareció en items_pedido. No agregó nada de items_pedido. Entonces. En teoría, la intuición nos dice que tenemos que crear un Dao para items_pedido. Cerramos esa base de datos. Pero no tenemos que crear un nuevo Dao.

[04:53] Hay una propiedad en la notación OneToMany que nos permite que a la hora de realizar una acción en la entidad pedido, realice esa acción en cascada para la entidad que está relacionada, que en este caso sería la entidad items_pedido. Entonces esa propiedad se llama cascade.

[05:15] Y el tipo cascade=CascadeType, tenemos una serie de opciones. Esa alteración en cascada, esa acción en cascada puede ocurrir cuando yo elimine un archivo de pedido, cuando yo guarde por primera vez un archivo en pedido, cuando actualice, cuando hago el merge que lo traigo de la base de datos o en todos los casos, que es el que me interesa.

[05:43] Entonces, cada vez que yo realice una operación con pedido, que haga una alteración en items_pedido. El valorTotal estaba como nulo. Cuando yo coloco el nombre de una variable y no le asigno un valor ella va a estar inmediatamente como nulo, así que tengo que colocar un primer valor.

[06:01] Puedo hacer BigDecimal. Vamos a inicializarla con cero, pero acá en el método de agregar item, vamos a colocar que ese valor va a ser igual a ese mismo valor, this.valorTotal.add porque es un BigDecimal, y vamos a traer el valor de la clase item.

[06:29] En item, yo voy a tener el precio que lo configuramos del pedido y la cantidad, entonces yo podría colocar getCantidad()*item.getPrecioUnitario(). Esto lo tendría que colocar dentro de un bigDecimal y va a quedar todo horroroso.

[06:55] Entonces, lo que yo voy a hacer para darle un poco más de estilo sería colocar item y vamos a crear un nuevo método o se va a llamar getValor() dentro de la entidad items_pedido, vamos aquí, me da la opción de crear un nuevo método. Vamos a eliminar esto acá, y va a ser this.precioUnitario que es del tipo BigDecimal multiplicado por nuevo BigDecimal que va a recibir (this.cantidad).

[07:40] Entonces esa forma ya yo asigné el valor para valor total. Vamos a asignarle el valor de la palabra total, inicialmente es cero, en esta parte del método yo le asigno el nuevo valor. Y ahora con la propiedad cascade de la notación OneToMany él debería asignar los valores en la tabla de items_pedido.

[08:08] Vamos a ejecutar, a ver si está todo bien. Él realizó el insert de categoría, el insert de producto, seleccionó el producto con id1, realizó un insert de cliente, el insert de pedido y realizó el insert de items_pedido.

[08:23] Vamos a revisar qué tenemos en la tabla. Colocamos la contraseña, conectamos, la categoría, perfecto, producto, correcto, cliente Juan con id1. Bien. El pedido, calculó el valor y el item pedido que estaba faltando, colocó el precio unitario que es 800, la cantidad que la pasamos ahora a la instancia del items_pedido, el pedido al que está relacionado, el producto al que está relacionado y el id de esa tabla.

[09:04] Entonces, aparentemente está todo funcionando correctamente. Aquí ya nosotros pudimos comprobar en la clase de RegistroDePedido todas las operaciones, ya hemos instanciado un cliente, instanciamos un pedido, instanciamos un items_pedido y nos encontramos ya que todas nuestras tablas se encuentren relacionadas.

[09:31] Entonces en la siguiente parte vamos a comenzar a realizar unas consultas un poco más avanzadas y a realizar operaciones que nos permiten traer diversos elementos de estas tablas.