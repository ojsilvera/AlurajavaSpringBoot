[00:00] Hola, para dar comienzo este tercera parte de la clínica médica, aquí nos encontramos con la diferenciador de actividades de Trello, donde podemos ver que ya nosotros tenemos en la parte de realizado lo que sería de los registros de médico, el listado de médicos, actualización, eliminación de médicos, así como para pacientes.

[00:21] Y a cada vez tenemos lo que sería el agendamiento de consultas y el cancelamiento de consultas. Entonces vamos a mover por hacer a haciendo lo que sería el agendamiento de consulta y vamos a seleccionarlo. Y en la descripción tenemos lo siguiente. El sistema debe contar con una funcionalidad que permita agendar citas, en la cual se debe llenar la siguiente información.

[00:42] Los datos del paciente, los datos del médico, la fecha en la que se va a realizar esa consulta y las siguientes reglas de negocio deben ser validadas por el sistema. Entonces, para indicar cuáles son los datos del paciente nosotros vamos a indicar el ID de ese paciente, el ID del médico y vamos a pasar la hora y la fecha en la que se va a realizar esa consulta.

[01:14] Acá en el diseño de Trello, nosotros vemos que la aplicación mobile va a contar con los siguientes campos. Vamos a poder indicar cuál va a ser el nombre del paciente, vamos a indicar el nombre del médico, vamos a seleccionar la fecha y el horario y vamos a tener un botón que nos va a permitir realizar el agendamiento de esa consulta.

[01:29] Entonces acá nos está indicando que algunos campos ya son obligatorios y únicamente el campo que no es obligatorio es el nombre del médico, entonces vamos a tener que el nombre del paciente es obligatorio, así como la fecha y hora de consulta. Acá tenemos un ejemplo de cómo se va a ver luego de haber llenado los campos, y luego de aplicar, de hacer el envío de esa petición, vamos a guardar esos datos en la base de datos.

[02:02] Entonces acá vemos que tenemos unas reglas de negocio que son un poco diferentes a las que nosotros realizamos en las partes anteriores. Estas reglas de negocios son un poco más complejas de las que podemos resolver con bim validation, ya que se ajustan al a ciertas condiciones que fueron desarrolladas por el cliente.

[02:20] Entonces, esas reglas de negocio están relacionadas al horario de atención de la clínica que es de lunes a sábado en el horario de 7:00 de la mañana, a 19:00 de la tarde, el horario, la duración del horario. El horario de anticipación con el que se deben realizar esas consultas, entonces nosotros vamos a tener un tiempo de al menos de 30 minutos de anticipación para realizar la cita.

[02:46] No se puede permitir agendar con pacientes inactivos o con médicos inactivos, entonces acá vemos que nosotros habíamos validado para cuando el paciente, el ID del paciente se encontraba nulo o cuando los datos del médico se encontraba nulo. Acá vamos a ver cómo hacer cuando uno de los campos tiene un cierto valor, que en este caso va a hacer que se encuentre inactivo.

[03:12] No podemos permitir programar más de una consulta para el mismo día para el mismo paciente, y podemos permitir una cita con un médico que ya se encuentra en cita con otro paciente. Como hemos mencionado en el diseño, la elección del médico es opcional, entonces vamos a ver cómo vamos a trabajar con eso.

[03:33] Entonces, si nos fijamos, la estructura va a ser la misma que el desarrollo de los cursos anteriores. Nosotros vamos a tener un controlador que va a recibir los datos iniciales, vamos a tener un procesamiento de esos datos y vamos a buscar los valores en la base de datos, solo que ahora vamos a tener un nuevo campo donde vamos a realizar estas nuevas validaciones.

[03:54] Entonces ahora sería un área de servicio o área simplemente donde vamos a colocar las reglas de negocio. Si nos fijamos nosotros vamos a tener una especie de receta, a la hora de aplicar nuevas funcionalidades, siempre vamos a tener un controlador, ya que ese es el lugar donde nosotros enviamos y recibimos peticiones. Esto es lo que conectan con la API de Postman o con Insomnia o con cualquier otra API externa.

[04:25] Vamos a tener los DTOs, así como las entidades JPA. Nosotros vamos a tener elementos que representan esos médicos, esos pacientes, así como las entidades que son las que van a representar las tablas en la base de datos. Vamos a tener los repositorios, que es un elemento en Spring que se encarga de realizar todas las conexiones con la base de datos, incluso realizar algunas consultas por nosotros.

[04:54] Hay algunas consultas más complejas que nosotros vamos a realizar. Eso lo vamos a ver acá en este curso. Vamos a tener la parte de migraciones en esta parte vamos a ver cómo utilizar Flyway para crear tablas y así como agregar nuevos registros de datos tanto para base de datos en la base de datos con la que vamos a estar trabajando a la hora de desarrollar nuestra aplicación, así como una base de datos de prueba.

[05:20] Vamos a ver cómo trabajar con Spring Security a la hora de utilizar Spring Doc. Y vamos a tener esta nueva parte que serían las reglas de ese negocio, entonces, esta nueva parte se va a encontrar en un componente parte que va a ser el componente de servicios donde se van a encontrar todas esas validaciones que nosotros estábamos viendo en la tarjeta de train.

[05:44] Entonces a continuación, vamos a ver lo que sería el desarrollo de todas estas actividades, comenzando por el desarrollo del controlador en Spring framework para el agendamiento de consultas.

