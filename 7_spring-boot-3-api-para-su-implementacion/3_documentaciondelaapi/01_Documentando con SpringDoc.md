[00:00] Hola. En la parte anterior, recapitulando lo que fue realizado, nosotros aplicamos los validadores para las reglas de negocio de la clínica del servicio de clínica. Implementamos esos validadores dentro del proyecto. Nosotros íbamos a recibir un conjunto de datos dentro del end point a través de la API de Postman.

[00:00] Entonces nosotros iniciamos enviando el ID de paciente, el ID del médico y la fecha en la que queríamos realizar esa consulta. El siguiente paso es recibir esos datos dentro del método en el controlador que nos va a enviar al servicio de agenda de consulta.

[00:51] Dentro de él, nosotros llegamos a realizar las validaciones y vamos a implementarlas en este servicio. Esas validaciones están relacionadas al horario de anticipación, al médico activo, paciente activo, médico con consulta y dejamos un desafío que nos permitía cancelar una consulta.

[01:09] También existe otro desafío que vamos a dejar para ustedes que sería el caso en el que nosotros vamos a obtener esa consulta. Nosotros tenemos un caso similar, es el caso donde nosotros obtenemos un médico, que es bastante simple, simplemente aplicaron dentro del controlador, el método get y podemos obtener a todas las consultas o podemos obtener una consulta por el ID.

[01:41] Retomando el caso de la cancelación de consultas que fue la que realizamos en la clase de servicio, nosotros vamos a recibir los datos, vamos a validar que ese ID de la consulta exista, caso no exista vamos a enviar un mensaje de error en la consola indicando que el ID de la consulta no existe.

[01:58] Si existe, vamos a aplicar un validador de cancelamiento, lo vamos a dejar acá adentro del paquete de desafío que nos permite verificar que esa consulta solamente puede ser cancelada con antecedencia mínima de 24 horas, verificándolo dentro de los datos, la fecha que estamos recibiendo en el HS.

[02:18] Una vez que hayan sido validados los datos nosotros vamos a buscar esa consulta en el repositorio y vamos a aplicar un método que se encuentra en la clase consulta en la entidad consulta que va a indicar el motivo de la consulta. Ese motivo puede ser que el paciente desistió, que el médico canceló por alguna razón, motivo o algún otro motivo.

[02:45] Acá pueden colocar diversos motivos y lo dejamos dentro de un enumerador para limitar las posibles opciones que puedan ser colocadas y evitar la mayor cantidad de errores. Entonces, luego de que se haya pasado el motivo, nosotros tuvimos que modificar la clase consulta para agregar un constructor, ya que nosotros dentro del servicio de agendar nosotros estábamos pasando los datos del ID como nulo, y acá tendríamos que agregar otro valor de nulo que sería el motivo de cancelación.

[03:16] Entonces agregando el constructor nosotros pasamos únicamente los datos que queremos que estamos recibiendo de la API. Entonces ahora de vuelta la API de Postman, nosotros acá conocemos cuáles son todos los endpoints, cuáles son las informaciones de parámetros que tienen que tener esos métodos. Conocemos los valores, incluso tenemos alguna información de lo que existe dentro de la base de datos.

[03:49] Sin embargo, cuando nosotros enviamos eso al cliente no necesariamente el cliente tiene conocimiento de toda esa información o puede que no conozca del lenguaje Java y del Spring Framework.

[04:01] Entonces, sería interesante dar algún tipo de documentación que le dé una ayuda, un soporte a la hora de utilizar la aplicación. Lo recomendable es no utilizar una documentación del tipo de archivo de texto o archivo Word y darle una mejor presentación que se integre con dentro de nuestro proyecto.

[04:22] Para eso nosotros tenemos una API externa que no es Postman ya que toma en cuenta como una API externa, pero tenemos una API que se integra dentro de nuestro proyecto y al ejecutarlo le va a permitir al usuario, que en este caso sería el cliente tener una especie de Postman o Insomnia, que es una API que le va a permitir testar y probar todos los endpoint y las funcionalidades de nuestro proyecto.

[04:56] Así nosotros vamos al link de openAPI. Vamos a ir openAPI.doc. Vamos a colocar Springdoc para buscar la API documentación. Esta es la API que nos va a permitir crear una documentación interactiva dentro de nuestro proyecto, que va a permitirle al cliente conseguir trabajar con los endpoints y darle una mejor ilustración de los parámetros que se están aplicando.

[05:40] Así, nosotros vemos acá en la introducción y ya inmediatamente nos está marcando una alerta de que para las personas que están utilizando Springboot en la versión 3 tenemos que ir a la documentación de Springdoc openapi en la versión 2. Vamos a cerrar acá.

[05:58] Lo primero que nos indica vemos que la URL se ha modificado el Springdoc en la versión 2 y lo primero que nos indica es que vemos a adicionar las dependencias de esta API dentro de nuestro proyecto, vamos a copiar y vamos a ir a nuestro proyecto de springbook dentro del archivo pom. Vamos a agregar al final esa nueva dependencia dentro de las dependencias.

[06:28] Entonces agregamos las dependencias y acá podemos seleccionar este icono que va a recargar las dependencias o podemos ir en la pestaña del lado derecho, acá donde dice API vamos a ir a dependencias y acá en el ícono de recargar todo el proyecto vamos a seleccionar. Entonces se están recargando las dependencias, vamos a esperar que carguen.

[06:56] Vemos que acá al final se ha agregado una nueva dependencia que es la dependencia de Springdoc. Entonces, ya de esa forma, nosotros tenemos nuestra nueva dependencia funcionando.

[07:08] Ahora de vuelta en la documentación de springdoc nosotros vemos que vamos a tener dos URL que se van a integrar inmediatamente luego de que nosotros estamos trabajando con ellas, que es la URL donde vamos a tener una interface de usuario similar al Postman que nos va a permitir, nos va a mostrar informaciones de los endpoints, de los parámetros, informaciones de usos y cómo el estado retornado luego de haber usado esos endpoints.

[07:43] También vamos a tener otra URL que nos va a dar toda la información en un formato JSON, relacionada a todos los endpoint, los parámetros, los servidores existentes así como otras informaciones adicionales de nuestro proyecto. Entonces para eso nosotros tenemos que recordar que nosotros estamos utilizando Json web token.

[08:08] Entonces al agregar estas nuevas páginas, estas extensiones, nosotros vamos a recibir un mensaje de alerta, ya que nosotros no tenemos acceso a esas URL, nosotros tenemos que ir a nuestro proyecto y en Spring Security las configuraciones de seguridad, nosotros vamos a agregar esas nuevas URL.

[08:47] Entonces, acá la primera que vamos a agregar sería el site HTML. Entonces vamos a ir de nuevo a la API de Spring y vamos a modificar este campo acá. Vamos a colocar el site de swagger-ui.html. El siguiente que tenemos que agregar sería, vamos a ir a la API nuevamente. En la API tenemos que colocar la versión 3 de API doc y todas las extensiones.

[09:28] Ahora vamos a volvernos a la API, colocar la versión 3 y vamos a colocar el patrón Regex, indicando que queremos tanto la página inicial, así como toda las sub direcciones que parten a partir de esta dirección. Y de igual forma lo vamos a hacer. Vamos a copiar esto acá y lo vamos a agregar las subdirecciones provenientes de la página swagger-ui.

[10:06] Y al realizar estas modificaciones, nosotros tenemos que ejecutar la aplicación nuevamente para garantizar que se hayan aplicado esos cambios. Luego de que haya cargado, vamos a entrar el servidor, el servidor de Google y revisar que tengamos acceso a esos nuevos sitios.

[10:33] Ya con nuestra aplicación cargada y corriendo en el puerto 8080, nosotros vamos a ir al servidor de Google. Vamos a duplicar esa pestaña y vamos a copiar este site. Acabamos a entrar a Localhost:8080, y vamos a ir a api-docs. Entonces nos encontramos con un archivo del tipo JSON, probablemente nos encontremos con un archivo de esta forma.

[11:04] Si nos encontramos con un archivo de esta forma, vamos a ir a Google o al servidor en que se encuentren y vamos a colocar json beautifier. Tenemos que instalar la extensión. O sea, esta extensión nos va a permitir darle un formato a este archivo JSON.

[11:32] Luego de que se haya agregado esa extensión, vamos a actualizar acá y nos vamos a encontrar con el JSON de esta forma. Entonces en ese archivo JSON, nos vamos a encontrar todos los récords, todas las clases que nosotros estamos enviando dentro de la API de Postman, aquí vemos que nos indica el tipo que tenemos que pasar.

[11:53] Y también tenemos los endpoints, tanto para pacientes, médicos, el login del token, consultas, pacientes por ID, médicos por ID, el Hello World, tenemos el servidor donde está corriendo, que es el puerto 8080 o cualquier otro servidor que estemos ejecutando dentro de esa aplicación, informaciones extras de api-doc.

[12:16] También vamos ahora a entrar a la página de swagger que es una interfaz de usuario, acá vamos a colocar localhost y vamos a colocar esa extensión. Entonces nosotros estamos consiguiendo tener acceso a estas páginas, ya que nosotros en Spring Security, colocamos que podíamos tener acceso a todas las extensiones derivadas de swagger-ui.

[12:45] Entonces aquí vemos que tenemos una interfaz de usuario realizada en HTML donde vamos a encontrar todos los endpoints para los controladores que nosotros realizamos. Entonces vemos que tenemos el controlador de paciente, controlador de médico, la autenticación, consulta y el hello world.

[13:02] Entonces acá vemos, vamos a entrar en el último, el de consulta, que fue el último que realizamos. Entonces en el consulta yo tengo el tipo, tenemos el ID médico, ID paciente, el ID de la consulta, el ID del paciente, el ID del médico o la posible especialidad, y nos va a dar el valor que retorna en caso de ser exitoso y tenemos también el caso de consultas.

[13:32] Entonces vamos a obtener de mexico-controller por ejemplo vamos a tener la lista de médicos, o sea que nos indica cuál va a ser el formato que debemos pasar en el archivo de JSON y acá tenemos un botón que dice intentar. Dentro de ese botón nosotros vamos a eliminar la orden. Si vemos, él nos dice el formato en el que tenemos que escribir el orden que es ascendiente o descendientes y vamos a ejecutar esta aplicación.

[14:06] Entonces, en la respuesta, nosotros estamos recibiendo un mensaje de error. Tenemos que eliminar esta coma, vamos a ejecutarlo de nuevo. Entonces vamos a recibir un mensaje de error, que es el error 403, ya que nosotros no pasamos de token. Entonces vamos a ir a la autenticación en la parte de login.

[14:30] Vamos a colocar, vamos a intentar pasar los datos. Acá sería María, sería el usuario y la clave sería 123456. Él se encarga de hacer la encriptación formato decrypt, ejecutamos y vamos a tomar el token que vamos a encontrar en el cuerpo de la respuesta.

[14:49] Nos dio la información del tiempo que demoró realizando esa respuesta y otras informaciones adicionales. Nosotros podemos modificar este site dentro de nuestra API de Spring. Vamos a ir al controlador de paciente y nosotros ese token lo queremos colocar en alguna parte.

[15:14] Entonces, nosotros en el API de Postman, nosotros teníamos que colocábamos el token en una pestaña adicional que era donde pasamos el video. Ahora acá en esta interfaz, nosotros no tenemos algo similar para pasar el token que estamos recibiendo del login.

[15:34] Esa configuración la vamos a realizar en la siguiente parte y que nosotros podemos alterar toda nuestra interfaz para colocar más características, así como informaciones que nos permitan agregar seguridad a través del token.