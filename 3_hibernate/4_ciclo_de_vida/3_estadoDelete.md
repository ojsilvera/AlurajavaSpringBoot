[00:00] Hola. En el video anterior nosotros vimos cómo actualizar un registro de la base de datos ahora en esta parte nosotros vamos a ver cómo eliminar ese registro.

[00:08] Entonces para eliminar un registro, tenemos que primero ese registro tiene que existir en la base de datos y tenemos que tenerlo con un estado managed o gerenciado. Nosotros vamos a utilizar el método remove del EntityManager, vamos a pasar la entidad para poder eliminar ese registro, utilizando el método commit o flush.

[00:32] Entonces, recordando el diagrama del video anterior, cuando nosotros instanciamos una entidad, tenemos esa entidad en estado transiente, realizamos el persist, pasa a estar a un estado Managed, a partir del cual nosotros podemos modificar y son los valores considerados para ser enviados a la base datos.

[00:49] Con el método commit y flush enviamos los valores o los sincronizamos con la base de datos. Y utilizando el método merge, podemos traer un elemento de la base de datos con estado Managed.

[01:01] Entonces, si nosotros queremos eliminar un registro nosotros tenemos que garantizar que ese valor se encuentra en estado Managed y que existe en la base de datos. Vamos a ver eso en la práctica.

[01:18] Aquí en la clase RegistroDeProducto, nosotros instanciamos la entidad categorías con el valor de celulares, le pasamos el valor del parámetro, realizamos la persistencia, hicimos una modificación, realizamos un flush, sincronizamos ese valor en la base de datos, el clear, pasa ese valor a un estado detached.

[01:40] Con el método merge llamamos a ese valor de la base de datos con un estado managed, lo resignamos a la entidad inicial, hicimos una modificación y teníamos una segunda actualización.

[01:53] Entonces en este punto nosotros tenemos nuestra entidad con un estado managed. Entonces en la siguiente línea, yo voy a llamar el método remove. El EntityManager me solicita una entidad que sería celulares y voy a sincronizar ese valor con el método flush.

[02:15] Voy a ejecutar esa aplicación y en la consola tenemos que él efectivamente creó las tablas, realizó el insert, el update, realizó el select del merge, realizó el segundo update a “SOFTWARE” y por último realizó el delete relacionado al método remové del EntityManager.

[02:36] Entonces, ¿qué pasaría si esa entidad se encuentra con un estado detached? Vamos a ver eso en la práctica. Entonces si yo luego de realizar el flush, yo realizo un clear, forzando las entidades a estar en un estado detached y ejecuto mi aplicación, ahora mi entidad categoría va a estar como detached.

[02:55] En la consola voy a ver una excepción. La excepción dice que estoy intentando remover una instancia que se encuentra como detached. Para yo devolver esa instancia a un estado managed o un estado gerenciado, yo voy a recordar la clase anterior donde yo utilicé el método merge para traer mi valor de la base de datos con el estado managed.

[03:21] Entonces voy a copiar acá, voy a pegar y ya con esta línea estoy garantizando que él va a estar viniendo de la base de datos con un estado Managed para luego poder removerlo. Si ejecuto mi aplicación veo que nos genera el error, creo las tablas y luego de haber realizado el select, cuando hizo el merge, realizó el delete para remover esa entidad.

[03:51] En este punto como yo estoy utilizando el método flush, yo puedo hacer un rollback, lo que quiere decir que yo puedo volver a mi valor anterior. Si yo había removido el valor de “SOFTWARE” realizando un rollback yo elimino esa última transacción y vuelvo a tener mi valor en la base datos.

[04:10] Si yo hubiese realizado el método commit esa operación sería definitiva. Entonces lo único que está faltando es agregar ese nuevo método dentro del DAO, va a ser el método remover, va a ser un método público que no va a retornar nada, lo vamos a llamar remover.

[04:33] Al igual que actualizar, va a recibir una entidad, una entidad categoría, la vamos a llamar categoría y tenemos primero que garantizar que se encuentre en un estado managed. Para eso vamos a resignar acá categoría, va a ser igual a this.em, llamando el merge y pasamos la categoría.

[05:12] Entonces con esto, nosotros estamos garantizando que la entidad se encuentre como Managed. Luego de eso, yo sí puedo utilizar el método remove del EntityManager. Entonces this.entityManager remove, paso la entidad que sería categoría y ya con esto queda construido nuestro método remover o eliminar de la clase DAO.

[05:36] La siguiente parte del curso nosotros vamos a ver los métodos de consultas, vamos a ver varios tipos de consultas, consultas por id, consultas con filtro, consultas con límites, lo que va a concluir todo lo que son las diferentes transacciones dentro del ciclo de vida de JPA.