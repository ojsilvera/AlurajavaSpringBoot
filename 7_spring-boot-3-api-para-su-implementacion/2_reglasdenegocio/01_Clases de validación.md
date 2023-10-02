[00:00] En la parte anterior nosotros realizamos todo lo que sería el cuerpo de las clases que nos van a permitir agendar una consulta en la base de datos para un paciente un determinado médico, entonces nosotros creamos la clase de consultaController, es la clase encargada de comunicarse con las API externas, recibir la información y guardarla en la base de datos.

[00:24] Sin embargo, nosotros dentro de la tarjeta de Trello vimos que tenemos algunas reglas que deben cumplirse, entonces nosotros tenemos que validar que ese ID existiera en la base de datos y tenemos que validar otras reglas de negocio que fueran para lo que nosotros construimos una clase de servicio para evitar colocar todas esas responsabilidades dentro de la clase controlador, ya que es la responsabilidad de la clase controlador únicamente comunicarse con APIs externas.

[00:56] De lo contrario violaría los principios de Liskov. Entonces, cada clase tiene que tener una única responsabilidad. En la clase de servicio la responsabilidad de ella va a ser procesar esa información para poder posteriormente enviarla al repositorio y guardar esa información en la base de datos.

[01:16] Nosotros podríamos colocar acá nuestras validaciones. De la misma forma que hicimos a la hora de seleccionar médico, que era una de las reglas de negocio, indicaba que en caso de que el médico fuese nulo, el id del médico fuese nulo, nosotros llegamos a seleccionar un médico aleatorio.

[01:37] Nosotros hicimos las validaciones de integridad para verificar que ese ID existiese en la base de datos y que no fuese nulo. Ahora vamos a realizar validaciones un poco más complejas que no podemos realizar con bin validation ni son validaciones tan simples como únicamente verificar si el ID es nulo.

[01:58] Entonces nosotros vamos a aplicar un design pattern, que nos va a permitir colocar todas esas clases de validación de forma más ordenada y más de más elegante. Y también va a permitir que esta clase siga creciendo y que a la hora de darle mantenimiento sea más complejo.

[02:22] Entonces, para eso nosotros vamos a crear dentro de la clase de consulta un paquete llamado validaciones y vamos a ver las reglas de negocio. La primera regla de negocio es el horario de atención de la clínica es de lunes a sábado de 7:00 a 19:00 de la tarde. Las consultas tienen duración fija de una hora.

[02:45] Entonces esa no es una validación que vamos a realizar dentro de nuestras validaciones, ya que eso queda fijado dentro de la información que se pasa al recibir los datos. Las consultas tienen que hacerse con al menos 30 minutos de anticipación. Eso está relacionado al momento en que se realiza la consulta, una validación.

[03:12] Tenemos que verificar que el paciente y que los médicos no se encuentren inactivos, que el médico no tenga ya una cita con otro paciente y que el paciente no realice más de una cita por día. Entonces vamos a hacer la primera validación que sería horario de funcionamiento.

[03:36] Entonces, para eso vamos a crear un método que se va a llamar público, va a ser un método público. Y va a enviar un mensaje, una excepción en caso de que sea verdadero. Entonces va a llamar validar y va a recibir los datos de la consulta. Entonces, lo que nosotros queremos hacer es verificar que no sea domingo, ya que el horario de atención de la clínica es de lunes a sábado, ni que se encuentre fuera del horario de atención que es de 7:00 de la mañana y 19:00 de la tarde.

[04:09] Vamos a crear una variable acá que se va a llamar domingo. Y vamos a utilizar de la clase DayOfWeek, la clase numeradora, vamos a verificar si eso es igual a la fecha datos.fecha, getDayOfWeek. Si eso se cumple, nosotros nos encontramos en el domingo.

[04:39] En caso de que sea domingo, enviamos un mensaje de error. Si domingo, si el valor de domingo es verdadero nosotros vamos a enviar una nueva excepción. No vamos a enviar validación integral ya que tenemos una validación de integridad, vamos a enviar una validación, una excepción. La excepción sería el horario de atención de la clínica que es de lunes a sábado de 7:00 a 19:00 horas.

[05:14] Como nosotros estamos viendo que la comparación entre domingo y la fecha de la consulta es igual, va a retornar un valor de true. Entonces nos encontramos en el domingo. Sin embargo, está faltando verificar el horario de apertura. Variable antes de la hora de apertura de hora de abrir antesDeApertura y lo siguiente, verificar despuesDeCierre.

[05:58] Si se encuentra después de la hora de cierre o antes de la hora de abrir, nosotros también vamos a enviar ese mensaje de error, para eso vamos a verificar la fecha de los datos, vamos a obtener la hora y vamos a verificar que sea menor a 7:00. El formato del localDateTime es un formato de 24 horas. Acá también vamos a tener la fecha, vamos a obtener la hora.

[06:32] Si es mayor a las 19:00 horas, que serían las 7:00 de la tarde entonces vamos a enviar ese mensaje de error. Entonces, antes de la apertura o después del horario de cierre. En caso de que esto se cumpla, enviamos el error. La siguiente condición es el horario de anticipación, las consultas deben programarse con al menos 30 minutos de anticipación más. Vamos a crear otra clase HorarioDeAnticipacion.

[07:07] Al igual que lo hicimos con la clase anterior, nosotros vamos a crear un cuerpo. De acá nosotros vamos a modificar las condiciones, solamente vamos a corregir el mensaje. Entonces, dentro de ese método yo tengo que verificar la hora en el momento en que se está realizando esa consulta y la hora en la que se está registrando la consulta.

[07:34] Si la diferencia es de menos de 30 minutos, entonces esa consulta no puede ser realizada. Entonces vamos a colocar, vamos a obtener el momento actual. Lo vamos a llamar ahora de la clase LocalDateTime.now. Y vamos a obtener la fecha: var horaDeConsulta.

[08:06] Si la hora de consulta, horaDeConsulta. Si la diferencia entre horaDeConsulta es de menos de 30 minutos, diferenciaDe30Min, entonces, esa consulta no puede ser realizada. Para eso vamos a utilizar Duration.between el momento ahora y la hora de la consulta. Entonces, en caso de que esto se cumpla, de que sea menor a 30 vamos a obtener los minutos, y en caso de que sea menor a 30 nosotros tenemos que enviar un mensaje indicando que esa consulta no puede ser realizada.

[09:02] Si la diferencia de minutos es verdadera, es decir, que es menor a 30, nosotros vamos a enviar un mensaje de error throw new ValidationException indicando que las consultas tienen que tener al menos 30 minutos de anticipación. Entonces, con eso ya tenemos la segunda validación.

[09:28] La siguiente validación es que no se pueden permitir agendar pacientes inactivos, vamos a crear otra clase que se va a llamar PacienteActivo. Ahora nosotros tenemos que verificar en la base de datos si el parámetro activo para ese paciente se encuentra como true o como false.

[09:58] En caso de que el parámetro activo se encuentre falso, nosotros tenemos que enviar un mensaje de error indicando que esa consulta no se puede realizar para ese paciente. Entonces lo primero que tenemos que hacer es verificar que el ID de ese paciente no sea nulo. Si el ID de ese paciente es igual a nulo, vamos a retornar.

[10:29] En caso de que no sea nulo, nosotros vamos a crear una variable llamada pacienteActivo y vamos a buscar en el repositorio. Para eso tengo que inyectar acá el repositorio, crear un parámetro privado PacienteRepository, vamos a llamar paciente y le voy a anotar con la anotación @Autowired, y aquí en el siguiente video vamos a inyectar estas validaciones dentro de la clase de servicio y les voy a mostrar cómo hacerlo. Por los momentos nosotros no vamos a utilizar la anotación @Autowired.