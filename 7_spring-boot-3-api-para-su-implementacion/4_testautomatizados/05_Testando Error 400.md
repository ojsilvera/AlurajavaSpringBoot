[00:00] Hola. En la parte anterior nosotros realizamos la prueba para el método de seleccionar médico en un cierto horario dentro del repositorio de médico y verificamos los dos posibles casos. El caso en el que el médico se encuentra ocupado con otro paciente y el caso en el que ese médico se encuentra disponible.

[00:20] Cuando el médico se encontraba en consulta con otro paciente, nosotros íbamos a retornar nulo. Y cuando el médico se encontraba disponible para esa especialidad y en ese horario, nosotros retornábamos el médico que fue algún médico aleatorio, que en el caso sería el único médico que teníamos registrado.

[00:41] Entonces vimos que las fases de una prueba son las siguientes, dado un conjunto de valores, cuando se realiza alguna acción, entonces tenemos que comparar que ese valor que estamos buscando en la base de datos efectivamente reciba el resultado de ese dato que en este caso sería nulo.

[01:10] Entonces, dado el conjunto de valores iniciales, la fecha, el médico registrado del paciente registrado y la consulta para esos dos cuando busquemos en el repositorio en la base de datos, cuando realicemos esa búsqueda, entonces vamos a verificar con el método de hacer, que nos permite realizar las pruebas unitarias con JUnit, vamos a verificar que esa búsqueda en el en la base de datos tenga un cierto valor que para este caso en este escenario sería nulo.

[01:41] Al igual que para el segundo caso, nosotros también, dado un conjunto de valores iniciales, cuando realizamos la búsqueda en la base de datos, nosotros verificamos que esa búsqueda era igual al médico, el único médico que teníamos registrado. Entonces hay dos formas de registrar ese médico.

[02:03] Nosotros en este caso registramos el médico mediante la construcción de métodos internos en la clase de prueba, nosotros también podríamos utilizar flyway para registrar tanto el paciente como el médico y la consulta y tenerlo interno dentro de la base de datos de prueba, recordando que el nombre de la base de datos de prueba se guía por vollmed_api_test, diferente de la base de datos vollmed_api.

[02:32] Y acá no puedo realizar esta modificación de este modo, ya que como yo comencé inicialmente con esta configuración, si yo altero las configuraciones de Wayfly tendría que ir a la base de datos y borrar los archivos y generarlos todos nuevamente. Entonces como yo comencé con esta configuración vamos a continuar con esa configuración sabiendo que podemos alterar estos valores para crear una base de datos de prueba.

[03:05] Entonces, ahora el siguiente componente que tenemos que probar serían los controladores, y para eso nosotros vamos a seleccionar la consulta, el controlador de las consultas, específicamente el método agendarConsulta. Entonces nosotros vamos a verificar que a la hora de recibir los valores de la petición, cuáles son los estados que estamos retornando y que los valores que nosotros estemos recibiendo de esa requisición sean correctos.

[03:35] Entonces para nosotros realizar esas pruebas vamos a hacer clic derecho dentro del controlador, vamos a ir a generar y vamos a seleccionar las pruebas, vamos acá a seleccionar el método de agendarConsulta y seleccionamos OK. Crea automáticamente el método.

[03:54] En la parte interior nosotros habíamos trabajado con @DataJpaTest, que es la anotación, que nos permite trabajar con accesos a la base de datos y consultas. Acá vamos a trabajar con @SpringBootTest que es una anotación que nos permite trabajar con todos los componentes dentro del contexto de Spring, entonces acá nosotros podemos utilizar repositorios, los servicios y los controladores.

[04:22] Ahora nosotros tenemos que verificar los diferentes estados de que nosotros podemos retornar cuando realizamos una petición.

[04:30] Entonces, cuando nosotros realizamos una requisición, tenemos el estado 400 en caso de que los valores sean inválidos, el estado 404 en el caso de que el usuario no haya sido encontrado, el estado 403 cuando la autorización no ha sido pasada que es cuando nosotros no pasamos el token y el estado 200, que es cuando el usuario ha sido encontrado exitosamente.

[04:54] Entonces yo voy a trabajar con el primer escenario, y para indicar cuál va a ser ese escenario voy a colocar acá escenario 1 y vamos a colocar la anotación @DisplayName una descripción de ese método. Entonces “Debería retornar estado http 400 cuando los datos ingresados sean inválidos”.

[05:31] Entonces hay dos estrategias para nosotros realizar las pruebas para este controlador, una donde nosotros inyectamos un servidor y realizamos una requisición de verdad dentro de la aplicación, para eso tendríamos que utilizar la anotación @RestAndPlay donde vamos a tener un servidor creando una petición en nuestra aplicación.

[05:55] El controlador va a recibir esa petición, va a realizar la búsqueda en el repositorio, va a realizar las validaciones con el componente de service y luego va a retornar el estado en caso de que sea encontrada o en caso de que los datos sean inválidos. Esa es una primera estrategia. La segunda estrategia es donde nosotros vamos a simular que se realizó la petición y nos vamos a enfocar únicamente en este componente, ignorando el resto de los componentes.

[06:28] Entonces nosotros vamos a simular esa petición, no vamos a crear un servidor sino que es vamos a simularlo y vamos a ignorar el restante de los componentes que serían los repositorios, los servicios o cualquier otro componente, y vamos a ver el Estado que retorna cuando realizamos la petición con esos datos.

[06:47] Entonces como nosotros vamos a hacer una simulación, vamos a hacer un mock, vamos a inyectar dentro de la clase de prueba el atributo MockMvc que lo vamos a llamar mvc. Para inyectarlo dentro de nuestra clase de prueba tenemos que recordar que hay que usar la anotación @Autowired y junto con esta, tenemos que colocar la anotación @AutoConfigureMockMvc.

[07:17] De esa forma, esta anotación se encarga de configurar todos los componentes necesarios para realizar una simulación de una petición para ese controlador. Ahora, lo siguiente que nosotros tenemos que hacer es utilizar ese MockMvc para realizar una petición, o sea, la petición que nosotros estamos probando es la petición del tipo post.

[07:44] Ahora la URL para ese post sería URL “consultas”. Vamos a ver la dirección de acceso, consultas. Y tenemos que retornar una respuesta. Entonces, si vemos acá, nosotros tenemos el dato que le estamos pasando, sería la ruta que sería post, un post consulta, vamos a realizar una petición del tipo post en la dirección consulta y tenemos que retornar cuando given, dado este valor, cuando generemos esa petición.

[08:31] Entonces, hacer, aquí vamos a colocar //then. Ese then va a ser un una verificación assertThat. ¿Entonces, qué es lo que necesitamos verificar? Tenemos que verificar que el estado, la respuesta que estamos recibiendo de esta requisición, de esta petición, sea el estado 400.

[09:02] Entonces acá yo tengo que guardar esta petición dentro de una variable que la voy a llamar response o respuesta. Acá aún me está generando un error, tenemos que importar los valores. Y el siguiente error es que nosotros, como nosotros estamos tratando las excepciones, tenemos que agregar un throw dentro de la firma de nuestro método.

[09:28] Agregamos un throw. De esa forma queda corregido el error, la excepción que se estaba presentando. Y ahora vamos a colocar, vamos a importar, vamos a verificar que ese response, vamos a obtener el estado y que sea igual, isEqual. Vamos a colocar getStatus. Vamos a importar acá.

[09:55] Tenemos que importar la librería y vamos a verificar que el estatus HttpStatus sea igual a BAD_REQUEST. Tenemos que obtener el valor y cerramos la verificación. Entonces acá vamos a colocar given, dados unos valores iniciales, y when. Nuestro when sería cuando se realiza la petición, entonces nosotros en esta parte estamos realizando esos dos primeros pasos.

[10:36] Vamos a dar los valores iniciales que sería cuál es el tipo de consulta que vamos a hacer, el tipo de requisición y cuál va a ser la ruta. Y cuándo sería cuando realicemos la petición. Entonces, en ese caso tenemos que confirmar que el estado de la respuesta sea igual al estado 400, que es BAD_REQUEST.

[11:00] Entonces vamos a ejecutar esta aplicación y ver qué obtenemos como retorno. Entonces, una vez que ya se cargaron los datos, vemos que el resultado esperado no, no fue el deseado. Nosotros estábamos esperando un estado 400. Esa prueba falló, acá cada indica, el símbolo amarillo indica que la prueba falló y dice que el estado esperado era el estado 400, pero recibimos el estado 403.

[11:36] Entonces, recordando que nosotros teníamos que enviar el token antes de realizar cualquier petición, entonces nosotros tenemos que también simular el envío de ese token dentro de nuestra petición. Entonces para eso nosotros vamos a utilizar la anotación @WithMockUser y tenemos que importar la librería.

[11:58] En este caso la librería no se encuentra, entonces cuando nosotros no encontramos la librería dentro de las dependencias podemos utilizar la herramienta de agregar la dependencia interna, queremos una herramienta que nos permite buscar dependencia de Maven o podemos simplemente ir a un navegador como Firefox o Google, buscar la dependencia para esa anotación, copiarla.

[12:24] En este caso yo ya tengo esa anotación copiada. Copié mis dependencias y las voy a colocar en el archivo pom, donde está el resto de las dependencias, vamos a actualizar mis dependencias acá, con esa nueva dependencia. Vamos a revisar en Maven que se haya cargado efectivamente, entonces acá tengo la nueva dependencia sprint security para la parte de prueba.

[12:51] Ahora, en mi clase de prueba para el controlador, yo voy a conseguir importar la clase @WithMockUser. Ahora vamos a ejecutar esa aplicación nuevamente, vemos que se modificó el resultado. Esta vez no fue un resultado inválido, nosotros tuvimos un resultado positivo para esa prueba. Los iconos se encuentran en verde indicando que el resultado esperado, que era el estado 400, nosotros recibimos el resultado esperado que fue el estado 400.

[13:31] Entonces, en la siguiente parte, nosotros vamos a probar lo que sería el estado 404, que es el caso en el que nosotros recibimos los valores, pero ese usuario o ese ese médico no se encuentra registrado dentro de la base de datos.