[00:00] Hola. En la parte anterior nosotros realizamos las pruebas y con esto finalizamos el desarrollo de nuestra aplicación. Ahora, una vez que nosotros desarrollamos la aplicación en su totalidad, realizamos todas las pruebas, todas las verificaciones y la ejecutamos, nosotros vamos a querer realizar un deploy o en algún servidor o en alguna nube.

[00:20] Entonces, para eso, nosotros tenemos que entregar un archivo ejecutable, y eso lo vamos a hacer a través Maven. Entonces Maven, además de ayudarnos con la descarga de las dependencias para nuestra aplicación, él nos ayuda a realizar el empacotamiento de todo lo que hemos desarrollado a lo largo del curso para hacer el deploy posteriormente dentro de un servidor.

[00:44] Entonces nosotros tenemos que tener un archivo con las clases compiladas, que es el que vamos a colocar dentro del servidor, y de esa forma va a ejecutar la aplicación para que esté disponible para otros usuarios. Entonces, para eso nosotros acá teníamos en nuestras configuraciones de la API, nosotros estábamos trabajando con una base de datos local.

[01:14] Generalmente nosotros vamos a estar trabajando con bases de datos que se pueden encontrar en otros servidores o en alguna ruta que no necesariamente es la de esta máquina. Adicionalmente, va a tener otra contraseña u otro usuario, y esas contraseñas no pueden encontrarse visibles de esta forma.

[01:37] Entonces nosotros tenemos que buscar una forma de realizar la seguridad para evitar que quede expuesta la contraseña y el usuario, así como la ruta de la base de datos a una persona que pueda tener intenciones maliciosas.

[01:55] Entonces, en resumen, nosotros vamos a realizar el empaquetamiento de nuestra aplicación, vamos a trabajar con los perfiles, en los ambientes donde vamos a trabajar, nosotros ya mostramos que estábamos trabajando con el ambiente de prueba únicamente para las pruebas donde teníamos una base de datos aparte de la base de datos que estábamos utilizando para el desarrollo de la aplicación.

[02:20] Entonces nosotros vamos a tener un tercer perfil que es el perfil de producción. Ese perfil es el perfil donde nosotros vamos a colocar las configuraciones que van a ir al servidor final. Entonces, para eso nosotros vamos a copiar este archivo que es el archivo de aplicaciones. Lo vamos a pegar dentro de la carpeta de recursos.

[02:40] A este archivo le vamos a colocar raya o trazo, prod, indicando que va a hacer el perfil de producción. Ahora, ya que nosotros estamos colocando el perfil de producción, tenemos que, vamos a eliminar esto acá y acá vamos a colocar que esas consultas de SQL no van a ser realizadas.

[03:11] Entonces no le tenemos que colocar como falso las consultas y el formato que deseamos. Ahora tenemos que usar variables de ambiente para evitar exponer la ruta, así como el usuario y la contraseña, dentro de nuestra aplicación. Para eso vamos a utilizar el siguiente comando. Entonces ${DATASOURCE_URL} De la misma forma lo vamos a hacer para el usuario.

[03:46] Acá vamos a colocar DATASOURCE_USERNAME. Ya acá vamos a colocar $DATASOURE_PASSWORD. Entonces, de esta forma estamos indicando a Spring framework, que este va a ser el formato con el que vamos a pasar la URL, entonces así protegemos la aplicación de dejar las contraseñas de usuarios y la ruta de la base de datos expuestos.

[04:14] Adicionalmente, yo tengo que colocar acá el perfil, el perfil que se encuentra activo. Entonces, ya que este es el perfil de producción, vamos a colocar profile.active: prod. Entonces, ya con eso, nosotros estamos indicando acá que estamos activando el perfil de producción para esta configuración.

[04:49] Y dentro de la aplicación convencional, vamos a activar los perfiles profiles.active. Acá vamos a activar todos los perfiles, que sería el perfil de desarrollo, el perfil de test y el perfil de producción.

[05:07] Entonces, ya que yo tengo toda la configuración realizada, vamos a verificar eso, la aplicación, la llave de acceso de token la puedo dejar acá y los errores, los registros de errores tampoco los va a pasar, entonces voy a dejar esta configuración acá.

[05:33] Las URL y el usuario se encuentran ya protegidos con las variables de ambiente y los perfiles se encuentran configurados para el diferente uso. Entonces vamos a ir a la pestaña de Maven y en la parte de API vamos a ir a donde dice ciclo de vida y en package vamos a correr, Maven build.

[05:55] Acá nosotros tuvimos un error. Cuando nosotros colocamos profiles, no es profiles sino profile, sin la S. Vamos a intentar ejecutar la aplicación nuevamente. Esta vez sí se ejecutó correctamente, vemos que el realizó el compilado de forma exitosa, ejecutó las cuatro pruebas y realizó en el lado izquierdo, en el panel izquierdo.

[06:25] Nosotros vamos a encontrar ahora una carpeta llamada target con todas las clases que fueron generadas y un archivo ejecutable que es el que nosotros vamos a tomar y vamos a descargar dentro de alguno de los servicios Cloud, como Amazon, Azure o Google Cloud.

[06:41] Este archivo nos indica la versión, que es 001 API y el formato que es la extensión Java. Entonces, de esa forma, nosotros podemos tomar ese archivo y realizar el deploy en algún servicio. En la siguiente parte vamos a ver cómo se realizan estas actividades dentro de la consola.