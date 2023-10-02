[00:00] Hola. En la parte anterior, nosotros configuramos la base de datos para nuestras pruebas y seleccionamos el repositorio, el método que vamos a probar. Entonces en MedicoRepositorio nosotros vimos que tenemos el método findByActivo, que ya es validado por Spring framework, método que utiliza el patrón en patrones de consulta en inglés y él realiza automáticamente esa consulta SQL en la base de datos.

[00:32] También tenemos el último método findActivoById, donde tenemos una consulta bastante simple para realizar esa prueba como desafío que nosotros por tener esta consulta un poco más compleja, consideramos interesante realizar las pruebas y verificar que el médico que estuviéramos obteniendo es que este método efectivamente nos dé cómo retorno un médico correcto.

[01:00] Entonces, esta consulta se encarga de verificar si en la base de datos ese médico con esa especialidad y esa fecha se encuentra disponible. En caso que no se encuentre disponible retorna nulo y en caso de que se encuentre disponible, va a retornar el médico.

[01:14] Entonces de vuelta en la clase de prueba, nosotros ya mencionamos que vamos a tener dos posibles casos. Entonces para clasificar cada uno de esos casos, vamos a colocar acá escenario 1 y vamos a colocar una descripción de que realiza esta primera prueba.

[01:36] Entonces esta primera prueba acá, vamos a utilizar la anotación @DisplayName donde vamos a colocar la operación que va a realizar este método de prueba. Entonces acá vamos a colocar: “debería retornar nulo cuando el médico se encuentre en consulta con otro paciente en ese horario”.

[02:10] Entonces, como va a depender del horario, lo primero que se nos viene a la cabeza es que vamos a tener que registrar un horario, entonces ese horario vamos a hacer, por ejemplo, el próximo lunes o el próximo martes con un horario dentro del horario de funcionamiento de la clínica.

[02:27] Vamos a registrar esa hora acá para trabajar con ella, acá vamos a colocar próximo lunes a las 10:00 de la mañana. Vamos a utilizar la clase LocalDate y acá vamos a fijar el día de la semana, para fijar un horario o un día en específico. Nosotros utilizamos el método with.

[03:00] Vamos a colocar TemporalAdjusters para ajustar el día de la semana y vamos a colocar que ese día de la semana va a ser el lunes. Lo siguiente sería colocar la hora, vamos a necesitar el día y la hora, y la hora va a ser a las 10:00 de la mañana.

[03:17] Entonces ya tenemos el horario que vamos a colocar dentro de nuestro método de prueba. Nosotros vamos a necesitar la especialidad y la hora. Entonces, ya con eso, nosotros podemos llamar el médico del repositorio. Entonces vamos a colocar acá una variable var médicoLibre. Y para eso nosotros vamos a tener que utilizar el repositorio de médico.

[03:46] Vamos a inyectar acá un atributo privado, va a ser MedicoRepository. Y para poder utilizarlo dentro de nuestra clase de prueba tenemos que inyectarlo con la anotación @autowored. De ese modo, nosotros vamos a instanciar ese repositorio dentro de nuestra clase de prueba.

[04:10] Ya con ese atributo funcionando, nosotros vamos a hacer la consulta del médico, entonces para realizar esa consulta vamos a seleccionar un médico con especialidad en esa fecha. ¿Cuál va a ser los atributos? Los atributos son la especialidad que es un enumerador. Va a ser cardiología y la fecha en la que acabamos de escribir previamente, que sería el próximo lunes a las 10:00 horas.

[04:36] Entonces ya tenemos y estamos obteniendo el método del repositorio. Para realizar las pruebas nosotros tenemos de JUnit las diferentes clases estáticas de las clases de assertion. Esas clases nos permiten hacer diferentes comparaciones y retorna verdadero o falso.

[05:02] Eso en caso de que sea verdadero, de que se cumpla esa condición, esa assertion, la prueba pasa efectivamente, en caso de que no se cumpla esa prueba que estamos realizando con los assert, él va a fallar. Nosotros vamos a utilizar, vamos a probar que ese médico libre, sea nulo.

[05:27] Entonces nosotros vamos a importar del paquete de assertion, todo lo que sería la librería que nos va a permitir hacer las diferentes comparaciones, entonces aquí estamos comparando ese valor de médico que estamos trayendo de la base de datos utilizando el repositorio, y vamos a verificar si ese valor es nulo.

[05:51] Para verificar si es nulo, nosotros primero tenemos que registrar un médico, tenemos que registrar un paciente y tenemos que registrar una consulta, nosotros vamos a realizar toda la operación donde registramos un médico, registramos un paciente y vamos a crear una consulta con ese médico y con ese paciente para que ella, luego de que se encuentre en la base de datos cuando realice la búsqueda, se va a encontrar de que ese médico no se encuentra disponible y nos va a retornar nulo.

[06:20] En el siguiente caso, vamos a probar el caso en el que no va a haber, no vamos a registrar la consulta y debería retornar el médico que estamos registrando. Entonces nosotros vamos a tener que registrar un médico, vamos a tener que registrar un paciente y por último vamos a registrar una consulta. RegistrarConsulta.

[06:55] Entonces, yo acá ya tengo los métodos previamente diseñados que nos permiten hacer el registro de un médico, de un paciente y el método que registra la consulta. Lo voy a copiar acá. Y voy a ir describiendo lo que hacen esos métodos, entonces acá yo tengo el método de registrarConsulta.

[07:22] Este método va a recibir el médico que estamos registrando, va a recibir también el paciente y la fecha que vamos a enviar. Entonces, acá yo voy a enviar un médico, voy a enviar el paciente y la fecha, que sería el próximo lunes.

[07:41] Entonces en el método de registrar consulta voy a registrar en la base de datos ese médico, ese paciente y el horario que va a ser lo que vamos a buscar dentro en el repositorio y nos va a retornar para este caso particular nulo. Acá nos está dando un error, que es el error de entity manager.

[08:02] El entity manager es el encargado de realizar el puente entre nuestra aplicación y la base de datos. Cuando nosotros utilizamos el entity manager en las aplicaciones, nosotros tenemos que instanciarlo a través de a través del Entity Manager Factory.

[08:18] Pero acá, Spring framework nos permite utilizar el TestEntityManager, que él se va a autoinstanciar únicamente para realizar las pruebas. Entonces solamente para ambientes de prueba, nosotros vamos a tener este TestEntityManager que es un gerenciador que cuando nosotros ejecutemos la prueba él va a estar activo.

[08:41] Él va a realizar todas las operaciones donde va a crear una instancia y va a hacer esa conexión con esa base de datos. Vamos a llamar a este EntityManager em y vamos a inyectarlo con la anotación @Autowired. Entonces ya tenemos el EntityManager funcionando.

[09:00] Estamos realizando una persistencia para esa consulta, donde recibimos un médico, un paciente y la fecha, que sería el próximo lunes. Estamos registrando también un médico, acá en médico voy a registrar un médico y los valores para ese médico serían el nombre, el email, el documento y la especialidad.

[09:20] El nombre vamos a coloca “Jose”. El email sería “j@gmail.com”. El documento voy a colocar un documento estándar “123456” y la especialidad de los enumeradores vamos a seleccionar CARDIOLOGIA para verificar efectivamente que esa especialidad que estamos buscando en el repositorio coincida con ese médico que estamos registrando en la base de datos.

[09:55] Ahora necesitamos registrar a un paciente con un nombre, un email y un documento, entonces simplemente vamos a colocar registrarPaciente, vamos a colocar un nombre, vamos a colocar acá “Antonio”, acá va a ser “a@gmail.com” y el documento va a ser un documento estándar.

[10:22] Ya hemos registrado el médico, el paciente, el horario en el que se va a realizar la consulta, registramos esa consulta entre ese médico y ese paciente y realizamos la búsqueda en la base de datos para un médico con esa especialidad y esa fecha. Entonces nosotros para esa consulta en el repositorio deberíamos obtener algún resultado. El que nosotros estamos esperando es que dé nulo.

[10:49] Una vez que se han registrado los datos, solamente queda ejecutar nuestra prueba, vamos a ejecutarlo y vemos que esa prueba pasó efectivamente, entonces acá vemos la descripción, debería retornar nulo cuando el médico se encuentre con otro paciente en ese horario.

[11:09] Si nosotros vemos los detalles, vemos que él realizó el registro en la base de datos para el médico, él realizó un insert de médico, realizó un insert para los pacientes para la consulta y luego que él realizó, él realizó acá una búsqueda. Entonces si nosotros vemos acá él intentó seleccionar un médico que se encontrase activo con esa especialidad y que no se encontrase con consulta y en esa fecha.

[11:39] Entonces seleccionó un médico aleatorio dentro de la especialidad y vio cómo nosotros lo habíamos registrado, un médico con este paciente nos va a retornar nulo. Entonces el siguiente caso, vamos a copiar de acá, el siguiente caso es en el caso en el que el médico, el escenario 2 en el que el médico sí se encuentra disponible para ese paciente.

[12:07] Para eso sencillamente nosotros tenemos que registrar un médico. No vamos a registrar el paciente ni vamos a registrar una consulta. Entonces, a la hora de nosotros realizar una búsqueda en la base de datos, deberíamos encontrar que el médico que estamos buscando, el médico libre, sea igual al médico que estamos instanciando.

[12:35] Entonces ya registramos un médico. Vamos a cambiar, cambiar acá la descripción. Debería retornar un médico cuando realice la consulta en el repositorio. “Debería retornar un médico cuando realice la consulta en la base de datos para ese horario”.

[13:09] Entonces, si nosotros probamos esta segunda prueba, este segundo test, deberíamos obtener en que pase esa prueba, ya que nosotros estamos comparando lo que estamos obteniendo del repositorio, que es un médico y tendría que ser igual esta vez no a un valor nulo, sino tienen que ser igual a un elemento del tipo médico.

[13:35] Entonces vemos que efectivamente debería retornar un médico cuando realicé la consulta en la base de datos para ese horario. Entonces, esos son los dos casos para nuestra consulta de seleccionar el médico con especialidad en fecha para medico Repository. En la siguiente parte vamos a ver cómo testar los controladores y testar los estados 400 y 404.