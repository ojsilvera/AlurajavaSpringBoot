[00:00] Luego de haber compilado la aplicación, ahora vamos a intentar simular el deploy en un servicio de nube o en un servidor local. Entonces lo primero que tenemos que hacer es revisar dónde se encuentra ese archivo dentro de la consola. Para eso vamos a utilizar el comando ls target.

[00:20] Vemos que el archivo se encuentra ahí en la versión 001, vamos a verificar que la versión con la que estamos trabajando que es java -version sea compatible con la que fue compilada la aplicación dentro de IntelliJ.

[00:37] Si nosotros verificamos en la estructura del proyecto vemos que tenemos ya compilada en la versión 17. Nosotros podemos modificar la versión de Java a una versión anterior o una versión superior dentro de las opciones que él ofrece. Entonces, continuando, ahora vamos a intentar compilar ese archivo con el comando java –jar, pasando el nombre y la ruta donde se encuentra.

[01:01] Entonces java –jar target/api- 0.0.1-SNAPSHOT.jar. Ejecutamos la aplicación. Él está compilando. Él realizó todo el proceso, vemos que luego de que compila y ejecuta la aplicación, acá en la parte superior, él vio que no teníamos un perfil configurado cuando nosotros intentamos ejecutar la aplicación, entonces él va a ejecutar por default el perfil de desarrollador o el perfil inicial que no tenía la extensión test o producción.

[01:52] Entonces él tiene un perfil default que es el perfil sin extensión. Ahora nosotros vamos a aplicar acá "Ctrl + C" y vamos a intentar ejecutar el perfil de producción, para eso vamos a pasar la flag --spring.profiles. Esta vez sí es con la S. Indicamos que vamos a activar el perfil de producción.

[02:20] Él intentó compilar, está cargándolo todos los valores y nos genera un error. Entonces si nosotros recordamos, acá nos está indicando qué nosotros no hemos pasado, cuál es la ruta de la base de datos, ni la ruta ni el usuario ni el contraseña, recordando que en el perfil de producción nosotros colocamos variables de ambiente para proteger esas claves de acceso.

[02:47] Entonces lo que vamos a hacer es acá luego de la palabra java, vamos a colocar todos los valores para esas variables de ambiente. En los servicios de cloud, ustedes van a encontrarse en alguna parte como Google o en Amazon, encontrarse en alguna parte donde ustedes pueden configurar esas variables de ambiente o si se encuentra en un escritorio como Windows pueden configurar sus variables de ambiente en la parte de propiedades del sistema.

[03:21] Entonces acá en donde dice variables ambiente pueden configurar las variables que tienen para ese programa, entonces acá vamos a colocar –DDATASOURCE_URL. Vamos a pasar la URL, que sería jdbc:mysql://localhost/vollmed_api.

[03:56] La siguiente es pasar el usuario. Sería desde -DDATASOURCE:USERNAME=root y por último, la contraseña. –DDATASOURCE_PASSWORD=2812.

[04:27] Vamos a verificar, acá vamos a hacer un enter. Y esta vez está compilando. Él buscó el perfil de producción, por los momentos no ha encontrado ningún error. Entonces, las variables de ambiente fueron configuradas, él ejecutó la aplicación y ya no encontramos la aplicación corriendo dentro de nuestro ambiente del escritorio con las variables previamente pasadas dentro de la consola.

[04:54] Entonces el mismo proceso es un sistema de cloud sin servidor y ya de esa forma, nosotros tenemos nuestra aplicación desarrollada y aplicada dentro del servidor exitosamente. Entonces ya con esto concluimos lo que sería el desarrollo de la aplicación donde nosotros ascendamos consultas con médicos y pacientes, realizamos todas las pruebas y todos los diferentes pasos que tiene que tener una aplicación en la parte del backend.