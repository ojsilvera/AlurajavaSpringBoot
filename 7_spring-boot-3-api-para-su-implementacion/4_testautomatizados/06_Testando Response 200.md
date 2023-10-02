[00:00] Hola. Continuando con las pruebas para el controlador de las consultas, en la parte anterior nosotros probamos el estado 400 cuando los datos ingresados eran inválidos. Vimos que nosotros teníamos que hacer una simulación de la requisición para testar únicamente ese componente, obviando todos los componentes restantes, que serían el repositorio y los servicios donde realizábamos la validación.

[00:27] Ahora vamos a probar el caso 200, que es cuando nosotros enviamos un JSON y vamos a retornar un JOON a la aplicación que está haciendo la petición. Entonces, para eso vamos a copiar acá esta primera prueba y la descripción para este caso, debería retornar http 200 cuando los datos ingresados son válidos.

[00:57] Ahora esto va a ser el escenario 2 y gran parte de lo que nosotros estamos realizando acá se mantiene igual, nosotros vamos a enviar una respuesta, realizada por MockMvc, que es una simulación de lo que sería la consulta, la petición a través de una API externa.

[01:17] Vamos a performar, vamos a desempeñar un una petición del tipo post en la dirección “consultas” y tenemos que retornar una respuesta. Entonces, esta vez el estado esperado va a ser el estado 200, que es equivalente a OK. Solo que esta vez nosotros en el perform vamos a agregar algunos valores.

[01:45] Nosotros tenemos que agregar el contenido que vamos a enviar a la API que en el caso sería Postman. Entonces nosotros en la API de Postman nosotros enviamos un JSON. Entonces ese JSON, además de estar compuesto por los parámetros del detallamiento de consulta necesita algunos valores, como el encabezado, la fecha en la que se está realizando y el tipo de archivo que se está enviando.

[02:18] Entonces, para evitar eso, ahí tenemos una serie de herramientas que nos provee los métodos de perform donde nosotros podemos especificar el tipo, que el tipo sería MediaType, vamos a enviar una aplicación del tipo JSON. Existen otras aplicaciones, como del tipo XML o un formato de imagen.

[02:49] Entonces en este caso nosotros vamos a trabajar con las aplicaciones JSON. Caso de que ustedes quieran enviar una imagen, este formato tienes que cambiar ya que las imágenes están compuestas de bytecode, entonces la configuración en este caso sería diferente.

[03:08] Ahora, adicionen ya que se ha especificado cuál es el tipo del contenido, tenemos que especificar el contenido en sí. Entonces el contenido, ya mencionamos, que es un elemento del tipo JSON. Nosotros tenemos que enviar un elemento del tipo JSON que es DatosDetalleConsulta, donde nosotros tenemos una serie de parámetros.

[03:31] Esos parámetros serían el ID, el ID de paciente, el ID del médico y la fecha, entonces la fecha, recordando que la fecha que tenemos que colocar es una fecha con una hora de anticipación. Entonces, acá en la parte superior, vamos a colocar un parámetro llamado fecha, que va a ser del tipo LocalDate.now y vamos a colocar una hora después, haciendo la especificación de que la consulta que se va a realizar va a ser una hora después del momento actual.

[04:08] Entonces ya tenemos la fecha aquí, el momento en que se va a realizar la consulta. Ahora tenemos que especificar los parámetros que serían el ID, vamos a suponer un ID del número 2. El ID del médico sería 5 y la fecha sería la fecha que estamos creando como parámetro.

[04:30] Acabemos, que nos está generando un error y es porque este formato es un es un elemento del tipo OJO, que es un objeto de Java Object. Nosotros tenemos que convertir este objeto Java a un objeto del tipo JSON. Para eso nosotros vamos a inyectar dos atributos dentro de nuestra clase de prueba que se llaman JacksonTester.

[05:00] Primero va a ser del tipo de DatosAgendarConsulta y lo vamos a llamar agendarConsultaJacksonTester. ¿Qué es lo que hace este atributo? Esta clase toma un objeto que es del tipo Java y lo va a transformar en un objeto del tipo JSON.

[05:27] Entonces acá voy a inyectar esa propiedad con la anotación @Autowired y acá nosotros vamos a recibir un JSON también de respuesta, tenemos que hacer la transformación de JSON a un objeto del tipo Java. Entonces para eso voy a anotar JacksonTester solo que esta vez va a ser DatosDetalleConsulta y va a ser detalleConsultaJacksonTester.

[05:56] Vamos a inyectarlo con la anotación @Autowired, entonces ya vemos que esta clase se encarga de transformar un objeto del tipo Java a un tipo de JSON y viceversa, transforma también un objeto del tipo de JSON al tipo Java. Entonces acá vamos a copiar esto temporalmente y vamos a colocar agendarConsultaJacksonTester y dentro de él vamos a escribir ese objeto.

[06:31] Entonces, acá por último, vamos a decirle que queremos obtener el archivo JSON, aquí estamos teniendo un error. DatosDetalle y colocamos DatosDetalle, es DatosAgendar. DatosAgendarConsulta. Los parámetros para agendar consulta son el ID del paciente, que es el 2, el ID del médico y la especialidad.

[07:04] La especialidad sería, vamos a colocar la especialidad también en un parámetro. Sería var especialidad y vamos a colocar acá la clase de numerador Especialidad.CARDIOLOGIA. Ahora vamos a pasar ese parámetro, vamos a ver y tenemos que pasar la fecha y la especialidad.

[07:34] Entonces, ya con eso le indicamos a JacksonTester que escriba un elemento del tipo DatosAgendarConsulta y que obtenga el JSON que es el que se va a enviar dentro de la respuesta, dentro de la aplicación simulada para obtener una respuesta. Entonces ya tenemos la primera prueba realizada que es la prueba donde le indicamos cuál es el estado que queremos obtener.

[08:01] También tenemos que indicarle cuál va a ser el JSON esperado. Entonces vamos a crear un parámetro acá, vamos a llamar JsonEsperado y esta vez vamos a utilizar detalleConsultaJacksonTester donde vamos a escribir un elemento del tipo DatosDetalleConsulta, que es el record que nos retorna la clase.

[08:31] Entonces acá vamos a colocar los parámetros. Los parámetros que él requiere son el ID, el ID del paciente, el ID del médico y la fecha. Entonces aquí sería el ID del es nulo, el ID del paciente que es 2l, dos del tipo long, el ID del médico que es 5, la fecha. Eso es todo. Acá al final vamos a indicarle que queremos obtener el JSON.

[09:02] Entonces vamos a hacer, vamos a verificar ahora, a verificar que ese JsonEsperado, vamos a copiar acá, sea igual al que vamos a obtener en la respuesta. No. Acá vamos a obtener que la respuesta response, vamos a obtener el contenido de la respuesta como string que sea igual al JsonEsperado.

[09:47] ¿Entonces qué estamos describiendo acá? Estamos describiendo lo siguiente. Estamos enviando una fecha que va a ser una hora después de la hora actual en la que estamos realizando este procedimiento, estamos colocando el parámetro de la especialidad, estamos colocando la especialidad dentro de un parámetro y estamos generando una respuesta o una aplicación simulada.

[10:09] Entonces esa aplicación va a enviar los datos que se encuentran en un archivo del tipo DatosAgendarConsulta, que son transformados a través de JacksonTester. Él va a retornar una respuesta y vamos a validar esa respuesta con el primer assert, la primera verificación. Tenemos que verificar que esa respuesta sea igual al estado 200.

[10:33] Por último, tenemos que verificar el cuerpo del JSON que estamos retornando, para eso tenemos que escribir cuál es el cuerpo del JSON que deberíamos recibir. Sería JsonEsperado, y vamos a transformar ese elemento de tipo Java, un elemento del tipo JSON para poder compararlo con el JSON que estamos retornando en la respuesta de la aplicación simulada.

[10:59] Entonces vamos a ejecutar este test a ver cuál es el resultado. Ahora, una vez que ya ha cargado la segunda prueba realizada, nosotros nos encontramos con un error. Ese error indica que no fue encontrado el JacksonTester para esta prueba. Entonces nosotros tenemos que colocar una anotación adicional a la parte superior de la clase, que es la anotación @AutoConfigureJsonTesters.

[11:31] La anotación se encargará de hacer todas las configuraciones para esta clase de prueba relacionadas al parámetro JacksonTester que es el encargado de realizar esas transformaciones de elementos de tipo Java a tipo JSON. Ahora si ejecutamos nuevamente nuestra aplicación. Entonces, una vez que cargó este segundo intento de prueba, vemos que ya no entregó un error de compilación, sino que simplemente falló la prueba.

[12:00] Entonces vamos a ver qué indica. Acá indica lo siguiente, está diciendo que estábamos esperando un estado de 200, pero recibimos el estado 400, recordando que el estado 400 es que las informaciones que fueron pasadas son inválidas. ¿Por qué ocurre esto?

[12:17] Cuando nosotros estamos enviando el JSON dentro de nuestra aplicación simulada, él está realizando todo el proceso dentro de lo que sería la base de datos real, entonces nosotros estamos tomando este JSON y lo estamos enviando en la clase controlador, que es la que recibe los archivos de las API externas.

[12:39] De allí lo estamos enviando a la clase de servicio, que a su vez lo envía la clase de repositorio para hacer una búsqueda en la base de datos y guardarlo. Luego, por último, va a retornar los valores que nosotros deseamos, que en este caso serían los detalles de la consulta con el ID de esa consulta que fue agendada.

[13:03] Entonces, para eso nosotros tenemos que simular esa clase de servicio para indicarle a la aplicación que no tiene que hacer una búsqueda dentro de la base de datos real, sino le vamos a indicar directamente cuál va a ser el retorno.

[13:19] Entonces acá vamos a inyectar un nuevo parámetro, que va a ser AgendaDeConsultaService y lo vamos a anotar con la anotación @MockBean siendo referencia de que vamos a simular esa clase de servicio.

[13:37] Ahora, dentro de mi método de prueba voy a utilizar una comparación que es agendaDeConsultaService, y vamos a colocar una agenda. Entonces cuando se realice el asentamiento de esta consulta que sería esta de acá, DatosAgendarConsulta, acá podemos colocar esta o podemos colocar any, indicando que puede ser cualquier petición.

[14:13] Entonces, cuando enviemos cualquier petición o esta que estamos colocando acá, nosotros tenemos que retornar lo siguiente, tenemos que retornar DatosDetalleConsulta. Entonces ahora como estamos utilizando DatosDetalleConsulta, podríamos colocarla dentro de una variable que se llame datos y pasar acá simplemente el parámetro datos.

[14:47] Entonces, cuando se intente agendar cualquier JSON, nosotros vamos a retornar este parámetro. Entonces, acá vamos a reemplazar nuevo DatosDetalleConsulta por la variable datos. Vamos a intentar ejecutarlo de nuevo, para ver cuál es el resultado.

[15:11] Esta vez tenemos que las pruebas pasaron para el estado 200 entonces acá estamos recibiendo que afirmativamente la prueba pasó. Nosotros ya con esto finalizamos lo que serían las pruebas, está faltando únicamente la prueba 404. Recordando que el estado 404 es cuando nosotros hacemos una petición en la base de datos buscando un valor y esa página no se encuentra o no existe.

[15:41] Entonces, una forma de hacerlo es buscando alguna de esas consultas con el ID incorrecto que va a retornar el estado 404, entonces lo dejo como desafío. Acá también yo puedo ejecutar todas las pruebas. Nosotros teníamos que podíamos ejecutar las pruebas de forma individual, seleccionando el icono verde del lado del método o puedo ejecutar todas las pruebas, que es lo que vamos a hacer ahora, para ver que todas las pruebas estén pasando.

[16:12] Entonces, vemos acá que se están realizando las pruebas para los controladores y para los repositorios. También dejamos como desafío hacer las pruebas para las validaciones y pueden realizar todas las secuencias de pruebas para las otras consultas, las consultas simples.

[16:31] Entonces, mientras más pruebas tenga la aplicación, más estable y más confiable va a ser a la hora de hacer el deploy en el servidor. Entonces, en la siguiente parte vamos a ver cómo hacer ese deploy. Vamos a hablar de las variables de ambiente y de los diferentes perfiles con los que se está trabajando.