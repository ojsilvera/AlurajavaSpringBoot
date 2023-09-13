[00:00] Hola. Finalizada la breve historia de lo que es JPA y Hibernate, de cuál fue su origen y tecnología, vamos a comenzar a desarrollar un pequeño proyecto donde vamos a mostrar las funcionalidades básicas de JPA con Hibernate.

[00:16] Para esto nosotros vamos a utilizar la IDE de Eclipse o pueden utilizar la IDE de su preferencia, como Visual Studio Code o IntelliJ. Recomendamos que utilicen Eclipse para mantener la secuencia de los videos y tener la menor cantidad de errores de configuración.

[00:35] Vamos a suponer que vamos a crear una pequeña aplicación, donde se almacenen diversos productos para una tienda. El nombre de esa tienda puede ser Alura, puede ser Coca-Cola, puede ser el nombre que ustedes quieran.

[00:52] Entonces, estos productos van a tener un cierto nombre, van a tener una descripción, un precio y una categoría. Como ustedes pueden ver, estos productos van a estar almacenados en la base de datos, también van a tener un cierto edit.

[01:06] Entonces nosotros vamos a mostrar cómo vamos a generar todas estas características para cada atributos y vamos a configurar todo el proyecto desde el inicio hasta el final del video. Colocamos los diversos productos y las relaciones entre los productos y las categorías.

[01:25] Entonces, lo primero que vamos a hacer es crear un nuevo proyecto Maven, seleccionamos crear un proyecto simple, siguiente, el grupo id va a ser com.latam.alura.tienda y el artifact id va a ser tienda.

[01:41] Inmediatamente se crea una estructura de carpetas donde van a ir nuestras clases, carpeta de recursos, que son archivos ocultos, las carpetas de pruebas, nuestras dependencias y, el archivo de las dependencias vamos a abrir el archivo pom.xml.

[02:03] Nosotros vamos a utilizar el manejador de dependencias Maven para descargar las diversas dependencias. Por default, Eclipse configura nuestro proyecto y Java la versión 5. Nosotros vamos a colocar Java en la versión 11 utilizando una tag.

[02:19] Esta tag nos permite configurar Java en la versión 11 que es lo que vamos a utilizar a lo largo del proyecto. Lo siguiente que tenemos que hacer es configurar nuestra dependencia.

[02:29] La dependencia ustedes la pueden conseguir de la página Maven.repository que es la página oficial donde se encuentran todas las dependencias de los diversos proyectos. Nosotros primero vamos a crear una etiqueta, una tag raíz que va a ser dependencias.

[02:46] Y por cada dependencia tenemos que crear una tag de dependencias. Dentro de nuestra tag nosotros vamos a tener un groupId, vamos a tener un artifactId y vamos a tener una versión.

[03:08] Entonces la primera dependencia que nosotros queremos agregar es la dependencia de Hibernate. Para eso nosotros nos creamos en el groupId organización.hibernate. El artefactoId va a ser hibernate-entitymanager y la versión va a ser la versión 5.6.14, versión final.

[03:38] Entonces ya con esto tenemos, si guardamos, vemos que el panel de la izquierda se han agregado nuestras dependencias para Hibernate. Entonces, tenemos hibernate-entitymanager, hibernate-core y hibernate-commons-annotations.

[03:53] Y aquí vemos que está java-persistence-api que sería que sería JPA. El resto son dependencias de las que necesita Hibernate para poder funcionar correctamente. La siguiente dependencia sería la dependencia de la base de datos.

[04:09] Nosotros tenemos que crear una nueva etiqueta donde va a ir la dependencia, la etiqueta del groupId que va a ser comunicación.h2database, el artifactId va a ser h2 y la versión de esta base de datos va a ser la versión 2.1.214.

[04:40] Entonces con eso ya tenemos configurada nuestras dependencias de Hibernate y de la base de datos. Vemos que aquí se agregó, si volvemos acá, se agregó la base de datos. Y tenemos un pequeño error, que esto se resuelve seleccionando la carpeta tienda, van a ir a donde dice Maven y van a seleccionar actualizar proyecto.

[05:06] Ahí van a seleccionar OK, y se corrige ese error. En la siguiente parte nosotros vamos a comenzar a configurar la base de datos con el archivo de persistencia.hxm.

