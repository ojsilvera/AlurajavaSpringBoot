[00:00] ¿Qué tal? Bienvenidos a su segunda clase de su curso de Spring Boot 3 desarrollando un API Rest. Hasta el momento hemos visto cómo crear un Hello World usando Spring MVC, ya creamos nuestro controller y podemos imprimir Hello world cuando llamamos al endpoint Hello.

[00:16] Desde ahora ya vamos a comenzar de por sí a desarrollar digamos un proyecto más profesional. El Hello world fue solo para validar la idea y aprender más o menos cómo generar el proyecto Sprin, cómo hacer un setup lo más básico posible para usar MVC, y ahora vamos a ver algo cercano a lo que se podrían encontrar en el mundo laboral.

[00:35] Por ejemplo, normalmente ustedes han encontrado con una UI. El equipo desarrollo de UX van a crear una UI y les van a decir: “Bueno, necesitamos este formulario de registro de médico”, por ejemplo. Entonces para esto aquí hay dos frentes.

[00:53] El primero es el front end, que ya dijimos que no lo vamos a abarcar por el momento, y el segundo sería el back end, que es lo que estamos haciendo ahorita en el API. Y la idea ahora es hacer la comunicación entre el front end, que sería través de esta pantalla que ven aquí del nuevo perfil del médico, cómo enviar los datos que nosotros pongamos en este formulario hacia nuestro API, hacia el back end. Y eso es lo que vamos a descubrir ahora.

[01:20] Nuevamente, como no vamos a realizar una aplicación front end en este caso, vamos a usar Insomnia, que es una herramienta similar a Postman, para los que son familiarizados con Postman, para simular los requests que nuestro cliente de front end podría realizar a nuestro API.

[01:39] Entonces lo que vamos a hacer ahora es abrir nuestro browser y buscar por insomnia.rest y vemos que eso es un framework, es una herramienta para testear API, específicamente lo que estamos haciendo nosotros ahora, desarrollado por Kong, que es una empresa americana, que desarrolla gateways y básicamente software.

[02:00] Vemos todas las funcionalidades que Insomnia puede tener aquí. Vemos que es ampliamente usado por Netflix, en Nasdaq, RedBull, por Facebook, entonces sí es una herramienta ya probada por el mercado, es una herramienta muy buena que tiene plugines open source, típico de la empresa Kong, y vemos aquí que también tiene algunos tutoriales, cómo puedes testear API.

[02:23] Sin más que decir, entonces vamos a instalar Insomnia en este computador y obviamente la versión gratuita, que es para nosotros, fines de estudiantes vamos a descargar y en unos minutos ya voy a tener instalado esto en mi computador. Ustedes también lo van a poder tener. Y bien, ya finalizamos la instalación aquí en mi computador.

[02:49] Si tengo un computador Windows, la instalación será diferente que aquí en mi caso que fue una Mac, y ya tenemos Insomnia abierto, aquí ya tenemos el programa instalado abierto. Entonces vamos a explorar un poco cómo es que funciona esto.

[03:03] Vemos que tenemos aquí bien similar, muy parecido a Postman, que tenemos para seleccionar el tipo de request que queremos hacer: get, post, put, patch, delete, options, entonces nada nuevo hasta ahí. Lo que vamos a hacer ahora es crear una nueva librería.

[03:21] Para esto Insomnia nos pide que registremos una organización, vamos a hacer este setup también en un segundo plano. Yo lo voy a hacer aquí y después vamos a iniciar propiamente con la creación, librería de requests. Pues bien, ya realicé el proceso de registro en Insomnia.

[04:10] Y ahora yo tengo ya un proyecto personal creado aquí. Lo que voy a hacer ahora es simplemente comenzar a configurar mi proyecto, por ejemplo, tengo aquí las configuraciones del proyecto, dice que mi proyecto personal, que es lo que yo estoy desarrollando ahora para este curso y voy a agregarle aquí lo que es un nuevo request.

[04:30] Para eso le voy a dar clic a button create, request collection y le voy a poner aquí voll med requests porque son los requests que yo voy a usar para hacer mis interacciones con Insomnia y API. Ya tengo aquí en mi libreta creada y lo que voy a hacer ahora es crear un nuevo HTTP request.

[04:54] Entonces voy aquí en nuevo, me crea aquí get new request, porque por defecto es un get y vamos a intentar probar un post contra nuestro API. Si recuerdan, el endpoint de nuestro API era http://localhost:8080/, y si queremos registrar un médico pónganle médico.

[05:22] Y como es un post tenemos que es el método post porque estamos enviando los datos. Si tú envías datos estás haciendo un post, si actualizas, un put, si obtienes, un get. Es lo básico de Rest. Para esto vamos a iniciar nuestro servidor porque no está iniciado, entonces salimos de aquí.

[05:40] Ejecutamos con el botón play, vemos que está haciendo el build, está iniciando la aplicación. Agrandamos esto un poco y ya está, la aplicación ya inició. Obviamente no hemos implementado este endpoint de médicos aún pero vamos a tener nuestro request ya listo, ya vamos a dispararlo aunque sea para ver que la conexión entre Insomnia y nuestro API sea exitosa.

[06:06] Entonces lo que voy a hacer ahora es en el body, hay una parte del body que es básicamente el cuerpo de nuestros requests. Recuerden que los postRequest incluyen una parte del cuerpo que puede ser en formato JSON, formato XML, texto, etcétera. Con esto lo incluimos dentro del request y podemos enviar los datos. Adivinen qué.

[06:27] Necesitamos enviar datos hacia nuestro back end. Son los datos de registro del médico. Entonces vamos a agregarle aquí un body y seleccionamos JSON aquí en la parte del body. Entonces, aquí podemos crear un objeto en JSON.

[06:46] Yo ya tengo uno aquí creado que son los datos del médico con los datos básicos que necesitamos: nombre, email, documento, especialidad, la dirección y bueno, dentro de la dirección tenemos también la calle, distrito, ciudad, número y complemento. Vamos a copiar esto y lo vamos a pegar aquí.

[07:07] Entonces ya tenemos nuestro JSON creado. Este es el cuerpo JSON que va a llegar o debería llegar a mi endpoint de médicos aquí en mi controller. Entonces si yo lo envío, vamos a ver que me da un 404 not found en el path médicos. ¿Qué quiere decir esto? En efecto me request no fue exitoso porque no lo encontró, pero la conexión entre mi cliente que es Insomnia y el API que estoy construyendo fue exitosa, solo que el path no está disponible aun porque obviamente no le hemos creado.

[07:45] Entonces ya sabemos cómo crear nuestro request en Insomnia. Yo aquí por fines didácticos lo que voy a hacer es renombrar esto a registrar médicos, porque rename request puede confundirse con otros requests que vamos a crear posteriormente.

[08:04] Entonces ya tenemos allí registrar médicos en este path que va a ser médicos, y con este que normalmente se llama payload. El body que enviamos normalmente de request post, se llama payload también. Se escribe payload pero se pronuncia payload. Es el término más común que ustedes van a encontrar en otras documentaciones, en otras cuentas.

[08:28] Entonces bien, por ahora ya finalizamos por este video, ya tenemos el setup de Insomnia, en el próximo video ya vamos a verlo desde el otro lado, desde el punto de vista del API, cómo vamos a recibir estos datos y qué es lo que vamos a hacer con ellos para que persista. Nos vemos.