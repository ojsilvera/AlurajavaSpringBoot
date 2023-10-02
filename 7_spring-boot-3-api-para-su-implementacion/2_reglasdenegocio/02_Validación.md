[00:00] Entonces sí, nosotros necesitamos realizar una búsqueda en la base de datos, una búsqueda particular donde no vamos a traer todos los elementos del paciente, sino únicamente el parámetro activo, y el parámetro activo es buscando por el ID. Entonces vamos a realizar una consulta de la misma forma que lo hicimos para con el médico.

[00:26] Entonces, ahora sería acá findActivoById. Lo que voy a pasar acá sería el datos.idPaciente. Ahora, como ese método no existe, vamos a crear ese método dentro del pacienteRepository y vamos a crear una consulta. Esa query, de la misma forma que lo hicimos anteriormente, tenemos que tener tres comillas y vamos a seleccionar el parámetro activo from Paciente. Acá coloqué a m. Una p.

[01:19] Puede ser m también, pero vamos a colocar p, indicando que es de paciente. From Paciente where p.id= :idPaciente. Entonces, ya con esta consulta, nosotros vamos a estar recibiendo un parámetro booleano en pacienteActivo. Si pacienteActivo se encuentra activo, entonces nosotros podemos agendarlo.

[01:56] Entonces lo que nosotros queremos es que el paciente se encuentre inactivo para enviar un mensaje de error. Entonces si pacienteActivo es igual a falso, va a negar esa condición, enviamos un mensaje de error: throw new ValidationException. Vamos a enviar un mensaje. Entonces no se pueden permitir agenda. No permitir agenda, no se puede permitir agendar agendas citas con pacientes inactivos en el sistema. Perfecto.

[02:56] Para médicos se hace la misma variación. Lo voy a dejar como desafío para que ustedes lo hagan. Sin embargo, en el siguiente video ahí ya van a encontrar esa validación realizada. Sería bastante bueno que se desafíen a sí mismos para realizar esa validación y pensar un poco.

[03:17] Los va a ayudar bastante en su proceso de formación. La siguiente validación que vamos a hacer es que no se pueden permitir más consultas para pacientes en el día. Entonces, a esa nueva clase la vamos a llamar paciente sin consulta. PacienteSinConsulta. Entonces, para eso nosotros tenemos que verificar que ese paciente exista dentro del intervalo. En caso de que exista nosotros vamos a enviar un mensaje de error.

[04:02] Entonces lo primero que tenemos que hacer es crear nuestro método public void validar. Va a recibir los datos de la consulta. Vamos a crear nuestro método. Vamos a crear dos variables, uno que va a cumplir con el primer horario, indicando que el primer horario en el que ese paciente pueda asignar una nueva consulta, vamos a colocar acá primer horario. Para eso vamos a utilizar la fecha y vamos a modificarla al horario de las 7:00 de la mañana.

[04:51] Entonces sí, independientemente de la fecha que estemos recibido acá vamos a modificar a las 7:00 y vamos a ver el último horario, el último horario como la duración es de una hora, como último horario entonces de datos.fecha, tenemos que asignar esa fecha, datos withHour sería 18 horas.

[05:24] Entonces, ya con eso tenemos la fecha en la que el paciente puede asignar la consulta. Vamos a verificar pacienteConConsulta. Entonces, para eso yo necesito verificar si existe un id para ese paciente en la base de datos, con una fecha entre ese intervalo que sería las 7:00 y las 18:00 de la tarde. Entonces, para eso ya necesitamos inyectar el repositorio ya que voy a hacer una consulta, vamos a hacer private PacienteRepository y lo vamos a llamar repository.

[06:23] Entonces voy a utilizar el repositorio. Y acabo de utilizar el método existBy. Vamos a consultar. ¿Entonces, acá dónde tenemos que consultar? Aquí no tenemos que consultar en el repositorio de paciente. Acá tenemos que consultar en el repositorio de las consultas. Si existe una agenda ya para ese día con el id de ese paciente, dentro de ese intervalo, entonces nosotros no podemos permitir que se realice la consulta. Entonces acá vamos a modificarlo.

[07:00] ConsultaRepository. También se va a llamar Repository. ¿Entonces, qué es lo que vamos a verificar? Vamos a utilizar el patrón donde escribimos la consulta en inglés y dejamos a sprint realizar nuestra consulta SQL de forma automática. ¿Entonces qué vamos a colocar? existByPaciente ya que el parámetro que existe dentro de consulta es pacienteId. PacienteIdAndFechaBetween, y pasamos los parámetros.

[07:56] ¿Entonces, qué parámetros tenemos que indicar? Tenemos que indicar los datos, el idPaciente. La fecha de 7:00 horas, que sería primer horario y la última hora, el último horario. Entonces, si existe un paciente dentro del repositorio de consultas, si existe una agenda dentro del repositorio de consultas, nosotros tenemos que enviar un mensaje de error.

[08:28] Entonces acá vamos a colocar if(pacienteConsulta) es true, nosotros también vamos a enviar un error. Throw new ValidationException enviando un mensaje de error. Entonces acá este método no existe en el repositorio, tenemos que crearlo. Vamos a crear ese método en el repositorio de consulta.

[08:54] Y vemos que él está retornando void, es el método de tener que retornar un booleano. Y los parámetros de ese método, de la interface serían el ID del paciente, la fecha del primer horario y la fecha del último horario. Entonces vamos a verificar que en consulta nosotros estamos usando paciente_id y estamos utilizando datos, acá estamos, acá tenemos que cambiarlo de fecha a dato.

[09:35] Entonces vamos a crearlo de nuevo, vamos a corregirlo acá en el ConsultaRepository. Acá sería dsto. Vamos a colocar dato. Se ha corregido el error. Ahora están faltando médico activo y paciente con fecha. Médico con otra consulta. Entonces, para el caso del médico, vamos a iniciar el médico, lo vamos a dar para que lo finalice.

[10:17] Entonces sería MédicoConConsulta. Nosotros tenemos que hacer de la misma forma que hicimos con PacienteSinConsulta. Entonces vamos a verificar, vamos a crear nuestro método público, voy a enviar un mensaje, voy a llamar validar DatosAgendarConsulta y acá hicimos en PacientesSinConsulta, nosotros tomamos el horario, creamos el método existsByPacienteIdAndDataBetween.

[11:08] En caso de que sea verdad, tenemos que enviar un mensaje de error que sería “el paciente ya tiene una consulta para ese día”. Entonces, acá en MedicoConConsulta hay que inyectar el repositorio. Sería private. Vamos a realizar una consulta. ConsultaRepository. Vamos a llamar repositorio y vamos a hacer ese chequeo dentro de nuestro método.

[11:57] Entonces tenemos que verificar una variable para MédicoConConsulta. Vamos a llamar en el repositorio, entonces sería existByMedicoIdAndData. Entonces acabamos de pasar datos, el id del médico. Y vamos a pasar de los datos la fecha. Vamos a crear este método que va a retornar también un booleano.

[13:03] Entonces ya tenemos existByMedicoIdAndData, damos id acá con MédicosConConsulta. Y de la misma forma que nosotros hicimos, tenemos que validar que ese ID no sea nulo. Entonces acá teníamos que hacer if(datos.idMedico)==null return, caso que no sea contrario sigue con el nulo.

[13:36] Si medicoConConsulta es true, nosotros estamos retornando ahora un booleano, vamos a enviar un mensaje de error: throw new ValidationException. Vamos enviar un mensaje de error indicando “este médico ya tiene una consulta en ese horario”. Nosotros estamos pasando la fecha en la que se va a realizar esa consulta.

[14:12] Va a verificar esa fecha dentro de su programa de consulta y si consigue conseguir el ID del médico, va a conseguir que encuentre otra fecha. En caso de que eso se cumple, es porque ese paciente, este médico está trabajando con otro paciente.

[14:28] Entonces tiene que retornar un mensaje de error. El único método que nos está faltando acá es el de MédicoActivo, lo vamos a dejar como desafío. Sin embargo, en el próximo video lo van a encontrar ya resuelto. Es igual que PacienteActivo, simplemente vamos a cambiar los datos a MédicoActivo.

[14:53] Entonces. Intentan realizarlo sin ver el ejercicio, simplemente pensando, para que vean dónde se están equivocando y lo puedan desarrollar sus habilidades de pensamiento.