[00:00] Hola. En el video anterior nosotros realizamos el mapeamento para dos entidades que se encontraban relacionada con la cardinalidad ManyToOne. Eso quiere decir que muchos productos tenían una única categoría.

[00:14] Cuando nosotros intentamos realizar la persistencia de la entidad producto con la entidad categoría, sin antes haber persistido la entidad categoría, es nos arrojó una excepción que era la excepción TransientPropertyValue.

[00:29] En él quería decir que nosotros estábamos intentando guardar un elemento que aún no existía en la base de datos, entonces para eso nosotros vamos a explicar en esta parte lo que son los ciclos de vida y los diferentes estudios en los que se puede encontrar una entidad.

[00:45] Y que a la hora de que nosotros estamos trabajando con el EntityManager, nosotros vamos a ir pasando de un estado a otro y eso va a ser lo que vamos a llamar el ciclo de vida.

[00:58] Entonces inicialmente yo tengo aquí en este diagrama cuando yo utilizo la palabra clave new, en una clase, esa entidad va a pasar a estar en un estado transiente. Esto significa que va a ser una entidad que ya fue instanciada pero no va a ser considerada para ser registrada en la base de datos.

[01:20] Entonces, todos los elementos que se encuentren como estado transiente JPA los va a ignorar y solamente va a trabajar con los elementos que se encuentran en el siguiente estado.

[01:31] El siguiente estado que nosotros vamos a tener es el estado Managed. En el estado Managed, nosotros para pasar a él tenemos que utilizar, tenemos que instanciar primero el EntityManager y persistir esa entidad que se encuentra como estado transiente.

[01:47] Cuando nosotros realizamos la persistencia pasamos de esa entidad al estado Managed o administrado. Todas las entidades que se encuentran con el estado Managed o administrado son entidades que cuentan como candidatas para ser registradas en la base de datos. Entonces luego de que yo hago el commit o el flush, yo envío efectivamente, sincronizo esos valores que fueron pasados como parámetro dentro de la entidad dentro de la base datos.

[02:15] O sea al yo realizar el commit o el flush, yo sincronizo mi base de datos, creo un nuevo id y genero un nuevo registro, una nueva fila en la base de datos. Luego de que yo he realizado el commit y el close, esa entidad para estar a un estado de detached.

[02:35] Entonces, el estado de detached es un estado donde se comporta similar al estado transiente y a quién JPA no lo reconoce o va desconsiderar todos los elementos que se encuentran como detached o separados.

[02:51] Entonces, todas las entidades que se encuentren en detached, JPA las va a ir ignorando y solamente va a ir trabajando, va actualizar registros de las entidades que se encuentran con el estado Managed o administrado.

[03:06] Entonces para explicar mejor esto de los ciclos de vida, yo voy a ir a la clase registro de producto y voy a trabajar únicamente con el EntityManager y una entidad, que va a ser la entidad categoría. Entonces aquí yo tengo mi entidad categoría instanciada. Instancié mi EntityManager, pero no estoy realizando ninguna persistencia.

[03:30] Y simplemente instancé la categoría y pasé un parámetro en el constructor. Vamos a ejecutar esta aplicación y en el registro vemos que está funcionando todo correctamente y creó la tabla, creó la tabla categoría, creó la tabla producto y realizó, anexó la llave extranjera del id categoría dentro de la tabla producto.

[03:55] Pero no realizó ningún insert, no hay ninguna persistencia de valores. Entonces para realizar una persistencia tengo que utilizar el método persist del EntityManager, me está indicando que tengo que pasar una entidad, en este caso va a ser la entidad celular.

[04:14] Y si yo ejecuto esta aplicación va a ver que el registro está corriendo perfectamente, genero las tablas, categoría, productos, realizo la alteración e inserto este nuevo valor que sería el nombre celulares dentro de la tabla categoría. Entonces, todo lo que ocurre luego de haber realizado la persistencia, JPA lo va a estar observando.

[04:40] Entonces a partir de este momento si yo hago algo una alteración dentro de la entidad categoría JPA va a estar atento de esas alteraciones y va a realizar modificaciones en la base de datos. Entonces, vamos a dar un ejemplo de eso.

[04:55] Se puede tomar la entidad celulares, voy a configurar el nombre y ahora no va a ser celulares, sino que va a ser “LIBROS”. Yo voy a modificar esa categoría, que yo estoy instanciando aquí inicialmente, voy a realizar la persistencia. Ahora esa entidad va a estar en un estado Managed. Quiere decir que va a ser considerada para ser guardada en la base de datos.

[05:23] Voy a modificar el nombre de celulares a libro y voy a hacer el commit. Podría utilizar el método flush, que sincroniza los valores con la base de datos. Entonces voy a ejecutar la aplicación, guardo acá, se corren los registros, creó las tablas, él realizó el insert, que es correspondiente a la persistencia del primer valor que yo envié cuando instancié la categoría celulares.

[05:54] Y luego él realizó un update correspondiente a la alteración. Cuando se encuentre con el estado Managed, él va a considerar esa entidad para ser modificada o ser observada y prestar atención de todos los cambios que se han realizado dentro del estado Managed.

[06:17] Una vez que yo realizo el commit y el close o que hay algún clear, esa entidad vas a estar en un estado detached. Entonces si yo hago alguna modificación, luego de haber realizado el close, por ejemplo celulares y modifico el nombre, ahora va a ser “SOFTWARE”. Presten atención a las modificaciones entonces.

[06:54] Nosotros vamos a instanciar nuestra entidad categoría, vamos a realizar, vamos a asignarle un nuevo valor a ese parámetro, realizamos la persistencia y con esto realizamos el insert en la base de datos.

[07:07] Al nosotros realizar una modificación de esa entidad que fue persistida y por lo tanto se encuentra con el estado Managed, él va a realizar un update dentro de los registros. Luego de que nosotros confirmamos esa operación, esa transacción y cerramos la conexión con el método close del EntityManager, si nosotros nuevamente modificamos la entidad “CELULARES”, vamos a modificar el parámetro, el atributo nombre, esa última modificación no debería ser considerada dentro de los registros.

[07:41] Entonces, vamos a confirmar eso, vamos a ejecutar la aplicación y vemos que efectivamente él creó las tablas, realizó el insert equivalente al primer valor que fue asignado al instanciar la categoría, realizó un update correspondiente a la modificación dentro del estado Managed y luego de que nosotros cerramos la transacción con el método close y modificamos el valor para la entidad celular, él no hizo un nuevo update correspondiente de “LIBROS” a “SOFTWARE”.

[08:19] Entonces, nosotros en la siguiente parte vamos a ver cómo traer los elementos que se encuentran en el estado detached, que luego de que nosotros cerramos la conexión, para un estado Managed y continuar realizando alteraciones en esos elementos.