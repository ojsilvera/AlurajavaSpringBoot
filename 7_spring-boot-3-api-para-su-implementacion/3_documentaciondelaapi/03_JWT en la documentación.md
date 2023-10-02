[00:00] Hola. En la parte anterior nosotros intentamos oobtener acceso al listado de médicos, ingresando con el usuario María, nosotros obtuvimos el controlador. Nosotros utilizamos el endpoint de usuaria para la autenticación de usuario. Colocamos el usuario María y la contraseña, ejecutamos ese endpoint, copiamos el endpoint.

[00:30] Sin embargo, teníamos el problema que no teníamos dónde colocar ese token. Entonces, si vamos de vuelta a la documentación de Spring-doc, llegamos a la parte de beare, nosotros nos vamos a encontrar que para agregar una autorización en el encabezado de nuestras peticiones, tenemos que agregar un método del tipo vean, colocar la anotación bean para ejecutar ese método de forma automática dentro del contexto de Spring framework.

[01:01] Así como colocar la anotación de requerimientos de seguridad dentro de todos los controladores que vayan a tener acceso a ese token. Entonces, lo primero sería colocar, copiar ese método. Vamos a ir de vuelta a nuestra API y en la parte de infraestructura nosotros vamos a agregar un nuevo paquete que va a ser todo lo relacionado a la documentación.

[01:24] Ese paquete se va a llamar springdoc y dentro vamos a crear una nueva clase que va a tener ese bean. Entonces se va a llamar SpringDocConfigurations. Dentro de esta clase, nosotros vamos a agregar ese bean que estamos copiando.

[01:44] Y esta clase, al importar el bean nos va a retornar un elemento del tipo OpenAI, con un componente que va a recibir una llave de identificación llamado bearer-key, que es el que vamos a pasar a cada uno de nuestros controladores indicándole cuál va a ser el esquema de seguridad.

[02:04] El esquema de seguridad es del tipo bearer de Json Web Token. Si nosotros revisamos en el Postman, nosotros tenemos acá diferentes tipos de autorizaciones y la que nosotros estamos utilizando es bearer Json web token. Entonces, acá nosotros colocamos el token y luego de eso nosotros conseguimos hacer las consultas de los endpoints.

[02:34] Adicional, el método bean ejecuta de forma automática ese método, pero para que esta clase se encuentre en el contexto, tenemos que colocar la anotación @Configuration indicando que esta clase también va a ser autoinstanciada en el contexto de Spring framework.

[02:56] Entonces acá voy a colocar a otro vean que no va a retornar nada, va a retornar el elemento del tipo void y va a retornar simplemente un mensaje en consola, primero una línea colocando “bearer is working”.

[03:21] Ya tenemos el mensaje. Ahora en la documentación de Springdoc nos indica que otro de los elementos que tenemos que hacer es agregarle la anotación requerimientos de seguridad en cada uno de los controladores que van a solicitar ese token.

[03:37] Entonces vamos a ir a los controladores. En el controlador de autenticación, nosotros no lo necesitamos colocar, ya que nosotros le damos acceso a la autenticación a través de las configuraciones de seguridad. Entonces los controladores que necesitan acceso a ese token son las consultas, el controlador de médicos y el controlador de pacientes.

[04:03] Vamos a ejecutar esta aplicación nuevamente. Vamos a esperar que cargue la aplicación en el puerto 8080, vamos de nuevo al servidor. En el servidor vamos a ir a la interfaz de usuario, vamos a recargar esa interfaz y vamos a obtener el token nuevamente.

[04:22] Entonces vamos a seleccionar, acá try out. Vamos a colocar el usuario María y la clave 3456. Vamos a ejecutar copiando el token. Vemos que esta vez nosotros tenemos un campo que nos va a permitir colocar ese token de autorización, entonces acá nos indica que tenemos que colocar el valor.

[04:45] Y una vez que nosotros seleccionamos autorizar, ese valor va a quedar guardado dentro de la interfaz de usuario en cuanto se esté ejecutando la aplicación, nosotros cerramos, vamos a obtener el listado de pacientes, le damos a seleccionar acá try out. Y vamos a colocar acá ejecutar.

[05:09] ¿Qué estamos obteniendo? El listado de pacientes para un elemento del tamaño 1, vamos a colocar tres. Vamos a ejecutarlo nuevamente. Acá estoy obteniendo los tres primeros pacientes, pacientes con ID 1, el paciente con ID 5 y el paciente con ID 3. Nos está dando más informaciones.

[05:30] Si vamos al médico, nosotros también podemos obtener el listado de pacientes. Vamos a colocar try out. Si eliminamos acá, ejecutamos y estamos obteniendo una lista de tamaño 1 con el paciente. Si nosotros modificamos acá, vamos a colocar tamaño 4, estamos obteniendo los cuatro primeros pacientes.

[05:58] De esa forma, Spring nos indica cuál es el funcionamiento, nos dice acá que por ejemplo tenemos que colocar el ID para obtener el paciente. Ya sabemos que tenemos al paciente con ID número 1, vamos a ejecutarlo, tenemos el paciente y de la misma forma podemos crear nuevos pacientes, actualizar pacientes o eliminar un paciente ya existente, así como para los médicos.

[06:25] Entonces, repasando este es un elemento, nosotros podemos realizar otro tipo de configuraciones. Podríamos colocar mensajes, vamos a dejar como desafío qué otro tipo de configuraciones se pueden agregar dentro de esta interfaz, pero básicamente esto les permite utilizar una interfaz que se ajuste a las necesidades del cliente y se integre directamente con el proyecto.

[06:48] De esa forma, el cliente no tendría que instalar una API como Postman y podríamos colocar mensajes adicionales para el configurado que ya el cliente va a recibir una vez que él comience a ejecutar la aplicación.

[07:00] En la siguiente parte, nosotros vamos a ver todo lo que serían tests automatizados para nuestra aplicación y eso sería todo por la parte de documentación.