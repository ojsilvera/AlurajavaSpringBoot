[00:00] Hola. En la parte anterior, nosotros hablamos de las consultas con la estrategia de carga del tipo eager y lazy. Mostramos que todos los elementos del tipo ToOne, como ManyToOne o OneToOne y es por default, vienen con la estrategia del tipo eager, y todos los elementos con la estrategia ToMany por default vienen con la estrategia de lazy.

[00:24] Mencionamos que es parte de las buenas prácticas que toda nuestra aplicación sea lazy, para evitar el consumo excesivo de memoria y agilizar aumentar la velocidad de nuestra aplicación, ya que vamos a evitar que estén siendo consultados valores o informaciones que no sean deseados dentro de nuestra consulta.

[00:45] Sin embargo, uno de los problemas que puede ocurrir cuando nosotros agregamos el parámetro lazy a una notación que es del tipo eager, nos encontremos con una excepción, ya que puede ocurrir que para ese punto el EntityManager se encuentre cerrado.

[01:04] Entonces primero vamos a ejecutar esta aplicación sin cerrar el EntityManager. Y luego vamos a cerrar el EntityManager para ver qué ocurre. Entonces, nosotros estamos realizando un select, vemos que la función ocurre perfecto. Realizamos un select en los atributos de la entidad pedido, con el id que indicamos y luego él realiza un select en los atributos de la entidad cliente.

[01:33] Por último, nos da como retorno el nombre del cliente. Pero vimos que primero realiza un select para pedidos y luego él realiza un select para obtener el nombre del cliente. Vamos a ver qué ocurre si antes de solicitar el nombre del cliente cerramos el EntityManager. Ejecutamos la aplicación, cerramos el EntityManager y tenemos que él obtiene todos los elementos de la entidad pedido, él realizó un select en la entidad pedido.

[02:06] Y a la hora de realizar un select en la entidad cliente, él arroja una excepción que es una excepción bastante famosa, que es la lazyInitializationException, que dice que no existe una excepción para obtener el cliente con ID número 3. Ustedes podrían pensar en primera instancia que sería simplemente no cerrar el EntityManager.

[02:32] Pero no siempre eso es posible. En este caso, nosotros podemos hacerlo porque nos encontramos a una clase main y nosotros tenemos total control de la aplicación. Pero a la hora de nosotros tener una aplicación en desarrollo, nosotros podemos encontrarnos que después del Dao, en la consulta Dao, ya se haya cerrado el EntityManager, que es parte de las buenas prácticas.

[02:55] Realizar la consulta e inmediatamente cerrar el EntityManager para evitar el consumo excesivo de memoria. Entonces, vamos a dejar el EntityManager cerrado acá. Vamos a ver para resolver ese problema. Ahora vamos a tener que realizar una consulta planeada. ¿Qué es una consulta planeada?

[03:12] Son consultas, donde nosotros ya planificamos cuáles son los elementos que vamos a obtener posteriormente y aún si nosotros nos encontramos con el EntityManager que se encuentra cerrado, que la conexión se encuentra cerrada, que es lo que nos da acceso a la base de datos, nosotros ya tenemos esos registros almacenado dentro de nuestra variable pedido.

[03:35] Entonces para eso, ya no vamos a poder utilizar el método find del EntityManager, sino que vamos a tener que ir al Dao y realizar esa consulta. Entonces dentro del Dao de pedido, nosotros vamos a crear un nuevo método. Ese método nos va a retornar un pedido, con todos los atributos y se va a llamar consultarPedidoConCliente(). Vamos a pasar como parámetro un id.

[04:09] Establecemos nuestra consulta. Vamos a hacer un string jpql, ponemos comillas y realizamos un select con el token pero de la tabla Pedido, tenemos que recordar que va el nombre de la entidad y colocamos el token para realizar la conexión. SELECT pero FROM Pedido p WHERE p.id= sea igual al atributo que estamos pasando como parámetro.

[04:49] Ahora, hasta este punto solamente estamos llamando el pedido p. Pero como el cliente tiene una estrategia de carga del tipo lazy, entonces no va a ser consultada. Nosotros solamente vamos a tener en este punto el pedido. Para nosotros obtener el cliente, nosotros vamos a usar un recurso de JPA que sería la palabra join fetch, que nos permite realizar un join con la entidad deseada, en este caso la entidad cliente.

[05:21] Entonces vamos a colocar JOIN FETCH. Vamos a realizar un JOIN FETCH. ¿Con quién? Con la entidad cliente, p.cliente. Eso queda establecido en nuestra consulta. Ahora vamos al retorno, retorno EntityManager em.createQuery. Vamos a pasar la consulta y el tipo de retorno, que va a ser Pedido.class.

[05:52] Vamos a configurar los parámetros, setParameter. Y aquí va a ser el id y el atributo id. Por último, vamos a obtener el resultado, y cerramos ese retorno. Ahora es necesario en esta clase de prueba que nosotros instanciemos el pedido Dao. Va a ser pedidoDao = new PedidoDao, y pasamos el entity manager como atributo.

[06:36] Ahora importamos esa clase. Ahora si nosotros podemos hacer uso de nuestro nuevo método, nuestra consulta, pedidoDao, consultar pedidos con cliente. El id va a ser 2l de tipo long y vamos a guardar esa consulta en una variable que se va a llamar pedidoConCliente.

[07:08] Vamos acá que nos da un error, pero nosotros estábamos trayendo un pedido, lo vamos a reemplazar con pedidoConCliente. Entonces esta este punto, nosotros estamos trayendo un pedido que debería tener el cliente, cerramos la conexión y vamos a ver qué ocurre.

[07:29] Ejecutamos la aplicación. Y vemos que efectivamente, el realizó un select de los elementos en la entidad pedido y realizó un join. Entonces, ahora va a tener un comportamiento como si fuera eager, ya que nosotros estamos indicándole que esa entidad que se encontraba como lazy, ahora va a ser del tipo eager, pero solamente para esa consulta. Nos da el retorno que es María.

[07:58] Ya con eso nosotros le damos una solución a esos elementos que se encuentran como lazy. Sin embargo, es importante mencionar que si ustedes se encuentran una aplicación que ya está funcionando y no contiene los parámetros de tipo lazy, al colocar ese parámetro, ustedes se pueden encontrar con que su aplicación comience a arrojar excepciones, por lo que ustedes van a tener que pensar cuál va a ser la consulta, en qué momento.

[08:31] Y cuál va a ser la estrategia para aplicar esas consultas planeadas, para evitar así la excepción e incrementar el desempeño de su aplicación a la hora de funcionar. Entonces, con eso queda todo finalizado sobre el desempeño a la hora de tener los elementos ManyToOne o OneToOne.

[08:56] Es parte de las buenas prácticas colocar la estrategia del tipo lazy y recordar cuál vas a ser el momento en el que van a realizar sus consultas planeadas, ya que podemos encontrarnos que para un cierto punto, el EntityManager se encuentre cerrado. En la siguiente parte, nosotros vamos a hablar un poco más sobre otros recursos de JPA. Nos vemos ahí.