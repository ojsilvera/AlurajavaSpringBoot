[00:00] Hola. Continuando con el desarrollo de nuestro curso, en esta parte vamos a comenzar a configurar la base de datos, nosotros seleccionamos la base de datos h2. Ustedes pueden seleccionar la base de datos de su preferencia como MySQL o Postgre o cualquier base de datos de memoria.

[00:14] Nosotros seleccionamos h2, ya que nos permite crear de forma automática las tablas y las columnas, así como los elementos existentes en la base de datos de forma más rápida y enfocarnos únicamente a lo que sería JPA y Hibernate.

[00:32] Entonces, para esto nosotros tenemos que crear un archivo llamado persistence.xml, donde van a estar las diferentes unidades de persistencia y las propiedades para esa base de datos.

[00:43] Entonces vamos a ir a la carpeta tienda, van a ir a la parte de recursos, van a seleccionar nuevo y van a crear una nueva carpeta, esa carpeta tiene que tener como nombre META-INF. Tiene que ser ese nombre en mayúscula, ya que es el nombre que se busca dentro de la aplicación por default.

[01:09] Seleccionan finalizar y seleccionan esa carpeta. Dentro de esa carpeta, van a seleccionar archivo, nuevo y van a seleccionar otro. Van a seleccionar archivo XML y van a crear, colocarle el nombre persistence.xml. Tiene que ser ese nombre exacto ya que nuevamente es el nombre que es buscado dentro de la configuración en el proyecto.

[01:38] Seleccionamos finalizar y ya tenemos previamente una tag o una etiqueta que indica la versión con la que vamos a estar trabajando, y el codificado del teclado. Lo voy a colocar acá, una tag que ya tenía previamente copiada, la vamos a proveer en el proyecto.

[01:57] Esta es la tag de persistencia donde van a ir todas las unidades de persistencia y dentro de las unidades de persistencia, las propiedades de la base de datos. Nos estaría indicando que precisamente está faltando dentro una etiqueta, una tag que es la persistence-unit.

[02:16] Esta tag es la que corresponde a la base de datos con la que estamos trabajando. Entonces por cada base de datos que nosotros estemos usando, vamos a tener una unidad de persistencia. El nombre para nuestra base de datos nosotros elegimos tienda pero pueden colocarle el nombre que tenga más lógica con su proyecto, y en este caso el nombre que mejor se adhiere es tienda.

[02:41] Lo siguiente que tenemos que colocar es el tipo de transacciones, cómo se van a manejar esas transacciones a lo largo del proyecto. Entonces vamos a hacer transaction-type. Entonces, tenemos dos valores posibles para el transaction-type que es “JTA”.

[03:00] Este valor es cuando nosotros estamos utilizando un servidor externo que maneja todas esas transacciones de forma automática por nosotros. O, en el caso de nuestro proyecto, nosotros vamos a estar manejando todas las transacciones, nosotros vamos a utilizar el caso de “RESOURCE_LOCAL”.

[03:22] Es cuando nosotros usamos una aplicación en Stand alone donde vamos a indicarle cuál es el momento de la transición que estamos. Y todo lo que es RESOURCE_LOCAL. Entonces, dentro de la unidad de persistencia nosotros vamos a tener una tag de propiedades. Y dentro de esas propiedades vamos a tener diversas propiedades individuales.

[03:45] La primera propiedad que vamos a tener para nuestra base de datos es el driver o el controlador, que son las características del software que nos permiten conectar nuestra base de datos con la aplicación. La encargada de hacer todas esto va a ser JPA entonces tenemos que colocar ya ex persistence.jvc. Y vamos a colocar aquí driver. Va a ser la primera propiedad que vamos a configurar.

[04:13] El valor para esa propiedad va a ser organización.h2.Driver. La siguiente propiedad está relacionada con la ruta donde se va a encontrar esa base de datos. También va a ser controlada por JPA. JDBC. Y va a ser la ruta URL. Entonces la ruta va a ser “jdbc:h2:mem:tienda.”

[04:55] Por último, están faltando dos propiedades básicas, que sería el usuario y la contraseña con la que nosotros vamos a acceder a esa base de datos. Entonces sería propiedad. Property, aquí tenemos que eliminar esto. Voy a colocar name. Nuevamente sería “javax.persistence.jdbc.user” Y vamos a colocar el usuario con el que nos vamos a registrar en la base de datos.

[05:29] Y el valor va a ser por default para la base de datos h2: “sa”. La última propiedad faltante sería la contraseña. Entonces sería “javax.persistence.jdbc.password”. Por default para la base de datos h2 tenemos el password vacío.

[06:01] Se puede configurar una contraseña para su base de datos. Y lo último que estaría faltando sería el dialecto. Entonces el dialecto se refiere a las características internas de cómo se comunica esa base de datos con nuestra aplicación, ya que ustedes pueden tener un booleano que sea del tipo verdadero o falso, true false, o 1-0.

[06:20] Vamos a colocar esa última propiedad que va a ser de hibernate.dialect. El valor para esa propiedad va a ser “org.hibernate.dialect.H2Dialect”. Con esto estamos indicando cuáles van a ser las características particulares de nuestra base de datos.

[06:57] Entonces, para MySQL va a existir un dialecto y para Postgre va a existir otro. Entonces, por último, lo que vamos a hacer es guardar todas estas configuraciones y a lo largo de nuestro del proyecto vamos a ir agregando más propiedades dentro de nuestro archivo de persistence que le van a dar otras características a la hora de ver los resultados.

[07:20] Entonces eso es todo por ahora y nosotros ya creamos nuestras dependencias y configuramos la base de datos. En el siguiente proyecto vamos a comenzar a crear nuestro modelo de entidades.