[00:00] Hola, ya en la clase anterior, nosotros desarrollamos todo lo que serían los validadores que nos van a permitir registrar en la base de datos nuevas consultas que cumplan con las reglas de negocio de la clínica.

[00:12] Ahora nosotros tendríamos que instanciar en teoría cada una de esas clases, y pasar el parámetro datos al método validar que se encuentra dentro de la clase para poder validar, para realizar esas validaciones de las reglas de negocio.

[00:28] Pero de esa forma no es la forma más adecuada, no sería una buena forma, ya que a la hora de que nosotros tengamos que eliminar alguna de esas validaciones, porque ya no tiene sentido dentro del negocio, nosotros tendríamos que ir a eliminar esa clase, ese validador y luego venir a la clase de servicio, intervenir dentro de la clase de servicio y modificarlo, eliminando ese atributo, ese parámetro que estamos instanciando.

[01:03] Entonces nosotros vamos a mostrar acá un método que nos va a permitir seguir los principios solid, el pilar de polimorfismo que nos va a permitir adaptar una interface a múltiples finalidades, y va a dejar nuestro código con la mejor presentación posible.

[01:28] Entonces, si nosotros vemos cada uno de esos validadores, ellos tienen algo en común. La clase HorarioDeAnticipación tiene una firma que es pública, retorna un elemento del tipo void, o sea no retorna nada. El nombre es validar, y va a recibir como parámetro un elemento llamado datos del tipo DatosAgendarConsulta.

[01:51] Eso se cumple para HorarioDeFuncionamientoClinica. Se cumple para MedicoActivo. Tiene el método público, se llama validar, nos retorna nada y recibe un único parámetro. A pesar de que tiene un atributo, el método y la firma es la misma que la de las anteriores. MédicoConConsulta también cumple esa firma.

[02:16] PacienteActivo y PacienteSinConsulta. Entonces lo único que va a modificar es el atributo que se encuentra dentro de alguna de las clases. Pero existe una estrategia, un recurso que nosotros podemos implementar dentro de Java que son las interfaces, donde nosotros tenemos múltiples clases que implementan el mismo método con la misma firma, una misma funcionalidad.

[02:48] Nosotros podemos crear una interface para indicarle a los desarrolladores que eso va a hacer un patrón que se debe seguir. Entonces nosotros vamos a crear una clase, a hacer una interface y la vamos a llamar validador de consultas. Entonces, de esta forma, nosotros le indicamos a los desarrolladores que tienen que seguir un patrón que cumpla con esa firma.

[03:20] Entonces dentro de las interfaces nosotros vamos a colocar métodos abstractos. La interface es una clase abstracta que son métodos que no tienen cuerpo, simplemente sirven para indicar cuál va a ser la firma de los métodos que van a ser implementados dentro de las clases que implementen en esa interface.

[03:42] Entonces nosotros, ya como ya veríamos verificado la firma de cada una de esas clases es esta. Yo voy a copiar acá ese método y de la interface validadorDeConsultas y lo voy a copiar acá. Ya con eso tengo asignado el método que yo deseo implementar dentro de cada uno de esos validadores.

[04:09] Para yo conseguir implementar esta interface dentro de cada una de las clases voy a ir a cada uno de los validadores, voy a colocar la palabra implements y voy a colocar el validador de consulta. Entonces como vemos ya se está implementando el validador de consultas dentro de la interface, aquí voy a eliminar esto temporalmente.

[04:33] Si nosotros no colocamos el método, él automáticamente nos genera un error y nos dice que se tienen que implementar los métodos que se encuentran dentro de la interface.

[04:45] Como ese método ya estaba elaborado, simplemente voy a dejar el método con el cuerpo y así nosotros cumplimos con el pilar de polimorfismo que es uno de los pilares de Java de programación orientada a objetos que nos indica que nosotros podemos utilizar un mismo método, con diferentes funciones.

[05:10] Entonces, por ejemplo, en el horario de anticipación nosotros, el método de validarConsulta o validar verifica que la agenda de esa consulta sea 30 minutos antes. Pero dentro de la clase horario de funcionamiento de la clínica al yo implementar el validador de consulta, ahora ese método validar está proviniendo de la interface, él va a tener otra función, otra finalidad, que es verificar que la consulta no se esté realizando fuera del horario permitido.

[05:50] Entonces, nosotros vamos a hacer lo mismo con MédicoActivo, vamos a implementar la interface ValidadorDeConsultas, que se encuentra operativa. Entonces vemos como el polimorfismo va a adaptarse a cada una de las finalidades de la clase. MédicoConConsulta vamos a implementar ValidadorDeConsultas.

[06:21] En paciente activo también vamos a hacer lo mismo, implementar ValidadorDeConsultas, y por último, en PacienteSinConsulta. Entonces, a la hora de que una persona quiera ingresar un nuevo validador simplemente tendría que cumplir con esa norma, con ese patrón para crear la clase y va a implementar esa interfaz automáticamente la interfaz le va a indicar que tiene que implementar un método que va a ser el método validar.

[06:56] Entonces el polimorfismo se va a encargar de asignar la diferencia entre esa nueva clase y los validadores que ya se encuentran funcionando. Entonces, ahora nosotros tenemos que colocar una anotación de sprint que le va a indicar a nuestro proyecto que ya esa clase se encuentra operativa, de otra forma no es conocida dentro del proyecto.

[07:24] De esta forma, sin ninguna anotación, el proyecto no sabe que existe. Nosotros tendríamos que instanciarla dentro de la clase de servicios utilizando la palabra new HorarioDeAnticipación. Pero Spring nos permite utilizar las anotaciones. Esta no es una clase de controlador, tampoco es una clase de servicio, ni tampoco es un repositorio.

[07:46] Entonces nosotros habíamos mencionado que teníamos la clase component, es que es la clase de anotación raíz de la que derivan los servicios, los repositorios y los controladores. Entonces yo voy a anotar la clase pacienteSinConsulta como un componente y voy a inyectar el repositorio con la anotación @Autowired.

[08:10] Entonces, ahora Spring sabe que el repositorio de consulta se debe inyectar dentro de la clase de pacienteSinConsulta, y sabe que esta clase de pacienteSinConsulta se encuentra disponible donde quiera ser inyectada, que nosotros la vamos a inyectar dentro de la clase de servicio. Entonces vamos a colocar el resto de las anotaciones.

[08:30] Vamos a colocar @Autowired y la anotación @Component. En MédicoConConsulta también vamos a colocar la notación @Component para indicar que se encuentra disponible dentro de nuestro proyecto la anotación @Autowired de la consulta de MédicoConConsulta, entonces siempre que nosotros estemos tengamos que indicar dónde se va a inyectar una clase que está siendo auto instanciada por Spring, nosotros utilizamos la anotación @Autowired.

[09:05] Y cuando queramos auto instanciar una clase, nosotros tenemos que verificar cuál es la finalidad de esa clase, en este caso es un componente simple, podríamos utilizar la clase @Service y él ya funcionaría de la misma forma, ya que también de un cierto modo es un servicio, al realizar un servicio de validar consulta. Vamos a dejar esta clase acá como @Service.

[09:34] Voy a eliminar este espacio. Y voy a colocar el restante @Component. Acá también @Component. Entonces, de esta forma ya todas las clases se encuentran operativas dentro del proyecto. Tengo que ir a mi clase de servicio, e indicarle que yo quiero usar cada una de esas clases que ya se encuentran instancias dentro de la clase de servicio.

[10:02] Entonces, lo primero que se nos viene a la mente es asignar un atributo del tipo de horarioDeAnticipación y colocar la anotación @Autowired que sería privado, horarioDeAnticipación, colocar el nombre del atributo y colocar la anotación @Autowired.

[10:23] Ahí nosotros tendríamos que hacer eso con cada una de las clases y a la hora que nosotros deseemos modificarlo, tendríamos que eliminar el atributo y la clase. Entonces nuevamente estamos violando el principio de modificación de open close. Entonces, lo que nosotros vamos a crear es una especie similar al Design Pattern Strategy.

[10:50] Vamos a crear un atributo que Spring nos permite utilizar, que es nNosotros vamos a crear una lista que va a recibir un elemento del tipo ValidadorDeConsulta. Esa lista la vamos a llamar validadores. Entonces, de esta forma, nosotros simplemente tenemos una lista, una lista que está recibiendo una interfaz.

[11:22] Pero cuando yo coloco acá la anotación @Autowired, Spring automáticamente sabe que todos los elementos que estén implementando la interfaz ValidadorDeConsultas van a ser inyectados dentro de esta lista y van a encontrarse disponibles.

[11:41] De esa forma cuando se agreguen nuevas validaciones o se elimine alguna de esas validaciones, nosotros no tendríamos que intervenir dentro de la clase de servicio, sino simplemente eliminar esa clase y Spring automáticamente sabe que ya esa clase no existe dentro de la lista.

[12:02] Entonces, nosotros podríamos agregar 100 clases, eliminar 15 clases y no tendríamos que llevar un registro de cuáles clases tenemos que alterar dentro de mi clase de servicio. Entonces, ya esta clase se encuentra cerrada para modificación y nos permite crear extensiones para esos validadores.

[12:23] Otro principio que nosotros estamos creando es el principio de la S, de single responsabilty. Nosotros tenemos una única responsabilidad para la clase de servicio, que es revisar, recibir ese parámetro y realizar esa consulta y cada una de esas clases tiene una única función que es recibir el parámetro y validar.

[12:50] Esta clase que es la clase horarioDeFuncionamiento también tiene una única función, valida el HorarioDeFuncionamientoClínica. MedicoActivo chequea si ese médico se encuentra activo. Entonces nosotros estamos asignando una única responsabilidad para cada una de esas clases.

[13:12] Y el siguiente principio que nosotros estamos utilizando dentro de nuestro proyecto es el principio de inversión de dependencias, que nos indica que las clases, las clases de alto nivel tienen que depender de abstracciones o interfaces y no de clases de bajo nivel.

[13:32] Entonces para eso es importante saber que las clases de alto nivel son las clases que se encuentran directamente relacionadas con las reglas de negocio. Entonces esas clases que se encargan de buscar la consulta, que una clase que se encargue de guardar una consulta, de buscar alguna de las consultas o de asignar nuevas consultas por id, esas clases van a estar asociadas directamente con las reglas de negocio.

[14:00] Ahora las clases que estén asociadas van a hacer clases de alto nivel porque se encuentran relacionadas con las reglas de negocio. Y las clases que son de bajo nivel son clases que se encargan de realizar conexiones. Entonces nosotros no podemos colocar estas clases de alto nivel dependiendo de validación.

[14:20] Nosotros las tenemos que colocar que dependan de interfaces o abstracción. De esa forma nosotros a la hora de realizar una modificación, nosotros no tenemos que intervenir dentro de nuestra clase, sino eliminar, seleccionar cuál es el elemento que nosotros deseamos eliminar y modificar algún elemento dentro de la interfaz.

[14:52] Entonces, ya con eso, nosotros tenemos nuestro parámetro funcionando dentro de la clase de servicio, ahora simplemente tenemos que pasar los parámetros. Para pasarle ese parámetro, vamos a colocar el atributo validadores. Vamos a aplicar un forEach para recorrer todos los elementos que se encuentran dentro de esa lista.

[15:15] Entonces esa lista va a estar conformada por cada uno de los validadores que nosotros creamos y vamos a utilizar un arrow function para utilizar el método validar pasándole los datos que estamos recibiendo como parámetro.

[15:30] Entonces si vemos él automáticamente se encarga de enviar esos datos a cada uno de esos validadores y verificar si cumple con las condiciones deseadas para la clínica. Entonces, se cumplen los principios solid, estamos siguiendo el pilar de polimorfismo y ya creamos nuestra clase de servicio, que nos permite agendar un registro en la base de datos que cumple con las normas de HorarioDeAnticipación, HorarioDeFuncionamiento de la clínica o MedicoActivo, etcétera.

[16:10] Entonces solamente nos está faltando testar este proyecto hasta este punto. Lo vamos a hacer en la siguiente parte utilizando la API de Postman.