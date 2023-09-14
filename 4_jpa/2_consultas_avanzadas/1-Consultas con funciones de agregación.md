[00:00] En la parte anterior, nosotros agregamos nuestro primer pedido, nuestro primer cliente en la base de datos. Vimos que es bastante similar al curso anterior, donde agregamos un producto por categoría ya que nosotros, antes de agregar el pedido, tenemos que agregar primero un cliente.

[00:17] La diferencia es que esta vez nosotros tenemos una relación entre pedidos y productos a través de una tercera tabla, donde los valores que se almacenan en esa tabla, en esa entidad se agregan de forma automática a través del parámetro que nosotros colocamos en la notación OneToMany que es el parámetro cascade.

[00:40] Este valor nos permite que al realizar modificaciones en la entidad pedido esos valores, esas modificaciones se agreguen en la entidad items_pedido en forma de cascada, sea para eliminar, sea para actualizar, o sea, para agregar un nuevo pedido. Entonces se agregan de forma automática y no necesitamos agregar un Dao para items_pedido.

[01:02] En esta parte nosotros vamos a realizar consultas un poco más avanzadas que nos van a permitir aplicar las funciones de agregación. Las funciones de agregación son aquellas que recorren todos los elementos en la tabla y realizan una operación en conjunto.

[01:22] Entonces nosotros vamos a tener el valor promedio average con suma, máximo y mínimo. El valor de sumatoria, él va a recorrer todos los elementos en la tabla pedidos, por ejemplo. Y dependiendo de la columna que queramos analizar va a ser la sumatoria en el caso de ejemplo que nosotros vamos a aplicar del valor total, entonces va a ser la sumatoria total de todos esos elementos y nos va a retornar un único valor.

[01:54] Entonces vamos a nuestra aplicación. Nosotros recordamos que nosotros tenemos en el Dao diferentes tipos de consultas como tenemos los accesos a la base de datos como guardar, actualizar, tenemos eliminar un registro, pero también tenemos las consultas, consultar por id, consultar todos los elementos en la base de datos, él retorna una lista, consultar por nombre.

[02:19] Nosotros no tenemos nombre en pedidos, entonces esta consulta no aplica. Acordamos que esto lo copiamos del Dao de productos. Consultar por nombre de categoría tampoco aplica. Nosotros no tenemos categorías en el pedido, pero podríamos consultar por nombre de cliente.

[02:38] Eso lo dejamos como ejercicio y consultar precio por nombre de producto, podría ser consultar precio por nombre de cliente también. No aplica en este caso, pero lo dejamos como ejercicio. Entonces acá vamos a agregar una función de agregación, que nos va a retornar un valor único.

[03:00] Ese valor único, hacer del tipo BigDecimal y la función se va a llamar valorTotalVendido. Entonces, primero tenemos que realizar nuestra consulta, entonces, al igual que en otras consultas creamos una string jpql, unas comillas, el string va a ser “SELECT”. ¿La consulta nosotros qué queremos?

[03:30] El valor total para eso vamos a usar la función sumatoria. ¿Y qué valor queremos sumar de la entidad pedido? El valor total. Entonces vamos a ir a PedidoDao, vamos a hacer (p.valorTotal) FROM Pedido p; entonces, recordamos que este p es un token o un parámetro auxiliar que nos va a permitir identificar la tabla.

[04:09] Estos dos, el select y el from pueden ser escritos tanto en mayúsculas como minúsculas. Pero el nombre de la entidad o de la tabla tiene que ser escrito tal cual como nosotros colocamos el nombre de la clase. Y el nombre del parámetro del atributo, también tiene que ser igual al nombre del atributo dentro de la entidad de la clase.

[04:34] Ahora vamos a realizar el retorno de nuestro método, que va a hacer EntityManager createQuery. Vamos a pasar jpql que es nuestra consulta, y nos retorna un BigDecimal.class. createQuery(jpql), vamos a ver qué error dice. BigDecimal. Ah, aquí me estaba faltando colocar el método getSingleResult.

[05:15] Ahora ya con esto queda listo nuestro método valor total vendido, vamos a la clase RegistroDePedido y luego del commit, nosotros vamos a llamar el Dao de pedido, pedido.Dao.valorTotalVendido(). Ese valorTotalVendido lo vamos a guardar en una variable del tipo BigDecimal. Lo vamos a llamar valorTotal de esa variable, y vamos a imprimir en la consola ese resultado.

[05:58] O sea, hacemos un system.out con el valor de esa consulta y vamos a colocar acá un string. (“Valor Total: “+) Vamos a colocar esa variable. Vamos a ver cuál va a ser el retorno, entonces si nosotros vemos el resultado dio 4000. Es el resultado del precio unitario del producto multiplicado por la cantidad.

[06:32] Recordamos que en itemsPedido nosotros vamos a tener la cantidad, el producto y el pedido. ¿Cuál es el precio unitario? El precio unitario de ese producto, sería 800. Aparentemente, todo está correcto. Si nosotros acá vamos al Dao y sustituimos esta función por la función MAX, como nosotros tenemos un único valor, un único registro, nos debería retornar el mismo valor de la sumatoria total.

[07:07] Es que nosotros no tenemos más valores para comparar. Entonces, como vemos, en efecto, nosotros vamos a tener el valor de 4000. En la medida en que nosotros vayamos agregando más valores, él va a realizar el procesado de la información y va a comparar los valores entre ellos.

[07:26] Esas operaciones se realizan dentro de la base de datos. En la próxima clase nosotros vamos a seguir hablando sobre consultas y consultar con diferentes parámetros de diferentes tablas.