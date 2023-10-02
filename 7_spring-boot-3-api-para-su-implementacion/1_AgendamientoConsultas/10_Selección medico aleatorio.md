[00:00] Hola, en el video anterior nosotros comenzamos a construir lo que sería el cuerpo del método que nos va a permitir seleccionar un médico de forma aleatoria en la base de datos. Ahora en esta parte vamos a crear las validaciones para los datos, que nos van a permitir realizar el algoritmo dentro de la base de datos para seleccionar un médico.

[00:24] En Trello vamos a ver las reglas de negocio nuevamente y vemos que las condiciones que se deben cumplir para el médico es que no se pueden permitir programar citas con médicos inactivos, es decir, ese médico tiene que tener estatus activo y la elección del médico es opcional, entonces podemos recibir un valor de nulo.

[00:44] En caso de que no exista el ID, el sistema debe elegir de forma aleatoria un médico que se encuentre disponible en la fecha y hora ingresada. Sin embargo, cuando la persona ingresa el ID del médico, él ya está indicando cuál es el especialidad de ese médico que va a atender a ese paciente, esa persona sabe cuál es el médico que lo atiende es generalmente y va a indicarle el ID correcto.

[01:10] En caso de que no indiquen un ID, ¿cuál va a ser la regla con la que vamos a seleccionar a ese médico? Entonces nosotros vamos a encontrarnos con ese problema y una tenemos que consultar con el cliente o con quien realizó las instrucciones para agregar un nuevo valor que nos permite resolver esa dificultad.

[01:35] Entonces, una posible solución es indicar cuál va a ser la especialidad del médico, ya que no tendría mucha lógica indicarle al paciente que está yendo por un problema de piel, indicarle a un pediatra o un cardiólogo a un geriatra. Entonces nosotros tendríamos que asignar un dermatólogo y eso lo podríamos hacer a través de la especialidad.

[01:59] Entonces nosotros tenemos que pasar dentro de los parámetros la especialidad, una vez que se haya confirmado esa nueva modificación, nosotros vamos a ir a nuestro proyecto, y vamos a comenzar a realizar las validaciones. La primera validación es que el médico, el ID del médico no sea nulo. Si es diferente de nulo vamos a seleccionar de la base de datos con el repositorio el médico con ese ID.

[02:41] Entonces, datos.idMedico. Ya con eso vamos a retornar el ID del médico. En caso de que el ID sea nulo, nosotros tenemos que comenzar a trabajar con la especialidad, entonces acá estamos viendo que estamos utilizando el método getReferenceById, que es similar a existsById, un método que viene directamente del repositorio y acá nosotros utilizamos como alternativa del optional el get en el findById.

[03:15] Entonces es una forma de simplificar, lo hace más rápido, ya que está evitando llamarlo directamente del findById. Entonces, de vuelta en las validaciones, vamos a realizar la validación de la especialidad.

[03:31] Entonces, si los datos contienen la especialidad, ¿qué necesitamos que tenga la especialidad? Que sea igual a null, ya que si es igual a nulo, nosotros le vamos a enviar un mensaje de error, indicándole que la validación de integración que la especialidad debe seleccionar “debe seleccionarse una especialidad para el médico”.

[04:07] Entonces, vemos acá que nos está arrojando un error, ya que esa especialidad no se encuentra dentro del record, dentro del DTO que nosotros asignamos. Entonces para retomar lo que habíamos mencionado, si el ID es diferente de null, nosotros vamos a retornar un ID dentro de la base de datos que se ajuste con ese ID.

[04:28] En caso de que el ID sea nulo, tenemos que asegurarnos de que la especialidad no sea nula. Entonces, en caso de que esa especialidad sea nula, de que no haya asignado una especialidad, tenemos que mandarle un mensaje de error, una excepción diciéndole que le se debe seleccionar una especialidad para ese médico.

[04:53] Acá para corregir esto vamos a ir a datos, a agendar consulta y vamos a agregar la especialidad. Yo podría colocar not null acá, pero utilizando esta validación de bim validation yo no voy a conseguir enviar un mensaje para el cliente, entonces yo lo voy a dejar de esta forma para conseguir enviar a través del throw un mensaje de error.

[05:26] En caso de que la especialidad no sea nula ahí si vamos a conseguir realizar el algoritmo para enviar un médico de forma aleatoria, entonces ese algoritmo lo vamos a crear en el repositorio. Vamos a crear un método en la interface que se va a llamar seleccionarMedicoConEspecialidadEnFecha. ¿Cuáles son los parámetros que vamos a colocar?

[06:00] Vamos a enviar la especialidad que no es nula y tenemos que enviar la fecha de la consulta. Ese método no existe. Lo vamos a crear. Entonces vemos que ya ha creado nuestro método. Si nosotros lo dejamos de esta forma, el método no va a funcionar, ya que para que funcione tener que cumplir este patrón, tener que escribirse en inglés y luego de que se escriba findBy, luego del By tiene que indicarse el atributo que existe en este caso dentro de la clase médico.

[06:36] Entonces la clase médico podríamos colocar findById, findByActivo, findByEmail, o por cualquier otro de los parámetros o atributos dentro de la clase médico. Como esto es un poco más complejo, nosotros vamos a hacer uso de la anotación @Query en la que nosotros podemos escribir consultas en la base de datos.

[07:00] Entonces en el curso de JPA que también se encuentra en Alura nosotros hablamos bastante sobre las consultas en JPA que les va a abrir un poco la mente sobre cómo realizar esas consultas utilizando JPA y se relaciona bastante con lo que vamos a hacer ahora.

[07:18] Entonces, la forma de escribir esas consultas en la anotación @Query es tres comillas y cerramos con tres comillas. A partir de ahí, podemos comenzar a crear nuestra consulta. La consulta sería tenemos que seleccionar todos los elementos de la entidad médico con el parámetro m donde el atributo activo sea igual a 1.

[07:52] En caso de que sea 0, es falso, entonces nosotros vamos a colocar 1, ya que ese es el valor booleano de forma numérica. La siguiente condición que tiene que cumplirse es que la especialidad sea igual a la especialidad que estamos enviando del parámetro, entonces este valor de acá es el que vamos a asignar desde luego de los dos puntos, especialidad.

[08:28] Ya con eso estamos indicándole que seleccione todos los médicos que se encuentren disponibles, que se encuentren activos y que contengan esa especialidad. Para ordenarlos de forma aleatoria vamos a utilizar la palabra reservada order by rand. La palabra rand los ordena de forma aleatoria y la palabra limit one va a limitar a un único médico, entonces nosotros tenemos que retornar un único médico.

[08:57] Acá estamos dejando la fecha sin usar. Esa fecha la vamos a utilizar dentro de las condiciones. Entonces, ¿cómo le indicamos al proyecto que ese médico se va a encontrar dentro de ese intervalo de tiempo? Entonces el ID, voy a colocar acá, el ID que nosotros estemos seleccionando tiene que encontrarse, el ID de ese médico tiene que encontrarse disponible.

[09:26] Entonces todos los ID que tengan una fecha asignada no van a cumplir esa condición. Entonces vamos a colocar m.id no se encuentra, not in, y vamos a realizar una sub query o una sub consulta. Dentro de esa consulta vamos a retornar una tabla, de una única columna de la cual vamos a seleccionar el ID que no se encuentre en la condición que vamos a comenzar a escribir entonces.

[09:59] Entonces esa sub query o esa sub consulta va a ser la siguiente: select c.medico.id, nosotros tenemos que hacer una consulta con parámetros, vamos a seleccionar un único parámetro del médico, médico.id from Consulta con el parámetro c. Entonces tienen que notar que acá yo usé el parámetro m para la consulta exterior y acá dentro utilicé el parámetro c.

[10:40] Si yo acá, yo acá este parámetro puedo cambiarlo por cualquier letra o por cualquier nombre de la misma forma que hago con esta c. Lo importante es mantener la consistencia. Entonces seleccionar el ID dentro de la consulta, ¿entonces, cuáles son los parámetros de la consulta? Yo tengo el parámetro médico, los parámetros pacientes y los parámetros data que corresponden a la fecha.

[11:10] O sea, que vamos a colocar, seleccionar c.data=:fecha. Entonces el parámetro que nosotros contamos colocando acá en la búsqueda del ID tiene que ser igual a la fecha, entonces todos los médicos que corresponden a esa fecha es porque ya están asignados a un valor, entonces vamos a seleccionar todos aquellos que no se encuentren asignados.

[11:48] Entonces, todos los valores que se encuentran disponibles los va a seleccionar un médico que no se encuentra en ese valor y los va a ordenar de forma aleatoria. Si ya con eso queda elaborada nuestra consulta, que sería una consulta con una consulta interna.

[12:09] Ahora vamos a ir a la AgendaDeConsultaService, vemos que ya está funcionando, en la siguiente parte, nosotros vamos a crear las validaciones, las validaciones que corresponden a la tarjeta de Trello, que son estas validaciones más compleja que nos van a permitir darle más definición a las necesidades del proyecto.

[12:37] Ahora ya para finalizar vamos a subir nuestro proyecto al repositorio, para eso tenemos que descargar el software Git. Y una vez que lo hayan descargado van a seleccionar clic derecho dentro de la carpeta del proyecto. Van a seleccionar la opción Git Bash Here que va a abrir la consola donde vamos a inicializar nuestro repositorio local.

[12:56] Para inicializar ese repositorio local, vamos a colocar el comando git init. Como ven, inicialicé el repositorio localmente dentro de su computador. Nosotros vamos a subir este proyecto a un repositorio en la web. Entonces vamos a utilizar el comando git status para ver cuál es la siguiente acción.

[13:16] Ya nos indica que hay algunos archivos que deben ser commitados. Son los archivos relacionados al proyecto, y para eso vamos a listar los archivos que queremos commitar con el comando git add * y asterisco indicando que los queremos commitar todos.

[13:32] En el comando git status vamos a ver ahora cuál es la siguiente instrucción. Entonces dice que los cambios ya fueron actualizados y los que vamos a enviar al repositorio local son los que se encuentran en verde. Vamos a seleccionar git commit, vamos a invitarlo al repositorio local.

[13:53] Con el flag -m colocamos un mensaje para indicar primer commit. Luego que hayamos realizado en el primer commit vamos a conectar con el servidor remoto. Vamos a copiar el link y vamos a agregarlo el origen al servidor remoto. Seleccionamos enter y ahora tenemos que actualizar nuestra carpeta con los archivos que se encuentren dentro del repositorio. Pero

[14:31] Para eso vamos a utilizar el comando git pull, vamos a copiar la ruta donde se encuentran esos archivos y vamos a colocar la flag --allow-unrelated-histories, ya que van a haber algunos archivos como el README que no se encuentran dentro de esta carpeta.

[14:52] Seleccionamos enter y nos va a mostrar esta pantalla, donde vamos a colocar el mensaje del merge. No vamos a realizar ninguna modificación, vamos a colocar dos puntos wq. Ya se encuentran mergeados o combinado los archivos del repositorio externo con el repositorio local.

[15:17] Y ahora, por último, vamos a realizar un push de este repositorio en la web. Vamos a utilizar git push. Eso nos está indicando que tenemos que modificar ese comando git push –set-upstream origin master. Ya con eso queda actualizado nuestro repositorio localmente y en la web. Ahora de vuelta en nuestro proyecto, si vemos ha cambiado un poco la estructura de IntellyJ.

[16:03] Acá voy a tener una pestaña donde voy a poder ver los cambios que esté realizando. Acá voy a realizar un mensaje como primer cambio en intellij. Ahora vemos que tenemos algunos cambios. Vamos a seleccionar ese cambio que fue realizado y vamos a colocar un mensaje: commit from intellij.

[16:37] Vamos a seleccionar commit and push. Vamos a seleccionar nuevamente. Él nos indica cuál es el cambio que se está realizando. Y vamos a realizar el push en ese repositorio externo. Vamos a utilizar log in vía GitHub. Va a colocar. Y con eso ha sido actualizado nuestro proyecto.

[17:05] En la siguiente parte vamos a hablar sobre las validaciones y vamos a realizar las reglas de negocios un poco más complejas que se encuentran dentro de la tarjeta de Trello.