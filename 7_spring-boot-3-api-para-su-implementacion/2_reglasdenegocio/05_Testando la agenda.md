[00:00] Hola. En la parte anterior, nosotros implementamos las validaciones dentro de la clase de servicio, ahora vamos a verificar que estén funcionando correctamente y posteriormente vamos a aprobar cada uno de los casos dentro de la API de Postman.

[00:14] Entonces, cuando nosotros realizamos la clase de servicio, hubo un pequeño error que cometí. Si nosotros analizamos detenidamente, nosotros estamos recibiendo los datos dentro de la clase de servicio en el método de agendar y la primera condición que nos encontramos es vamos a hacer una consulta en la base de datos para el paciente y en caso de que el ID para ese paciente se encuentre, nosotros vamos a enviar un mensaje de error.

[00:45] Entonces eso no es lo correcto. Lo correcto sería enviar un mensaje de error en caso de que no sea encontrado el ID. Para eso vamos a utilizar el signo de interrogación para negar esa condición. De la misma forma, con el repositorio de médicos, en caso de que exista el ID para ese médico, nosotros estamos arrojando una excepción y lo correcto es en caso de que no exista ese ID, enviar ese mensaje de error.

[01:14] Ya hemos corregido el primer error, ahora vamos a ejecutar la aplicación para ver dónde se encuentran los otros errores que hemos detectado en la aplicación. Al intentar ejecutar la aplicación, vemos que en la clase de repositorio de médicos el ID no fue encontrado. Si vamos al repositorio de médico, vemos que nosotros copiamos este método del repositorio de paciente.

[01:42] Lo correcto es podríamos haberlo copiado. El tema es que pasar el parámetro correcto que sería algo así como idMédico y tenemos que colocarlo en el lado derecho de la consulta. El lado izquierdo corresponde al atributo de la clase médica. Entonces, si acá colocamos algo como ids entonces tenemos que indicar que acá también tendría que tener la s.

[02:12] En este caso, vamos a dejarlo cómo está. De verdad vamos a ejecutar la aplicación nuevamente. Ahora nos encontramos que cuando estaba intentando realizar la consulta en el repositorio de consultas, se encontró que la propiedad existByPacienteId no existía.

[02:36] Entonces el JPA de Spring framework tiene su patrón de búsqueda en inglés y una simple letra puede representar un error a la hora de ejecutar nuestra aplicación, entonces lo correcto sería exists, con s, ByMedicoId. Entonces, si nosotros nos equivocamos con una letra, vamos a recibir un error a la hora de ejecutar nuestra aplicación.

[03:05] Entonces de la forma correcta, vamos a ir donde se encuentran aplicados estos métodos. Vamos a ir a la clase ConsultaRepository. Acá este se encuentra en MédicoConConsulta. Vamos a intentar ejecutar la aplicación nuevamente. Luego de haber ejecutado nuestra aplicación y estar corriendo exitosamente, vamos a ir a nuestra tarjeta de Trello para verificar cada uno de los casos de las reglas de negocio.

[03:42] Ya con la aplicación corriendo en el puerto 8080, vamos a verificar cada una de las reglas de negocio. Entonces las primeras reglas de negocio que tenemos que verificar es que el id del paciente y el del médico existan, también vamos a verificar que el horario en el que se está intentando realizar la consulta se encuentren dentro del intervalo de funcionamiento.

[04:03] Entonces, si intentamos realizar esa consulta, por ejemplo el día domingo, nos vamos a encontrar con un error o si lo intentamos realizar a las 6:00 de la mañana también debería arrojarnos un error. Vamos a intentar realizar consultas con pacientes inactivos, con médicos inactivos y con médicos que ya tengan un paciente para ese horario, así como pacientes que ya tengan una consulta asignada para ese día.

[04:31] Entonces vamos a ir a la aplicación de Postman. Vamos a comenzar a probar cada uno de esos casos. Vamos a ejecutar. Entonces nos encontramos con el estado 403. Es que nosotros no hemos enviado la autorización. Recordamos que tenemos que recibir primero el token, vamos a ir a la clase de login y vamos a enviar la clave.

[04:54] Entonces Spring hace la transformación de este número con encriptado decrypt y recibimos el token luego de haber procesado la información. Vamos a copiar ese token, vamos a ir a la requisición de consulta y en la requisición, vamos a ir a autorización, vamos a colocar el token y en el cuerpo vamos a intentar enviar estos valores nuevamente.

[05:24] Entonces no estamos recibiendo ningún error. Vamos a ir a la aplicación y tenemos el siguiente mensaje de error. El mensaje nos indica que el ID para el paciente no fue encontrado. Para nosotros recibir ese mensaje de error dentro de la API de Postman, tenemos que ir a la infra en el tratador de errores y vamos a copiar de acá esta última sección.

[05:54] Vamos a colocar error, un nombre para esta aplicación, errorHandlerValidacionesDeNegocio. El error que nosotros estamos recibiendo es la validación de integridad. Además de la validación de integridad, tenemos que colocarla, vamos a pasar como el atributo Exception. Vamos a eliminar esta línea y vamos a colocar la validación de integridad.

[06:36] ValidacióndeIntegridad. Acá tenemos que enviar el mensaje en el cuerpo de la aplicación y vamos a ejecutar esta aplicación nuevamente. La detenemos. Ya con la aplicación corriendo de nuevo en el puerto 8080, vamos a ir a la aplicación de Postman y vamos a intentar ejecutar la petición de nuevo.

[07:07] Entonces, vemos que estamos recibiendo “este id para el paciente no fue encontrado”. O sea, ya estamos tratando ese mensaje de error. Lo siguiente, vamos a colocar el ID número 1, vamos a colocar un médico que no existe. Nuevamente “el id para ese médico no fue encontrado”.

[07:28] Ahora vamos a colocar una consulta con el id de paciente número 1 y el id médico número 1. Entonces, nosotros estamos recibiendo aún ese primer mensaje que configuramos al inicio del curso donde estamos recibiendo el ID de pacientes todos nulos. Vamos a ir a la aplicación. Y dentro de la aplicación nosotros vamos a ir al controlador donde se encuentra ese retorno.

[08:06] Acá, nosotros vamos a asignar el retorno de ese servicio a una variable que sería response. El nombre de esa variable va a ser la respuesta que la vamos a enviar dentro del cuerpo del ResponseEntity. La vamos a llamar response. Ahora voy a ir a la clase de servicio AgendaDeConsultaService y tengo que asignarle un retorno a ese método.

[08:38] El retorno para ese método va a ser nuevo agenda, va a ser DatosDetalleConsulta. Y luego el detalle de la consulta va a ser esa consulta que estamos creando. Acá sería consulta. No tenemos un constructor dentro de la clase de consulta dentro del record consulta y vamos a crearlo, entonces tenemos que crear el constructor y dentro, vamos a colocar this y vamos a pasar cada uno de los parámetros.

[09:25] Entonces el primer parámetro sería consulta.getId. El siguiente, consulta.getPaciente. Vamos a obtener el ID para el paciente, también vamos a obtener el ID del médico. Y por último, la fecha en la que se realizó esta consulta. De esa forma, vamos a colocar punto y coma. Aquí tenemos que cambiar el retorno, "Ctrl + V". Vamos a cambiar el retorno de void a DetalleConsulta y ya tenemos el controlador enviando el mensaje con los datos de esa consulta.

[10:24] Vamos a ejecutarla de nuevo. Esa última consulta que nosotros realizamos con el ID de paciente número 1 y el ID del médico número 1 fue realizada exitosamente, ahora nosotros vamos a intentar realizar una consulta con el ID de paciente número 4, número 3, por ejemplo. Y el ID de México número 4.

[10:53] Vamos a enviar la petición. Y vemos que fue asignada una consulta con ID número 6, el ID de paciente 3 y la fecha en la que se realizó esta consulta. Ahora en las tarjetas de Trello vamos a comenzar a probar los casos de las reglas de negocio. Vamos a probar estos dos casos de acá. Son los casos más simples.

[11:17] El caso en el que tenemos un paciente inactivo y un médico inactivo. Entonces yo sé ya por referencia de que el paciente número 2 se encuentra inactivo. Entonces no estamos recibiendo un mensaje de error, vamos a ir a la aplicación a ver qué está sucediendo.

[11:39] Entonces, acá yo tengo lo siguiente. Ahora yo tengo que este médico ya tiene una consulta de horario, ¿pero por qué no estamos recibiendo un error para esa consulta? El error que nosotros tratamos en la parte anterior fue el error de validación de integridad y este error se llama ValidationException.

[12:07] Entonces yo tendría que crear otro método error que va a contener esa clase. Entonces voy a copiar esa clase que sería la ValidationException. Voy a pegarla acá y voy a importar esa clase. Acá tengo que cambiar errorHandlerValidaciones. Acá vamos a cambiar, dejar estas validaciones de negocio aquí, validaciones de integridad.

[12:46] Pero nuevamente con la aplicación corriendo en el puerto 8080 vamos a ir a la aplicación de Postman y vamos a intentar agendar una consulta con el médico, por ejemplo médico 3. Y el paciente que sabemos que se encuentra inactivo el número 2. hacemos una petición. Y sé que no se puede permitir agendar citas con pacientes inactivos.

[13:08] También sabemos que el médico con ID 5 se encuentra inactivo, entonces vamos a hacer una petición para hacer agendar esa consulta y sé que no se pueden permitir agendar citas con médicos inactivos. Ese médico se encuentra inactivo y el paciente de ID número 2 también se encuentra inactivo.

[13:30] Al inicio nosotros realizamos una consulta para el médico de ID 1 y el médico de ID número 4. Ambos médicos son de ortopedia. Ahora vamos a intentar realizar una consulta para el paciente con el ID 3 y el médico con ID número 1 a ver qué sucede. Ese médico ya tiene una consulta en ese horario y el médico 4 también tiene una consulta en ese horario.

[13:59] Entonces nosotros no vamos a llenar ese campo, y sé que el paciente ya tiene una consulta para ese día. Vamos a variar acá el paciente, vamos a colocar el paciente número 5. Entonces, debe seleccionarse una especialidad para ese médico. Podría colocar acá IdMedico y dejar el campo vacío. Entonces, de igual forma, dice que debe seleccionarse un ID para ese médico, una especialidad.

[14:35] Entonces vamos a colocar acá la especialidad, yo sé que para esos dos médicos que quería seleccionar eran del área de ortopedia, “especialidad: ORTOPEDIA”. Como yo estoy tratando esas especialidades con un enumerador, tengo que recordar pasar el nombre de la especialidad de la misma forma en que se encuentra en el numerador o dar un tratamiento para ignorarla si se encuentra en mayúsculas o minúsculas.

[15:12] Entonces acá voy a intentar realizar una consulta para ortopedia y para el ID número 5. No estamos recibiendo ningún mensaje, vamos a ir a la aplicación y ver qué está sucediendo. En la aplicación estamos recibiendo un mensaje de error. El mensaje de error indica que ese ID no puede ser null. ¿Entonces, qué es lo que estaba pasando?

[15:33] Nosotros estamos recibiendo los datos. El ID del paciente que tiene que encontrarse se encuentra, él continúa realiza las validaciones. Busca un paciente con ese ID. Como no tenía, el ID del médico se encontraba nulo, él intenta seleccionar un médico aleatorio, con los datos que fueron enviados, que sería la especialidad. Y como no encontró un médico disponible para ese horario, el médico, este valor de médico se encuentra nulo.

[16:13] Entonces nosotros tenemos que dar un tratamiento de error en caso de que ningún médico se encuentre disponible, que lo vamos a saber con el retorno de médico aleatorio que va a ser null. Entonces vamos a copiar de acá esta condición y luego de haber consultado si existe un médico aleatorio disponible nosotros vamos a modificar esta consulta y colocar: if(medico==null) nosotros vamos a enviar un error diciendo “no existen médicos disponibles para este horario y especialidad”.

[17:01] Vamos a ejecutar nuestra aplicación nuevamente. Ya con la aplicación corriendo vamos a ir a la aplicación de Postman y vamos a intentar realizar esta petición de nuevo. Vemos que no existen médicos disponibles para este horario y especialidad. Entonces podemos cambiar la especialidad de algunas de las especialidades disponibles.

[17:26] Vamos a revisar acá las especialidades. En las especialidades disponibles yo, vamos a revisar las especialidades? Vamos a intentar cardiología. En cardiología vamos a moverlo acá. Entonces vemos que conseguimos reagendar una consulta para el paciente número 5 en este horario, en la especialidad de cardiología.

[17:58] Vamos a intentar realizar otra consulta con otro médico en ese mismo día, ahora vamos a intentar con el paciente de ID número 5 y con pediatría. Entonces, vamos a intentar acá modificar por pediatría. Y dice que el paciente ya tiene una consulta para ese día.

[18:24] Entonces ya hemos probado el caso en el que no se permite programar más de una consulta el mismo día para el mismo paciente, cuando intentamos agendar una consulta de cardiología a pediatría. Tampoco podemos programar una cita para un médico que ya tiene otra cita programada en la misma fecha.

[18:49] Verificamos la regla en la que la opción del médico es aleatoria, verificamos también la regla del horario del intervalo de funcionamiento de la clínica y de que el ID exista enviar un mensaje de error. La validación de 30 minutos de anticipación por el horario en el que se está realizando este video no la vamos a poder realizar, vamos a dejarlo como ejercicio.

[19:17] Y también vamos a dejar como ejercicio la actividad de cancelamiento de consulta, entonces con las herramientas que ya hemos dado hasta este punto podemos realizar el caso en cancelamiento de consulta. Sin embargo, en la siguiente parte ustedes van a encontrar esta actividad ya resuelta.

[19:35] Sin embargo, recomendamos altamente que realicen ese desafío e intenten utilizar los métodos, los repositorios y el servicio que ya se colocó para aplicar el cancelamiento de consulta.