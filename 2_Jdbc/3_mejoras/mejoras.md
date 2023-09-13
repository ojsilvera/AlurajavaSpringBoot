# prepared statedment

[00:00] Hola, ¿cómo les va? Vamos siguiendo acá con el curso de JDBC. Hemos desarrollado casi todas las funcionalidades de la pantalla, pero ahora vamos a revisar un contenido importante antes de avanzar con el curso. Vamos acá a ver el método guardar de productoController.

[00:18] Venimos aquí en productoControlar, a ver, guardar, aquí está. Aquí nosotros estamos concatenando las variables que recibimos de la pantalla, recibimos acá de la pantalla un map con los valores de producto y lo concatenamos en la query de insert. Vamos concatenando las strings. Entonces volvamos ahora para el formulario de nuestra aplicación.

[00:46] Acá yo voy a registrar un nuevo producto, voy a escribir acá un mouse. Y voy a poner mouse inalámbrico con 100 cantidades. Voy a guardar. Un error acá ¿qué pasó con esto? Error de sintaxis de SQL a ver acá arriba. Mismo problema. ¿Qué dice acá? Mouse inalámbrico. Hay un error en la sintaxis de mouse inalámbrico, pero no me quedó muy claro, vamos acá al formulario.

[01:30] Hay una comilla sencilla acá, una comilla simple, ¿será que es eso? Me parece que sí, vamos a ver qué pasa. Bueno, estamos sospechando acá de la comilla simple y lo que tenemos acá en el lógica no está muy claro, entonces vamos a hacer lo siguiente para estar más seguros de lo que está pasando. Acá está query nosotros la vamos a imprimir en el método antes de ejecutarla.

[01:56] Entonces vamos a extraer esta string a una variable. Voy a poner sqlInsert, y antes de ejecutarla vamos a hacer un System.out.println(sqlInsert). Ahora vamos a ver qué está pasando, voy a bajar la aplicación y levantar una vez más. Vamos a probar una vez más, okay, mouse, comilla simple, mouse inalámbrico, 100 cantidades. Guardar. Ahí está el error, vamos a ver cómo fue la impresión de la query.

[02:37] Vemos acá INSERT PRODUCTO. Ya vi qué pasó, ¿vieron también? Bueno, acá tenemos VALUES, abre paréntesis, comilla simple, mouse comilla simple, comilla simple una vez más, o sea, hay dos comillas simples después de la palabra Mouse y recuerden que en SQL las comillas simples sirven para señalar una string. Entonces acá está el problema y esto es más grave de lo que estamos imaginando.

[03:08] ¿Por qué? Este ejemplo es un ejemplo sencillo de error, porque pudo haber sido un error de tipeo del usuario. Y está bien, no es un error inocente, la intención del usuario no fue romper la aplicación, pero hay personas que sí están ahí buscando vulnerabilidades en la aplicación para hacer mal a una empresa y a los desarrolladores también.

[03:32] Y en lugar de solamente romper acá la ejecución del código con problemas de sintaxis equivocada pueden estar agregando otros comandos de SQL en el campo para poder hacer, por ejemplo, borrar toda la aplicación. Por ejemplo, si el usuario conoce bien nuestra aplicación, podría hacer algo de esta forma acá, acá ponemos mouse inalámbrico, comilla simple, 20.

[04:01] Cerramos acá, ponemos punto y coma y escribimos DELETE FROM PRODUCTO. Y esto es un fallo súper grave, super grave. Imagina el tamaño del problema si esto pasa con empresas que tienen miles de usuarios y su funcionamiento es crítico además.

[04:18] Este tipo de acción que vivimos acá se llama SQL Injection y esto es el hecho de intentar inyectar scripts SQL en un campo de formulario o URL para intentar romper una aplicación o buscar informaciones que son críticas y que son sensibles. Este es un error súper común y que mucha gente sale intentando encontrar esa vulnerabilidad en todas las aplicaciones que están disponibles ahí en la web. ¿Entonces, qué podemos hacer para protegernos?

[04:48] Bueno, nosotros podríamos crear una validación para detectar caracteres especiales y comandos de SQL y agregarla en todos los locales que se conecten a la base de datos. ¿Y si nos olvidamos de algún método nuevo más adelante, nos olvidamos de algún comando, nos olvidamos de algún carácter especial? Volvemos al mismo problema.

[05:11] Por suerte, el JDBC tiene una opción para validar las informaciones de la query y evitar que este caso ocurra. Vamos acá al Controller en Eclipse, productoController, y hasta el momento estuvimos trabajando con el statement, la interfaz statement. Una vez instanciada, nosotros enviamos la query con los valores concatenados en las cláusulas del comando SQL.

[05:36] Pero ahora en lugar de crear un statement, nosotros vamos a estar preparando un statement. Y cuando hacemos eso, nosotros pasamos la responsabilidad de administrar los parámetros del comando SQL para el JDBC. Vamos a ver cómo queda.

[05:50] Bueno, aquí en el método guardar vamos a cambiar acá el connection.create statement para connection.prepareStatement. Y este prepareStatement nosotros vamos a copiar esta query de acá, la copié, la voy a cortar en realidad. Ahí está, la corté y tenemos acá el (INSERT INTO PRODUCTO (nombre, descripción, cantidad) y en lugar de concatenar los valores, nosotros vamos a declarar que son tres valores y son tres puntos de interrogación.

[06:25] O sea, esta es la nueva sintaxis de nuestro string de query. Entonces borramos de esto acá y esta información también no es más necesaria. Otro detalle acá es que el statement ahora va a cambiar su tipo, no va a ser más un statement y sí un PreparedStatement. Ahí está. También del paquete java.sql, y para configurar los valores de la query, nosotros podemos setear los atributos de la query siguiendo el orden de las interrogaciones.

[06:59] Entonces para el nombre acá, que es el primer parámetro del orden de valores, nosotros vamos a hacer un statement.setString y voy a decir que es el valor 1 de producto.get("NOMBRE"); bueno, vamos a hacer lo mismo para descripción. Entonces statement.setString en la posición 2 va a ser el producto.get("DESCRIPCION"):

[07:40] Y el statement.setInt en este caso porque es una cantidad que es un valor entero, nosotros vamos a poner acá 3 de (Integer.valueOf(producto.get("CANTIDAD"); acá de este caso estoy haciendo una conversión de vuelta para el integer, porque nuestro map es de stringe string. Quedó más legible.

[08:14] Voy a borrar acá este comando de imprimir y ahora sí, quedó más legible porque nosotros estamos declarando acá la query, la query bonita acá con los valores, con las interrogaciones, y ahora estamos seteando las variables, los parámetros en otro momento, el lugar de estar concatenando en la string.

[08:34] Queda más organizado el código y más seguro también, ya que pasamos la responsabilidad para el JDBC. Lo único acá ahora es que el execute quedó un poco desubicado, el parámetro acá de statement.RETURN_GENERATED_KEYS quedó desubicado también. Acá nosotros lo vamos a agregar entonces como un segundo parámetro del método de preparedStatement.

[09:00] Acá, nosotros lo cambiamos de lugar y allí estamos agregando el RETURN_GENERATED_KEYS en esta parte y ahora el execute queda solito acá sin nada. Bueno, el restante del código acá abajo queda igual y ahora vamos a ejecutar una vez más la aplicación para poder ver cómo está funcionando. Acá yo la bajé porque hay que hacer un build y actualizar y voy a ejecutarla una vez más.

[09:29] Bueno, ahí está la aplicación. Vamos a intentar entonces hacer un SQL injection. Voy a hacer un mouse. Voy a poner acá la comilla simple y voy a poner acá mouse inalámbrico, comilla simple, coma, 20, cierro acá, punto y coma, DELETE FROM PRODUCTO. Y la cantidad 20 acá también, porque si no, no válida.

[10:01] Hago un guardar y registro registrado con éxito, perdón, y acá esta nuestro registro con el mouse con la comilla simple, el mouse inalámbrico con el valor del comando SQL que antes daba un error de SQL injection. O sea, los comandos de SQL y los caracteres especiales fueron tratados acá en el formulario como parte del texto porque el preparedStatement se encargó de normalizar la string y tratar todo su contenido como un texto.

[10:30] De hecho, un texto común que debe ser guardado en la tabla. Encontramos acá dos ventajas por estar utilizando el preparedStatement. La primera que recién vimos es que nos protegemos de riesgo de estar sufriendo ataques de SQL injection. Y la segunda es que mejoramos la legibilidad del código. Así, nosotros no nos perdemos más con tanto texto concatenado en la query.

[10:54] Ahora que hicimos esto con el método de guardar, vamos a hacer lo mismo para los otros métodos. Entonces acá, siguiendo de acá para arriba, ya que guardar es el último, vamos a hacer acá que el statement va a ser un preparedStatement. A ver, acá está, nosotros vamos a copiar esta query.

[11:18] Vamos a mover la query en realidad para acá y vamos a cambiar su tipo para un preparedStatement. Ningún cambio más en el listado, ya está. Así es nuestra lógica. Ahora, siguiendo para los próximos métodos, el método de eliminar. Acabamos de estar haciendo un preparedStatement y esta query de acá, nosotros vamos a estar haciendo un ("DELETE FROM PRODUCTO WHERE ID = ?").

[11:53] Luego, vamos a estar primero cambiando el statement para un PreparedStatement y vamos a hacer un statement.setInt en el parámetro 1, de posición 1, la primera posición, el id, el execute acá queda solo, sin nada y nada más. Ya está con el método de eliminar. Y ahora por último, el método de modificación.

[12:20] Entonces, para hacer un poco más rapidito, voy a copiar acá el preparedStatement para pegar acá porque es lo que cambia y su tipo a cada statement también. La query de UPDATE, vamos a hacer, ¿qué vamos a estar haciendo? Vamos a tomar acá de este lugar, vamos a agregar acá en el preparedStatement como parámetro.

[12:42] Pero en lugar de estar otra vez concatenando la query, vamos a estar agregando signos de interrogación. Entonces, ahí está. Vamos poniendo las interrogaciones y ya tenemos todos los parámetros. Pero lo que nos falta es el statement.setString para en la posición 1 poner el valor de nombre para actualizar, el statement.setString en la posición 2 para la descripción.

[13:19] El statement.setInt ahora, porque estamos hablando de la cantidad, entonces en la posición 3 vamos a agregar la cantidad, la variable ya del parámetro. Y por último statement.setInt id 4, en la posición 4 de la query, el id que es el WHERE de la condición de UPDATE.

[13:43] Con eso finalizamos. Ya está. Tenemos todos los métodos protegidos con la utilización del preparedStatement y también con una legibilidad mejorada. Nos vemos en la próxima clase.

# tomando control de la transaccion

[00:00] Hola. Vamos a avanzar con la mejoras en nuestro proyecto. Vamos a incrementar un poco la funcionalidad de creación de un producto y agregar una regla de negocio a ella. Nuestro depósito ahora tiene una limitación de solo poder soportar 50 cajas de un mismo producto por registro.

[00:16] Entonces si nosotros registramos un producto con cantidad mayor que 50, el código de BackEnd va a tener una lógica para dividir este procesamiento en dos operaciones de Insert. Vamos al código.

[00:31] Acá en el método guardar de productoController vamos a hacer lo siguiente. Vamos a realizar los cambios aquí para que podamos soportar este tipo de operación. Lo primero que vamos a hacer acá es extraer los valores del Map de producto para variables, porque la vamos a estar iterando, y vamos a crear una variable más acá para señalar un valor máximo. El campo cantidad puede tener por cada registro. El valor va a ser 50, como había dicho.

[00:59] Entonces acá el producto.get("Nombre"); voy a dar un "Ctrl + 1", extract to local variable, va a ser nombre acá, descripción= y el último va a ser la cantidad. Entonces abro acá la descripción y pongo cantidad. Voy a mover estos pedazos acá de código juntos para que queden acá arriba en el inicio de nuestra lógica.

[01:40] Y como había dicho voy a declarar una variable más del tipo Integer, que es el máximoCantidad con valor de 50. Ahí está. Ese es el inicio de la lógica. Antes de seguir con la lógica de negocio, haremos una refactorización acá en este código. Acá vamos a tomar esta parte del statement.set los valores, hasta el resultado y lo vamos a mover para un método, lo vamos a extraer para un método.

[02:12] Entonces voy a hacer un command o "Ctrl + 1" extract to method. Este método va a llamarse de ejecutaRegistro, donde va a estar recibiendo como parámetro el nombre, la descripción, la cantidad y el statement que nosotros inicializamos arriba para hacer su ejecución, la asignación de los parámetros y su ejecución.

[02:39] Miren una cosa acá. Me faltó cerrar la clase anterior la conexión acá del método guardar. Voy a compensar este fallo con el con.close ahora. Listo, compensado el fallo. Ahora vamos a nuestra lógica. Esta lógica debe ser ejecutada por lo menos una vez en el caso de que la cantidad de productos sea menor o igual que 50.

[03:02] Entonces nosotros podemos hacer acá un loop con el do while y la lógica va a quedar más o menos así: do, y acá vamos a hacer con esta lógica. Primero voy a cerrar porque me da un poco de cosa dejarlo abierto. Entonces do while, acá voy a poner la condición despuésm pero dentro del bloque de do while, nosotros vamos a hacer lo siguiente.

[03:27] Vamos a tomar un int cantidadParaGuardar, va a ser y acá voy a utilizar una librería. ¿Se acuerdan de las libs? La libs de MySQL, ahora va a utilizar la librería de matemática. Acá va a utilizar la Math.min. Yo quiero tomar el valor mínimo entre dos valores. ¿Qué valores son esos? La cantidad y el máximo de la cantidad.

[03:58] O sea, si es la cantidad tiene valor 100 y máximoCantidad es 50, el valor mínimo acá va a ser 50. Si el valor cantidad es 40 por ejemplo y el máximoCantidad es 50, el valor de cantidad para guardar va a ser 40. Entonces tomamos esta lógica acá, utilizamos una librería para abstraer esta lógica que hoy vamos a estar haciendo con los ifs y en lugar de estar enviando la cantidad como parámetro, vamos a enviar el cantidadParaGuardar. Ahora sí.

[04:33] ¿Qué hacemos ahora con eso? Bueno, si vamos a esta ejecutando y tomando siempre el menor valor posible para ir guardando y pensando que el máximo que podemos guardar es 50, entonces si la cantidad es mayor que 50, la próxima vez que pasemos por este lazo, por este loop, nosotros tenemos que guardar lo restante.

[04:56] Entonces si estamos guardando 60 cucharas, por ejemplo, vamos en la primera pasada, a guardar 50 y en la segunda tenemos que guardar 10. ¿Cómo va a quedar la lógica acá?

[05:09] cantidad -= maximoCantidad. ¿Se entiende acá? Acá voy a estar haciendo una substracción del valor de cantidad del máximoCantidad. Entonces cada vez que pasemos, mientras la cantidad sea mayor que 50, vamos a estar sustrayendo 50. Perfecto. Acá, ¿cuál va a ser la condición para parar? Mientras cantidad>0 yo ejecuto mi loop. Voy a guardar acá el código, voy a levantar la aplicación y la vamos a probar. Tenemos la aplicación acá ejecutando.

[05:59] Lo que vamos a hacer primero es guardar 100 linternas. Acá voy a poner linternas con pilas recargables. Ahí está, 100 linternas. Guardar. Ahí está. Dos registros de 50. Pusimos 100 en el formulario y fueron guardadas 50 de cada uno en cada registro. Vamos a crear un registro de zapatillas, zapatillas de fútbol.

[06:37] Vamos a poner 40 zapatillas. Ahí fueron guardadas 40 también. Ahora vamos a hacer lo siguiente. Vamos acá a registrar algunas botellas y botellas de vidrio, vamos a poner 74 botellas de vidrio. Acá fue registrado con éxito. Mira, 50 guardadas primero, y después, 24 botellas que fue el restante.

[07:10] O sea, la lógica funciona bien y estamos agregando ahí cortado, cada 50 productos nosotros registramos uno nuevo en la tabla. ¿Pero ahora qué pasaría si en el medio de la ejecución ocurre un error en la aplicación? ¿Todos los productos serían registrados? ¿Solo una parte o ninguna?

[07:34] Vamos a simular un error acá para ver qué puede pasar. Acá en el método ejecutaRegistro, nosotros vamos a poner una condición que antes de cualquier cosa, vamos a hacer un if(cantidad < 50) Si la cantidad es menor que 50 nosotros vamos a lanzar una RuntmeException, que dice ("Ocurrió un error"). Voy a bajar entonces la aplicación. Espera un poco.

[08:11] Me faltó acá, me faltó poner el new. Ahora sí, voy a bajar a la aplicación para ejecutarla una vez más. Ahora acá con la aplicación levantada vamos a registrar 60 platos. Entonces voy a poner acá platos de plástico, esos de fiesta, y la cantidad 60. Okay, guardar. No tenemos nada devuelto acá en la pantalla y en el log tenemos el error que pusimos para que se ejecute.

[08:46] Vamos a hacer lo siguiente porque no se recargó nada. Vamos a reiniciar la aplicación para ver qué pasa. Se reinició la aplicación y podemos ver acá que 50 de los platos fueron guardados y los 10 fueron perdidos. ¿Qué pasa acá? Lo que está pasando es que para cada ejecución del Insert la aplicación está abriendo una transacción para guardar los datos, devuelve el resultSet y cierra la transacción.

[09:13] El segundo intento va a pasar lo mismo. Se abre una nueva transacción, se insertan los datos, se devuelve un resultSet y se cierra la transacción. El tema es que cuando es lanzada una excepción, parte de la información es guardada y la otra parte es perdida. ¿Hay alguna forma de arreglar eso? Tomando el control de la transacción.

[09:36] Nosotros podemos tomar la responsabilidad del JDBC, que es manejar la transacción y hacerla nosotros para que la operación quede entera dentro de una sola transacción y garantizar que o se guarda todo o no guardamos nada. Aquí nosotros vamos a hacer lo siguiente.

[09:54] Acá en el método guardar, después que abrimos la conexión, nosotros recuperamos la conexión y luego de eso, nosotros vamos a setear para que ella no haga el commit de la transacción. El comando para tomar el control de la transacción va a ser, luego de abrir la conexión, vamos a hacer con.setAutocommit(false);

[10:14] Con eso nosotros configuramos acá que la conexión no va más a tener el control de la transacción y el que tiene el control de la transacción somos nosotros, y nosotros ahora podemos decir dónde el commit va a ser realizado. Ahora vamos a probar esta configuración para ver qué pasa con la base de datos.

[10:34] Nosotros vamos a reiniciar acá, voy a reiniciar la aplicación y ver cómo va a portarse la aplicación intentando agregar 60 zapatillas nuevas. Acá tenemos la aplicación levantada y vamos a agregar ahora. Ya tengo zapatillas de fútbol, ahora vamos a agregar nuevas zapatillas. Estas van a ser zapatillas de básquet. Ahí agregué 60 unidades. Puse para guardar.

[11:02] Hay un error en el log de la aplicación y no vemos nada todavía. Vamos a reiniciar la aplicación para ver si se guardó la información. Ahí levantó la aplicación otra vez y las zapatillas de básquet no fueron guardadas acá. El autoCommit funciona. Nosotros los pusimos como un false y no fue commiteada la transacción.

[11:23] Entonces aquí en el código ya podemos sacar esta situación de prueba que le hace el error y volver a intentar guardar nuevamente las 60 zapatillas. Voy a levantar la aplicación una vez más. Bueno, y acá en el formulario vamos a intentar nuevamente agregar las 60 zapatillas de básquet. Zapatillas de básquet, 60.

[11:47] Ahí hago clic en guardar. Tengo registrado con éxito. En el log también están 19 y 20 el id, pero no aparecieron acá en nuestro listado. ¿Que pasó con eso? En el log tenemos que está todo bien, pero no aparece acá en la tabla. Esto pasa porque nosotros sacamos la responsabilidad del JDBC para concluir la transacción pero ahora nosotros no podemos registrar ningún producto.

[12:16] Resolvimos un problema pero ahora creamos otro. Este va a ser el tema para la próxima clase, en donde vamos a aprender cómo tratar esta situación y arreglar todo para que la aplicación vuelva a funcionar nuevamente. Nos vemos.

# Manejando el commit y el rollback

[00:00] Hola. En la clase anterior vimos qué podemos hacer para garantizar que la operación sea realizada por completo o no haga nada si ocurre un error. Aprendimos con eso a tomar el control de la transacción con el comando setAutoCommit de la conexión.

[00:14] Pero cuando realizamos esa configuración, llegamos al punto de que la aplicación ya no registra ningún producto más y la idea para nuestra transacción es garantizar que o registramos la cantidad total de producto o no registramos nada.

[00:30] ¿Por qué seguiremos con esta regla? Imaginémonos acá que tenemos dos cuentas bancarias y una de ellas que es la cuenta de origen, quiere hacer una transferencia para la cuenta de destino. En una transferencia entre cuentas, el dinero sale de la cuenta de origen, se sustrae de su saldo y va para la cuenta de destino, que recibe este dinero y lo suma a su saldo.

[00:54] Si en el momento acá de esta transferencia hay un error en la operación, o sea tenemos acá una X. Y cuando la cuenta de origen se bajó su saldo, se hizo la transferencia en el momento de llegar a la cuenta de destino, un error. ¿Ahí qué pasa? ¿La cuenta de origen pierde el dinero? En realidad no. Esa transacción no va a ser concluida pero sí revertida.

[01:26] Como hubo un error acá, al momento de llegar el dinero a la cuenta de destino, el valor que salió de la cuenta de origen debe volver a esta cuenta para que su saldo quede ahí mantenido sin ninguna modificación. En la caja va a ser presentado un error para el usuario informando que hubo un fallo en la transferencia.

[01:44] Ahora imagina si esta operación es ejecutada en dos transacciones distintas. En la primera el dinero sale de la cuenta de origen y se concluye. O sea, chau saldo, ya se fue el dinero que quieras transferir. Y en la segunda, el dinero transferido para la cuenta de destino tiene un error, o sea se pierde el dinero.

[02:05] Ni la cuenta de origen va a tener el dinero de vuelta y ni la cuenta de destino va a tener su dinero que fue transferido de la cuenta de origen. Eso no puede pasar. Por eso nosotros tenemos que garantizar que toda la operación quede dentro de una sola transacción. La cantidad total de productos debe ser registrada por completo por el mismo motivo que una transferencia de dinero entre cuentas debe ser completa por entero o nada cambia.

[02:32] Porque si hay un error en el medio del proceso, todas las operaciones de la base de datos deben ser revertidas. Ahora, vamos para la solución del problema en el código. Cuando trabajamos con el control manual de una transacción, o sea con el AutoCommit(false); nosotros tenemos que agregar explícitamente el comando de commit en el código.

[02:55] El comando con.commit lo vamos a agregar afuera del bloque de do while. Y va a ser acá con.commit(); para garantizar que todos los comandos del loop hayan sido ejecutados correctamente. Ahora sí, estoy levantando la aplicación y cuando vaya a guardar las 60 zapatillas ellas tienen que ser todas guardadas ahí sin ningún problema, sin ocurrir ningún fallo.

[03:21] Vamos a ver acá las zapatillas de básquet, 60 unidades, guardar y ahí tenemos registrado con éxito y acá aparecieron las 60 zapatillas. Un registro con 50 y un registro con 10. Igualmente para garantizar que no tengamos errores, dejar el código con la mejor calidad y cobertura de escenarios de error, nosotros podemos agregar acá el comando de rollback, que la transacción si ocurrió un fallo.

[03:50] Vamos a hacer lo siguiente acá. Nosotros vamos a agregar un bloque de try catch acá, que va a mantener toda esta lógica de do while y del commit y si hay un catch acá con SQL, una exception en realidad, si hay una exception, cualquiera que sea, nosotros vamos a hacer un con.rollback.

[04:18] Es así. Y al final cerramos la conexión y ya está. O sea, si la ejecución acá tiene un error, él ejecuta registro o cualquier cosa que hay acá dentro del try tiene un error, vamos a caer en el catch, nosotros vamos a hacer un rollback de la transacción, vamos a cerrar la conexión y no hay ningún problema. Nosotros cancelamos la ejecución de estas transacciones.

[04:42] Aprovechando acá yo cerré la conexión pero podemos cerrar también el preparedStatement. Entonces voy a hacer un statement.close() también para tener un mejor control de la transacción. Ahora sí estamos controlando de verdad la transacción del método de registrar un producto.

[05:00] Si sale todo bien, tenemos un commit y si ocurre un error, tenemos un rollback de la transacción. ¿Vamos a probar el rollback? Vamos a agregar aquí, en el ejecutaRegistro una vez más la lógica de if (cantidad < 50) lanzamos un throw new RuntimeException ("Ocurrió un error") Ahí está. Vamos a probarlo una vez más.

[05:33] Voy a levantar la aplicación. Ahora acá yo voy a borrar las zapatillas para intentar agregarlas una vez más. Ahí borré una, borré la otra y ahora vamos a agregar las 60 zapatillas de básquet. 60. Guardar. Registrado con éxito. Mira qué bien. O sea, no hubo nada, algo registrado con éxito. Tenemos un fue insertado el producto de id 23 pero nosotros no tuvimos nada. ¿Por qué?

[06:10] O guardamos todo o no guardamos nada. Para que quede más claro acá nosotros vamos a hacer lo siguiente. Voy a bajar esta aplicación y acá, cuando ocurra el rollback o el commit, yo voy a imprimir en la consola. Acá voy a tener un ("COMMIT") y en el catch voy a poner un ("ROLLBACK"). Así vamos a ejecutar una vez más y vamos ver que quede más claro, porque vimos que hubo un éxito pero no hubo registro y quedó un poco confuso.

[06:40] Así que acá está la aplicación, no tenemos nada y ahora vamos a agregar las 60 zapatillas de básquet. 60. Guardar. Éxito pero, en la consola tenemos el ROLLBACK. O sea, hubo un error en la ejecución, nada fue guardado y se hizo un rollback de la transacción. Ahora garantizamos que la transacción o guarda todo o no guarda nada.

[07:13] Y con eso aprendimos cómo funciona el control de transacciones de aplicaciones del mercado. Generalmente son códigos así que son creados en aplicaciones reales. Vamos cada vez más mejorando la calidad de nuestro código y nuestra aplicación. Nos vemos en la próxima clase para aprender un recurso nuevo que va a dejar nuestro código aún más sencillo.

# Utilizando el try-with-resources

[00:00] Hola. En la clase anterior aprendimos a tener el control de las transacciones de una forma clara. Aprendimos que una transacción generalmente involucra un conjunto de operaciones. Como en nuestro caso, para guardar una cierta cantidad de registros para el mismo producto. Una cosa que venimos viendo también es que toda la conexión que abrimos, luego de utilizarla tenemos que cerrarla.

[00:23] Y en la transacción de registrar un producto, vimos también que nos habíamos olvidado de cerrar el preparedStatement. Y ahora veo acá también en el ejecutaRegistro, que el resultSet también debería estar cerrado. Acá, resultSet también es algo que deberemos estar haciendo un close. Y si veo un poco más en la aplicación seguramente me olvidé de poner el close en algún otro método.

[00:51] O sea, tenemos acá para una transacción por lo menos tres objetos en cada funcionalidad que tenemos que preocuparnos con la apertura y la clausura de ellos. Ya vimos que es fácil olvidarnos de ese detalle, de cerrarlos explícitamente. Aquí en nuestra aplicación no hay mucho problema, pero en aplicaciones del mundo real, olvidar este detalle puede generar muchos problemas en el futuro, principalmente de performance en la aplicación y en la base de datos.

[01:20] Porque si nos olvidamos de cerrar todas las conexiones que abrimos, podemos llegar a agotar las conexiones disponibles de la base de datos y parar toda la aplicación. Sería un gran problema. Agrego un problema más. En el catch estamos haciendo un rollback acá.

[01:40] Pero si ocurre un error antes de ejecutar este comando, nosotros podemos tener el lanzamiento de otro error inesperado y nunca revertir la operación y tampoco cerrar la conexión. ¡Cuántos problemas!

[01:52] ¿Entonces la solución es salir poniendo el close en todos lados, dejar acá un recuerdo en la pantalla para que "Icaro, no te olvides de poner el close en los comando que estás abriendo de conexión, preparedStatement y resultSet"? No. No hay que ponerse locos con eso.

[02:08] Por suerte, porque desde la versión 7 de Java hay un recurso llamado Try With Resources. El Try With Resources nos permite declarar recursos que van a ser utilizados en un bloque de try catch con la certeza de que estos recursos van a ser cerrados o finalizados automáticamente después de la ejecución del bloque.

[02:33] Un requisito para eso es que estos recursos deben implementar la interfaz autoCloseable. Esos bloques aún pueden tener los bloques de catch y final para trabajar en algún manejo de excepción como el rollback que estamos haciendo en nuestro método de registro de productos. Antes de que vayamos a la implementación voy a contar una cosita más.

[02:54] En la versión 7 de Java, nosotros solamente podríamos utilizar estos recursos inicializados dentro del bloque de Try With Resources. Pero desde la versión 9 de Java es posible utilizar variables final dentro de la declaración de los recursos, dejando el código más limpio. Mira la diferencia entre cada implementación.

[03:15] Acá, con el resultSet vamos a ver cómo quedaría con la versión 7 y como quedaría con la versión 9. Primero, vamos con la versión 7. Sería acá: resultSet acá tenemos, aquí, y lo que vamos a hacer, abrir el try con paréntesis. Sí. Esa es la sintaxis del Try With Resources.

[03:38] Este pedazo acá de resultSet voy a agregar dentro de este paréntesis y voy a abrir llaves y voy a cerrar las llaves. Este close ya no es más necesario. Ahí está nuestra sintaxis de cómo es en la versión 7 de Java. Como había dicho, la clase necesita implementar la interfaz AutoCloseable, que es el caso de resultSet, acá esta el autoCloseable, por eso Eclipse no se queja.

[04:12] Con eso ya tenemos el Try With Resources y la propia JVM se ocupa de estar cerrando estos recursos. Ahora vamos a ver cómo quedaría la diferencia entre la 7 y la 9. ¿Cómo es en la 9 ahora? En la 9 nosotros podemos tomar esto de acá, este resultSet lo dejo acá afuera, como final y yo solamente hago lo siguiente: try(resultSet) y con eso ya estamos.

[04:45] Queda ahí a criterio de ustedes cuál de las versiones van a utilizar. A mí me gusta más esta de la versión 9, porque ya es más actualizada, queda más sencillo también el código dentro del paréntesis de try. Queda más tranquilo, más escueto.

[05:03] Bueno. Y ahora que ya hicimos eso con el resultSet, vamos a hacer lo mismo con la conexión y el statement acá del método guardar. Entonces acá, en donde estamos tomando la conexión del connectionFactory, nosotros vamos a hacer lo siguiente. Vamos a declarar la conexión como final, voy a hacer un try(con) abro acá las llaves, vengo hasta este con.close, hago la indentación, cierro acá.

[05:33] El con.close ya no es más necesario y voy a hacer lo mismo con el statement. Entonces el preparedStatement lo voy a declarar como un final, acá voy a hacer un try(statement) abro llaves, todo este código de acá lo pongo adentro del try y el statement.close ya no es más necesario tampoco. Ahí está. Acá quedó un poco raro.

[06:04] Un try, después otro try, entonces vamos a juntar los dos para hacer de la forma que había comentado. Entonces este try de arriba, yo lo voy a copiar acá, lo voy a cortar en realidad y ahora sí, dejamos este try así y lo único que falta es indentar el código. Ahora sí está todo formateado correctamente.

[06:29] Rompió un poco la sintaxis de la query pero ahora sí tenemos el try de la conexión con el resource, el try del statement seguido de un catch con el rollback. Ahora nosotros podemos hacer lo mismo para las otras operaciones de listado. Vamos a tomar acá la conexión, la declaro como final, hago un try(con) y seguimos aquí poniendo todo adentro del try, borro acá el close.

[07:08] Con el statement hago lo mismo, final statement, hago un try (statement), sigo acá con todo eso. Cierro y listo. El resultado queda acá dentro del otro try también, perdón. Siguiendo acá tenemos el de eliminar. Vamos a hacer otra vez final de la conexión, try(con), abro acá, estoy peleando acá con el teclado.

[07:51] Vamos acá, el try, cierro, borro esto, en el statement hago lo mismo con el final, try(statement), abro el try aquí, hago lo mismo acá, cierro y listo. Por último el de modificación que igualmente hacemos acá el final try(con), abro acá. Antes de indentar voy allá, a adelantar eso también del statement. Hago el try del statement, ya lo abrí, y ahora cierro las dos llaves, indento el código y listo.

[08:42] Dio un poquito de trabajo pero, por lo menos de esta forma nosotros ya no tenemos más que preocuparnos con estos comandos de close que ya fueron todos eliminados y no tenemos que estar preocupándonos más con abrí un recurso, lo tengo que cerrar, que locura, un montón de cosas para hacer.

[09:02] Ahora ya está todo más por cuenta de JVM. Listo, mira qué lindo quedó el código. Quedó acá más sencillo, menos líneas de código, menos instrucciones, menos locuras de con.close, statement.close. Quedó más profesional el código, tiene estilo acá. Ese es el camino. Con esto terminamos el contenido de esta clase. [09:28] Para la próxima vamos a ver cómo escalar nuestra aplicación manteniendo algunas conexiones pre creadas.
