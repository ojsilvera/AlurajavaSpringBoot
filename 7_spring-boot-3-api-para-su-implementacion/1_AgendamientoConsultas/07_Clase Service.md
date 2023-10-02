[00:00] En la parte anterior nosotros realizamos todo el esqueleto de las consultas, le hicimos el controlador, las entidades, los DTOs que nos permiten enviar y recibir información dentro de nuestra API, los repositorios y la migración donde creamos la consulta relacionándola con llaves extranjeras, con la tabla de médicos y pacientes.

[00:23] Como nosotros habíamos mostrado, es una especie de receta donde siempre vamos a tener todos esos elementos. Ahora, vamos continuando con las tarjetas de Trello, donde se encuentran los diferentes elementos del proyecto, nos vamos a encontrar con las validaciones, son un poco más complejas que las validaciones que ya venimos haciendo con bim validation, donde podemos colocar validaciones de campo obligatorio o un tipo de formato determinado.

[00:53] Ahora las validaciones tienen, están relacionadas con el tiempo de anticipación, la duración de la consulta, si los pacientes se encuentran inactivos, si se pueden permitir en el sistema o no que está relacionado con la exclusión de pacientes y nos puede permitir agenda de consultas con un médico que ya tenga un paciente en ese horario.

[01:19] Entonces, como vemos, estas validaciones son un poco más complejas y no las vamos a poder realizar con bim validation. Tenemos que implementar un servicio que realice todas esas condiciones. Entonces de vuelta en nuestra aplicación nos encontramos en la clase de ConsultasController. Y la finalidad de los controladores es gerenciar o administrar el flujo de información entre nuestra aplicación y las aplicaciones externas.

[01:42] Nosotros podríamos colocar dentro de este método agendar, podríamos colocar esas validaciones que van a ser realizadas, como por ejemplo que es el médico y datos médicos, el id médico es diferente de nulo y que haga alguna opción.

[02:03] Sin embargo, de esta forma nosotros estamos violando el principio de responsabilidad única ya que nosotros dentro de una clase que tiene como responsabilidad gerenciar flujo de información, estamos agregando una nueva responsabilidad que sería la responsabilidad de validación.

[02:20] Entonces esa validación la vamos a crear dentro de otra clase, sería una clase de servicio. Vamos a crear dentro del paquete consulta, vamos a llamarla agenda de consultas service. AgendaDeConsultaService para indicar que es un servicio.

[02:42] Como es un servicio, el servicio se tiene que encontrar disponible y tenemos que inyectarlo dentro de nuestro controlador. Recordando que para que una clase se encuentre disponible, nosotros lo podemos anotar con la anotación @Component o con alguna de sus anotaciones hijas, como serían @Service, @Repository o @Controller.

[03:10] Entonces, eso va a depender de la de la funcionalidad, de la finalidad que tenga esa clase. En este caso sería un servicio, entonces nosotros lo vamos a anotar con la anotación @Service, vamos a remover estas anotaciones de acá. Y vamos a crear un método a va a ser el método agendar.

[03:32] Va a ser del tipo público no va a retornar nada. La vamos a llamar agendar. Ese método va a recibir de DatosAgendarConsulta que era el record y el nombre de ese parámetro a se va a llamar datos también. ¿Entonces, qué es lo que yo quiero hacer en este nuevo método?

[03:59] Lo que yo quiero hacer es, al igual que nosotros hacíamos para MédicoController, es guardar la información que está llegando de donde la API externa, de la aplicación externa, entonces nosotros vamos a recibir esos datos y, a través del repositorio, vamos a guardar esa información en la base de datos.

[04:20] Entonces lo que yo tengo que hacer es inyectar un atributo, ConsultaRepository. Lo vamos a llamar ConsultaRepository también. Y recordando que para que Spring Boot sepa dónde inyectar el valor de ese repositorio, nosotros tenemos que colocar la anotación @Autowired.

[04:43] Si nosotros no colocamos esta anotación, el valor de este atributo va a ser simplemente nulo. Entonces, como nosotros no necesitamos que sea nulo, nosotros queremos que tenga los diferentes métodos que se encuentran en el repositorio, nosotros vamos a colocar la natación @Autowired para poder usar los diferentes métodos que se encuentran internos dentro de esa interface.

[05:07] Ahora sí, nosotros podemos usar el método de consultar el método save de la clase de ConsultaRepository que nos está solicitando una entidad. La entidad que nosotros tenemos que pasar acá es una entidad del tipo consulta. Entonces nosotros vamos a crear una variable, que se va a llamar consulta.

[05:27] Y acá sí podemos colocar la palabra nuevo Consulta donde vamos a pasar los diferentes valores, el id va a ser nulo, acá tengo que pasar una clase de médico. Lo que tengo que pasar la clase paciente y por último, datos.fecha. Entonces, de esa forma, yo puedo pasar acá la clase consulta.

[05:58] Ahora ya quiero inyectar este servicio dentro del controlador, para eso vamos a hacer lo mismo que hicimos con el repositorio, solo que lo vamos a hacer con el servicio, entonces vamos a colocar un atributo privado que se va a llamar AgendaDeConsultaService. El nombre de este parámetro se va a llamar servicio.

[06:21] Y lo vamos a anotar con la anotación @Autowired para que Spring framework sepa dónde debe inyectar esa clase que está siendo instanciada. Ahora yo sí puedo usar la clase de servicio y llamar el método agendar para pasarle los datos que estamos recibiendo de Postman con el id del médico, el id del paciente y la fecha en la que se realiza esa consulta.

[06:52] Ahora sí podemos realizar las diferentes validaciones, o podemos indicarle dónde van a ser las validaciones dentro de este nuevo método que va a ser un método de servicio. Sin embargo, yo estoy acá, instanciando un nuevo médico y un nuevo paciente.

[07:08] Yo tengo los valores de esos médicos y de ese paciente dentro de la base de datos. Por lo tanto, yo tengo que buscar ese paciente y ese médico utilizando los repositorios de médico y paciente. Entonces vamos a copiar este consultaRepository dos veces y vamos a reemplazar acá PacienteRepository.

[07:37] Le vamos a llamar paciente. Y acá se va a llamar MédicoRepository. De acá lo vamos a llamar, el valor de ese parámetro se va a llamar MédicoRepository. Ya tenemos inyectada nuestras clases de repositorio dentro de nuestro servicio, ahora sí podemos hacer una consulta en la base de datos a través de esos parámetros.

[08:08] Entonces vamos a crear una variable, que vamos a llamar la paciente y vamos a utilizar pacienteRepository y vamos a buscar find, vamos primero a buscar simplemente findById. FindById vamos a colocar el ID del paciente. Ya con eso tenemos una variable del tipo paciente. Si vamos acá, esa variable es del tipo optional.

[08:43] Para que esa variable sea del tipo paciente, yo tengo que aplicar el método get que se encuentra dentro del método findById. Ahora sí, yo estoy asignando un elemento del tipo paciente dentro de la variable paciente. Vamos a crear una nueva variable para médico, var medico. Y vamos a usar médicoRepository.findById.

[09:18] Acá coloco datos.idMédico. Y voy a tener el valor de la base de datos. Ahora sí, yo puedo pasar el paciente, voy a reemplazar este nuevo paciente que va a tener todos los valores nulos por este nuevo paciente que nosotros hemos solicitado en la base de datos y acá vamos a inyectar dentro del constructor el médico que estamos buscando en la base de datos, en el constructor de la consulta que tenía un médico con todos los valores nulos.

[09:54] Ahora nosotros sí podemos crear nuevas validaciones, acá nosotros simplemente estamos inyectando un paciente y un médico sin verificar si ese paciente o ese médico se encuentra activo. Más adelante vamos a ver cómo realizar esas validaciones, vamos a realizarlas en otras clases, pero hasta este momento tenemos nuestra clase de servicios funcionando.

[10:20] Y si nosotros ejecutamos nuestra aplicación nuevamente, vamos que él está cargando los valores, él va a cargar sin errores. No encontró ningún error a la hora de cargar los valores. Y ya tenemos separadas las responsabilidades para los servicios y para el flujo de información entre aplicaciones externas y la aplicación que estamos desarrollando.

[10:53] En la siguiente parte vamos a ver cómo crear esas validaciones para ajustarla a las necesidades del cliente que fueron marcadas en la tarjeta de Trello.