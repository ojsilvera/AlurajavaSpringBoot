Una de las pruebas que haremos es la de las interfaces Repository.

Necesitamos escribir una prueba automatizada y, en el caso de Java, la biblioteca estándar es JUnit. La primera acción lógica a tomar es agregar JUnit al proyecto como una dependencia.

Con IntelliJ abierto, abriremos el archivo "pom.xml". Si observamos las dependencias del proyecto, tenemos las de Spring Boot, Lombok, MySQL, Flyway, pero no JUnit. La verdad es que no necesitamos agregar esta dependencia porque ya está integrada en el proyecto.

En el primer curso, cuando creamos el proyecto en el sitio de Spring Initializr, automáticamente agregó la siguiente dependencia a nuestro proyecto:

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>COPIA EL CÓDIGO
Por lo tanto, sería interesante crear una prueba para nuestra interfaz MedicoRepository y escribir escenarios de prueba para este método seleccionarMedicoConEspecialidadEnFecha.

Haremos esto seleccionando el método deseado y utilizando el atajo "ALT + Insert". De las opciones que aparecen en la pantalla, seleccionaremos la opción "Test".

Se abrirá una nueva ventana. Allí, tendremos el nombre de la nueva clase de pruebas siguiendo el estándar de JUnit ("MedicoRepositoryTest"). IntelliJ ya insertará esta clase en el paquete "src > test > java", específico para clases de prueba automatizadas.

Justo debajo, la ventana pide que confirmemos el método que queremos probar (debajo de "Generate test methods for:"). Hacemos clic en el cuadro de diálogo junto al método seleccionarMedicoConEspecialidadEnFecha y seleccionamos el botón "OK".

Se ha creado nuestra clase de prueba. Al expandir el menú Project, verá que se creó la carpeta en "src > test > java > med.voll.api > domain medico".

Si ha explorado el proyecto del curso, habrá notado que, al crearlo con Spring Initializr, incluso crea una clase de ejemplo de pruebas automatizadas llamada "ApiApplicationTests". Podemos eliminarla, ya que no se utilizará.

Para probar una clase Repository, utilizaremos algunos recursos de Spring Boot destinados a pruebas automatizadas. Como queremos probar un Repository, necesitamos insertar la anotación @DataJpaTest en ella.

En nuestro caso, podemos solicitar que Spring no use la base de datos en memoria, sino la propia base de datos de la aplicación. Esto resultará en una prueba que sea lo más fiel posible a nuestro entorno. Usaremos esta opción. La desventaja es que la prueba será un poco más lenta, aunque más fidedigna.

Para usar este enfoque, necesitamos insertar la anotación @AutoConfigureTestDatabase(). Como parámetro, escribiremos replace = y presionaremos "CTRL + Espacio" para recibir sugerencias automáticas. Una de ellas es "Replace.NONE". Seleccionamos esto presionando "Enter" y veremos que el parámetro cambió a replace = AutoConfigureTestDatabase.Replace.NONE.

@DataJpaTest
@AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.NONE)
@ActiveProfiles("test")
class MedicoRepositoryTest {

   @Test
   void seleccionarMedicoConEspecialidadEnFechaEscenario1() {


   }

}COPIA EL CÓDIGO
Sin embargo, tendremos otro problema: nuestra base de datos ya tiene muchos registros registrados. Esto puede interferir en la prueba automatizada. Lo ideal es que usemos la misma base de datos (MySQL), pero con otra base de datos exclusiva para las pruebas.

Con esto, los datos que ya tenemos en el entorno de desarrollo no afectarán a los datos utilizados para las pruebas automatizadas.

Para realizar este cambio, accederemos a "src > main > java > resources > application.properties". Este es el archivo de propiedades de la aplicación que queremos usar en el entorno de desarrollo, pero queremos otra configuración para el entorno de pruebas.

Para ello, duplicaremos este archivo haciendo clic en "application.yml" y presionando el atajo "CTRL + C", seguido de "CTRL + V". Luego, renombraremos la copia a "application-test.properties".

Podemos tener varios archivos de propiedades y "-test" funciona como un perfil. Así, "application.yml" sigue siendo el archivo predeterminado y "application-test.yml" se utiliza solo para el entorno de pruebas.

Abriremos el archivo "-test" y eliminaremos todas las propiedades, excepto la primera, que corresponde a la URL de la base de datos. En ella, modificaremos solo el nombre de la base de datos. En lugar de ser "vollmed_api", será "vollmed_api_test".

spring:
 datasource:
   url: jdbc:mysql://localhost/vollmed_api_test?createDatabaseIfNotExist=true&serverTimezone=UTC
   username: root
   password: 2812COPIA EL CÓDIGO
Por ahora, no está compilando porque el método seleccionarMedicoConEspecialidadEnFecha() necesita dos parámetros: la especialidad y la fecha. Como especialidad, pasamos el parámetro Especialidad.CARDIOLOGIA.

En cuanto a la fecha, no podemos tomar la fecha actual como parámetro del método, ya que cada vez que se ejecute el test, tendremos un día diferente y, por lo tanto, el comportamiento del test también será diferente.

Por eso, crearemos una variable llamada proximoLunes10H. En la línea de arriba, definiremos esta variable como var proximoLunes10H= LocalDate.now().with(TemporalAdjusters.next(DayOfWeek.MONDAY)). Con esto, el próximo lunes se calcula en función de la fecha actual. Luego, pasamos la hora utilizando .atTime(10, 0), indicando que son las 10 de la mañana.

@Test
@DisplayName("deberia retornar nulo cuando el medico se encuentre en consulta con otro paciente en ese horario")
void seleccionarMedicoConEspecialidadEnFechaEscenario1() {

   var proximoLunes10H = LocalDate.now()
           .with(TemporalAdjusters.next(DayOfWeek.MONDAY))
           .atTime(10,0);

   var medicoLibre = medicoRepository.seleccionarMedicoConEspecialidadEnFecha(Especialidad.CARDIOLOGIA,proximoLunes10H);

   assertThat(medicoLibre).isNull();
}COPIA EL CÓDIGO
Podríamos ejecutar la prueba ahora, pero ¿qué pasa con la base de datos? Anteriormente, definimos que el banco utilizado será el mismo que el de la aplicación, pero con una base de datos específica para pruebas. Flyway ejecuta las migraciones y crea todas las tablas normalmente en la base de datos de prueba, pero esta está vacía.

Esta es otra desventaja de este tipo de prueba automatizada: toda la información que debe estar registrada previamente en la base de datos debe hacerse manualmente.

Por lo tanto, antes de llamar al método seleccionarMedicoConEspecialidadEnFecha(), necesitaremos registrar un médico, un paciente y una consulta en la base de datos, ya que son la información necesaria para este escenario.

// Trecho de código suprimido

var medico =
var paciente =
var consulta =

// Trecho de código suprimidoCOPIA EL CÓDIGO
Sin embargo, necesitamos un método para registrar cada una de estas informaciones (médico, paciente y consulta). Podríamos inyectar el pacienteRepository y el consultaRepository en la clase, pero también es posible utilizar otro enfoque: usar el Entity Manager de la propia JPA.

@Autowired
private TestEntityManager em;COPIA EL CÓDIGO
Crearemos un nuevo atributo anotado con @Autowired y usaremos el TestEntityManager, utilizado específicamente para pruebas automatizadas. A continuación, utilizaremos el Entity Manager para guardar el médico, el paciente y la consulta.

Una buena práctica es organizar el código de prueba con métodos privados. De esta manera, no dejamos el escenario de pruebas demasiado largo. Además, esta información deberá ser utilizada en otros escenarios de prueba. Por lo tanto, los métodos privados contienen información reutilizable.

private void registrarConsulta(Medico medico, Paciente paciente, LocalDateTime fecha) {
   em.persist(new Consulta(null, medico, paciente, fecha, null));
}

private Medico registrarMedico(String nombre, String email, String documento, Especialidad especialidad) {
   var medico = new Medico(datosMedico(nombre, email, documento, especialidad));
   em.persist(medico);
   return medico;
}

private Paciente registrarPaciente(String nombre, String email, String documento) {
   var paciente = new Paciente(datosPaciente(nombre, email, documento));
   em.persist(paciente);
   return paciente;
}

private DatosRegistroMedico datosMedico(String nombre, String email, String documento, Especialidad especialidad) {
   return new DatosRegistroMedico(
           nombre,
           email,
           "61999999999",
           documento,
           especialidad,
           datosDireccion()
   );
COPIA EL CÓDIGO
Por ahora, necesitamos un método para registrar cada una de estas informaciones (médico, paciente y consulta). Podríamos inyectar el pacienteRepository y el consultaRepository en la clase, pero también es posible utilizar otra aproximación: usar el Entity Manager de la propia JPA. Crearemos un nuevo atributo anotado con @Autowired y utilizaremos el TestEntityManager, utilizado específicamente para pruebas automatizadas. Después, utilizaremos el Entity Manager para guardar el médico, el paciente y la consulta.

Una buena práctica es organizar el código de prueba con métodos privados. De esta forma, no dejamos el escenario de pruebas demasiado largo. Además, esta información necesitará ser utilizada en otros escenarios de prueba. Por lo tanto, los métodos privados contienen información reutilizable.

Los métodos anteriores sirven para crear los DTOs que representan al médico, al paciente y la consulta, además de métodos para guardarlos en la base de datos usando el Entity Manager.

Volviendo al escenario de prueba, llamaremos a registrarMedico en la línea var medico=. Tendremos que pasar un nombre ("Medico"), un correo electrónico ("medico@voll.med"), un documento("123456") y la especialidad del médico (Especialidad.CARDIOLOGIA).

Haremos algo similar con el paciente: llamaremos al método registrarPaciente, con un nombre ("Paciente"), un correo electrónico (paciente@email.com) y un documento (00000000000).

Por último, llamaremos al método para registrar la consulta (registrarConsulta). Los parámetros son el médico y el paciente que acabamos de registrar. La fecha es el próximo lunes a las 10 de la mañana (proximoLunes10H).

var medico=registrarMedico("Jose","j@mail.com","123456",Especialidad.CARDIOLOGIA);
var paciente= registrarPaciente("antonio","a@mail.com","654321");
registrarConsulta(medico,paciente,proximoLunes10H);COPIA EL CÓDIGO
Con eso, hicimos las llamadas y registramos todo en la base de datos. No necesitamos guardar la consulta en una variable, así que podemos eliminar la línea var consulta = que estaba presente en el código anterior.

Observa por la Consola que se inicia el servidor y Spring. Además, la inserción del médico, paciente y consulta se realizó. A continuación, llamamos al método para hacer la consulta de un médico aleatorio disponible en ese horario y la prueba se realizó con éxito. Por lo tanto, esta consulta devuelve un número.

Un factor importante en las pruebas de Repositorio: todos los registros que insertamos se eliminarán al final de la ejecución del método para que un método de prueba no interfiera en los demás. Por lo tanto, cada método de prueba se ejecuta de manera aislada.

Este es el comportamiento estándar de Spring: al finalizar una prueba, hace el rollback automáticamente. Por lo tanto, cuando se ejecuta una nueva prueba, la base de datos se restablecerá a cero.

Una vez creado el primer escenario de prueba, es más fácil crear los demás. Ahora haremos el escenario "Debería devolver médico cuando esté disponible en la fecha". En este escenario, tenemos un médico registrado, pero está disponible para la consulta. Podemos mantener la misma fecha (proximoLunes10H).

Crearemos un médico en la base de datos. Sin embargo, no necesitamos registrar pacientes ni consultas. Podemos eliminar las dos líneas que se refieren a ellas.

Por otro lado, el assert de este escenario no debe ser nulo, en su lugar, reemplazamos el .isNull() por isEqualTo(medico), es decir, debe ser igual al médico registrado anteriormente.

El médico está registrado y se guardará en una variable. Cuando hagamos la consulta para elegir al médico disponible aleatoriamente, medicoLibre debe ser el resultado, ya que es el único disponible en la fecha.

@Test
@DisplayName("deberia retornar un medico cuando realice la consulta en la base de datos  en ese horario")
void seleccionarMedicoConEspecialidadEnFechaEscenario2() {

   //given
   var proximoLunes10H = LocalDate.now()
           .with(TemporalAdjusters.next(DayOfWeek.MONDAY))
           .atTime(10,0);

   var medico=registrarMedico("Jose","j@mail.com","123456",Especialidad.CARDIOLOGIA);

   //when
   var medicoLibre = medicoRepository.seleccionarMedicoConEspecialidadEnFecha(Especialidad.CARDIOLOGIA,proximoLunes10H);

   //then
   assertThat(medicoLibre).isEqualTo(medico);
}COPIA EL CÓDIGO
Recuerda que ya no estamos trabajando con un Repository, así que no vamos a utilizar la anotación @DataJpaTest, sino la anotación @SpringBootTest en la clase. Esta anotación se utiliza cuando queremos levantar el contexto completo de Spring para simular nuestra clase Controller.

import org.springframework.boot.test.context.SpringBootTest;

import static org.junit.jupiter.api.Assertions.*;

@SpringBootTest
class ConsultaControllerTest {

}COPIA EL CÓDIGO
Ahora, el esquema es el mismo que antes: queremos probar el método agendar(), así que comenzaremos creando un método de prueba: void agendarEscenario1(). Encima del método, colocamos la anotación @Test seguida de la anotación @DisplayName para describir mejor el escenario de prueba.

Nuestra API está usando Bean Validation, así que si llega una solicitud con datos inválidos, debe devolver el código 400. Queremos que este sea nuestro escenario de prueba, así que lo definimos en la anotación @DisplayName:

Hay varios escenarios de prueba posibles; lo que incluimos en el código a continuación será el primero de ellos.

// Trecho de código suprimido

@SpringBootTest
class ConsultaControllerTest {

    @Test
    @DisplayName("deberia retornar estado http 400 cuando los datos ingresados sean invalidos")
    void agendarEscenario1() {

    }

}COPIA EL CÓDIGO
Para poder simular una solicitud HTTP en el Controller cuando no hay una solicitud real, se utiliza la clase de Spring llamada MockMvc. Para hacer esto, declaramos un atributo llamado "mvc" y le añadimos la anotación "@Autowired". La clase MockMvc simula solicitudes HTTP utilizando el patrón MVC.

Para poder inyectar MockMvc en la clase ConsultaControllerTest, además de la anotación "@SpringBootTest" en la clase, necesitamos la anotación "@AutoConfigureMockMvc".

// Trecho de código suprimido

@SpringBootTest
@AutoConfigureMockMvc
class ConsultaControllerTest {

    @Autowired
    private MockMvc mvc;

    @Test
    @DisplayName("deberia retornar estado http 400 cuando los datos ingresados sean invalidos")
    void agendarEscenario1() {

    }

}COPIA EL CÓDIGO
Ahora, vamos a disparar la solicitud: simplemente utilizamos MockMvc y declaramos el método perform(). Este método realizará una solicitud a nuestra API.

Entre los paréntesis, tendremos varios métodos estáticos, como GET, POST, PUT, DELETE. Uno de los métodos que queremos llamar desde nuestro Controlador es agendar(), un método POST (@PostMapping). Entonces, llamamos al método estático POST en perform(), abrimos y cerramos paréntesis.

A continuación, queremos el retorno, ya que necesitamos guardar lo que se devolverá. Para ello, llamamos al método .andReturn() para obtener el retorno, seguido del método .getResponse(). Lo guardaremos en una variable llamada response.

La idea es llamar a response, porque necesitamos guardarlo en algún lugar.

Sin embargo, hubo un error de compilación. Al posicionar el cursor sobre el método perform(), vemos la advertencia de que hay una excepción no tratada.

Este método puede lanzar una excepción; como no queremos hacer su tratamiento, colocamos un throws en la firma del método. Con el cursor posicionado sobre perform(), pulsamos "Alt + Enter"; se sugerirá como primera opción "Agregar excepción a la firma del método".


// Trecho de código suprimido

    @Test
 @DisplayName("deberia retornar estado http 400 cuando los datos ingresados sean invalidos")

    void agendarEscenario1() throws Exception
{
       var response = mvc.perform(post(urlTemplate:"/consultas"))
            .andReturn().getResponse();

    }

}COPIA EL CÓDIGO
Ahora haremos la afirmación: vamos a verificar si el código de estado es 400, porque dispararemos la solicitud pero no llevamos ningún cuerpo en ella.

La solicitud no tiene ningún parámetro, pero recuerde que, en la solicitud de programar una cita, el médico es opcional, mientras que el paciente y la fecha son obligatorios.

Como no estamos proporcionando ni la ID ni la fecha, debería devolver "error 400". Primero haremos las aserciones para eso.

Después de disparar la solicitud, declararemos el método assertThat() e importaremos el estático de la misma manera que hicimos anteriormente, con el atajo "Alt + Enter". En este caso, seleccionamos la penúltima opción Assertions.assertThat, que proviene del paquete org.assertj.core.api.

Entre paréntesis, colocaremos response.getStatus() seguido de isEqualTo(), donde pasaremos 400. Para hacer esto, usaremos la clase de utilidad de Spring HttpStatus, del paquete org.springframework.http. Después de eso, agregamos la constante BAD_REQUEST seguida del método value().

{
       var response = mvc.perform(post(urlTemplate:"/consultas"))
            .andReturn().getResponse();
//then
assertThat(response.getStatus()).isEqualTo(HttpStatus.BAD_REQUEST.value());

    }COPIA EL CÓDIGO
De esta forma, será devuelto el código 400.

El bloque de código anterior es el método utilizado para probar el código 400: primero, se dispara una solicitud a la dirección "/consultas" mediante el método POST, sin llevar ningún cuerpo; a continuación, guardamos el resultado (.andReturn()) y el getResponse() en una variable y verificamos si el estado de la respuesta es 400, ya que en este escenario, este es el error que debe ocurrir.

Una vez finalizada nuestra prueba, podemos ejecutarla haciendo clic con el botón derecho en la clase ConsultaControllerTest y seleccionando la opción "Ejecutar". Observe que Spring levanta el servidor, pero no se dispara una solicitud real, sino una simulada.

En este caso, mi prueba falló: tenemos la información de que se esperaba el error 400, pero se devolvió el error 403.

org.opentest4j.AssertionFailedError:
expected: 400
 but was: 403
Expected :400
Actual   :403COPIA EL CÓDIGO
Esto sucede debido a Spring Security. Para hacer una reserva a través de la URL, necesitamos estar conectados y no lo hemos hecho en esta prueba.

Se puede argumentar lo siguiente: en esta prueba, no estamos probando seguridad, autenticación y autorización. Dicho esto, consideraremos que se ha iniciado sesión para probar la llamada a la API independientemente de si estamos o no conectados.

¿Cómo informar a Spring que se debe ignorar la autenticación?

Encima del método, además de las anotaciones @Test y @DisplayName, pondremos una tercera anotación de Spring: @WithMockUser.

 @Test
 @DisplayName("deberia retornar estado http 400 cuando los datos ingresados sean invalidos")
@WithMockUser

    void agendarEscenario1() throws Exception
{
       var response = mvc.perform(post("/consultas"))
            .andReturn().getResponse();
//then
assertThat(response.getStatus()).isEqualTo(HttpStatus.BAD_REQUEST.value());

    }

}COPIA EL CÓDIGO
Esta anotación sirve para indicarle a Spring que debe hacer una simulación de un usuario, considerando que estamos logueados al ejecutar el test, para hacer una llamada con autenticación. Si queremos llamar un método con autenticación, pero sin pasar el usuario, y hacer una prueba de seguridad, usamos esta anotación para que Spring simule el inicio de sesión. Después de hacer esto, guardamos y volvemos a ejecutar el test, y se devolverá el error 400.

En ConsultaControllerTest.java, donde ya tenemos el primer escenario @Test, simplemente tendremos que copiar y pegar para realizar las modificaciones de los siguientes escenarios.

Primero, renombraremos el método de programación para agendarEscenario2() y el contenido de @DisplayName() a "Debería devolver el código http 200 cuando la información es válida".

El assetThat() con response.getStatus() ya no será BAD_REQUEST, sino OK para devolver el código 200. Sin embargo, en este método necesitaremos enviar un JSON válido.

Para esto, el .perform() recibirá post() en el que pasaremos .content() para enviar el JSON. Podríamos escribirlo manualmente como una cadena, pero esto no es recomendable porque es muy trabajoso, o podríamos usar una clase de Spring para hacer la creación del JSON más fácil.

Antes de eso, tendremos que llamar a .contentType() para enviar la cabecera HTTP que indica que se están enviando datos en formato JSON. Esto se hacía automáticamente en Postman, pero aquí tendremos que hacerlo manualmente. Dentro de los parámetros, pasaremos como parámetro la clase MediaType de Spring que proviene del paquete org.springframework.http, seguida de .APPLICATION_JSON.

Inyectamos otra clase de utilidad además de MockMvc llamada private JacksonTester<> que tiene genéricos con el tipo de objeto con el que trabajará. En nuestro caso, deberá ser del mismo tipo DatosAgendarConsulta recibido en el método agendar() del ConsultaController.

Copiaremos esta clase y la añadiremos dentro de los genéricos de JacksonTester<>. Luego, llamaremos al atributo DatosAgendarConsulta.

Duplicaremos este atributo porque necesitaremos dos JSONs, el que llega a la API y el que se devuelve por ella. En este último, lo que llegará será el genérico DatosDetalleConsulta y el atributo será DatosDetalleConsulta.

//trecho de código suprimido

class ConsultaControllerTest {

 @Autowired
private MockMvc mvc;

@Autowired
private JacksonTester<DatosAgendarConsulta> agendarConsultaJacksonTester;

@Autowired
private JacksonTester<DatosDetalleConsulta> detalleConsultaJacksonTester;

//trecho de código suprimido

}COPIA EL CÓDIGO
En el archivo ConsultaController.java, podemos observar que el método agendar() recibe DatosAgendarConsulta pero devuelve otro dato, que es DatosDetalleConsulta. Por lo tanto, en nuestro test, debemos tener dos JacksonTester<> para simular el JSON de entrada y salida que se devuelve.

Volviendo a nuestro test, dentro de .content(), pasaremos DatosAgendarConsulta con .write() recibiendo el objeto new DatosAgendarConsulta, donde pasaremos la identificación de un médico y un paciente, como 2l y 5l por ejemplo. También necesitaremos pasar una fecha y la especialidad. Lo guardaremos en variables antes de response, donde var fecha será igual a LocalDateTime.now(). La fecha puede ser actual porque estamos llamando al controller directamente, por lo que no haremos validación, simplemente cambiaremos la hora con .plusHours(1) para agregar una hora más, dejando claro que es una fecha en el futuro. En una nueva línea siguiente, crearemos la var especialidad que será igual a Especialidad.CARDIOLOGIA, por ejemplo.

Al instanciar DatosAgendarConsulta, pasaremos los ids del médico, del paciente, la fecha y la especialidad. Sin embargo, no podemos pasar .write() directamente a .content() porque devuelve otro tipo de objeto. Por lo tanto, justo después de su paréntesis de cierre, llamaremos a .getJson() para convertirlo en una cadena JSON.

El objeto JacksonTester<> toma lo que pasamos como parámetro y lo convierte en JSON en formato de cadena sin necesidad de crearlo manualmente.

@Test
@DisplayName("deberia retornar estado http 200 cuando los datos ingresados son validos")
@WithMockUser
void agendarEscenario2() throws Exception {
   //given
   var fecha = LocalDateTime.now().plusHours(1);
   var especialidad = Especialidad.CARDIOLOGIA;
   var datos = new DatosDetalleConsulta(null,2l,5l,fecha);

   // when

   when(agendaDeConsultaService.agendar(any())).thenReturn(datos);

   var response = mvc.perform(post("/consultas")
           .contentType(MediaType.APPLICATION_JSON)
           .content(agendarConsultaJacksonTester.write(new DatosAgendarConsulta(2l,5l,fecha, especialidad)).getJson())
   ).andReturn().getResponse();

   //then
   assertThat(response.getStatus()).isEqualTo(HttpStatus.OK.value());

}COPIA EL CÓDIGO
Ya hemos hecho la solicitud, llevando la cabecera contentType() y el JSON creado por JacksonTester<>.

En las afirmaciones assertThat(), solo estamos verificando si el código HTTP está siendo devuelto como 200. Pero además de eso, deberemos verificar si el JSON que se está devolviendo es el que esperamos.

Crearemos una variable jsonEsperado que será igual a DatosDetalleConsulta.Json con .write() recibiendo como parámetro new DatosDetalleConsulta().

Esta clase recibirá un objeto del tipo Consulta o las identificaciones de la consulta, del médico, del paciente y de la fecha.

El ID de la consulta, como no llamaremos a la base de datos, no recibiremos un identificador correcto, por lo que en principio lo pasaremos como nulo.

La identificación del médico deberá ser 2l, del paciente 5l, seguida de la misma fecha. Después de crear el objeto, aplicaremos .getJson() para devolver un JSON.

En la línea siguiente, llamaremos al assertThat() que contiene response.getContentAsString() para tener el contenido como cadena. Luego, aplicaremos isEqualTo(jsonEsperado).

//then
assertThat(response.getStatus()).isEqualTo(HttpStatus.OK.value());

var jsonEsperado = detalleConsultaJacksonTester.write(datos).getJson();

assertThat(response.getContentAsString()).isEqualTo(jsonEsperado);COPIA EL CÓDIGO
Ejecutaremos esta prueba y esperaremos a que termine la ejecución. Tendremos un error indicando que JacksonTester<> no fue encontrado, ya que para poder inyectarlo, es necesario tener otra anotación encima de la clase llamada @AutoConfigureJsonTesters.

@SpringBootTest
@AutoConfigureMockMvc
@AutoConfigureJsonTesters
class ConsultaControllerTest {

//trecho de código suprimido

}COPIA EL CÓDIGO
Al ejecutar nuevamente, no habrá errores, pero la prueba fallará. Se realizó la selección de la base de datos y se disparó la consulta, pero eso no es lo que queríamos, ya que queríamos acceder solo al controlador de manera aislada, y por eso falló.

Falta indicarle a Spring que no use la base de datos real. En ConsultaController.java, veremos que se está inyectando la clase AgendaDeConsultaService que está accediendo a la base de datos.

Para solicitar un mock de este objeto, volvemos a la clase de prueba y declaramos otro atributo private AgendaDeConsultaService agendaDeConsultaService y, encima de él, colocamos la anotación @MockBean.

Con esto, le decimos a Spring que cuando necesite inyectar este objeto en el controlador, debe aplicar el mock y no inyectar una agendaDeConsultaService real.

//trecho de código suprimido

class ConsultaControllerTest {

 @Autowired
private MockMvc mvc;

@Autowired
private JacksonTester<DatosAgendarConsulta> agendarConsultaJacksonTester;

@Autowired
private JacksonTester<DatosDetalleConsulta> detalleConsultaJacksonTester;

@MockBean
private AgendaDeConsultaService agendaDeConsultaService;

//trecho de código suprimido

}COPIA EL CÓDIGO
Guardaremos y volveremos a ejecutar la prueba. Veremos que no se ejecutó la consulta ni se accedió a la base de datos, pero la prueba falló de nuevo. El retorno dice que el JSON devuelto debería ser la identificación nula, la del médico 2 y la del paciente 5, además de la fecha actual, pero lo que llegó fue un JSON vacío "". Entonces, por alguna razón, no devolvió nada, es decir, recibió el código 200 pero el cuerpo llegó vacío.

Esto sucedió porque, en nuestro controlador, llamamos a agendaDeConsultaService.agendar(), pero nuestra agenda es un mock, que por defecto devuelve nulo. Entonces, nuestro dto está nulo, y al momento de hacer la conversión, este dto devuelto por Spring es null.

Es un mock pero necesitaremos simular diciendo que, cuando el método agendar() sea llamado, devolveremos la información proporcionada. Para hacer esta configuración, volveremos al archivo de prueba y, antes de disparar la solicitud de verdad, usaremos Mockito, que es la biblioteca de mocks que Spring usa .

Después de var especialidad y antes de var response, llamaremos al método when() y haremos la importación automática de la biblioteca. Entonces, cuando se llame a agendaDeConsultaService.agendar(), tendremos el thenReturn() para devolver el nuevo objeto DatosDetalleConsulta esperado.

Más adelante, en jsonEsperado, recortaremos la línea de new DatosDetalleConsulta() y escribiremos datos, que se pasará en el thenReturn(). A continuación, lo lanzaremos a una nueva variable llamada datosDetalleConsulta, que es igual a new DatosDetalleConsulta() con null, 2l, 5l, fecha.

En when(), el contenido de .thenReturn() será solo datos. Por lo tanto, cuando la agenda que es el mock tenga el método .agendar() llamado, no importará el parámetro para devolver los datos.

Con esto, dispararemos la solicitud y, finalmente, verificaremos si el JSON devuelto es igual al objeto esperado.

@Test
@DisplayName("deberia retornar estado http 200 cuando los datos ingresados son validos")
@WithMockUser
void agendarEscenario2() throws Exception {
   //given
   var fecha = LocalDateTime.now().plusHours(1);
   var especialidad = Especialidad.CARDIOLOGIA;
   var datos = new DatosDetalleConsulta(null,2l,5l,fecha);

   // when

   when(agendaDeConsultaService.agendar(any())).thenReturn(datos);

   var response = mvc.perform(post("/consultas")
           .contentType(MediaType.APPLICATION_JSON)
           .content(agendarConsultaJacksonTester.write(new DatosAgendarConsulta(2l,5l,fecha, especialidad)).getJson())
   ).andReturn().getResponse();

   //then
   assertThat(response.getStatus()).isEqualTo(HttpStatus.OK.value());

   var jsonEsperado = detalleConsultaJacksonTester.write(datos).getJson();

   assertThat(response.getContentAsString()).isEqualTo(jsonEsperado);

}