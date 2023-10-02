Ya hemos implementado pruebas automatizadas y consideramos que hemos terminado el proyecto. Cuando terminamos un proyecto completo o una parte de él, queremos ponerlo en funcionamiento. Surge la siguiente pregunta: ¿cómo se puede disponibilizar un proyecto?

Build del proyecto

Hasta ahora, solo ejecutamos el proyecto localmente, en nuestra propia computadora donde corremos la aplicación, la base de datos y las pruebas. Sin embargo, para poner a disposición este proyecto, debemos alojarlo en algún servidor, ya sea interno de la empresa o algún servicio en la nube como Amazon, Google Cloud y Azure.

La idea es generar la compilación de nuestro proyecto y disponibilizar para su ejecución en algún servidor. Además, tendremos que hacer algunos ajustes en nuestra aplicación antes de alojarla.

El ajuste principal que se debe hacer está relacionado con la base de datos. Las configuraciones de la base de datos de nuestra aplicación se encuentran en el archivo application.yml; vamos a abrirlo en "src > main > resources".

spring:
 profile.active: dev, test, prod
 datasource:
   url: jdbc:mysql://localhost/vollmed_api
   username: root
   password: 2812
 jpa:
   show-sql: true
   properties:
     hibernate:
       format_sql: true

server:
 error:
   include-stacktrace: never
api:
 security:
   secret: ${JWT_SECRET:123456}COPIA EL CÓDIGO
En esta carpeta, además de application.properties, tenemos application-test.yml, configurado solo para sobrescribir la base de datos de la aplicación durante la ejecución de las pruebas.

spring:
 datasource:
   url: jdbc:mysql://localhost/vollmed_api_test?createDatabaseIfNotExist=true&serverTimezone=UTC
   username: root
   password: 2812COPIA EL CÓDIGO
En application.yml, tenemos las configuraciones de la base de datos que apuntan a "localhost". Con esto, le decimos a Spring que la base de datos se está ejecutando en la propia máquina y la base de datos se llama "vollmed_api"; el usuario de la base de datos es "root"; y la contraseña de la base de datos es "root".

Estas son las configuraciones fijas de la base de datos, pero solo funcionan localmente. Es posible que en el servidor donde vamos a disponibilizar el proyecto, la base de datos se encuentre en otra computadora, es decir, puede haber dos servidores: uno donde se alojará la aplicación; y otro donde se alojará la base de datos.

Por lo tanto, la dirección no será "localhost". Queremos flexibilizar estas configuraciones, tanto de la dirección de la base de datos como del usuario y la contraseña, para que podamos sobrescribir los parámetros en el entorno de producción.

Una forma de hacerlo es aplicando el concepto de ambientes, de perfiles, tal como lo hicimos para las pruebas. La prueba está en otro archivo (application-test.yml). Para el entorno de producción, podemos crear un tercer archivo separado.

Archivo application-prod.yml

Para crear este archivo, seleccionamos application.yml en el panel "Project" a la izquierda y presionamos "Ctrl + C" para copiar. Se abrirá una ventana para que renombramos el archivo; lo llamaremos application-prod.yml. Después de eso, presionamos "Enter" para finalizar la acción. "Prod" es una abreviatura de "production" (entorno de producción).

La carga de estos archivos funciona de la siguiente manera: Spring siempre carga todas las propiedades de application.yml, y si le indicamos que estamos en el entorno de producción, también carga las propiedades de application-prod.yml.

En este archivo, solo sobrescribiremos las propiedades deseadas. Las que queramos reutilizar no necesitan duplicarse: las dejamos en el propio archivo application.yml.

En este caso, queremos sobrescribir la URL de la base de datos, el usuario y la contraseña, además de las dos siguientes propiedades: show-sql y format_sql. En un entorno de producción, no queremos generar registro de SQL, por lo que definiremos esas propiedades como "false".

La propiedad stacktrace permanecerá como "never" y el secreto también no sufrirá alteraciones, por lo que podemos eliminar esas dos líneas de código; se leerán de application.yml.

spring:
 profile.active: prod
 datasource:
   url: jdbc:mysql://localhost/vollmed_api
   username: root
   password: root
 jpa:
   show-sql: false
   properties:
     hibernate:
       format_sql: false

server:
 error:
   include-stacktrace: never
api:
 security:
   secret: ${JWT_SECRET:123456}COPIA EL CÓDIGO
Una vez hecho esto, ¿cómo pasar el nombre de usuario, la contraseña y la URL de la base de datos? Todavía no sabemos cuáles serán las propiedades y no es interesante dejarlas fijas en el código.

De hecho, esta es una buena práctica de seguridad: no debemos exponer contraseñas y otros aspectos de seguridad en el código fuente de la aplicación.

Para resolver este problema, solemos usar variables de entorno. En este caso, la idea es la siguiente: en la propiedad spring.datasource.url, escribimos $, abrimos llaves y escribimos el nombre de la variable de entorno (DATASOURCE_URL), similar a lo que hicimos con el secreto del token JSON Web. Haremos lo mismo en las otras dos propiedades, pero en la primera tenemos la variable DATASOURCE_USERNAME y en la segunda, DATASOURCE_PASSWORD.

spring:
 profile.active: prod
 datasource:
   url: ${DATASOURCE_URL}
   username: ${DATASOURCE_USERNAME}
   password: ${DATASOURCE_PASSWORD}
 jpa:
   show-sql: false
   properties:
     hibernate:
       format_sql: false

server:
 error:
   include-stacktrace: never
api:
 security:
   secret: ${JWT_SECRET:123456}COPIA EL CÓDIGO
Con eso, Spring sabe que estas tres propiedades hacen referencia a variables de entorno. La idea es que busque esas variables en un sistema operativo o en un parámetro cuando ejecutemos la aplicación (aprenderemos cómo hacerlo más adelante) y reemplace en esas propiedades el valor asignado a ellas.

De esta manera, podemos tener otro archivo properties exclusivo para el ambiente de producción y sobrescribir solo lo que deseamos. El resto seguirá siendo extraído de application.yml.

De esta forma, configuramos nuestra base de datos en el ambiente de producción a través de variables de entorno. ¡Esta es una buena práctica!

Ahora, surge la siguiente pregunta:

Una vez configurado y finalizado el proyecto, ¿cómo generamos el ejecutable de esta aplicación y lo enviamos para que se ejecute en el servidor, ya sea en un ambiente en la nube o interno de la empresa?

Cómo ejecutar el proyecto?

Para hacerlo, basta con utilizar el comando java. Lo único que necesitamos tener instalado en el servidor donde vamos a ejecutar la aplicación es Java en la versión 17, utilizada en este curso.

Con Java instalado, digitamos java -version para mostrar esta información en la terminal:

PS C:\Users\public\alura\springboot> java -version
java version "17.0.6" 2023-01-17 LTS
Java(TM) SE Runtime Environment (build 17.0.6+9-LTS-190)                       
Java HotSpot(TM) 64-Bit Server VM (build 17.0.6+9-LTS-190, mixed mode, sharing)
PS C:\Users\public\alura\springboot> COPIA EL CÓDIGO
El comando para ejecutar el proyecto esta compuesto por el comando java, por el parametro -jar, y por el camino al archivo:

java -jar target/api-0.0.1-SNAPSHOT.jarCOPIA EL CÓDIGO
PS C:\Users\public\alura\springboot> java -version
java version "17.0.6" 2023-01-17 LTS
Java(TM) SE Runtime Environment (build 17.0.6+9-LTS-190)                       
Java HotSpot(TM) 64-Bit Server VM (build 17.0.6+9-LTS-190, mixed mode, sharing)
PS C:\Users\public\alura\springboot> java -jar .\target\api-0.0.1-SNAPSHOT.jar COPIA EL CÓDIGO
A continuación, presionamos "Enter" para ejecutar. En principio, la aplicación se inicia, pero vamos a observar el comienzo del registro, debajo de la pantalla de inicio de Spring. En las primeras líneas, aparece el mensaje de que la aplicación se está iniciando ("Starting ApiApplication"), y en la segunda línea, se muestran información sobre el perfil.

No hay ningún perfil activo, por lo que se utilizará el perfil "default", es decir, Spring solo leerá el archivo application.yml.

Sin embargo, queremos que se lea el archivo application-prod.yml. ¿Cómo podemos hacer para que, al ejecutar el proyecto desde la línea de comandos, se considere "prod" como perfil activo?

Detenemos la aplicación y presionamos la flecha hacia arriba para listar el último comando. Ahora, antes del parámetro -jar, agregamos otro parámetro: --spring.profiles.active=prod.

PS C:\Users\public\alura\springboot> java -jar .\target\api-0.0.1-SNAPSHOT.jar --spring.profiles.active=prodCOPIA EL CÓDIGO
Así, pasamos el perfil activo al momento de ejecutar el proyecto: solo necesitamos pasar el parámetro -- y el nombre del parámetro que Spring espera (spring.profiles.active=prod). Después del nombre del perfil, que en mi caso es "prod", viene el parámetro -jar seguido de la ruta del archivo .jar.

Luego, presionamos "Enter" y ejecutamos de nuevo. Sin embargo, se producirá un error. Si vamos al inicio del registro, veremos los mensajes de que la aplicación se está iniciando y que el perfil "prod" está activo (The following 1 profile is active: "prod").

Sin embargo, recuerde que en el archivo application-prod.yml dijimos que la URL, el nombre de usuario y la contraseña de la base de datos deben recuperarse de las variables de entorno. No se encontraron en el sistema operativo, por lo que se produjo una Exception.

En el log, aparecerá una mensaje indicando que no se pudo cargar la parte del repositorio y persistencia, porque la URL no se identificó y debería iniciarse con "jdbc", pero por ahora se está utilizando ${}.

Caused by: java.lang.IllegalArgumentException: URL must start with 'jdbc'COPIA EL CÓDIGO
Entonces, ¿cómo pasar las variables de entorno? ¡De la misma manera que pasamos el parámetro de perfil! Con el proyecto detenido, presionamos la flecha hacia arriba y escribimos el siguiente comando:

java -DDATASOURCE_URL=jdbc:mysql://localhost/vollmed_api -DDATASOURCE_USERNAME=root -DDATASOURCE_PASSWORD=root -jar target/api-0.0.1-SNAPSHOT.jar  - -spring.profiles.active=prod COPIA EL CÓDIGO
Antes del parámetro -jar, debemos insertar nuevamente el parámetro -D, reemplazando las tres variables de entorno. En cada parámetro, se reemplaza una variable, así que primero tenemos -DDATASOURCE_URL=, seguido de la dirección del servidor de la base de datos, que puede ser la propia máquina o la IP de otra máquina.