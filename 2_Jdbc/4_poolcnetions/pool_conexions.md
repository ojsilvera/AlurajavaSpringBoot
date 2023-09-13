# ¿Qué es un pool y un datasource?

[00:00] Hola, ¿cómo les va? Antes de seguir con los nuevos contenidos del curso, vamos a hacer una revisión de cómo estamos con el proyecto. Nosotros estamos conectando nuestra aplicación con la base de datos MySQL. Aquí tenemos MySQL y tenemos nuestra aplicación Java. Y esas tienen una conexión.

[00:26] Pero nosotros aprendimos que estas dos partes no se conectan directamente. Voy a aumentar un poquito acá. Estas dos partes no se conecten directamente. ¿Por qué? Porque una es Java y la otra parte es una base de datos que tiene su propio protocolo de comunicación y hacerlo directamente no es tan sencillo así.

[00:50] Para resolver eso, nosotros agregamos un driver a nuestra aplicación, entonces tenemos acá un driver MySQL que nos facilita esta conexión, entonces desde el driver nosotros logramos hacer nuestra conexión a la base de datos. Y para cada base de datos tenemos un driver específico.

[01:16] Ahora nosotros ya estamos utilizando el MySQL, pero si nosotros cambiamos la base para el SQL Server, nosotros también tenemos que cambiar el driver de la aplicación. Y en lugar de ir al MySQL, estamos yendo a driver de SQL Server. Y eso cambia todo otra vez. Si hacemos eso, tenemos que salir modificando todo el código de la aplicación para cambiar las interfaces específicas de cada driver, como vimos en el inicio del curso.

[01:52] Para resolver esta situación, nosotros tenemos una interfaz llamada JDBC, que desde sus clases e interfaces logramos acceder a la implementación de los drivers de forma transparente, entonces con el JDBC acá, no importa para nosotros qué base de datos estamos utilizando, nosotros vamos a lograr conectarnos a ellos porque tenemos las interfaces y queda todo lo que es específico, queda transparente para nosotros.

[02:27] Bueno, con eso nosotros no sufrimos más cuando cambiamos la base de datos, entonces no importa qué base de datos es, con el JDBC nos conectamos acá con el MySQL y está todo bien. Avancemos un poco más. Avanzamos con el desarrollo y vimos que siempre repetimos la rutina de abrir una conexión con la base de datos.

[02:52] Enviamos nuevas informaciones de URL de conexión, usuario y contraseña, todas las veces. Si agregamos un nuevo método, una nueva clase que se conectaba a la base de datos, teníamos que replicar esta lógica y otra vez tendríamos un trabajo gigante de mantenimiento por culpa de esta replicación de código.

[03:14] Para resolver eso y facilitar aún más nuestro desarrollo, nosotros realizamos la refactorización del proyecto y acá nosotros utilizamos el patrón de diseño factory para crear la clase connectionFactory. Tenemos acá ahora connectionFactory, ¿qué hace? Ella centraliza esta lógica de apertura de una conexión con la base de datos.

[03:39] Entonces nosotros no tenemos más que estar replicando esta lógica para cada método, cada clase que estamos utilizando. Tenemos todo ahí en esta connectionFactory. Entonces entra un componente más a nuestra aplicación, acá el connectionFactory que hace este medio de campo acá para nosotros. Para arreglar un poquito más esto de acá voy a ponerlo en el tope, ahora sí.

[04:09] Y acá la connectionFactory que nos facilita eso. Listo, acá está la base de nuestro proyecto hoy. Ahora analicemos la siguiente situación. Todas las requisiciones que realizamos hoy en la aplicación hasta la base de datos son de una única conexión.

[04:26] Para cada operación que realizamos en la pantalla, la aplicación abre la conexión con el connectionFactory, realiza la operación en la base de datos y la cierra al final, pero cambiemos un poco el contexto y vayamos acá a la página de Alura. Acá en la página de Alura tenemos muchas categorías de cursos.

[04:52] Si hacemos un clic acá en cursos, tenemos las categorías, y cuando elijo una categoría acá voy a esta pantalla y ella muestra todos los cursos que están disponibles acá. Y supongamos que cada información de esta que tenemos en la pantalla está guardada en una base de datos.

[05:09] Y cada clic que hago acá para ver más informaciones del curso, una conexión con la base de datos es abierta. Entonces, cuando entro acá al curso de lógica de programación, se abre una nueva conexión, pero aquí en la página de Alura, al mismo tiempo que estoy accediendo a las páginas, hay otras personas que también están haciendo lo mismo.

[05:33] ¿Y cómo funcionaría esto en nuestra aplicación? Si realizamos una requisición y otra persona también la hace, ¿va a haber una cola para que la próxima requisición sea procesada al final de la primera? No tiene sentido, imagina el tamaño de la cola con miles de usuarios intentando acceder a las páginas de los cursos de Alura y esperando una eternidad.

[05:54] Entonces nuestra aplicación debe estar disponible para que más personas puedan utilizarla al mismo tiempo, pudiendo utilizar más conexiones con la base de datos en paralelo. Pero todo eso tiene un límite. ¿Hasta cuántas conexiones una base de datos puede atender? No importa cuál base de datos estamos utilizando, si hay es MySQL, Postgre SQL, SQL Server.

[06:17] Todas las bases de datos tienen un límite y pueden caer si llegan a eso. ¿Entonces cómo podemos solucionar esta situación y lograr atender a múltiples usuarios sin ahogar a nuestras bases de datos? La mejor alternativa acá es implementar una solución que pueda disponibilizar una cantidad equis de conexiones abiertas para atender a las requisiciones paralelas que ocurran.

[06:41] Pero nosotros no podemos dejar que la aplicación siga abriendo conexiones sin límite, entonces debemos poder configurar una cantidad mínima, una cantidad máxima de conexiones. Esta implementación va a comunicarse con el JDBC para abrir la cantidad establecida que nosotros configuramos de conexiones y listo.

[07:03] Entonces, acá en nuestro dibujo nosotros vamos a agrandar un poquito más acá porque vamos a tener un nuevo elemento acá. Entra acá una nueva cajita que va a estar ayudándonos a manejar esta cantidad de conexiones que están recreadas ¿Y esta cajita quién la implementa? ¿Nosotros? No. Por suerte, nosotros no necesitamos implementar esta funcionalidad porque hay un montón de librerías que ya tienen a esta necesidad.

[07:31] Incluso estas soluciones, conocida como pool de conexiones. Entonces aquí vamos a poner un nombre, pool de conexiones. Ahí está su nombre. Voy a subir el nombre acá para que quede más lindo. Y ahora sí.

[07:51] O sea, tenemos un pool de conexiones que va a comunicarse con el JDBC para mantener una cantidad mínima y una cantidad máxima de conexiones abiertas en la aplicación para que pueda atender a las requisiciones sin que tenga una cola muy grande y que no ahogue la aplicación.

[08:09] Tal como los drivers de base de datos, también hay varias opciones para drivers que manejen un pool de conexiones. El C3P0, acá voy a agregar, C3P0 es una de las opciones más conocidas en el mercado. Y su implementación es bastante sencilla, cómo vamos a ver más adelante en el curso.

[08:30] Para utilizarlo bien vamos a aprovechar las ventajas del JDBC para utilizar una nueva interfaz llamada datasource. Esta interfaz va abstraer la implementación del pool de conexiones para nosotros y con esta nueva estructura, la connectionFactory que tenemos no va más a tener la responsabilidad de crear una conexión para nosotros.

[08:52] Lo que ella va a hacer ahora es solicitar una conexión abierta para el data source, entonces acá esta cajita del pool de conexiones va a estar adentro de una super caja y acá yo voy a agrandar un poquito más el dibujo, así nosotros no nos perdemos, pero vamos a tener acá una super caja en donde este pool de conexiones del C3P0 va a estar acá dentro.

[09:23] Para traerlo, lo envío hacia atrás, ahora sí. Esto acá también. Ahí tenemos. Y esta super caja, como había dicho, va a llamarse datasource. Está en el tope, ahí está. Aquí adentro tenemos el pool de conexiones de C3P0, que es el que vamos a utilizar y acá dentro vamos a tener varias, pero varias pelotitas.

[09:57] Vamos con las pelotitas acá que son nuestras conexiones de base de datos que tenemos acá, todas preparadas con el mínimo y el máximo que podemos llegar, entonces acá va a estar siempre con el mínimo y cuando utilicemos todas, van a ser creadas más hasta que llegue al tope que configuremos.

[10:20] Y ahí el connection Factory va a solicitar el datasource y va a decir en lugar de la connectionFactory decir: "JDBC, dame una nueva conexión". El connectionFactory va a decir: "datasource, dame una conexión que tienes ahí en tu en tu pool de conexiones y yo sigo acá con mi trabajo", y el datasource es el que va a manejar toda esta parte de le doy una conexión nueva de una conexión que ya tengo acá creada, veo acá con mis configuraciones cómo esto va a ser manejado.

[10:53] De esta forma, nosotros no tenemos nuestra aplicación con una configuración sostenible de conexiones abiertas, así no tenemos ningún problema de performance ni de agotamiento de recursos, tal como las aplicaciones reales del mercado, y por ahora es eso.

[11:13] En las próximas clases vamos a tener un poco más de acción, implementando la utilización de esta nueva dependencia del pool de conexiones. Vamos a ver cómo funciona el control del pool de conexiones y cómo funciona una implementación de la interfaz de datasource.

# Creando un pool de conexiones

[00:00] Hola, ya revisamos el proyecto y planteamos los próximos pasos para dejar nuestra aplicación más completa y siguiendo las prácticas del mercado. Ahora vamos a implementar el pool de conexiones para que nuestra aplicación tenga un mejor control de las mismas, sin comprometer tanto la experiencia de los usuarios como la base de datos.

[00:19] Lo primero que vamos a hacer es agregar el driver de C3P0 a nuestra aplicación. Y acá desde que empezamos con el proyecto estamos tratando la importación de librerías como dependencias del Maven, y con esta no va a ser distinto.

[00:33] Acá en Eclipse nosotros vamos a abrir el archivo pom.xml para agregar esta dependencia de pool llamado C3P0, y junto con ella vamos a agregar una dependencia más también que se llama mchange como Java. Ya les muestro cómo va a quedar el Código.

[00:49] Acá en la tag de dependencies, en donde agregamos todas las dependencias, nosotros vamos a hacer la dependency, agregamos una acá y la primera va a ser la de C3P0. Entonces su groupId va a ser com.mchange, ese es el groupId, y el artifactId va a ser c3p0, así. Y la versión que vamos a estar utilizando en este curso es la 0.9.5.5. Listo, esta es la dependencia de C3P0.

[01:30] La otra dependencia que vamos a agregar es esta de acá, dependency y ahí ponemos el groupId, que va a ser también com.mchange. El artifactId va a ser mchange-commons-java y la versión va a ser la 0.2.20. Okay, ¿pero qué son estas dependencias?

[02:04] Bueno, la primera acá, la de C3P0, nos va a dar la posibilidad de configurar un pool de conexiones y esa segunda del mchange-commons-java nos va a dar la posibilidad de agregar más detalles del datasource vía el log de la aplicación en la consola.

[02:22] Bueno, cuando con las dependencias agregadas ahora, nosotros vamos a la clase connectionFactory para realizar los cambios necesarios para la configuración del pool de conexiones. La idea acá es que la connectionFactory utilice las conexiones desde el pool de conexiones, en lugar de salir creando una conexión de forma pura, como estamos haciendo ahora.

[02:42] Bueno, aquí en la connectionFactory entonces vamos a crear un constructor connectionFactory acá, pongo el nombre de la clase y ya me aparece la ayuda para el constructor. Y acá en el constructor nosotros vamos a crear una variable que va a hacer el pooledDataSource. ¿Y qué va a recibir este esta variable? Va a ser un new de ComboPooledDataSource();

[03:11] A ver si ya se hizo el auto complete y ahí está. Esta clase es la de C3P0. En esta instancia del pool nosotros vamos a estar configurando la URL de la base de datos, el usuario y la contraseña, tal como estamos haciendo con la conexión. Entonces yo voy a estar copiando acá esta variable para que sea más rápido y con el pooledDataSource yo voy a hacer un setJdbcUrl. ¿En dónde?

[03:37] Acá voy a copiar esta URL que ya tenemos y la pegamos acá. La segunda cosa que vamos a hacer es en el pooledDataSource vamos a poner el setUser. Y en el user, vamos a escribir la string ("root"). Y por último, en el pooledDataSource vamos a poner un setPassword. Y el Password va a ser el ("root1234").

[04:09] Inicializamos este objeto, ¿pero qué hacemos con él ahora? Bueno, ahora lo que vamos a hacer es en la connectionFactory nosotros vamos a crear un atributo privado llamado DataSource de la clase java.sql y acá datasource también. Y nosotros vamos a asignar este pooledDataSource a este atributo.

[04:34] Entonces this.datasource = pooledDataSource, ahí está. Y por último, nosotros vamos a cambiar esta implementación de recuperar conexión y en lugar de estar utilizando todo lo que hacíamos de JDBC, nosotros vamos a estar haciendo, borrando esto y vamos a dar un return this.datasource.getConnection(); por fin vamos a organizar los importes que no estamos más utilizando y listo.

[05:04] Cambiamos, agregamos dos dependencias y cambiamos una sola clase y ya podemos ver que el proyecto no se rompió. Vamos a ejecutar la aplicación para ver si las cosas siguen funcionando. Ahí voy a levantar la aplicación. Bueno, ahí está la pantalla con todos los productos listados y todo sigue funcionando normalmente.

[05:23] La única diferencia es que en lugar de estar creando una conexión por el driver manager, nosotros estamos tomando la conexión desde el pool para realizar las operaciones en la base de datos. Y para complementar la utilización de las dependencias que agregamos, podemos ver acá en la consola, ahí voy a agrandar un poquito más.

[05:43] Podemos ver acá en la consola que tenemos las informaciones sobre la instanciación del pool de conexiones. Acá podemos ver que en el Initializing c3p0 pool tenemos un montón de configuraciones: acquireIncrement, acquireRetryDelay, CommitOnClose, hay un montón de configuraciones acá y yo les recomiendo leer la documentación de C3P0 para entender qué hace cada una.

[06:13] Les recomiendo leer la documentación. ¿Por qué? Porque acá, para no salir mucho del objetivo del curso, nosotros vamos a enfocarnos en algunas configuraciones que son clave. Entonces ya configuramos acá el pool de conexiones, voy a agrandar acá la pantalla. Ahora sí.

[06:29] Ya las configuramos acá y para la próxima clase vamos a ver más características que podemos configurar como la cantidad máxima y la cantidad mínima de conexiones que este pool puede mantener abiertas. Y también tenemos que ver qué va a pasar si necesitamos consumir más conexiones que las que están en el pool. Nos vemos en la próxima clase

# probando el pool

[00:00] Hola. Vamos a seguir con las configuraciones del pool de conexiones, ya lo dejamos acá configurado en la clase de connectionFactory, pero aún no realizamos la prueba real de que este pool realmente funciona, levantamos la aplicación y vimos que está todo bien, pero vamos a hacer una prueba de las buenas.

[00:17] Pero antes de hacer las pruebas, vamos a realizar una configuración adicional acá en el político de conexiones que es para determinar la cantidad máxima de conexiones que este pool puede mantener.

[00:28] Entonces acá en la connectionFactory, nosotros vamos a setear la cantidad máxima de conexiones en el pool con el método de acá de pooledDataSource.setMaxPoolSize y vamos a decir que tiene un valor de 10, o sea, el máximo de conexiones que podemos mantener abiertas acá va a ser de 10 conexiones.

[00:51] Y ahora que guardamos eso nosotros vamos acá, en el paquete de pruebas vamos a crear una nueva clase que se llama PruebaPoolDeConexiones. Y en ella vamos a hacer algunas pruebas para ver cómo funciona eso. Acá en la clase PruebaPoolDeConexiones, nosotros vamos a crear el método main y acá vamos a poner la lógica para hacer la prueba de una simulación de múltiples conexiones a la base de datos.

[01:22] Entonces lo primero que vamos a hacer acá es instanciar una nueva ConnectionFactory. Acá tenemos una ConnectionFactory, ahora sí, la vamos a asignar a una nueva variable. Y esta variable nosotros la vamos a hacer a interarla en un loop de 20 iteraciones para solicitar la apertura de 20 conexiones.

[01:44] Entonces hacemos acá un for (Int i = 0; i < 20; i++) Acá, adentro del loop vamos a hacer un connectionFactory.recuperaConexion(). Ya me había olvidado el nombre del método. RecuperaConexion, la vamos a asignar a una conexión. Acá, a ver, acá está una conexión. Conexión con como siempre ponemos el nombre.

[02:22] Bueno, ahí el Eclipse dejo conexión, dejemos conexión entonces. Hemos sacado la conexión y vamos a imprimir que estamos abriendo la conexión de número. Y acá vamos a hacer (i + 1); porque quiero saber cómo es, qué número de conexión es esta es la que estamos abriendo.

[02:49] Acá voy a hacer un throws del SQLException. Y ahora vamos a ver cómo funciona eso. Vamos a ejecutar esta clase y vamos a ver en la consola qué está pasando. Está la consola, voy a agrandar un poquito y tenemos acá un for de 0 hasta que i sea menor que 20, pero tenemos 10 conexiones abiertas hasta el momento.

[03:16] ¿Qué pasó con eso? Nosotros solicitamos 20 conexiones, pero fueron abiertas las 10 conexiones del pool. Está bien, el loop está parado, esperando que una conexión se quede disponible para utilizarla. ¿Eso también es así en el mundo real? Sí, es así que funciona. Si llegamos al tope de conexiones de pool, el próximo cliente va a tener que esperar un ratito hasta que el procesamiento de un cliente termine y él va a poder utilizar la próxima conexión libre.

[03:46] De esta forma, nosotros limitamos la apertura descontrolada de conexiones y no saturamos la base de datos. Y esta cola de espera para una próxima conexión es muy rara de suceder en el mundo real, porque los procesamientos son muy rápidos. Entonces acá vamos a la consola de MySQL y vamos a ver cómo está el listado de conexiones abiertas.

[04:07] Ya estamos acá con la consola abierta y vamos a ejecutar el comando show. A ver, ahora sí, show processlist; Ahora sí. Y podemos ver acá la tabla de conexiones abiertas, podemos ver acá 1, 2, 3, 4, 12 filas, acá dice, mejor que estar contando, acá abajo dice 12 filas que están acá en nuestra tabla.

[04:35] O sea, hay 12 conexiones abiertas, 10 de ellas son conexiones nuestras que estamos acá abiertas. Una de estas conexiones es la conexión de la query que ejecutamos ahora la de show processlist, y esta es una conexión que queda ahí, de la propia base de datos.

[04:54] Con esta prueba nosotros podemos jugar un montón para realizar muchas otras pruebas y explorar las otras configuraciones de C3P0. Recomiendo una vez más dar una ley de la documentación de C3P0 para aprender más sobre esta librería y aprovechar sus recursos de manera optimizada.

[05:12] Bueno, y ahora que probamos, que el pool está funcionando, vamos a dar seguimiento a los otros temas para completar más aún nuestra aplicación y seguir aprendiendo algunas prácticas del mercado también. Nos vemos en la próxima clase.

# capa de persistencia en DAO

[00:00] Hola. Para avanzar con el curso y la evolución de nuestra aplicación, vamos a revisar el método guardar de la clase productoController. Estamos realizando la operación de insert en la tabla de producto, con los parámetros que recibimos en el método, y lo enviamos como parámetros de try(statement).

[00:18] Hasta ahora venimos tratando los atributos de las tablas como variables sueltas, sin ninguna representatividad del producto en el código, tal como tenemos en la tabla de la base de datos.

[00:29] La idea ahora es, en lugar de estar asignando variables sueltas, como estamos haciendo acá, recibidas como parámetros, vamos a crear una forma de representar el producto directamente en el proyecto en Java. O sea, vamos a crear un modelo y para eso, nosotros vamos a crear una clase en un nuevo paquete y esta clase va a ser llamada de producto, para representar justamente la tabla de producto.

[00:56] Entonces acá, en nuestro Explorer nosotros vamos a hacer un new de package y el paquete va a llamarse com.alura.jdbc.modelo. ¿Por qué? Van a ser las clases de modelo que representan las tablas, pero en la aplicación. Tenemos el paquete y aquí en el paquete vamos a hacer un new class que va a llamarse de producto. Perfecto.

[01:25] Ahí tenemos la clase producto, que va a empezar a representar la tabla de producto. Bueno, como una idea es que el producto, acá la clase, represente la tabla, entonces esta clase tiene que tener los mismo campos de la tabla. Los campos son entonces un private Integer id; vamos a tener también un private String descripcion; vamos a tener un private String nombre;

[01:55] Acá voy a cambiar el orden para que quede igual que la tabla. Por último un private Integer cantidad; ahí está. Todos estos atributos están como privados para que no tengamos el encapsulamiento de la clase.

[02.12] Por ahora, vamos a dejarlos así. Vamos a crear los métodos, los getters, setters, constructores acorde vayamos necesitando en el desarrollo del proyecto. Voy a guardar acá en la clase. Guardé el producto, dejé los campos acá y ahora volvemos para el productoController en el método guardar. Voy a agrandar una vez más acá, ahí está.

[02:35] Vamos a entrar al método que llama el guardar. O sea, para saberlo vamos a hacer un clic acá, en el método guardar, clic derecho del mouse y vamos a elegir esta opción de acá: Open Call Hierarchy. Hacemos un clic en ella y acá se abrió el método rojito acá, guardar de ControlDeStockFrame.

[02:58] De esa forma nosotros logramos saber quién está llamando a este método. Puede ser en más de un punto de la aplicación. En este caso tenemos un solo punto que es el método guardar del frame. En este método de guardar nosotros estamos tomando los datos del formulario y lo estamos agregando acá, adentro de un HashMap.

[03:19] Esto de acá, este HashMap lo estamos enviando al productoController para hacer el guardado allá, el insert en la tabla de producto. Esto nosotros lo vamos a cambiar. Entonces acá, este HashMap va a tornarse el producto ahora. Entonces vamos a cambiar el HashMap para el producto que recién creamos. Vamos a tomar estas variables que están acá, todas estas de producto de input, que tenemos de nombre, descripción y la cantidad entero.

[03:49] En lugar de estar transformando todo en string, vamos a hacer un new Producto() y adentro acá del constructor que aún no tenemos, nosotros vamos a estar agregando nuestros parámetros para este constructor. Al final de esto, nosotros vamos a crearlo para asignar los valores a las variables.

[04:13] Como la cantidadInt ya está en el tipo que nosotros tenemos en la clase de producto, nosotros no necesitamos hacer la conversión de string.valueOf como estábamos haciendo. Entonces esta parte se borra, el producto acá, como el Eclipse se queja, nosotros hacemos un control o command 1 primero para importar la clase y ahora sí vamos a crear un constructor para este tipo producto.

[04:41] Lo voy a mover acá para dejar un poco más ordenado. Ahora sí. El primer campo es el nombre, el segundo es la descripción y el tercero es la cantidad. Esos campos van a ser un this.nombre = nombre; this.descripcion = descripcion; y this.cantidad = cantidad; ahí está.

[05:12] Inicializamos nuestro objeto y lo estamos enviando para el método guardar de productoController. Acá el método guardar queda acá rojito, una queja, porque nosotros estamos enviando un objeto del tipo producto y en la declaración del método, de la firma del método, estamos esperando un map del String string. Lo que vamos a hacer acá es cambiar esto para el producto también.

[05:38] Producto, ahí está. Importo la clase, guardo todo y cuando vuelvo para el frame ya no se queja más, está todo bien. Vayamos ahora entonces para el productoController porque acá tenemos que seguir haciendo unos cambios. Acá como cambiamos el map por el objeto del producto, ya no tenemos más cómo buscar las informaciones por la clave del HashMap.

[06:06] ¿Entonces qué vamos a hacer acá? El producto.get va a ser getNombre, vamos a crear un método para esto, getNombre. Lo mismo va a pasar para la descripción. Vamos a crear este método también, y ya no necesitamos más hacer este cambio, esta conversión en realidad, porque ya tenemos acá el getCantidad con el tipo correcto.

[06:35] Lo que no tenemos todavía es la declaración de estos métodos en la clase de producto. En lugar de salir creando una por vez acá, vengamos a la clase de producto y vamos a hacer lo siguiente. Vamos en el teclado a utilizar las siguientes teclas: La command o Control y la 3, número 3 y vamos a escribir ggas, que tiene la opción de generate getters and setters.

[07:04] Acá acemos un clic, en este caso vamos a estar haciendo un select getters, pero solamente de los tres campos que estamos utilizando. El de id todavía no lo vamos a utilizar entonces no lo vamos a generar. Ahí lo generamos, están todos los getters creados, guardé la clase y ya tenemos todo bien hecho acá también. Aquí podemos hacer una mejora más todavía.

[07:30] Mira una cosa. Nosotros acá en el método ejecuta registro, podríamos en lugar de estar pasando el nombre, la descripción y la cantidad, nosotros ya podríamos estar pasando directamente el valor de producto para guardar en la base de datos.

[07:48] Acá podemos seguir haciendo alguna mejoras, por ejemplo, el método acá de ejecutaRegistro, nosotros recibimos el producto, asignamos sus valores, sus atributos a variables y estamos enviando las variables para el método de ejecutaRegistro que realiza el insert en la base de datos.

[08:07] Lo que podemos hacer acá es, en lugar de estar utilizando el nombre, descripción y cantidad para guardar, enviar directamente el producto para esta clase, para este método, perdón, y acá en este método nosotros hacemos un Producto producto.

[08:27] Y en esos valores de setString, setString, setInt, nosotros utilizamos el producto.getNombre, producto.getDescripcion y producto.getCantidad. Ahí está. Nosotros podemos sacar esta lógica acá también del error. Podemos sacar. Para dejar el código un poco más sencillo, vamos a sacar esta lógica de valores máximos, para guardar en la base de datos, así nosotros podemos eliminar toda esta asignación de variables, para dejar más sencillo también.

[09:07] Entonces, ya aprendimos cómo funciona acá el control de transacciones, la vamos a seguir haciendo, pero la lógica ya no la tenemos más. Así estamos enviando el producto, recibimos acá la representación de un producto, un objeto. Lo están enviando para ejecutar el registro y acá solamente estamos utilizando sus valores, sus campos, para poder ejecutar de hecho la query de insert en la base de datos.

[09:38] Por fin, ¿qué vamos a estar haciendo? Acá en este resultSet, en lugar de estar imprimiendo el resultado acá, nosotros vamos a tomar este id que fue generado y lo vamos a asignar al producto. Entonces el producto.setId va a recibir este valor. Nosotros vamos a generar este método acá, el id.

[10.06] Vamos a hacer this.id = id; y acá en la impresión, en el system.out.println nosotros vamos a hacer lo siguiente. Voy a insertar el producto y esto vamos a cambiar para %s de string y vamos a arreglar el producto acá. Pero si hacemos esta forma, el toString del producto ¿va a estar haciendo qué? Va a imprimir la referencia del objeto en la memoria.

[10:37] Entonces nosotros tenemos que acá en el método, en la clase de producto, sobrescribir el método toString. Entonces hacemos aquí toString y el Eclipse ya nos ayuda con eso y hace la sobrescritura de este método para nosotros en lugar de llamar el super, nosotros vamos a hacer la siguiente lógica.

[11:00] String.format, vamos acá. Hacemos el format acá y vamos a dejarlo más o menos parecido con JSON. Va a hacer el "{id: %s, nombre: %s, descripción, %s, cantidad: %d}". Acá es una d porque es un valor numérico y ahí está. Cerramos la clave del JSON y ahora agregamos el this.id. Lo voy a poner más abajo para que podamos leer mejor.

[11:51] this.id, this.nombre, this.descripcion y this.cantidad; listo. Guardé los cambios y ahora vamos a ejecutar nuestra aplicación para hacer las pruebas de estos cambios. Bueno, ya se levantó la aplicación y acá voy a agregar un producto nuevo que es un teclado. Y va a ser un teclado inalámbrico de 10 cantidades.

[12.21] Voy a guardar, ahí lo guardé, se registró. Mira, teclado acá de id 25, y tenemos acá en el log de la aplicación en la consola: Fue insertado el producto {id: 25, nombre: Teclado, descripción, Teclado Inalámbrico, cantidad: 10}. Ahí está, ahí me equivoqué. En lugar de poner dos puntos, puse coma, pero ahí están los valores todos bien. Listo.

[12:49] Ahora tenemos la representatividad del producto con una clase Java representando la tabla de la base de datos. Ahora tenemos que replicar esta solución para los demás métodos.

[13.00] Entonces acá nosotros vamos a tomar esta referencia de producto para hacer lo mismo con el listado, para el de eliminación y el de modificación también. Pero antes, veamos una cosa. En todos estos métodos que nosotros creamos para realizar alguna operación en la base de datos, nosotros tenemos que recuperar la conexión, crear un PreparedStatement para ejecutar la operación.

[13:28] Nosotros ya vimos esta situación anteriormente cuando creamos la connectionFactory para evitar la replicación del código. ¿Cómo hacemos para evitar esta situación que encontramos ahora? Debe haber alguna forma de extraer esta parte para un método o algo similar. Bueno, por ahora nosotros quedamos por aquí.

[13:47] En la próxima clase vamos a ver cómo resolver esta situación y hacer una buena refactorización en esta clase para seguir utilizando el modelo de producto.

# DAO CON INSERT DE PRODUCT

[00:00] Hola. En la clase anterior creamos la representación de la tabla producto en la clase de modelo en la aplicación para que podamos realizar la persistencia de los datos. Pero acá en el productoController, nosotros vimos que siempre que vamos a realizar cualquier tipo de operación en la base de datos, nosotros tenemos que abrir una conexión, crear un statement, tenemos un montón de código repetido. ¿Cómo podemos mejorar eso?

[00:29] Nosotros podríamos crear una clase que mantenga todos lo que es necesario, como la conexión de la base de datos para persistir el producto y solamente tengamos que basar el objeto como parámetro. Sería una clase más específica para realizar operaciones en la tabla de productos. Vamos a probar esta idea viendo una clase llamada persistencia producto. ¿Qué les parece?

[00:51] Esta clase vamos acá, a abrir acá y crear un paquete nuevo. Vamos a poner un paquete new package com.alura.jdbc.persistencia y vamos a crear una nueva clase que se llama PersistenciaProducto. Ahora sí, con CamelCase. Acá voy a agrandar un poquito. Esta clase va a tener como atributo la conexión, entonces vamos a tener acá un private Connection, ya importo acá, con; y esta conexión nosotros vamos a asignarla desde un constructor.

[01:40] Entonces vamos a tener acá un PersistenciaProducto, un constructor, que recibe una (Connection con) también. Y nosotros la vamos a asignar a nuestro atributo de connection que tenemos en la clase. ¿Ahora qué vamos a hacer? ¿Qué estábamos diciendo? Que íbamos a registrar un nuevo producto, entonces podemos crear acá un método llamado guardarProducto.

[02:13] Entonces vamos a hacer así, vamos a hacer un public void guardarProducto y nosotros recibimos como parámetro un producto. Perfecto. ¿Qué lógica agregamos a este método? Importo acá el producto primero. Acá en este método, vamos a agregar la lógica de productoController, entonces todos este método que tenemos, vamos a copiar acá y pegar acá en la clase de persistenciaProducto.

[02:47] Lo mismo con el ejecutar registro, porque es el método que estamos finalmente haciendo la persistencia. Entonces esta lógica también viene para acá y lo que tenemos en productoController, podemos borrar esto, ya que lo movimos para persistenciaProducto. En esta lógica de guardar, nosotros podemos eliminar esta información, toda esta lógica y podemos hacer lo siguiente.

[03:16] Vamos a, en lugar de eso, vamos a instanciar un new PersistenciaProducto pero tenemos que enviar una conexión. Entonces vamos a hacer lo siguiente, vamos a hacer un (New ConnectionFactory().recuperaConexion()); vamos a hacer esto y vamos a asignar eso a una variable y este persistenciaProducto vamos a llamar al método persistenciaProducto.guardarProducto(producto); ahí está. Ya dejamos la lógica mucho más sencilla en el controller.

[04:08] Y si nosotros queremos hacer esto con el listado de productos, nosotros podemos hacer algo similar a esta lógica también, pero antes de seguir con eso vamos a entender qué está haciendo esta nueva clase que creamos, la persistenciaProducto. Nosotros tenemos acá nuestra aplicación en Java y la base de datos de MySQL y en el medio de este camino estamos agregando una cajita nueva acá, que es la clase persistenciaProducto.

[04:41] Ahí quedó el nombre chiquitito pero agrando un poquito acá. O sea, tenemos la clase persistencia producto que está en el medio del camino para nosotros. Acá estamos haciendo la aplicación, llama a persistencia producto, que accede a MySQL para realizar la operación de guardar el producto, un producto nuevo en la base de datos.

[05:09] La idea de esta clase es dar todo el acceso a las operaciones de base de datos para la entidad de producto. Entonces esta clase lo que está haciendo es tratar todas las operaciones en la tabla de producto. Entonces su finalidad es acceder a los datos de nuestro objeto.

[05:28] Si nosotros queremos guardar un nuevo producto, la aplicación va a crear un objeto acá, lo va a enviar para la clase persistenciaProducto, que va a ser la operación de insert en el MySQL en la base de datos. Este tipo de clase y su instancia tiene un nombre específico, esta clase de persistencia producto. Ella tiene un nombre específico, ese nombre es Data Access Object, que también es conocido como DAO.

[05:56] Las clases del tipo DAO, y acá voy a dejar arriba el nombre DAO Data Access Object, estas clases del tipo DAO trabajan con las operaciones de acceso a los datos de una entidad. Entonces nosotros podemos decir que esta clase de persistenciaProducto es un DAO que trabaja con la entidad de producto.

[06:28] Entonces nosotros podemos cambiar su nombre acá, podemos decir que en lugar de persistenciaProducto, ella se llama producto DAO porque es la clase que tiene, que realiza el acceso a los datos de producto. Entonces aquí en Eclipse, nosotros vamos a hacer lo siguiente. La clase persistenciaProducto acá está lanzando un errorcito que es de SQLException, está bien.

[07:06] Pero en la clase persistencia producto nosotros podemos cambiar su nombre acá, podemos cambiar su nombre en la clase persistencia producto, hacer un refactor y vamos a llamarla de ProductoDAO. Ahora sí tenemos esta clase con el nombre más alineado con los estándares en los patrones de diseño y listo.

[07:38] Otra cosa que podemos hacer acá para mejorar es, ya que tenemos la conexión, que la recibimos desde el objeto, desde el controller, nosotros no necesitamos más estar instanciando acá esta conexión, porque ya la tenemos en la propia clase. Entonces, esto de acá también podemos cambiar y ya lo estamos utilizando directamente acá en el Try with resources.

[08:06] Lo declaré como final acá para que no se rompa y ya estamos también, ya tenemos la conexión del DAO y lo estamos utilizando en el guardar producto. Ya sacamos esta responsabilidad del propio método de estar solicitando una conexión para el data source.

[08:21] Otra cosa que podemos hacer acá es cambiar el nombre del paquete que estamos. Ya no es más persistencia, nosotros podemos decir que el nombre de este paquete es DAO también, ya que vamos a tener todas las clases DAO acá.

[08:38] Entonces voy a guardar acá estos cambios y ahora si va a ser com.alura.jdbc.dao en donde vamos a estar guardando las clases DAO de nuestro proyecto. O sea, esta clase acá de producto DAO va a tener centralizadas todas las operaciones que se refieren al acceso a la tabla de producto. Van a estar ahí dentro de la clase producto DAO.

[09:06] Otra cosa que vamos a estar haciendo acá es, en el productoController estuvimos haciendo el persistenciaProducto, vamos a cambiar su nombre ya que no es más persistenciaProducto y si productoDAO. Hacemos acá un refactor, rename y ponemos productoDAO perfectamente.

[09:27] Y el método guardarProducto, ya que sabemos que este objeto solamente maneja las operaciones sobre la tabla de productoDAO, sobre la entidad de productoDAO, podemos decir que es el guardar. Entonces, productoDAO.guardar y ya sabemos que está haciendo una operación de guardar un producto nuevo en la base de datos.

[09:51] Listo. Más allá de realizar nuestro código una vez más, aprendimos un nuevo patrón de diseño que es el DAO. La finalidad de este patrón de diseño es tener un objeto que tiene como responsabilidad acceder a la base de datos y realizar las operaciones necesarias sobre la entidad.

[10:10] ¿Entonces este patrón sirve solamente para acceder a bases de datos? No necesariamente. Podemos acceder a cualquier fuente de datos con este patrón. La idea es justamente centralizar las operaciones en él para evitar la replicación de código. Agregamos una capa de persistencia a nuestra aplicación y ella va quedando cada momento más ordenada y completa, muy similar a las operaciones del mundo real.

[10:36] En la próxima clase nosotros vamos a finalizar la refactorización del código moviendo el resto de las operaciones del listado borrado y modificación para el DAO.

# operacion del listado del productoDAO

[00:00] Ahora que conocimos el patrón del diseño DAO y entendimos su responsabilidad, vamos a seguir refactorizando la clase productoController para mover toda la lógica de acceso a la base de datos para la clase productoDAO. La primera operación que vamos a mejorar va a ser la del método listar.

[00:16] La idea es mejorar este método para que, más allá de utilizar el producto DAO para acceder a la base de datos, nosotros también vamos a estar utilizando la clase de modelo producto para que tengamos una mejor representatividad del modelo en nuestro código.

[00:31] Lo primero que vamos a hacer aquí en el método listar va a ser instanciar un productoDAO. Vamos a hacer un productoDAO = new ProductoDAO y recibe en new ConnectionFactory().recuperaConexion(). Entonces aquí estamos instanciando el productoDAO que recibe una conexión de nuestro pool de conexiones. Pero si lo estamos instanciando aquí, vamos a estar repitiendo la operación que ya hicimos en el método guardar.

[01:08] Estamos instanciando el mismo objeto en varias partes de la clase de productoController. Entonces en lugar de instanciar productoDAO adentro de cada método del productoController, para estar repitiendo el código así, lo que vamos a hacer es convertir esta variable en un campo de la clase productoController.

[01:28] Y acá este productoDAO lo que vamos a hacer es moverlo de acá y lo vamos a llevar aquí hacia arriba. ¿Para hacer qué? Lo vamos a inicializar cuando nosotros inicialicemos el productoController. ¿Cómo se hace eso? En un constructor. Entonces aquí voy a crear un constructor de productoController, en donde cuando inicialicemos este objeto nosotros vamos a hacer un this.productoDAO = ProductoDAO, acá lo había copiado y ya lo tenía.

[01:57] new ProductoDAO con el connectionFactory().recuperaConexion(). Pero aquí una vez más, Eclipse se queja de SQLException. Llegamos a un punto en que tenemos que tratar esta situación de otra forma. No podemos más estar declarando que todos lo métodos lancen la SQLException.

[02:17] Aquí lo que está pasando es que, siempre que declaramos y nuestros métodos lanzan una excepción, nosotros delegamos la responsabilidad para que sea tratada en otro lugar. En nuestro caso la estamos tratando en ControlDeStockFrame. Acá, si miramos acá, en esta clase tenemos varios try catch, en donde estamos haciendo un catch de SQLException.

[02:40] Entonces eso está mal. No es una buena práctica el hacer eso, delegar las excepciones de una capa para otras. Lo ideal es que las tratemos en el mismo lugar en donde el error ocurre. Entonces, en este caso acá de connectionFactory ¿en donde tenemos que tratarla? Adentro de connectionFactory.

[03:00] Entonces vamos a entrar en el método recuperaConexion y en este comando acá de dataSource.getConnection(); que es donde ocurre la posible excepción, nosotros la vamos a agregar dentro de un bloque de try catch, igual como estamos haciendo en el ControlDeStockFrame, nosotros vamos a hacer un throw new RuntimeException.

[03:26] Ahí está. Y vamos a encapsular la excepción original y así tenemos una excepción no chequeada que podemos lanzar sin ningún problema. Va a ocurrir un error, pero por lo menos nosotros no tenemos que estar propagando esa declaración de que este método lanza una excepción y eso va subiendo hasta el primer lugar que lo llama.

[03:49] La idea es que con eso, de a poco vayamos sacando el throws SQLException de los otros métodos también. Acá podemos hacer lo mismo en productoDAO por ejemplo. Aquí, este throws SQLException de guardar nosotros podemos sacarlo y en ese try de acá, el primero, este exception, nosotros lo vamos a cambiar para SQLException, ahí está mejor.

[04:22] Y nosotros vamos a sacar este control también, de la transacción que ya vimos que funciona. La vamos a sacar, y aquí en lugar de estar haciendo un print stack trace o row back, vamos a estar haciendo otra vez el throw new RuntimeException(e); ahora sí, con la excepción encapsulada también. Listo.

[04:49] Aquí en productoController, en el método guardar, nosotros podemos sacar este throws SQLException y por consecuencia, en el ControlDeStockFrame, tenemos que venir al método de guardar también y sacar este bloque de try catch porque no es más necesario. Ahora sí sacamos la responsabilidad del ControlDeStockFrame para el método de guardado. Listo.

[05:15] Ahora vamos a volver aquí en el método de listar del controller. Y la idea es que nosotros tomemos el atributo de productoDAO que acá ya lo podemos sacar, de guardar, ya no necesita más y nosotros vamos a tomar el product DAO aquí, vamos a hacer un productoDAO.listar(); entonces este productoDAO tiene que devolvernos este listado de productos que el controller estará haciendo ahí.

[05:49] Entonces esta lógica de acá la vamos a mover para adentro del método listar de productoDAO. Ahora entonces vamos a, primero sacar este SQLException y todo este pedazo de código que tenemos aquí en el controller, nosotros lo vamos a cortar y mover para el nuevo método de productoDAO que vamos a crear ahora, haciendo command o "Ctrl + 1" y creamos el método en la clase productoDAO.

[06:15] Aquí voy a borrar esta parte y vamos a pegar el método aquí, está bien ahí. Ahora lo que vamos a hacer, ya tenemos aquí esta parte, esto acá lanza un SQLException. ¿Qué vamos a hacer? catch (SQLException e) y hacemos un throw new RuntimeException(e); con la excepción original encapsulada. Ahora, lo que tenemos que hacer es cambiar este map para el producto, para que tengamos la representatividad que habíamos dicho.

[06:56] Ya realizamos la primera parte que era mover la lógica de acceso a los datos para el productoDAO y ahora vamos a la segunda parte, en donde vamos a convertir el map para el producto. Empezando aquí, ya vamos a, en la declaración, a hacer un producto acá. Ya hacemos este cambio, en este list de resultado hacemos lo mismo también y acá en el map, en donde estamos mapeando el resultado para agregar al listado, nosotros vamos a hacer un producto.

[07:30] Podemos mantener el nombre fila, no hay problema, pero aquí, en lugar de estar haciendo un fila.set cada campo, vamos a crear el constructor de producto y vamos a estar recibiendo todos los valores que ya tenemos. Entonces, este ID es un entero, ya no necesitamos más enviar como un string, el próximo campo es el nombre ya lo podemos sacar también y agregarle el constructor.

[07:56] Acá estoy moviendo los valores. Pero si quieren pueden escribir también, pero aquí estamos haciendo ahora la descripción y por último la cantidad. Vean que estoy agregando los valores así como son: Int, string, string, Int otra vez. No estoy más convirtiendo todo para un string porque el producto tiene sus atributos con sus tipos ya bien declarados.

[08:25] Entonces esta parte de fila.put podemos sacar todo y por último, vamos a crear este constructor acá en producto. Ahí está. Vamos a cambiar los nombres. Acá los nombres son id, nombre, descripción y por último cantidad. Ahora vamos a asignar todos los valores, this.id = id; this.nombre = nombre; this.descripcion = descripcion; this.cantidad = cantidad; ahí está.

[09:09] ¿Ahora qué falta? Falta aquí en productoController cambiar este retorno para que sea un listado de producto. Ahora sí. Ya lo tenemos pero aún hay un errorcito aquí, vamos a ver qué pasa. No pasa nada más. Faltó solamente guardar el productoDAO, ahí está. Ahora sí, y por último en el ControlDeStockFrame, vamos al método de listado para cambiar el resultado de productos para.

[09:40] Acá podemos sacar también ya este try catch. Miren qué bueno eso. Este productos podemos hacer un elegí todo y puse, listo, var productos = this.productoController.listar(); y ete var en el Java 11 ya dinámicamente en scopes locales, ya en la asignación, nosotros cuando declaramos una variable Java tenemos que inicializar con su valor.

[10:10] En la inicialización, la JVM ya sabe cual es su tipo. Entonces, en este caso el var de productos va a ser del tipo list de productos. Acá por último, tenemos los gets del Map que tenemos que convertir para los getters que tenemos en la propia clase de producto. Entonces getId, getNombre, getDescripcion y el último acá getCantidad.

[10:41] ¿Qué falta? Falta crear el getId, entonces aquí venimos, hacemos un getId de Integer y hacemos un return this.id, pero para dejar mas organizado acá el código, voy a dejarlo junto de su set, así tenemos todo bien ordenado. Guardé acá los cambios, hice un organize imports y ahora vamos a probar.

[11:14] Listo. Todo sigue funcionando igual y nuestra aplicación va quedando cada vez más linda y completa, siguiendo buenas prácticas de programación y estándares de desarrollo del mercado.

[11:25] Vamos incrementando cada vez más la capa de persistencia y acceso a los datos acá en el productoDAO. Y las próximas operaciones que vamos a hacer son las de modificación y exclusión de un registro, que están en productoController todavía. Así nosotros vamos a completar todas las operaciones de ABM, que son alta, baja y modificación, y también la del listado.

[11:48] Ahora cada capa de aplicación tiene su responsabilidad bien definida. La capa DAO acá se encarga de mantener toda la lógica de acceso a la base de datos, las queries y traducción de result set para la clase de producto que es nuestro model, y la capa de controller se encarga de llamar las demás clases para completar la operación solicitada por la view.

[12:11] Y por último, la view, que es la que hace las requisiciones para el controller, para hacer todo esto que acá es nuestra pantallita del listado de productos y con el formulario que es la representación de nuestra clase ControlDeStockFrame. Todo esto que acabo de comentar es un patrón de diseño conocido como MVC, Model View Controller.

[12:35] Pero este tema voy a contar un poco más en la próxima clase. Por ahora quedamos por aquí y les dejo como desafío refactorizar las demás operaciones de productoController, que son las de eliminar un registro y de modificar un registro de producto siguiendo todo lo que aprendimos hasta aquí. Nos vemos en la próxima clase.

# MVC

[00:00] Hola. Ahora que estamos prácticamente con nuestra aplicación completa, vamos a realizar un poco el proyecto y entender que estuvimos haciendo hasta ahora. Después que configuramos la base de datos, realizando la instalación de MySQL y creando la base de datos de nuestro proyecto de control de stock, aprendimos cómo configurar nuestra aplicación Java.

[00:20] Vamos a agrandar un poquito la letra. Aprendimos a conectar nuestra aplicación Java a la base de datos de MySQL por medio de algunas librerías, que son la de JDBC y la de las principales, el driver de MySQL. Aquí tenemos las flechitas y de esta forma después de la instalación de MySQL aprendimos a conectar nuestra aplicación Java con la base de datos por medio de estas librerías.

[01:01] Después de esto nosotros aquí en Eclipse importamos un super proyecto, que a primera vista parecía complejo pero que de a poco fuimos aprendiendo cómo caminar por su código e implementar las funcionalidades que faltaban para darle vida y conectarlo con la base de datos.

[01:16] Este es un proyecto desarrollado en Java Swing, es la forma de desarrollar vistas de aplicación, así como el HTML para aplicaciones web. Pero la diferencia aquí es que ella no corre en un servidor de aplicaciones, sino en nuestra propia máquina, un ejecutable.

[01:32] Es una aplicación embebida. Hasta ahí todo bien. Ahora vamos a revisar un poco los componentes de esta aplicación. Nosotros cuando inicializamos la aplicación en el Main, nosotros llamamos a esta clase de ControlDeStockFrame que tiene un constructor que contiene todo el código que crea nuestra pantalla, que enlista y registra los productos. La pantalla es esta de acá que ya nos está acompañando en todo el curso.

[02.00] Esa pantalla acá tiene el formulario y el listado de productos que es construida por el ControlDeStockFrame, es responsable por presentar al usuario las informaciones buscadas en la base de datos de una forma ordenada. Esto aquí compone nuestra capa de view, que es la vista de la aplicación.

[02:18] Cada botón que tenemos aquí en la pantalla tiene una acción configurada y estas acciones ejecutan un conjunto de métodos. Por ejemplo, si entramos aquí en configurar acciones de formularios y vemos la acción del botónGuardar, este botón de guardar llama al método guardar, está aquí adentro, limpiar la tabla y cargar la tabla.

[02:40] Este método de guardar, ¿qué hace? Toma las informaciones del formulario y crea un objeto del tipo producto. Este objeto del tipo producto es el que representa nuestra tabla de producto en la base de datos, pero aquí en el proyecto de Java.

[02:58] Luego de eso, cuando crea el producto, lo envía para el productoController en el método guardar. La clase productoController también tiene las demás operaciones que nuestra lista ejecuta, como la de listar, eliminar y modificar. Aquí habíamos empezado agregando toda aquella lógica para abrir la conexión, ver la query, ejecutar la operación, devolver el resultado pero ahora tenemos solamente llamadas a métodos de la clase de productosDAO.

[03:31] El productoController pertenece a la capa de controller, que es la capa que hace la conexión de la vista con la capa de datos y contiene las lógicas de negocio para manipular los datos antes de guardar en la base de datos o para devolver a la pantalla.

[03:47] Por último tenemos aquí la clase de productoDAO que es la que contiene toda la lógica relacionada a operaciones de la base de datos con la conexión, con la creación de queries, con la conversión de un objeto para hacer la query para insert, para update o delete o también para tomar el resultado y convertir en result set en un objeto del tipo producto para devolver a la pantalla.

[04:15] Como había comentado tenemos todas las operaciones de alta, baja, modificación y de listado. La clase productoDAO tiene la finalidad de realizar las operaciones directas en la tabla de producto. Entonces ella tiene una conexión directa con el modelo de producto.

[04:34] Si nosotros llegamos a tener nuevas tablas en la aplicación, nosotros vamos a crear nuevas clases DAO y nuevas clases de modelo también para representar a estas tablas en la aplicación y para realizar las operaciones sobre ellas.

[04:48] El conjunto de clases de modelo, producto y de la clase productoDAO, forman nuestra capa de modelo, la model, que representa las entidades del negocio y realiza las operaciones sobre sus informaciones. Para este conjunto de capas que revisamos ahora, le damos en nombre de modelo MVC, de Model View Controller.

[05:10] Este modelo es un estándar de arquitectura de aplicación que ayuda a dividir las responsabilidades de una aplicación. Y estas responsabilidades están divididas en las tres capas que recién conocimos. Este modelo tiene como ventajas, más allá de la división de las responsabilidades, la facilidad de mantenimiento, claridad y reutilización del código.

[05:31] ¿Por qué tenemos que utilizar aquí la capa de controller si no tenemos ninguna lógica acá? Nosotros solamente enviamos todo lo que recibimos para la clase de productoDAO. Podríamos aquí, en el ControlDeStockFrame llamar directamente el productoDAO haciendo las operaciones directo de la View.

[05:51] Bueno, podríamos hacer eso, pero eso no es una buena práctica, porque terminamos creando una relación entre dos estructuras y tiene sus responsabilidades bien definidas. La vista debe mostrar la información devuelta por la base de datos y el DAO debe representar el modelo y realizar las operaciones que conecten la aplicación a la base de datos.

[06:14] Si para realizar la requisición desde la view hay una lógica que involucra más de una clase de modelo por detrás, ¿cuál de las dos capas debería tener la responsabilidad? ¿Deberíamos poner todo acá en la view o deberíamos agregar todo acá en el DAO? Ninguna de ellas. Por eso es que tenemos aquí la capa de productoController.

[06:37] Porque ella tiene su importancia en este caso porque ella, más allá de realizar esta conexión entre la vista y el modelo, ella también realiza las operaciones relacionadas a las reglas de negocio para completar una requisición. Entonces si nosotros tenemos aquí la entidad de producto y queremos relacionarla a una otra entidad, nosotros podremos hacer la operación directamente aquí en productoController y no impactaría la finalidad de ninguna de las otras dos capas.

[07:05] Así que, por más sencilla que sea la clase de productoController, su presencia tiene gran importancia justamente porque si el proyecto evoluciona, es en ella que empezaremos a agregar más lógicas de negocio. Espero que les haya gustado entender un poco más del concepto de lo que venimos desarrollando.

[07:24] El modelo MVC es sencillo y aún sigue siendo muy adoptado por empresas para desarrollar aplicaciones del mundo real. Hay otros modelos de arquitectura y variaciones de cada uno que pueden ser utilizados. Cada uno con sus ventajas y objetivos. Nos vemos en la próxima clase para realizar algunas mejoras finales en el proyecto y desarrollar una última funcionalidad.

# queries N + 1

[00:00] Hola, ¿cómo les va? Llegamos a un punto acá que nuestra aplicación está prácticamente completa. Estamos realizando todas las operaciones fundamentales sobre la tabla de productos. Revisando aquí en la pantalla podemos ver todas las funcionalidades que ya hemos desarrollado, por ejemplo, las del listado de productos.

[00:17] Aquí también tenemos el formulario en donde llenamos las informaciones, y si hacemos clic en guardar, nosotros creamos un nuevo producto. Nosotros podemos editar un producto acá también y cuando escribimos algo nuevo y hacemos clic en modificar, nosotros lo modificamos y también podemos eliminar un producto haciendo la selección de uno acá en el listado y después en el botón eliminar.

[00:41] Pero parece que la pantalla aún no está completa, porque tenemos aquí una caja de selección que dice "elige una categoría" y también tenemos aquí un botón para ver el reporte. ¿Y para qué servirían estos campos acá en el formulario, este campo acá de categoría y este botón de reporte?

[01:00] Lo que pasa es que nuestra aplicación es un éxito y tenemos un cliente que quiere mantener todos sus productos en ella, pero como su catálogo de productos es muy grande, es necesario hacer algunas mejoras acá para poder organizar mejor el contenido.

[01:15] Y por eso tenemos que hacer una mejora en el modelo de producto para que cada uno pertenezca a una categoría y además será necesario abrir un reporte con el listado de todos los productos por categoría. Vamos a la acción. Lo primero que vamos a hacer es aquí en el modelo de producto, hacer algunos cambios para agregar la columna de categoría.

[01:36] Hoy tenemos aquí los campos de id, nombre, descripción y cantidad, vamos a la consola de MySQL para hacer un select en la tabla de productos. Hacemos aquí un select * from producto. Y ahí tenemos estos productos registrados que ya aparecen en la aplicación.

[01:59] ¿Cómo podemos hacer esa mejora? El cliente requiere que cada producto tenga una categoría, nosotros podríamos crear una nueva columna acá del tipo texto y el usuario podría escribir la categoría para cada producto que va a registrar. Entonces un usuario podría venir acá y por ejemplo registrar una notebook y escribir que su categoría sería tecnología, por ejemplo, tecnología.

[02:28] Okay. Acá solamente para figurar un poco. Entonces pensemos que el usuario registro acá una notebook en la categoría tecnología, pero vino otro usuario, vino acá a la aplicación en el formulario y registró también una computadora de escritorio y escribió que su categoría es informática. Mira qué confusión ahora.

[02:57] Tenemos dos ítems que son de tecnología y están en categorías que son similares. Una es informática, la otra es tecnología. Mira qué confusión. Parece que un campo texto libre no es una buena solución, quizás podríamos crear una nueva tabla solo para registrar las categorías disponibles en la aplicación, así los usuarios tiene opciones precargadas para elegir y evitamos posibles confusiones para referirnos a una misma categoría de productos.

[03:27] Parece una buena idea, ¿no? Entonces vamos a hacer lo siguiente, voy acá a limpiar la consola, ahora sí, y vamos a crear esa tabla de categoría que va a ser lo siguiente, el comando: CREATE TABLE CATEGORÍA, ahí abrimos el paréntesis aquí y ahora ponemos el id del tipo INT AUTO_INCREMENT, coma.

[03:55] Ponemos nombre del tipo VARCHAR(50). Y aquí decimos que NOT NULL porque no queremos categorías nulas, coma, y decimos que la PRIMARY KEY es el id. Ahí cerramos y ponemos el comandito que aprendimos de la primera clase: Engine= InnoDB; ahí está creada la tabla.

[04:30] Vamos a hacer un select. Ahí está, y la tenemos vacía por ahora. Ahora vamos a ver una vez más los productos que tenemos acá registrados en la tabla, entonces hacemos un select * from producto y ahí tenemos un montón de productos. Acá tenemos 12 productos, pero vamos a ver cuáles son: una mesa, un celular, un vaso, cuchara, un mouse, linternas, zapatillas, botellas, platos y teclado.

[05:01] Bueno, podemos decir que tenemos aquí muebles para la mesa, muebles. Tenemos tecnología para celular, el mouse, linternas también y teclado. Tenemos también la parte de zapatillas podemos poner zapatillas? Para otra categoría y por último, vaso cuchara, botellas, platos. Podemos decir que es cocina, entonces tenemos acá una, dos, tres, cuatro categorías.

[05:36] Está bien. Entonces vamos a crear estas cuatro categorías, acá vamos a hacer lo siguiente: insert, voy a escribir con letras más grandes. INSERT INTO, espera un poco. Para ver mejor, si no, me pierdo. Ahora sí, hacemos un INSERT INTO CATEGORÍA y ponemos acá VALUES y ahí vamos a crear varias categorías al mismo tiempo.

[06:04] Entonces vamos a poner aquí ('Muebles'), que fue la primera para la mesa, después una más, tecnología, ('Tecnologia') la voy a dejar sin el acento. La próxima va a ser cocina, ('Cocina'), y la próxima, que es la última, va a ser ('Zapatillas'). Ahí está. Faltó algo, faltó declarar la columna. Era categoría. Acá ponemos nombre. Ahora sí. Ahora sí tenemos las cuatro categorías registradas. Listo.

[06:57] Okay, ahora que tenemos las cuatro categorías acá registradas en la tabla de categoría, nosotros podemos asignar las para cada producto que está en la tabla del producto. Entonces para eso podremos decir que acá en la tabla producto, el producto mesa puede referirse al id de la categoría mueble. El id 1.

[07:20] Pero para eso, para que tengamos esta referencia, nosotros tenemos que crear una columna nueva en la tabla de productos. Entonces vamos a hacer así, vamos a hacer un ALTER TABLE PRODUCTO y vamos a hacer un ADD COLUMN llamado categoría_id del tipoeEntero. Ahí está.

[07:45] Esta columna ahora, si hacemos un SELECT acá, a ver, voy a hacer un SELECT * FROM PRODUCTO, ahora tenemos la categoría id con todos los valores nulos, pero esta columna ahora puede tener la referencia para todos los productos. Tenemos todos los valores nulos, justamente porque recién creamos esta columna.

[08:08] Ahora lo que tenemos que hacer es vincular las categorías a los productos que tenemos acá registrados. Pero antes de salir y agregando los valores de los id a cada fila que tenemos acá en la tabla, vamos a entender un concepto importante de base de datos. Es el concepto llamado clave foránea.

[08:29] Esta clave es la que va a vincular las dos tablas de forma que sea creada una relación entre ellas y para agregar esta clave foránea acá, nosotros tenemos que hacer un nuevo cambio en la estructura de la tabla de producto, para decir que la categoría id es referencia a la columna id de la tabla de categoría. ¿Y cómo es este comando? Vamos a hacer así.

[08:50] ALTER TABVLE una vez más PRODUCTO y vamos a decir que ADD FOREIGN KEY y ahí decimos que la (CATEGORÍA_ID) REFERENCES CATEGORÍA(ID); ¿Acá qué estamos diciendo? Estamos cambiando la tabla de producto agregando una clave foránea en la columna categoría id que hace referencia a la columna id de la tabla categoría.

[09:27] Hacemos enter y ahí ya tenemos la clave foránea, vamos a hacer las pruebas, voy a limpiar la consola, lo primero que voy a hacer es un SELECT en las dos tablas FROM PRODUCTO. Ya escribí mal acá. SELECT * FROM PRODUCTO, ahora sí y SELECT * FROM CATEGORÍA.

[09:54] Vamos a hacer unas pruebas ahora, ya limpié la consola acá. Lo primero que vamos a hacer es, antes de asignar los valores entre las columnas para hacer la referencia, voy a hacer un SELECT * FROM PRODUCTO: para ver todos los productos y un SELECT * FROM CATEGORÍA; para ver todas las categorías también.

[10:14] Y ahora lo que vamos a hacer es asignar el valor de id de mueble para la mesa y vamos a hacer así. UPDATE PRODUCTO SET CATEGORÍA_ID = 1 WHERE ID = 1; Ahí ya hicimos el UPDATE. Y si hacemos un SELECT otra vez en producto, ya tenemos la mesa con la referencia para la categoría de ID = 1.

[10:48] Pero Icaro, eso lo podríamos hacer normalmente sin tener que crear ninguna clave foránea, ¿entonces por qué lo hicimos? No veo mucho sentido. Bueno, vamos a seguir con las actualizaciones y vamos a ver el por qué tenemos la clave foránea. Entonces voy a actualizar ahora el celular, voy a hacer lo siguiente: UPDATE PRODUCTO SET CATEGORÍA_ID = 5 WHERE ID = 2.

[11:20] Tenemos un error acá, mira qué dice: no se puede agregar o actualizar una hija porque hay un fallo en la constraint de la clave foránea porque no existe ninguna categoría acá de id 5. A ver FROM CATEGORÍA una vez más. No tenemos una categoría de id 5. Ahí está la ventaja de tener la clave foránea configurada porque evitamos de asignar valores inválidos de nuestras referencias.

[11:55] Bueno, aquí damos los primeros pasos de la mejora solicitada por nuestro cliente y con eso vamos aumentando un poco más la complejidad de nuestra aplicación. Ahora nosotros podemos tener una base de datos mejor estructurada con relaciones entre entidades que nos ayudan a entender el modelo y evitar que haya datos repetidos o fuera de patrón.

[12:15] Ahora podemos tomar todo eso que aprendimos y creamos aquí, en nuestra base, para llevar a nuestra aplicación. Queda como ejercicio para la próxima clase asignar todos los valores acá que tenemos que falta hacer un UPDATE en celular, en mouse, linternas y teclado para la categoría de tecnología, el vaso, la cuchara, las botellas, el plato en la categoría de cocina y las zapatillas las asignamos a la categoría de zapatillas.

[12:48] Y en nuestra aplicación en la próxima clase, nosotros vamos a agregar una clase de dominio que represente la categoría y sus respectivas capas del modelo MVC. Nos vemos.

# modelo controller y el dao de categorias

[00:00] Hola, ya atendimos el primer requisito de nuestro cliente que es relacionar cada producto a una categoría. Lo hicimos desde la base de datos, pero ahora necesitamos hacerlo en la aplicación también. Como creamos una nueva tabla en la base, nosotros necesitamos desarrollar las capas de controlar y model para esta entidad en la aplicación, recordando que el controller hace la conexión entre la view y la fuente de datos que contiene el modelo.

[00:27] Vamos a nuestra aplicación y completar las funcionalidades del listar categorías en la caja de selección y poder utilizar la categoría elegida para poder guardar un nuevo producto. Ahora, en la opción acá de categoría solamente tenemos una opción que dice: Elige una categoría. Vamos acá al código para ver cómo funciona la población de este campo en el formulario.

[00:51] Acá en Eclipse en el ControlDeStockFrame, nosotros acá arriba tenemos un JComboBox

[01:18] Entonces aquí en el paquete modelo nosotros vamos a hacer un new class y vamos a crear una clase de categoría también. Categoría, ahí está, la creamos. Aquí en ella vamos a agregar los mismos campos que tenemos en la tabla, que si vemos aquí en la consola son id y nombre, entonces voy viendo el Eclipse, vamos a declarar el private Integer id; private String nombre.

[01:46] Era nombre, ¿no? A ver nombre, nombre de la categoría. Por ahora es eso, no vamos a crear los getters y setters porque lo que estamos haciendo aquí es ir creando estos métodos de acorde a nuestra necesidad para no estar creando montón de código que nos vamos a estar utilizando.

[02:05] Ahora que creamos la clase categoría, podemos volver aquí a ControlDeStockFrame y ya cambiar este object para categoría. Ahora sí, y la importamos. Listo. Ya realizamos el primer cambio. Ahora Eclipse empieza a indicar algunos puntos de error en el código. Entonces vamos a hacer un clic aquí para ver dónde en dónde es el error que queda aquí en el método configurar campos del formulario.

[02:33] Aquí en este método lo que estamos haciendo es un comboCategoría que agrega un ítem que es un string que dice: "Elige una categoría" y también hay una parte de código acá que está con el comentario de TODO que es el por hacer. Entonces aquí tenemos que hacer algunas mejoras ya también.

[02:53] Lo primero aquí que vamos a hacer es, en este addItem vamos a hacer en lugar de estar enviando un string de la categoría, ya que el comboCategoría ahora no es más de objeto, vamos a agregar un new Categoria. Y aquí ponemos un id 0 que no existe, y la string de categoría.

[03:16] Como este constructor no existe, nosotros vamos a crearlo en la clase. Vamos a crear acá el constructor y luego vamos a asignar, voy a mover este método de acá para abajo, para dejar más ordenado. Y ahora voy a primero cambiar los nombres de los parámetro y asignarlos a los atributos de la clase.

[03:38] Entonces this.id = id; this.nombre = nombre. Y listo. Inicializamos ya la categoría para poner el primer elemento de nuestro listado de categorías en la cajita de selección. Ahora en ese pedazo acá de TODO, lo que vamos a hacer es completar la lógica para buscar las informaciones, acá sí entramos en listar, nosotros vamos a completar la lógica para buscar las informaciones de categoría directamente en la base de datos.

[04:09] Bueno, estamos aquí en categoría controller, y lo primero que vamos a hacer ya es cambiar esto de un listado de cualquier cosa que está devolviendo para hacer un listado de categoría. Entonces ya sabemos que el categoría controller, el método listar devuelve un listado de categoría.

[04:27] Y ahora, tal como hicimos con el modelo de producto, nosotros vamos a crear la clase de categoría DAO para abstraer toda la lógica de conexión con la base de datos referente al modelo de categoría. Entonces aquí ya voy a crear un private CategoríaDAO categoríaDAO; y por ahora, va a quejarse un poco Eclipse, pero deja que se queje un poco y ya, ya vamos creando los objetos.

[04:56] Entonces aquí creamos la categoríaDAO como un atributo de la clase. Y como hicimos en el productoController, vamos a crear un constructor acá de CategoríaController y en él nosotros vamos a inicializar la categoríaDAO, entonces vamos a hacer aquí un var de factory para tomar nuestro ConnectionFactory(); a ver, ahora sí, ConnectionFactory();

[05:24] Y vamos a decir que this.CategoríaDAO = new CategoríaDAO, que recibe nuestra (factory.recuperaConexion()); entonces estamos inicializando el DAO enviando una conexión del pool de conexiones. Ahora sí vamos a ¿hacer qué? ¿Crear el objeto? Aún no. Vamos ya a adelantar un poco más y en lugar de un return ArrayList vamos a hacer aquí categoríaDAO.listar();

[06:01] Aquí ya tenemos toda la funcionalidad del controller, solamente nos falta crear el DAO. Entonces vamos a hacerlo, hacemos aquí un control o comando 1 para crear la clase de categoría DAO. Aquí vamos a cambiar el paquete para poner en lugar de controller, el DAO. Hacemos un finish. Ya tenemos la categoría.

[06:24] Ahora la clase, perdón, ahora voy viendo aquí a nuestro controller, vamos a crear el constructor. Ahí lo tenemos. Y por último, vamos a crear el método listar. Ahora sí, ya tenemos todo, acá tenemos que inicializar nuestra categoríaDAO para poner la conexión a un atributo de conexión y poder desarrollar en el método del listado.

[06:50] Entonces vamos acá, declarar un private Connection del paquete java.sql, con; y acá vamos a cambiar el nombre y this.con = con; ya tenemos inicializado. Acá en el método de listar ya vamos a hacer lo siguiente, Vamos a empezar de a poquito, vamos a hacer crear primero nuestro resultado, que es un List<categoría>

[07:22] Vamos a decir que es el resultado = new ArrayList<>(); ahí lo tenemos. Y devolvemos este resultado. Por ahora es eso, ya vamos a poner la lógica para acceder a la base de datos. Y ahora lo que vamos a hacer acá es como hicimos en los otros metros del producto DAO, crear un PreparedStatement.

[07:48] Ahí lo importamos statement = con.preparedStatement. Y acá en el comando SQL nosotros vamos a hacer nuestro select de los datos de categoría, entonces es "SELECT ID, NOMBRE FROM CATEGORÍA"). Este es nuestro SELECT, ya está el comando.

[08:12] Ahora lo que tenemos que hacer es, ya se queja Eclipse, que es el try catch. Ya tenemos acá el SQLException, hacemos un throw new RuntimeException(e); con la SQLExcepcion ahí encapsulada, y listo. Okay, ahora vamos a hacer algo distinto.

[08:32] Acá, en lugar de estar haciendo como siempre hicimos de statement.execute, que devuelve un boolean y después tenemos que hacer un statement.getResultSet para tomar los resultados, vamos a utilizar un acceso directo para ejecutar la query y ya tomar el resultado.

[08:50] Este método que tiene ese acceso directo se llama executeQuery. Así de simple, executeQuery ya nos devuelve a ver, acá está el try-with-resources, acá el resultSet. Pero como yo estoy siguiendo la sintaxis del Java 9, voy a hacer un final acá de resulteSet, ahora sí, y el executeQuery nos devuelve ese resultado.

[09:24] Y acá yo pongo en lugar de executeQuery acá, el resultSet. Ahora sí, con resultSet. Ahí está. Bueno, así como hicimos el resultSet adentro de un try, nosotros también tenemos que hacer el try-with-resources de statement. Entonces acá los declaro como final y ahora sí el statement ya también está dentro de lo que necesitamos.

[09:58] Y ahora con este resultSet, nosotros vamos a tomar cada fila de resultado para crear un objeto del tipo categoría y agregar al listado de resultados. ¿Cómo lo hacemos? Hacemos un while (resultSet.next) ¿Se acuerdan de eso? Hace mucho. Bueno, (resultet.next) y ahí tomamos el new Categoría(resultSet.getInt de la columna "ID" y de resultSet.getString de la columna "NOMBRE".

[10:42] Ahí está, vamos a asignar eso a una nueva variable, var categoría = new Categoría. Ya la tenemos acá y, bueno, último, la agregamos a nuestro resultado.add(categoría); listo, perfecto, listo. Guardamos estos cambios de acá y volvemos para la clase ControlDeStockFrame.

[11:07] Ya tenemos acá el resultado de categorías y tenemos un pedazo de código acá comentado que tiene un categorías.forEach en donde estamos agregando todos los ítems de categoría. Acá saqué el comentario y listo, vamos a hacer las pruebas ahora, voy a guardar todo y vamos a hacer estas pruebas. Okay.

[11:28] Aquí abrimos la aplicación, pero en la caja de categorías estamos imprimiendo acá unos hashes del objeto, de la categoría. Dejamos pasar algún detalle acá, porque recuerda que antes estábamos agregando solamente el texto y funcionaba. Puede ser que esté pasando algo acá, vamos a hacer lo siguiente.

[11:51] Acá voy a cerrar la aplicación y en categoría vamos a sobrescribir el método toString. Voy a escribir acá toString y lo voy a sobrescribir y en lugar de llamar el super voy a devolver this.nombre. Ahora sí, vamos a probar una vez más. Bueno, ahora sí está mostrando la categoría, los muebles acá, tecnología, cocina, zapatillas. Muy bien. Ahora vamos a hacer lo siguiente.

[12:21] Este mouse inalámbrico voy a eliminarlo y voy a registrarlo una vez más porque estaba todo mal escrito, entonces vamos a poner acá mouse inalámbrico, 10 cantidades y la categoría tecnología. Voy a guardar y ahí está insertado con éxito. Vamos a la consola para ver si realmente insertó con el id correcto, vamos a ver acá.

[12:53] Voy a limpiar la consola, hacemos un SELECT * FROM PRODUCTO y tenemos el mouse inalámbrico con la categoría nula. ¿Qué pasó? Lo que pasó es que aún nos falta desarrollar la lógica para vincular el id de la categoría al producto. Por ahora ya hicimos un montón.

[13:18] Creamos acá la capa de model en el proyecto, tenemos la categoríaDAO, la categoría también, ya tenemos la capa de model, tenemos también la capa de controller y ya estamos agregando también el listado de las categorías en nuestra view acá, en nuestra vista.

[13:36] Ya tenemos concluida una tarea más del requerimiento de nuestro cliente. En la próxima clase vamos a desarrollar el próximo requerimiento que es el de asignar esta categoría que elegimos en la pantalla al producto que estamos registrando también.

# ralacionando el producto con la categoria registro

[00:00] Hola. Estamos avanzando con el desarrollo de los requerimientos de nuestro cliente para que la aplicación pueda organizar los productos en categorías. Ya tenemos la tabla creada y desarrollamos aquí la capa de model para tener la representación de la categoría en una clase Java.

[00:16] También tenemos el categoríaDAO que va a realizar las operaciones de base de datos sobre la identidad de categoría. Ahora estamos con la siguiente situación, cuando fuimos a probar el registro de un nuevo producto no estamos guardando la referencia de categoría a este nuevo producto. Vamos a ver qué pasa.

[00:35] Este es uno de los requerimientos de nuestro cliente, que notamos que está incompleto aún. Vamos a resolverlo en esta clase. En el formulario cuando hacemos el clic en el botón guardar, nosotros acá en el ControlDeStockFrame estamos llamando a ver en acciones del formulario, estamos llamando el botón guardar que llama el método de guardar en la clase acá y vamos a ver cómo funciona este método.

[01:00] Bueno, mirando acá el método, nosotros hacemos las validaciones del formulario, tomamos los valores, está bien y tenemos acá una parte de TODO que hace comboCategoría.getSelectedItem(); y recibe la categoría y acá no hacemos nada más con eso. Entonces aquí es en donde tenemos que completar nuestra funcionalidad para asignar la categoría a un producto.

[01:24] Lo primero que vamos a hacer acá es borrar este comentario de TODO y después vamos a en este getSelectedItem tenemos un objeto acá, nosotros tomamos un objeto, lo que vamos a hacer es convertir acá, hacer un catch explícito de objeto para categoría.

[01:45] Ahora sí, estamos haciendo este catch para tomar la categoría correcta y nosotros vamos a enviar esa responsabilidad de asignar el id de la categoría del producto para el productoController, ya que esto es una regla de negocio. Entonces aquí en el método guardar vamos a agregar un nuevo parámetro que va a ser la categoría.getId(); pero este método getId aún no existe en la categoría y nosotros vamos a crearlo ahora.

[02:14] Ahora voy a mover primero acá para dejar acá arriba del ToStringy y en lugar de un object, devolvemos un integer y return this.id. OK, guardemos todo acá. Ahora vamos a productoController en el método guardar, vamos a agregar un nuevo parámetro del tipo Integer categoríaId, y a esa categoría ID la vamos a asignar para el producto, entonces hacemos un producto.setCategoríaId, que recibe la categoríaId.

[02:52] Pero nosotros aún no reflejamos los cambios que hicimos en la base de datos acá en la clase de modelo. Vamos a hacer eso ahora, entonces ya con el SET categoríaId, vamos a crear este método de Set. Aahí está el método, deja bajar un poquito acá, voy a moverlo acá para arriba para dejar junto con los otros métodos de get y set.

[03:17] Y este categoría id yo voy a hacer lo siguiente, control o comando 1 y voy a elegir acá la opción de asignar el parámetro a un nuevo campo y acá Eclipse ya crea para nosotros el campo categoríaId, ya lo tenemos acá asignado, ya lo tenemos acá, Enel categoría en el producto y ya lo estamos enviando para el DAO también.

[03:40] Aún falta un detalle más, tenemos que entrar aquí a productoDAO.guardar y acá en la query de guardar el producto, nosotros tenemos que cambiar esta query para agregar un campo más, que va a ser la categoría id y una interrogación más, también acá, en nuestros parámetros de la query, del preparedStatement.

[04:04] Por último, en el statement acá vamos a hacer un setInt en la posición 4. Vamos a hacer un producto.getCategoríaId(); este método tampoco existe, lo vamos a crear. Como ya me gusta hacer, lo voy a mover acá para arriba para que quede junto de la categoría, ahí está, getCategoríaId(), que devuelve un this.categoríaId;

[04:46] Perfecto. Ya estamos entonces guardando las informaciones en la query y no necesitamos hacer ningún cambio más. Ahora vamos a levantar nuestra aplicación y hacer una prueba para ver cómo funciona. Ya levantamos la aplicación, lo primero que vamos a hacer acá es eliminar este mouse, ya que lo agregamos mal y no tenemos cómo editar la categoría, lo eliminamos y ahora vamos a registrarlo una vez más.

[05:10] Entonces pongo acá mouse inalámbrico, 10 y la categoría tecnología. Hago un clic en guardar, registrado con éxito y ahora vamos a ver en MySQL en la consola para ver si todo funcionó. Voy a poner acá un SELECT * FROM PRODUCTO; y ahí tenemos el mouse inalámbrico con la categoría 2 que es SELECT * FROM CATEGORÍA; tecnología.

[05:46] O sea, está todo bien guardado correctamente, está relacionado sin ningún problema. Terminamos una funcionalidad más de requerimiento del cliente y ahora solo nos falta la opción de reporte. Este botoncito acá, que por ahora no tiene nada. Le hacemos un clic acá, tenemos una pantalla vacía y la idea es mostrar todos los productos acá separados por categoría.

[06:11] Así, el cliente va a tener una información más ordenada, con un reporte que le muestre todos los productos agrupados por categoría. Nos vemos en la próxima clase para desarrollar esta funcionalidad.

## queuies N + 1

[00:00] Hola, el cliente está contento con lo que estamos haciendo para mejorar nuestra aplicación de control de stock, ya tenemos las funcionalidades principales acá para registrar los productos y en la clase anterior nosotros realizamos el registro de un producto con categoría.

[00:16] Para finalizar nuestra aplicación falta la funcionalidad de reporte para listar a todos los productos agrupados por la categoría. Ahora cuando hacemos un clic acá en el botón ver reporte nos abre una pantalla vacía. Aquí la idea es listar de forma sencilla todos los productos con sus categorías.

[00:35] Vamos al código para ver en dónde tenemos que agregar esta lógica. Aquí en la clase ControlDeStockFrame nosotros tenemos aquí el botón, a ver, botón reporte. Vamos al método configurarAccionesDelFormulario para ver cómo está su configuración.

[00:51] Aquí en el botón reporte tenemos la acción acá y esta acción llama al método abrirReporte. Si entramos a este método nosotros vemos que estamos inicializando aquí un new ReporteFrame enviando como referencia el frame que lo está llamando. Vamos a entrar entonces aquí a ReporteFrame para ver qué hace.

[01:14] Aquí en la clase ReporteFrame, nosotros tenemos un constructor en donde estamos iniciando la pantalla y también tenemos un método cargarReporte en donde tenemos aquí un TODO que va a hacer en dónde vamos a estar agregando la lógica. Aquí también en este método ya tenemos aquí un contenido, una variable de contenido que recibe como resultado acá el retorno del método cargarReporte de la categoría controller.

[01:43] Entonces vamos a entrar ahí a este método para ver qué tenemos que hacer. Bueno, aquí en este método está justamente comentado con el TODO y nosotros tenemos que justamente devolver nuestra lista de productos con categorías para el método de ReporteFrame. Aquí lo que vamos a hacer inicialmente va a ser así.

[02:04] Vamos a ver cómo funciona primero. Aquí vamos a estar devolviendo un this.listar(); para devolver primero todas las categorías. Entonces aquí cambiamos el tipo para categoría. Y por ahora, listo. Ahora en el reporteFrame nosotros vamos a borrar ese TODO, porque ya estamos empezando a hacer la lógica.

[02:26] Y aquí adentro del contenido, en cada fila que vamos a estar aquí creando nosotros vamos a agregar una propia fila aquí, justamente, vamos a cambiar este nombre para categoría, así queda más legible y entendemos que es que estamos agregando. Okay, bueno, voy a guardar estos cambios y voy a reiniciar la aplicación.

[02:49]La aplicación ya se reinició, ahora vamos a hacer un clic acá en ver reporte. Y ahora tenemos todas las categorías acá que tenemos registradas en la base, o sea ya funciona algo. Ahora tenemos que agregar a los productos. Para agregar a los productos, nosotros tenemos que buscar a los productos ¿con quién? Con el productoController.

[03:08] Entonces voy a crear un atributo acá, en el reporteFrame de productoController. Y aquí se llama productoController; voy a importar la clase, ahí está. Y en el constructor vamos a inicializarlo también: this.productoController = new ProductoController(); ahí está, pero hasta ahora, si venimos aquí a productoController nosotros tenemos como listar a todos los productos de la base.

[03:40] Ahora necesitamos tener una forma de buscar a los productos por categoría, porque aquí en el reporteFrame, nosotros hacemos un forEach de la categoría, entonces tenemos que para cada categoría buscar a sus productos para mostrar en el reporte. Como el producto tiene una columna que hace referencia a la categoría, nosotros podemos hacer esta búsqueda.

[04:03] Lo que tenemos que hacer entonces es aquí en productoController crear un método que haga una búsqueda de los productos por la categoría, entonces vamos a hacer lo siguiente. Hagamos aquí un public que devuelve un List de productos, entonces producto, aquí es el tipo, y va a ser también un nombre listar, pero como parámetro acabamos a sobrecargar el método.

[04:29] Como parámetro vamos a estar recibiendo una categoría porque queremos buscar al producto por la categoría. Entonces, aquí está la categoría. Muy bien. Y para devolver este resultado ¿qué vamos a hacer? Un return productoDAO, porque es quien hace quien realiza el acceso a la base de datos. Listar, enviando la categoría.getId().

[04:58] Ahí enviamos el id de la categoría y queremos buscar a todos los productos por el id de la categoría. Entonces aquí vamos a crear el método. Ya lo creamos. Y este método va a tener prácticamente la misma lógica del método del listado. Entonces, para ahorrar un poco de tiempo, voy a justamente copiar toda esta lógica de acá y vamos a hacer un cambio bastante sencillo.

[05:27] Entonces aquí voy a sobrescrbir esa parte, ahora sí. Acá voy a cambiar para categoríaId el nombre del parámetro y en donde tenemos el "SELECT ID, NOMBRE, DESCRIPCIÓN, CANTIDAD FROM PRODUCTO", vamos a hacer un "FROM PRODUCTO" WHERE, y acá vamos a agregar el WHERE CATEGORÍA_ID = ?")

[05:59] Lo que tenemos que hacer ahora es aquí, adentro de try (statement) hacer un statement.setInt en donde agregamos en el primer parámetro porque tenemos una sola interrogación, la categoríaId. Así estamos haciendo la búsqueda de productos por la categoría. Todo el restante de la lógica queda igual.

[06:22] Entonces ya tenemos cómo hacer la búsqueda de los productos por el id de la categoría. Okay. Terminamos aquí con productoDAO y productoController. Ahora volvemos a reporteFrame aquí en el método cargarReporte, aquí lo podemos finalizar de la siguiente forma. Para cada categoría que tenemos nosotros vamos a hacer la búsqueda de los productos en el productoController para poder agregar acá en el listado también como una nueva fila.

[06:50] Entonces aquí voy a incrementar un poco más este forEach, déjame formatearlo, ahora sí, y tenemos aquí estamos agregando la categoría que va a ser nuestro título de la línea, digamos una fila título, y para cada producto vamos a hacer un var productos. Déjame bajar un poquito. Ahí.

[07:18] Va a recibir el resultado de this.productoController.listar enviando la categoría. Ahí está, ya tenemos el listado de productos. ¿Ahora qué tenemos que hacer? Otro forEach. Entonces productos.forEach(producto) ¿Y qué vamos a hacer con eso? Vamos a hacer igual que aquí, un modelo.

[07:48] Modelo.addRow. En el addRow vamos a estar agregando lo siguiente. Vamos a, ahora sí me ayuda el Eclipse, vamos a hacer un new Object, así como hicimos arriba. Y acá ponemos los siguientes valores: ponemos una columna vacía porque no quiero que en la primera columna del reporte aparezca como muy abajo, entonces una columna vacía.

[08:24] Después producto.getNombre() y producto.getCantidad(). Estos son los valores que vamos a estar utilizando acá. Entonces, tenemos tres valores, perdón, dos valores, una columna vacía y dos columnas: una con el nombre y la otra con la cantidad de productos. Ahí está.

[08:48] Terminamos la lógica para hacer nuestro reporte. Ahora vamos a reiniciar la aplicación para probar el código una vez más. Se levantó la aplicación, ahora hacemos un clic acá en ver reporte y acá tenemos el reporte, o sea, tenemos aquí por cada categoría: muebles, tecnología, cocina, zapatillas, tenemos a sus productos también.

[09:10] Muy bien, no es de los reportes más lindos, pero es funcional. Llegamos a un resultado, tenemos la funcionalidad de reporte, aquí, para cada categoría que tenemos en la base de datos estamos haciendo una búsqueda de la lista de productos para poder imprimir en la pantalla. Si venimos aquí en el reporteFrame podemos ver que en el cargar reporte y en el listar abrimos dos conexiones a la base de datos.

[09:36] Entonces con dos conexiones a la base de datos, nosotros logramos buscar todas las informaciones de nuestro stock de la tienda. ¿Pero será que fueron dos conexiones? Vamos a dar una mirada más a fondo acá. Vamos a hacer lo siguiente. En cada método acaba de cargarReporte y de listar, nosotros vamos a imprimir la query que estamos ejecutando y ahí vamos a ver cuántas veces son ejecutadas estas queries.

[10:04] Vamos a empezar aquí por cargaReporte, voy a entrar acá, bueno, cómo llevamos el método listar vamos a categoría DAO. Acá en el listar voy a extraer esta query para una variable, entonces la hago acá. A ver, no lo tengo bueno, lo traigo acá. Listar variación querySelect = esto de acá, y ahí lo agrego acá, pero también voy a hacer un System.out.println de esta query para que la tengamos en la consola.

[10:45] Lo mismo. Voy a volver acá a reporteFram y lo mismo voy a hacer con el método listar de categoría. Entonces vamos a entrar acá en productoDAO listar por la categoría y vamos a hacer lo mismo. Voy a extraer esto acá. A ver, voy a extraer otra vez querySelect. Voy a poner el mismo nombre, como tenemos métodos distintos, no hay problema.

[11:11] querySelect, igual que nuestra query y voy a hacer un System.out.println tambien de esta query para ver en una consola cuántas veces estamos ejecutando este método. Vamos a reiniciar la aplicación y vamos a ver qué pasa. Ahí se levantó la aplicación, voy a limpiar la consola, vuelvo acá a la aplicación y ahora vamos a ejecutar reporte para ver cuántas veces se ejecutan las cookies.

[11:40] Acá hice un clic y se abrió el reporte y tenemos acá un SELECT ID, NOMBRE FROM CATEGORÍA. Una vez en la categoría, y una, dos, tres, cuatro selects a la tabla de producto. ¿Por qué? Como tenemos cuatro categorías acá en el reporte, nosotros fuimos cuatro veces a la base de datos para buscar a sus productos.

[12:03] Entonces acá nosotros estuvimos ejecutando cinco veces. O sea, tuvimos cinco conexiones a la base de datos para poder imprimir este reporte. Entonces para hacer una búsqueda entre dos tablas que son producto y categoría, estuvimos yendo varias veces a la base de datos, ahora en nuestro caso fueron pocas veces.

[12:23] Pero imaginemos un volumen mayor de datos o de relaciones. Ese número crece en n veces, es infinita la cantidad de veces. Y esto impacta directamente en la performance de nuestra aplicación, porque para cada iteración que estamos haciendo estamos abriendo una nueva conexión con la base de datos que tiene su costo.

[12:42] Esta solución que desarrollamos no está siguiendo las buenas prácticas de programación porque resolvimos un problema, pero creamos otros. Esta situación es conocida como queries N + 1, que es cuando para ejecutar una cierta funcionalidad, estamos yendo a la base de datos más de lo que es necesario cuando hay la posibilidad de ir una sola vez.

[13:04] Aquí estamos yendo a la base de datos en el método listar de categoría DAO, vamos acá en el reporteFrame, voy a agrandar un poquito más, estamos yendo a la base de datos cuando llamamos el cargaReporte que llama el listar de categoríaDAO y también estamos yendo a la base de datos, cuando llamamos al método listar por categoría de producto DAO.

[13:27] O sea para cada categoría que estamos haciendo acá en el for estamos yendo a la base de datos de productos para hacer esta búsqueda. Entonces por eso que estamos haciendo cinco conexiones a la base de datos en nuestro escenario. ¿Hay una forma de arreglar esta situación? Aprovechando la relación que hay entre las entidades, categoría y producto.

[13:48] Por ahora quedamos por aquí para que piensen un poquito cómo debe ser esta solución. Pero si tienen un poco de apuro, vamos para la próxima clase para conocer esta solución.

## inner join

[00:00] Hola. En las clases anteriores desarrollamos la última funcionalidad del reporte en nuestra aplicación y aprendimos cómo relacionar tablas con la creación de categorías para los productos. En nuestra entidad de productos nosotros agregamos una clave foránea y hace referencia a una de las categorías que tenemos registrada en la entidad categoría.

[00:20] Para crear el reporte, nosotros utilizamos una solución que no es muy buena, ya que genera n queries en la base de datos, porque nosotros aquí en el cargaReporte para cada categoría estamos yendo a la base de datos para listar a los productos de esta categoría, eso genera muchas conexiones con la base de datos.

[00:41] Y con el aumento del volumen de información y de utilización de la base de datos en la aplicación, eso puede generar problemas de performance más adelante. Vamos a la solución de este caso. Para cargar el reporte, nosotros creamos el método cargaReporte en la clase reporteFrame y en ella nosotros estamos buscando las categorías acá con el contenido para hacer un loop.

[01:06] Y por cada iteración de este loop nosotros estamos buscando los productos. La idea ahora de lo que podemos hacer es buscar a todas las categorías y productos en una sola query. Entonces vamos aquí a cargaReporte en la clase categoríaController, y en lugar de estar llamando el método listar que ya tenemos aquí que lista todas las categorías, nosotros vamos a crear otro método.

[01:32] Vamos a desarrollar un nuevo método del listado de estas categorías para el reporte. Entonces vamos a hacer lo siguiente. En lugar de estar devolviendo el resultado de listar, vamos a hacer así, vamos a hacer un return this.categoríaDAO. Ahora es la categoría dado que nos va a devolver esta información y vamos a crear un método llamado listarConProductos.

[01:58] O sea, este método lo que va a hacer es justamente lo que dice su nombre, es listar a las categorías con sus productos. La unión de estas dos tablas. Ahora vamos a crear este método acá en el categoríaDAO, ahí lo creamos y vamos a tomar como base lo que ya tenemos aquí en la lógica del método de listar.

[02:19] Entonces yo voy a copiar esta lógica acá ahora y ahí vamos a hacer los cambios de la query para poder dejarla de la forma que necesitamos, haciendo un join con la tabla de productos, entonces, ya copié el método. Vengo acá, lo pego, ahí está, voy a formatear. Listo, muy bien. El objetivo aquí ahora es cargar las informaciones de productos y las categorías punto en la misma query.

[02:46] En SQL, es posible hacerlo con un recurso de JOIN entre las tablas, más específicamente, el INNER JOIN. Ese recurso nos posibilita unificar dos tablas que tienen columnas en común y para nuestro caso la tabla producto tiene la columna categoría id, que hace referencia a la columna de id, a la de la tabla categoría.

[03:10] Entonces nuestra query aquí puede ser la siguiente, ya tenemos la base que es "SELECT ID, NOMBRE FROM CATEGORÍA"; lo que vamos a hacer ahora es darle un alias, un apodo a la tabla categoría. ¿Por qué? Porque para hacer el JOIN nosotros tenemos que identificar las tablas para poder saber de qué tabla es la columna que estamos haciendo la referencia.

[03:33] Entonces ahora estoy haciendo un CATEGORÍA C, entonces hacemos un SELECT C.ID y C.NOMBRE de la CATEGORÍA C, acá hacemos un "INNER JOIN PRODUCTO P". Y tenemos que poner una condición, entonces la condición va a ser ON. C.ID = P.CATEGORIA_ID.

[04:00] O sea, estoy haciendo una referencia de la clave primaria de categoría que es su id, con la clave foránea que tenemos en PRODUCTO P, que es la CATEGORÍA_ID. Y así hacemos el JOIN, ahí está, esta es nuestra query. Ya completamos, tenemos el JOIN entre las dos columnas. ¿Qué nos falta ahora? Devolver la información de productos.

[04:21] Entonces aquí en el SELECT hacemos C.ID, C.NOMBRE y ahora vamos a agregar P.ID, que es el ID del producto, P.NOMBRE y P.CANTIDAD que son las informaciones que nosotros estamos imprimiendo en nuestro reporte. Okay, voy a formatear un poquito más acá, ahora sí queda más linda la query. Voy a guardar todo y levantar la aplicación una vez más.

[04:48] O sea, voy a cerrar la aplicación que está acá levantada y la levanto una vez más para que probemos el resultado. Ahora vamos acá en nuestra aplicación, hacer un clic en ver reporte y mira qué pasó, tenemos muebles acá una vez, tecnología una, dos, tres, un montón de veces parece que ya rompimos acá la aplicación.

[05:12] Vamos a ver qué pasa, por qué no debería estar devolviendo tantos resultados así. O sea, voy a bajar acá la aplicación y lo que vamos a hacer es lo siguiente, vamos a copiar esta query en la consola de MySQL para entender qué está haciendo esta query y por qué devolvió tantos resultados. Entonces voy a copiar acá este contenido.

[05:31] Voy a llevar a la consola, acá está el SELECT, el FROM también. Y por último, el INNER JOIN. Lo estamos agregando también, ahora punto y coma y enter. Y mira qué está pasando acá. Estamos devolviendo todo el JOIN de categorías y productos. Tenemos acá muebles con la mesa, tenemos tecnología con el celular, la linterna, teclado y mouse. Cocina para vaso, cuchara, botellas y platos.

[06:02] Y las zapatillas. Y mira qué interesante eso. Nosotros estamos repitiendo la información de tecnología, entonces estamos mostrando tecnología una, dos, tres, cuatro, cinco veces, o sea, nuestro resultado de la query devuelve 12 filas para el reporte. Y las 12 filas acá en el reporteFrame, ¿qué estamos haciendo?

[06:29] Categoría. Porque estamos tomando las categorías todavía, entonces las 12 categorías estamos buscando otra vez a los productos en la base. Entonces aún tenemos que hacer algunas mejoras en este código para poder hacer que mostremos solamente la categoría una sola vez y los productos, la cantidad de veces necesaria, que es una por cada producto que tenemos relacionado con la categoría.

[06:53] Acá en la categoríaDAO de un método que creamos, vamos a arreglar la situación de la siguiente forma. Acá en el resultado, nosotros estamos asignando a las 12 filas con las categorías repetidas que hicimos con la query de INNER JOIN. Lo que vamos a hacer para resolver esta situación, para no repetir a la categoría, es la siguiente.

[07:14] Vamos a estar agregando las categorías en el listado y todas las veces que pasemos acá en el WHILE por cada categoría, vamos a ver si ella ya está agregada en el resultado. Si está agregada, nosotros la utilizamos y seguimos con el flujo. Si no está agregada, nosotros la creamos y la agregamos ahí en el listado.

[07:35] Entonces la lógica va a quedar más o menos así. Lo primero que vamos a hacer acá es extraer estas informaciones de resultSet en variables, entonces voy a tener acá la categoríaId. Y la próxima va a ser la categoríaNombre. Entonces hice la extracción, categoríaNombre y ya las tenemos acá como variables adentro de WHILE. Ya vamos a entender por qué estoy haciendo eso.

[08:08] La segunda parte que vamos a hacer en esta lógica es la siguiente. Esta categoría que estamos tomando acá, que estamos tomando la categoría, vamos a hacer así, vamos a decir que esta categoría va a recibir un siguiente resultado, voy a dar un enter acá y vamos a hacer así, vamos a buscar en el listado de resultados.

[08:28] Vamos a hacer un resultado.stream, vamos a filtrar, hacer un filter de la categoría que está acá en la stream, en donde la cat.getId, o sea, el id de la categoría sea igual a categoríaId. Y si encontramos cualquier resultado de esa categoría con id igual, nosotros la vamos a utilizar.

[08:56] Si nosotros no lo encontramos, o sea, vamos a tener acá una condición de .orElseGet, si nosotros no encontramos la categoría, vamos a tener una función acá que vamos a hacer lo siguiente. Vamos a hacer un new categoría y vamos a agregarla al resultado. Entonces esta lógica que dejé abajo la pongo acá dentro y está new categoría, yo la voy a asignar a una variable local que va a llamarse cat, así como hicimos con el lambda de arriba.

[09:35] Y este cat, nosotros lo agregamos al resultado. Y al final de eso nosotros hacemos un return cat; ¿por qué? Porque lo vamos a asignar a esta variable de acá. Para entender un poco más lo que hicimos acá, primero porque hicimos la extracción de las variables para no utilizar adentro de stream.

[09:59] ¿Por qué? Porque en stream, cada lambda que tenemos acá es otro contexto y si nosotros estuviéramos utilizando el resultSet acá adentro de este contexto, nosotros íbamos a tener que agregar cada pedazo de código de acá adentro de las lambdas adentro de un bloque de try catch.

[10:17] Por eso que hice esta extracción, así nosotros ya aprovechamos el propio try with resources, que ya tenemos acá afuera del WHILE, que ya tiene todo eso adentro de su contexto. La otra parte de la lógica que estuve hablando fue la siguiente. Acá estamos tomando el resultado, que es un list de categoría.

[10:40] Lo estoy transformando en un string y haciendo un filter, o sea, estoy buscando si en este listado ya tenemos una categoría con este id de esta variable, de este loop que estamos haciendo. Si ya existe, o sea, un findAny si encontramos cualquier resultado que tenga esta igualdad de la condición acá del filter, nosotros vamos a asignar este resultado a la variable de categoría.

[11:10] Si no existe nada de eso, o sea, es la primera vez que estamos pasando por esta categoría del id específico, entonces nosotros estamos creando el objeto de la categoría y lo estamos agregando a nuestro listado de resultados, vamos a ver cómo funciona ahora. Acá levanté la aplicación. Vamos a ver el reporte una vez más. Hice un clic acá.

[11:40] Y ahora sí estamos mostrando otra vez las categorías correctamente, o sea una sola vez, en lugar de estar repitiendo por cada fila que tenemos en el JOIN, pero seguimos acá ejecutando las queries N + 1. Aún tenemos que arreglar esta situación ya utilizando acá la información de producto que tomamos desde la query de JOIN.

## inner join 2

[00:00] Bueno, ahora vamos a aprovechar este JOIN que hicimos acá con producto para tomar acá en el resultSet las informaciones de producto e instanciar un objeto de producto para agregar junto con el resultado de la categoría. ¿Cómo lo vamos a hacer?

[00:15] Acá ya estamos tomando la categoría, o sea saliendo acá de todo este string, vamos a hacer así: var producto = new Producto que va a recibir el (resultSet.getInt()). Y acá voy a cambiar un poco. ¿Por qué estoy tomando el get "ID", que es el primer ID.

[00:41] Entonces voy a poner el alias acá. Ahora sí y voy a hacer un getInt de alias ("P.ID") otro alias de (resultSet.getString("P.NOMBRE") y por último, un a ver result, ahora sí, resultSet.getInt("P.CANTIDAD"). Ahí está, nosotros creamos acá el producto, que todavía no tiene un constructor de este tipo y entonces lo vamos a crear ahora.

[01:31] Estamos dando a crear el producto, o sea, no estamos importando el producto acá. ¿Qué pasa? New Producto. ¿Qué pasó? A ver, déjame ver acá. Voy a cambiar la variable producto. Ahora sí, listo. Producto producto = new Producto y ahora sí, vamos a crear este constructor que recibe el id, el nombre y la cantidad. Y la vamos a asignar a cada uno.

[02:08] this.id = id; this.nombre = nombre; this.cantidad = cantidad; ahí está. Perfecto, ya guardé acá, tenemos el constructor, tenemos el producto. ¿Pero cómo vamos a agregar ese producto al resultado que tenemos acá en el listado? Es lo siguiente. ¿Cómo tenemos acá viniendo acá en producto? Tenemos una referencia a la categoría id.

[02:40] En la categoría nosotros también podríamos estar agregando una referencia a los productos. ¿Cómo podría ser esta referencia? Podría ser así, ya que cada producto tiene referencia a una categoría, una categoría puede tener muchos productos como acá estamos viendo en nuestro reporte.

[03:00] Una categoría con muchos productos. Entonces acá en la clase de categoría vamos a crear un nuevo campo private List, ahí importo, list de producto productos. Ahí tenemos nuestra referencia de productos adentro de la categoría. ¿Y con los productos qué podemos hacer ahora?

[03:25] Acá en el categoríaDAO, podemos tomar esta variable de categoría, que nosotros tomamos de lambda y hacer un categoría.agregar(producto); y ahí creamos este método de agregar producto que vamos a hacer la siguiente lógica, if la condición de (this.productos == null) Hacemos un this.productos = new ArrayList.

[04:08] Ahí lo inicializamos y es nulo. Y después hacemos un this.productos.add(producto); Perfecto. Ya estamos entonces relacionando la categoría con el producto y estamos devolviendo este resultado. ¿Y ahora qué hacemos con eso?

[04:26] Venimos aquí a reporteFrame y en donde tenemos acá la parte en donde vamos a productoController que va a productoDAO para buscar al listado de productos por la categoría, nosotros podemos simplemente sacar esta parte y decir que la variable de productos es categoría.getProductos.

[04:55] Este método no existe, entonces vamos a crearlo acá ahora. Ahí yo voy a copiar este tipo porque vamos a devolver un listado de productos y devolvemos aquel this.productos. Y ahí tenemos nuestra lógica lista, porque simplemente sacamos el productoController de acá del escenario y agregamos el listado de productos de la categoría.

[05:19] Entonces acá nosotros podemos borrar el atributo de productoController, sacamos también el constructor y ahora podemos guardar todo acá lo que hicimos y levantar una vez más la aplicación para hacer la prueba. Acá con la aplicación levantada, vamos a ver el reporte una vez más y acá tenemos nuestro reporte ya con todo listo, todo ordenado acá, justamente como esperábamos.

[05:46] Y en la consola podemos ver que solamente fue ejecutada una query con el JOIN aprovechando solamente una conexión para acceder a toda esta información. Bueno, finalizamos las funcionalidades del cliente. Las desarrollamos con un buen código, siguiendo las buenas prácticas de desarrollo y garantizamos una buena performance de la aplicación.

[06:09] Seguramente nuestro cliente va a ponerse súper contento con todas las funcionalidades que entregamos y también con todo lo que aprendimos en este curso.
