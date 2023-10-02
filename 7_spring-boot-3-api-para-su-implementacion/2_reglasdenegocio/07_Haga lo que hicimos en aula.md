Para cada validación de las reglas de negocio, crearemos una clase específica para cada una de ellas. La primera regla trata sobre el horario de la clínica: "El horario de funcionamiento de la clínica es de lunes a sábado, de 07:00 a 19:00". Si llega una solicitud a nuestra API con una fecha programada para una consulta, ¿qué sucede si el cliente intenta programar una consulta para un domingo? ¿O para un lunes a las 4 de la mañana? Por eso necesitamos validar el horario de la consulta. Crearemos una clase para realizar esta validación.

En el IntelliJ abriremos el menú lateral del proyecto y, para organizar esta clase, crearemos un subpaquete. Con la carpeta "consulta" seleccionada, presionamos la combinación de teclas "Alt + insert" y seleccionaremos la opción "Paquete". Crearemos un nuevo paquete llamado "validaciones".

Dentro del paquete "validaciones", crearemos las clases. Primero, crearemos una nueva clase llamada "HorarioDeFuncionamientoClinica". La idea es crear un método dentro de esta clase para realizar la validación del horario de funcionamiento de la clínica. Crearemos el método "validar()" y recibiremos el DTO "DatosAgendarConsulta" como parámetro.

public class HorarioDeFuncionamientoClinica{

   public void validar(DatosAgendarConsulta datos) {

       }

}COPIA EL CÓDIGO
Escribiremos var domingo igual a DayOfWeek.getDayOfWeek(), usaremos este método para obtener el día de la semana, y para verificar si es igual usaremos equals con el parámetro que indica el día de la semana que queremos comparar, en este caso el domingo, equals(DayOfWeek.SUNDAY). Esto nos devolverá un booleano, true si es domingo y false si no lo es.

public class HorarioDeFuncionamientoClinica{
   public void validar(DatosAgendarConsulta datos) {

var domingo = DayOfWeek.SUNDAY.equals(datos.fecha().getDayOfWeek());

     }
}COPIA EL CÓDIGO
Seguiremos la misma lógica, será un booleano. Crearemos una variable llamada "antesDeApertura", igual a "datos.fecha().getHour())" y verificaremos si es menor que 7:

var antesDeApertura=datos.fecha().getHour()<7;COPIA EL CÓDIGO
Realizaremos lo mismo para verificar si el horario es después del cierre. Crearemos una variable llamada "despuesDeCierre", igual a "datos.fecha().getHour()" y comprobaremos si es menor que las 18:00.

var despuesDeCierre=datos.fecha().getHour()>19;COPIA EL CÓDIGO
El horario de funcionamiento de la clínica es de 7h a 19h. No puede haber una consulta a las 19h, la última consulta debe ser a las 18h. Además, una de las reglas de negocio dice que "Las consultas tienen una duración de 1 hora".

A continuación, haremos un if. Si es domingo, antes de la apertura de la clínica o después del cierre de la clínica, lanzaremos una excepción para indicar que es inválido, throw new ValidationException("Consulta fuera del horario de funcionamiento de la clínica").

if(domingo || antesdDeApertura || despuesDeCierre){
   throw  new ValidationException("El horario de atención de la clínica es de lunes a sábado, de 07:00 a 19:00 horas");
}COPIA EL CÓDIGO
El codigo quedo asi

public class HorarioDeFuncionamientoClinica{
   public void validar(DatosAgendarConsulta datos) {

       var domingo = DayOfWeek.SUNDAY.equals(datos.fecha().getDayOfWeek());

       var antesdDeApertura=datos.fecha().getHour()<7;
       var despuesDeCierre=datos.fecha().getHour()>19;
       if(domingo || antesdDeApertura || despuesDeCierre){
           throw  new ValidationException("El horario de atención de la clínica es de lunes a sábado, de 07:00 a 19:00 horas");
       }
   }
}COPIA EL CÓDIGO
¡Listo! Tenemos nuestra primera validación. El único objetivo de esta clase es ejecutar esa única validación. El código queda pequeño, simple y fácil de dar mantenimiento y de probar de manera automatizada.

Ahora tenemos que hacer el código de las otras validaciones. La siguiente validación de la lista es "Las consultas tienen una duración fija de 1 hora". Esta no necesitamos verificar, ya será implícita, la aplicación estará disponible de una en una hora para agendar la consulta.

Siguiente validación: "Las consultas deben ser agendadas con un mínimo de 30 minutos de antelación". Vamos a crear un validador para esto. En nuestro proyecto, dentro del paquete de validaciones, vamos a insertar una nueva clase llamada HorarioDeAnticipacion.

Crearemos un método similar al que hicimos anteriormente.

public class HorarioDeAnticipacion{

   public void validar(DatosAgendarConsulta datos) {

   }
}COPIA EL CÓDIGO
Vamos a agregar las variables horaDeConsulta y ahora:

public void validar(DatosAgendarConsulta datos) {

   var ahora = LocalDateTime.now();
   var horaDeConsulta= datos.fecha();

}COPIA EL CÓDIGO
Ahora compararemos la diferencia en minutos entre esas fechas para lanzar una excepción en caso de que sea inferior a treinta.

Crearemos una variable llamada diferenciaDe30Minigual a Duration.between pasando como parámetro ahora y horaDeConsulta, seguido de .toMinutes() para obtener la duración en minutos.

public void validar(DatosAgendarConsulta datos) {
   var ahora = LocalDateTime.now();
   var horaDeConsulta= datos.fecha();

   var diferenciaDe30Min= Duration.between(ahora,horaDeConsulta).toMinutes()<30;

}COPIA EL CÓDIGO
Ahora solo queda hacer un if. Si diferenciaDe30Min es menor que 30, lanzaremos una excepción con el mensaje: "La consulta debe ser agendada con una antelación mínima de 30 minutos".

public void validar(DatosAgendarConsulta datos) {
   var ahora = LocalDateTime.now();
   var horaDeConsulta= datos.fecha();

   var diferenciaDe30Min= Duration.between(ahora,horaDeConsulta).toMinutes()<30;
   if(diferenciaDe30Min){
       throw new ValidationException("Las consultas deben programarse con al menos 30 minutos de anticipación");
   }
}COPIA EL CÓDIGO
En la clase MedicoActivo, la única diferencia es que usamos el Repositorio, que aún no se está inyectando, pronto hablaremos de eso. Estamos buscando solo el atributo activo del médico, filtrando por el ID. Y si el médico no tiene ID, lanza una excepción.

Se creó el método findAtivoByID. En este caso, no quiero cargar el objeto completo del médico solo para verificar si el atributo activo está en true. Entonces, podemos hacer una consulta personalizada trayendo solo un atributo único, select m.ativo.

Luego tenemos la clase MedicoConConsulta. Aquí también es necesario consultar la base de datos para verificar si hay una consulta con este médico en la misma fecha.

Hicimos una consulta usando el patrón de nomenclatura de SpringData: existsByMedicoIdAndFecha(idMedico, fecha).

El PacienteActivo se parece al ValidadorMedicoActivo.

Y tenemos la validación para que el paciente no tenga consulta en la misma fecha, PacienteSinConsulta. También consulta la base de datos para ver si hay una consulta para este paciente, colocando la fecha de inicio y la fecha de finalización de ese día, tomando la primera y la última hora del día.

Vamos a crear una interfaz en el proyecto. En el panel lateral, con el paquete de validaciones seleccionado, usaremos el atajo "Alt + Insert", elegiremos la opción "Java Class", la nombraremos como ValidadorDeConsultas y elegiremos la opción "Interface".

Una vez creada la interfaz, dentro de ella declararemos el método que las clases tienen en común, validar(DatosAgendarConsulta datos). No es necesario usar la palabra clave "public" ya que es implícito que todos los métodos de una interfaz son públicos.

public interface ValidadorDeConsultas {
   public void validar(DatosAgendarConsulta datos);
}COPIA EL CÓDIGO
Aquí no es necesario usar "public" porque es implícito que todos los métodos de una interfaz son públicos. Ahora, vamos a cambiar cada una de las clases para implementar esta interfaz. Empezando por la clase HorarioDeAnticipacion, vamos a agregar "implements ValidadorDeConsultas " en la firma de la clase, antes de abrir las llaves:

public class HorarioDeAnticipacion implements ValidadorDeConsultasCOPIA EL CÓDIGO
Haremos lo mismo con los otros validadores. Tenemos 6 validadores, haremos esto para cada una de las 6 clases.

De esta manera, podemos estandarizar el proyecto. Cada validador debe implementar esta interfaz ValidadorAgendamentoDeConsulta y, obligatoriamente, debe implementar el método validar(DatosAgendarConsulta). Solo el cuerpo del método de cada clase será diferente.

Otra cosa importante: para poder inyectar estas clases en algún lugar, Spring necesita conocerlas. Entonces, encima de ellas debe haber alguna anotación de Spring.

Podríamos poner la anotación @Service para indicar que es un servicio, una validación. Pero vamos a usar la anotación @Component que es para componentes genéricos. Porque a veces tenemos una clase que no es ni una clase de configuración, ni un controlador ni un servicio. Entonces podemos poner el @Component para indicarle a Spring que esta clase es un componente genérico y lo cargará en la inicialización del proyecto.

Podría ser el @Service también, pero dejaré el @Component para mostrar algo nuevo para ustedes.

Vamos a insertar @Component en todas las clases de validación.

@Component
public class HorarioDeAnticipacion implements ValidadorDeConsultasCOPIA EL CÓDIGO
Ahora, con el @Component el Spring reconocerá estas clases y podremos inyectar el repository.

Podemos colocar @Autowired en las clases que tienen el repository como atributo, para que el Spring inyecte el repository automáticamente. El MedicoActivo quedará así, por ejemplo:

@Service
public class MedicoActivo implements ValidadorDeConsultas{
   @Autowired
   private MedicoRepository repository;

}COPIA EL CÓDIGO
En la interfaz no es necesario colocar ninguna anotación porque el Spring la carga automáticamente.

Para inyectar estos validadores en la clase service, la clase AgendaDeConsultaService, usaremos un esquema del Spring que nos facilitará la vida.

Podrías pensar que necesitamos inyectar cada uno de los validadores de la misma manera que estamos inyectando los repositorios. Pero ese es el problema que queremos evitar, no queremos declararlos uno por uno. Así que haremos un truco que el Spring nos permite hacer.

En el código de AgendaDeConsultaService, declararemos un atributo, lo anotaremos con @Autowired, pero este atributo será declarado como una lista de java.util.List y, dentro de la lista, declararemos la interfaz ValidadorDeConsultas y llamaremos a este atributo validadores.

@Autowired
private PacienteRepository pacienteRepository;
@Autowired
private MedicoRepository medicoRepository;
@Autowired
private ConsultaRepository consultaRepository;
@Autowired
List<ValidadorDeConsultas> validadores;COPIA EL CÓDIGO
Spring va a identificar automáticamente que estamos inyectando una lista y buscará todas las clases que implementan la interfaz ValidadorDeConsultas. Así, no importa la cantidad de validadores, el Spring inyectará uno por uno. Es mucho más práctico hacerlo de esta manera.

Ahora, en el método agendar(), antes de crear las variables del paciente y del médico, vamos a obtener esta lista de validadores y recorrerla con un forEach(v -> v.validar(datos)).

if(datos.idMedico()!=null && !medicoRepository.existsById(datos.idMedico())){
   throw new ValidacionDeIntegridad("este id para el medico no fue encontrado");
}

validadores.forEach(v-> v.validar(datos));

var paciente = pacienteRepository.findById(datos.idPaciente()).get();

var medico = seleccionarMedico(datos);

if(medico==null){
   throw new ValidacionDeIntegridad("no existen medicos disponibles para este horario y especialidad");
}COPIA EL CÓDIGO
De esta forma logramos inyectar todos los validadores y el código está bastante flexible.

Si queremos excluir un validador, basta con eliminar la clase de ese validador que queremos eliminar. No es necesario modificar la clase AgendaDeConsultaService, la lista simplemente quedará con una clase menos.

Observe cómo el código se ha vuelto flexible. Si surgen nuevas validaciones, si cambiamos una validación o si una validación deja de existir, no necesitaremos modificar la clase de servicio.

Ya hemos implementado la funcionalidad de programación de citas utilizando la clase de servicio y los principios SOLID. Pero aún no hemos probado. Ahora es el momento de probar, vamos a usar Postman para averiguar si todo funciona como se espera. En Postman , vamos a enviar una solicitud para programar una cita.

POST http://localhost:8080/consultas
{
    "idPaciente": 1,
    "idMedico": 1,
    "fecha": "2023-10-10T10:00,
}COPIA EL CÓDIGO
Se produjo un error y apareció un mensaje diciendo que no se pudo conectar al servidor. Tal vez haya ocurrido algún problema en el proyecto y se haya detenido. Verifiquemos en la terminal "Run ApiApplication" del proyecto.

Está mostrando que hay alguna consulta con problem

from Medico m
where
m.id = :idCOPIA EL CÓDIGO
Verifiquemos los repositories para localizar ese error. Empezaremos por MedicoRepository.

La última consulta que hicimos fue la findAtivoById.

@Query ("""
    select m.activo
    from Medico m
    where
    m.id = :id
    """)
    Boolean findActivoById(Long id Medico);
}COPIA EL CÓDIGO
Fue hasta bueno que ocurriera este problema para mostrarles algo importante. Esta consulta tiene m.id = :id. Spring Data asume que :id es el parámetro que viene en el método.

Pero en mi método, el parámetro no está como id, lo dejé como idMedico. Este problema ocurrió porque el nombre del parámetro en la query no coincide con el nombre del parámetro en el método, y por eso se produce este error.

El nombre del parámetro debe ser id, como está en la query:

   @Query("""
            select m.activo
            from Medico m
            where
            m.id = :id
            """)
    Boolean findActivoById(Long id);
}COPIA EL CÓDIGO
Guardemos y verifiquemos el código del archivo PacienteRepository. También tiene el mismo problema, en el findAtivoById. En lugar de idPaciente, dejaremos solo id.

Corregiremos el mismo error en PacienteRepository. Guardaremos el proyecto y supervisaremos la reinicialización del proyecto en la pestaña "Run".

En principio, la aplicación se inició normalmente. Volvamos a Postman y disparemos nuevamente la solicitud para programar una consulta.

POST http://localhost:8080/consultas
{
    "idPaciente": 1,
    "idMedico": 1,
    "fecha": "2023-10-10T10:00,
}COPIA EL CÓDIGO
Fue devuelto un 403 Forbidden. Tal vez ocurrió alguna excepción, vamos verificar en la pestaña "Run ApiApplication".

Se produjo la siguiente excepción:

java.lang.RuntimeException: ¡Token JWT inválido o caducado!

Esto sucedió porque ya hace algún tiempo que se hizo el inicio de sesión. Creo que el token de inicio de sesión tiene una validez de aproximadamente dos horas. Vamos a iniciar sesión de nuevo. En Postman, haga clic en "Iniciar sesión" y disparemos la solicitud.

POST http://localhost:8080/login
{
    "login": "maria@voll.med",
    "senha": "123456",

}COPIA EL CÓDIGO
Mostró un nuevo token aleatorio, que vamos a copiar y pegar en la pestaña "Bearer" de la solicitud "Agendar Consultas". Vamos a borrar el token anterior y pegar este nuevo token en el campo "Token".

Luego vamos a enviar la solicitud para agendar una consulta, haciendo clic en "Send". Ahora ha devuelto un código de respuesta 200 OK, pero las informaciones son nulas.

{
    "id": null,
    "idMedico": null,
    "idPaciente": null,
    "fecha": null,
}
COPIA EL CÓDIGO
Esto está sucediendo porque no hemos cambiado el controlador. El controlador sigue con el return new pasando los parámetros como nulo. Vamos a abrir el paquete de controladores y vamos al ConsultaController para arreglar esto.

En el return del ResponseEntity estamos pasando new DatosDetalleConsulta, por lo que todo se está pasando como nulo. Ya no debemos pasar esta información nula, debemos recibir el objeto de programación que se creó.

En la clase AgendaDeConsultaService, el método agendar() es void. Vamos a quitar este void e insertar el objeto DatosDetalleConsulta. Y al final del método agendar() pondremos return new DatosDetalleConsulta() pasando como parámetro el objeto consulta.

public DatosDetalleConsulta agendar(DatosAgendarConsulta datos){

   if(!pacienteRepository.findById(datos.idPaciente()).isPresent()){
       throw new ValidacionDeIntegridad("este id para el paciente no fue encontrado");
   }

   if(datos.idMedico()!=null && !medicoRepository.existsById(datos.idMedico())){
       throw new ValidacionDeIntegridad("este id para el medico no fue encontrado");
   }

   validadores.forEach(v-> v.validar(datos));

   var paciente = pacienteRepository.findById(datos.idPaciente()).get();

   var medico = seleccionarMedico(datos);

   if(medico==null){
       throw new ValidacionDeIntegridad("no existen medicos disponibles para este horario y especialidad");
   }

   var consulta = new Consulta(medico,paciente,datos.fecha());

   consultaRepository.save(consulta);

   return new DatosDetalleConsulta(consulta);

}COPIA EL CÓDIGO
Va a dar un error en "consulta", porque todavía no existe ese constructor, vamos usar el atajo "Alt + Enter" para crear el constructor que recibe el objeto consulta y llamamos a this(consulta.getId(), consulta.getMedico().getId(), consulta.getPaciente().getId(), consulta.getFecha()):

public record DatosDetalleConsulta(Long id, Long idPaciente, Long idMedico, LocalDateTime fecha) {
   public DatosDetalleConsulta(Consulta consulta) {
       this(consulta.getId(),consulta.getPaciente().getId(),consulta.getMedico().getId(),consulta.getFecha());
   }
}
COPIA EL CÓDIGO
Ahora tenemos un DTO con los datos siendo devueltos correctamente.

En ConsultaController, el método agendar() devuelve el DTO. Vamos guardar el DTO en una variable y en ResponseEntity.ok pasaremos el DTO, que fue devuelto por la service.

@PostMapping
@Transactional
public ResponseEntity agendar(@RequestBody @Valid DatosAgendarConsulta datos) {
   var dto= service.agendar(datos);
   return ResponseEntity.ok(dto);
}COPIA EL CÓDIGO
En la peticion Agendar consulta, vamos a testar el envio de un paciente que no existe en la base de datos:

POST http://localhost:8080/consultas
{
    "idPaciente": 88888,
    "idMedico": 1,
    "fecha": "2023-10-10T10:00"
}
COPIA EL CÓDIGO
Al enviar la solicitud, devolvió el código 403 Forbidden. No debería devolver 403. Volviendo a la terminal de la IDE, podemos ver que está enviando la excepción ValidationException"Id do paciente informado no existe". Pero no está apareciendo para el usuario porque aún no hemos agregado esta validación en la clase que maneja las excepciones. Vamos a corregir eso.

En el paquete "errores", accedemos a la clase TratadorDeErrores y creamos un nuevo método para ValidationException:

@ExceptionHandler(ValidationException.class)
public ResponseEntity errorHandlerValidacionesDeNegocio(Exception e){
   return ResponseEntity.badRequest().body(e.getMessage());
}COPIA EL CÓDIGO
Entonces, si ocurre un error de regla de negocio, queremos devolver 400 Bad Request y en el cuerpo queremos enviar el mensaje de error, body(ex.getMessage()). Se ha realizado el tratamiento para la excepción.

En Postman, reenviemos la solicitud POST para programar una consulta para un paciente sin ID en nuestra base de datos

POST http://localhost:8080/consultas
{
    "idPaciente": 88888,
    "idMedico": 1,
    "fecha": "2023-10-10T10:00"
}
COPIA EL CÓDIGO
Ahora funcionó correctamente. Devolvió el código 400 Bad Request y en el cuerpo el mensaje "¡Id del paciente informado no existe!". Si pasamos un idMedico que no existe, muestra el mensaje "¡Id del médico informado no existe!".

Ahora podemos añadir un paciente que fue excluido, al enviar la solicitud muestra el mensaje "No se puede programar una consulta con un paciente excluido". Y si se inserta un médico que fue excluido, mostrará el mensaje "No se puede programar una consulta con un médico excluido".

Vamos a probar una regla más, podemos intentar programar una consulta un domingo o fuera del horario de atención. Mostrará el mensaje: "Consulta fuera del horario de atención de la clínica".

Al intentar pasar una consulta sin médico, sólo con la especialidad, se produjo un error. En la terminal de IntelliJ apareció el mensaje:

Column 'medico_id' no puede ser nulo trató de guardar una consulta con un médico que no existe. No debería haber intentado guardar la consulta en la base de datos. Vamos a verificar el código de la clase AgendaDeConsultaService.

Faltó un detalle importante en la lógica de elegir un médico aleatorio. Faltó una verificación. Estamos verificando si viene el id del médico. Si lo tiene, consultamos ese médico en la base de datos. Si no lo tiene, verificamos si se está eligiendo la especialidad y, si se está eligiendo, buscamos un médico que esté libre en esa fecha.

¿Pero qué pasa si no hay ningún médico libre en la fecha elegida? Falta ese escenario. En este caso, el return medicoRepository.seleccionarMedicoConEspecialidadEnFecha devolverá nulo.

Entonces, si esta consulta devuelve nulo, es porque no hay ningún médico libre en esa fecha y la consulta no puede realizarse.

En la línea en la que estamos eligiendo un médico, necesitamos insertar un if para insertar el mensaje "¡No hay médico disponible en esta fecha!".

var paciente = pacienteRepository.findById(datos.idPaciente()).get();

var medico = seleccionarMedico(datos);

if(medico==null){
   throw new ValidacionDeIntegridad("no existen médicos disponibles para este horario y especialidad");
}