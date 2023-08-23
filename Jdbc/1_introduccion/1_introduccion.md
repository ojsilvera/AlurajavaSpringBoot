[00:00] Hola. Actualmente tenemos muchos tipos de servicios y productos en la web en donde estamos pudiendo registrarnos para estar utilizando a ellos. Alura es un gran ejemplo de esto. Aquí en Alura tenemos una plataforma online de cursos que están ahí digitalmente disponibles.

[00:15] Si elegimos una categoría por ejemplo, tenemos muchos cursos que están registrados y si queremos tornarnos alumnos de la plataforma, podemos venir aquí en el camino para la registración y cargar nuestros datos en el formulario, siguiendo todo acá con el nombre, el email y el país que vas a elegir, si quieres pagar, el medio de pago.

[00:36] Todas estas informaciones las tenemos guardadas en algún lado. Los cursos están ahí guardados en algún lugar y nuestros datos de registro también. Y esas informaciones son sensibles. Las informaciones personales son muy sensibles, no pueden estar ahí para que cualquier persona pueda acceder. Lo mismo las informaciones del curso ya que son una parte super importante de la plataforma.

[00:59] ¿Entonces dónde podemos estar guardando esas informaciones de una forma segura para que nadie pueda estar ahí accediendo directamente desde la página, por ejemplo? Imagina si todos los datos de los cursos son estáticos y están ahí disponibles solamente con inspeccionar la página para tomar las informaciones.

[01:16] ¿Entonces dónde podemos guardarlas? Lo más común en el mercado es estar utilizando un servicio de base de datos relacional. Los más utilizados y más conocidos en el mercado son el PostgreSQL, el SQL Server, el Oracle Database y el MySQL. Entre las opciones vamos a estar utilizando la de MySQL.

[01:39] Para descargarlo nosotros podemos hacer un clic aquí en downloads o, si estás yendo directamente a la pantalla, vas aquí a poner la URL en el navegador mysql.com/downloads. Aquí en esta pantalla de downloads, vamos a elegir la opción MySQL Community GPL Downloads.

[01:59] Aquí en esta pantalla vamos a estar eligiendo la opción que más nos atiende. Por ejemplo, si estás utilizando Windows, vas a hacer un clic aquí en MySQL Installer for Windows. Para mi caso, que estoy utilizando la Mac, voy a elegir la opción MySQL Community Server. Aquí en esta pantalla, nosotros podemos estar eligiendo las opciones de sistema operativo y nosotros vamos a estar trabajando con la opción de la versión 8.0.26.

[02:31] Voy a hacer un clic acá en downloads y si aparece esta pantalla acá para elegir de hacer login o de registrarse, no se desesperen, porque no es necesario. Hay una opción aquí que dice: "No, gracias. Solo quiero empezar mi download". Entonces hagamos un clic aquí y ya va a aparecer aquí abajo el download del instalador.

[02:54] Ahí está descargado el instalador, lo voy a mostrar acá y una cosa super importante. En este curso vamos a estar utilizando la versión 8.0.26. Es super importante que sigamos con esta versión, porque si estás utilizando una versión distinta de la que estoy mostrando acá, podemos estar teniendo algunos problemas de incompatibilidad de algún comando o de alguna sintaxis.

[03:17] Entonces combinamos ahí con la versión 8.0.26. Siguiendo aquí, vamos a ver el instalador. Si estás en Windows, abres el instalador de Windows, el ejecutable. Acá en Mac, vamos a estar abriendo acá este archivo que abre este paquete. Lo debe estar instalando.

[03:37] Y aquí tenemos todas las opciones para poder instalarlo. La licencia, voy a estar de acuerdo acá, el tipo de instalación es por defecto. No elegimos nada. Acá tengo que poner mi contraseña de admin de la máquina. Y ahí estamos instalando la aplicación, la base de datos.

[04:06] Bueno, aquí es una alerta de seguridad. Yo voy a poner aquí instalar sin ningún problema. Y nosotros tenemos que estar eligiendo aquí una contraseña para utilizar una base de datos.

[04:17] En este caso vamos a estar utilizando el Legacy Password Encryption. Va a hacer un Next acá, y vamos a poner una contraseña para el usuario del tipo root. O sea nuestra contraseña aquí va a ser root1234. Doy un finish acá, pongo mi contraseña otra vez y listo. Se terminó la instalación de MySQL en nuestra computadora.

[04:46] Hago un clic acá en cerrar, luego para la basura, ya no lo voy a utilizar más. Cierro acá y ahora lo que vamos a hacer, vamos a abrir la terminal o la consola de Windows. Acá voy a estar utilizando la terminal de Mac. Si estás en Windows, abres la consola. Si estas en Linux, también en la terminal.

[05:05] Aquí en la terminal, voy a agrandar un poco más, vamos a estar ejecutando la consola de MySQL. En mi caso que estoy en Mac OS, para abrir la consola acá desde la terminal, tengo que escribir el siguiente comando: /usr/local/mysql/bin/mysql -u root -p y hago enter. Ahí me pide la contraseña, que cuando registramos era root1234. Ahí está.

[05:45] Estamos en la consola de MySQL. Pero, Ícaro, espera un poco. Ya estamos instalando la base de datos y aun no nos has contado qué vamos a desarrollar. ¿Qué estamos haciendo? Eso es verdad. Fui un poco apurado acá, fuimos derecho a la acción y no conté la idea de este proyecto. La idea del proyecto es la siguiente.

[06:08] Nosotros vamos a estar desarrollando una aplicación que maneja el control de stock de una tienda y lo primero que vamos a estar haciendo es crear nuestra base de datos. Y para crear la base de datos acá desde la consola, el comando que vamos a estar escribiendo acá es create database, y vamos a poner el nombre control_de_stock.

[06:34] Hacemos un Enter y ahí uso una flechita porque ahí me olvidé de poner el punto y coma. Todos los comandos acá en la consola, tenemos que terminar con punto y coma, si no, la consola de MySQL va a estar pensando que es la continuación del comando que estamos escribiendo. Puse el punto y coma y dijo query ok.

[06:53] O sea, la base de datos ya está creada. Ahora para estar utilizando esta base de datos que recién creamos, vamos a estar utilizando otro comando bastante obvio que es use control_de_stock; y había dicho que era obvio porque estoy diciendo ahora justamente para utilizar la base de datos. Entonces use control_de_stock. Siguiendo aquí, ya estamos en la base de datos de control_de_stock, estamos en ella pero no tenemos ninguna tabla.

[07:27] ¿Ahora que vamos a hacer? Entonces vamos a estar creando una tabla para estar registrando nuestros productos. Entonces vamos a crear una tabla llamada producto. Ella va a representar todos los productos que tenemos guardados en el depósito. El script para crear esta tabla va a ser el siguiente: create table producto, abro un paréntesis, aquí puedo hacer un enter y voy a declarar los campos de esta tabla.

[07:55] Vamos a tener un ID del tipo entero, del tipo con la característica AUTO_INCREMENT. El AUTO_INCREMENT significa que, para cada registro insertado en la tabla, este valor va a ser incrementado automáticamente. Entonces nosotros no tenemos que estar preocupándonos con cual va a ser el próximo ID que estamos registrando ahí en la base de datos.

[08:20] La propia base de datos de MySQL ya va a estar encargándose de esto para nosotros. Una preocupación menos. Entonces pusimos el ID, hagamos aquí coma, seguimos aquí con enter, nombre del producto del tipo VARCHAR(50) NOT NULL, no quiero que el producto tenga nombre nulo. Sigo aquí con la descripción, que también es del tipo VARCHAR pero un poco más grande, de 255.

[08:51] Esto sí puede ser nulo, no hay problema, Seguimos aquí con la cantidad. Quiero saber cuántos productos hay disponibles en el depósito. Entonces, la cantidad del tipo INT también NOT NULL y su valor por defecto va a ser 0. O sea, si nos olvidamos de cargar esta información, ya inicia ahí, en la base de datos con 0 el registro nuevo.

[09:17] Hago aquí una coma más y declaro que la clave primaria, PRIMARY KEY de nuestra tabla va a ser la columna id. Con eso cierro el comando y escribo aquí una instrucción más antes de finalizar que es )Engine=InnoDB; ahora sí, punto y coma y enter. Ya está la tabla creada. Este comando acá, Engine=InnoDB, señala que queremos que esta tabla acepte operaciones dentro de una transacción.

[09:59] En resumen, es esto. Más adelante vamos a ver qué significa. Ahí ya ejecutamos el script y listo. Ya tenemos la tabla de productos creada. Si hacemos aquí un select todo, que es el asterisco, from producto; no hay nada, hace un empty set. Entonces vamos a insertar nuestro primer producto aquí en la base de datos. Vamos a hacer lo siguiente.

[10:27] Insert into producto (nombre, descripción, cantidad) values (‘Mesa’, ‘Mesa de 4 lugares’, 10). O sea, estamos registrando 10 mesas de 4 lugares en nuestra base de datos. Hago un punto y coma y ahí está, fue insertada la nueva fila ahí en nuestra tabla con el producto mesa. Vean que yo no declaré el id en el comando de insert.

[11:12] ¿Por qué? Como es un AUTO_INCREMENT no tengo que preocuparme con esto. Entonces si hago un select otra vez from producto, puse mal. Ahí va a dar un error. Voy a limpiar la consola, select * from producto, ahora sí, tenemos una mesa de 4 lugares, perdón.

[11:39] El id 1, que es nuestra clave primaria de AUTO_INCREMENT, que es una mesa, mesa de 4 lugares, la característica. Y tenemos 10 cantidades de ella. O sea, 10 mesas de 4 lugares en nuestro depósito. Vamos a hacer lo siguiente para comprobar eso del AUTO_INCREMENT para ver si es verdad lo que estoy diciendo. Vamos a agregar un producto más. Entonces vamos a hacer lo siguiente.

[12:01] Insert into producto (nombre, descripción, cantidad) values (‘Celular’, ‘Celular Samsung’, 50); ahí está insertado, vamos a ver que pasa. ¿Cuál va a ser el número del id? Si el AUTO_INCREMENT funciona de verdad, tiene que ser el número 2. Entonces select * from producto; y ahora sí, 1 mesa, 2 celulares. Ahí está. Perfecto.

[12:53] Ya tenemos dos productos en nuestra base de datos y por ahora listo. Vamos a avanzar ahora, creando una aplicación Java que pueda conectarse a esta base de datos. Por aquí ya quedamos. Instalamos el MySQL, creamos nuestra base de datos, creamos la tabla de producto y ya insertamos dos productos.

[13:15] Ahora nosotros vamos a estar creando nuestra aplicación en Java, que va a conectarse a esta base de datos, para realizar estas operaciones que estuvimos haciendo en la consola. Entonces, para la próxima clase, para que empecemos a desarrollar nuestra aplicación Java, vamos a estar utilizando la versión 11 de Java y vamos a estar utilizando también el Eclipse.

[13:37] Tiene que ser una versión que sea compatible con esta versión, porque si no, vamos a tener problemas. Nos vemos en el próximo video.