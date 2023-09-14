[00:00] Hola a todos. Continuando con el desarrollo de nuestro nuevo modelo, en esta parte, nosotros vamos a comenzar a crear nuestras nuevas entidades, los nuevos modelos para representar la tabla de clientes y la tabla de pedidos.

[00:15] Vamos a ver que esta tabla de cliente y de pedidos se parece con la tabla de productos y la tabla de categorías. La única diferencia es que, esta sería la tabla de categorías y va a tener nuevos atributos. No va a tener únicamente un nombre, sino también va a tener un DNI, pero es bastante similar con la tabla de productos y categorías.

[00:37] Más adelante nosotros vamos a relacionar estas cuatro tablas a través de una de otra tabla que, como habíamos mencionado, el cliente realiza un pedido, esos pedidos tienen un producto y, a su vez, esos productos están clasificados por categorías.

[00:55] Entonces, de vuelta en nuestro código nosotros vamos a comenzar a crear nuestra primera clase. Vamos a copiar acá la clase categoría y la vamos a pegar dentro del paquete de modelo, esta clase la vamos a llamar cliente. Ahora en ese cliente, vamos a agregarle únicamente un nuevo atributo.

[01:17] Sería del tipo string y va a ser el DNI o la identidad, es el identificador de cada usuario. Esa categoría tiene el nombre de esa tabla, tenemos que cambiarlo por “clientes”, ya que recordamos que JPA si lo indicamos con la notación @table él va a reconocer que el nombre de esa tabla que va a crear en la base de datos va a ser el mismo nombre de la clase.

[01:43] Entonces si nosotros queremos colocarle un nombre como “clientesxpto”, nosotros tenemos que especificarlo dentro de la notación @table. En este caso el nombre de la tabla va a ser clientes y ya tenemos los atributos mapeados.

[02:01] Tenemos el constructor default que es JPA nos lo solicita, y tenemos que agregar un constructor. Usando los campos nombre y DNI. Generamos el constructor default. Y vamos a generar también los getters y los setters para ese constructor.

[02:26] Generamos los getters y los setters y vamos a eliminar únicamente el setter para el ID, ya que nosotros no vamos a permitir que modifiquen el ID para ese cliente. Con eso queda mapeado la tabla cliente a través de la clase cliente y vamos a agregar una nueva clase, una nueva entidad dentro del paquete modelo. Copiamos. Pegamos.

[02:56] Y vamos a agregar la clase de pedir. Si ven que yo uso la palabra clase, la clase entidad, porque se pueden usar alternamente. En este caso las clases representan los modelos que nosotros estamos construyendo, pero como estos a su vez, representan una tabla en la base de datos nosotros llamamos a estas clases de entidades.

[03:22] Ahora en la clase pedida nosotros vamos a cambiar el nombre de esa tabla a pedidos. Vamos a eliminar el nombre, tenemos que agregar la fecha de registro que sería LocalDate fecha, es la fecha en la que se realizó ese pedido. Déjame ver qué otro atributo tiene. Tiene el valor total y el cliente. Vamos a importar acá.

[03:53] Tenemos que agregar el valor total que va a ser del tipo BigDecimal valorTotal, más adelante vamos a ver cómo relacionamos ese atributo, cómo obtenemos ese atributo de la tabla producto y tenemos que configurar el constructor. Constructor va a tener como único valor el atributo cliente. Hay que agregar el atributo del cliente.

[04:30] Cliente con el nombre cliente y para realizar la relación entre cliente y pedido, recordamos que un cliente tiene muchos pedidos entonces sería ManyToOne. Un cliente tiene muchos pedidos. Aquí faltó un punto y coma, e importamos la notación.

[05:00] Vamos a crear el constructor. Ese constructor va a tener como único campo, este valor de la fecha es autogenerada, el ID también es autogenerado por la base de datos, el valor total más adelante vamos a hablar de, lo vamos a obtener de los clientes y con un único valor que vamos a obtener en el constructor va a ser el cliente.

[05:26] Entonces aquí vamos a autogenerar el valor de la fecha LocalDate now. Entonces ya cada vez que nosotros instanciamos un pedido, tenemos automáticamente la fecha. Ya tenemos el constructor default, tenemos el constructor con atributo y ahora vamos a agregar los getters y los setters para la clase pedidos.

[05:57] Vamos a source, getters y setters, los seleccionamos todos y generamos los getters y setters. De esta forma queda construida la clase pedidos y la clase cliente, vemos cómo se relaciona la clase de pedidos a través del atributo cliente y vimos que un cliente puede tener muchos pedidos.

[06:19] Entonces un cliente tiene muchos pedidos, ManyToOne. En la siguiente parte vamos a ver cómo vamos a colocar el valor para el atributo valor total y cómo relacionamos las tablas pedido clientes con las tablas productos y categorías.