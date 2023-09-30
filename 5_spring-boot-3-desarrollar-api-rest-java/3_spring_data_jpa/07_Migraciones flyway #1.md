[00:00] Bien, ya vimos que el error que tenemos ahora es porque no tenemos la tabla médicos creada, no existe y para eso vamos a hacer por fin uso de la herramienta Flyway. Si ustedes recuerdan en el primer video de esta clase, seleccionamos Flyway como parte de las dependencias para descargar ahora.

[00:24] Si vemos el pom vamos a ver que de Flyway tenemos dos dependencias. La primera es flyway-core y la segunda es flyway-mysql. Flyway-core s la que nos va ayudar, digamos a hacer el trabajo en realidad de ejecutar las migraciones que es cómo se llama esto, y flyway-mysql es para el dialecto de base datos que vamos a utilizar, en este caso, MyQSL, valga la redundancia.

[00:45] Este tipo de herramientas son llamadas migrations. Son herramientas de migración de base de datos. Tranquilamente puede ser Flyway, tienes Liquibase, pero Flyway es ampliamente adoptado en el mercado y en principio es el mismo. No se preocupe si entienden flyaway, van a ser capaz de trabajar con cualquier tipo de migration con que se topen en su vida profesional.

[01:07] El principio es el mismo: es gestionar tu base de datos a través de código. ¿Cómo funciona esto? Yo como les dije podría tranquilamente darle clic derecho aquí, darle a new y crear mi tabla, pero yo lo quiero hacer usando Flyway. Para eso voy a venir aquí a mi carpeta de recursos, resources, darle clic derecho new, directory y voy a llamar migrations.

[01:36] Entonces ya tengo mi carpeta migrations y automáticamente Flyway la va detectar y va a decir: “Aquí está la migration de la base de datos”, pero hubo aquí algo que olvidé y es crear la carpeta primero, la carpeta padre db, y migrations va dentro de db. Esto por estructura de Flyway. Aquí en IntellyJ me la va a mostrar como db.migrations, pero en realidad es el directorio migrations dentro de db, por database.

[02:14] Sin más que decir nuevamente clic derecho, new. Los migration se gestionan con archivos .sql, lo que hace por principio ¿qué es? Ve el archivo sql y lo va a ejecutar sobre la base de datos con la que ya tiene conexión. Entonces, si yo quiero un archivo sql le voy a dar en file y aquí entra algo muy importante, pongan atención en esto.

[02:42] Flyway utiliza una nomenclatura, un tipo de padrón para nombrar los archivos con el cual él identifica qué archivo ya fue migrado y cuál no. Por ejemplo esta es la primera migration. Entonces es v1__ dos guiones bajos y de preferencia el nombre tiene que ser autoexplicativo. Por ejemplo, si yo voy a crear aquí la base de datos, voy a ponerle create-table, porque voy a quedar la tabla médicos, perdón, no voy a crear la base datos.

[03:20] Médicos.sql. Entonces, nuevamente el v1 y los dos guiones bajos es el patrón de Flyway para identificar qué es una migration y él va a decidir si se ejecuta o no, eso lo vamos a ver en práctica en unos minutos, pero solo para que la atiendan por ahora. Segundo, la segunda parte del nombre es algo autoexplicativo sobre lo que esta migration está haciendo. En este caso estamos creando una tabla llamada médicos.

[04:00] Entonces create-table-medicos. Y la tercera parte es la extensión del archivo .sql. Lo creamos y tenemos aquí create-table-médicos, tenemos aquí que escribir el código para crear la tabla. El código ya lo tengo aquí, no es un curso de MySQL entonces no vamos a profundizar mucho en la sintaxis, pero es básicamente esto: create-table-medicos, todo lo que ustedes ya conocen, aquí no hay mayor ciencia, no hay mucho que ver en realidad.

[04:35] Y diciendo primary key y listo, ya tenemos nuestra migration creada aquí, create-table-medicos. Ya tenemos el servidor porque si en algún caso, por ejemplo llega a ejecutarse, si yo llego guardar este migration y por ejemplo, si mi scribd está incompleto, puedo tener errores en mi base de datos luego.

[04:59] Entonces de preferencia si van a trabajar con migrations y con DevTools activado detengan el servidor porque si por ejemplo hay algún error de compilación aquí, si yo aún no termino de escribir, por ejemplo, mi tabla, pero quiero guardar, entonces mi tabla se va a crear con estos atributos.

[05:20] Quedamos aquí y vamos a iniciar el servidor. Vemos aquí que ya tenemos en el Flyway Community Edition, y me dice aquí por ejemplo: No migrations found. Are your locations set up correctly? Esto me dice claramente, si yo creé una migración, quizás el directorio no está nombrado correctamente. Y creo que es verdad porque yo escribí migrations en plural y debería ser en singular.

[06:08] Para eso voy a hacer un refactor. Y ya está db.migration. Voy a entrar a mi servidor nuevamente. Y vamos a ejecutar nuevamente ahora. Vamos a ver qué sucede. El servidor inicializó. Vamos a incrementar esto un poco y vamos a ver ahora sí que nuestro directorio está correctamente nombrado. Vemos que inicia aquí Flyway Community, etcétera, y 1 SQL migrations were detected.

[06:44] Pero no corrió porque no está siguiendo la convención del filename. ¿Eso qué quiere decir? Hay un error aquí en el cual no está consiguiendo identificar la versión correcta de Flyway. Vamos a explorar este error ahora.