[00:00] Entonces para comenzar el desarrollo de esta nueva funcionalidad, vamos a continuar con la aplicación de los cursos anteriores, donde registramos un médico y dejamos como desafío registrar pacientes. Y ya tenemos ese desafío ya elaborado.

[00:18] Nosotros tenemos el paciente, tenemos el médico y vamos a crear esta nueva funcionalidad. Para implementar esta nueva funcionalidad, vamos a aplicar la receta creando una nueva clase que se llama ConsultaController y vamos a copiar las anotaciones de alguna de las otras clases.

[00:40] Entonces de acá vamos a copiar la anotación @RestController y @RequestMapping. Entonces,o como habíamos mencionado, estas anotaciones lo que indica es que son componentes gerenciados por Spring. ¿Qué significa eso? Que ya no tenemos que usar la palabra new ConsultaController para poder hacer uso de esa clase, sino que, como ya no tenemos que realizar el uso de la palabra new, Spring automáticamente él instancia esa clase y la deja disponible para nuestro uso.

[01:17] Entonces tenemos que anotarla con la anotación @RestController o con la anotación @Controller. @RequestMapping indicamos cuál va a ser la ruta, la URL “/consultas”. Al colocar @Controller tenemos que colocar @ResponseBody ya que todo @RestController está conformado por la anotación @Controller y @ResponseBody, y el controlador a su vez está conformado por la anotación @Component como nosotros habíamos mostrado en el diagrama.

[01:50] Entonces yo podría acá reemplazar controlador por @Componen y funcionaría del mismo modo. Sin embargo, para indicar que es un controlador, un controlador Rest, vamos a dejar la opción controller y la anotación @ResponseBody. Lo siguiente es crear nuestro método, ese método va a retornar ResponseEntity que se va a llamar agendar.

[02:25] Y va a tener los siguientes parámetros. @RequestMapping, @RequestBody y @Valid para validar los campos de bin validation. Entonces acá tenemos que poner el tipo que va a ser DatosAgendarConsulta y vamos a recibir parámetro datos.

[02:59] Acá vamos a imprimir en la consola system.out.println(datos) y vamos a retornar new ResponseEntity.ok, vamos a pasar nuevo DatosDetalleConsulta. Todos los campos van a ser nulos por ahora, más adelante vamos a llenar esos campos. Ahora lo único que nosotros queremos es ver que se aplique esa funcionalidad.

[03:41] Entonces vamos a crear, ya creamos el controlador, lo siguiente es crear ese record. Entonces vamos a ir a más acciones, crear record, vamos a crear un nuevo paquete dentro de dominio, se va a llamar consulta. Y dentro de él vamos a colocar los atributos (Long id, Long idPaciente, Long idMédico) por último LocalDateTime fecha.

[04:23] La fecha no puede ser nula y tiene que ser una fecha posterior a la fecha actual, para eso vamos a utilizar la anotación @Future. Para pacientes, paciente tampoco puede ser nulo, eso ya tenemos el de DTO para agenda de consultas. Ahora vamos a crear DatosDetalleConsulta. Vamos a más acciones.

[04:55] Crear record. Lo vamos a crear dentro del paquete consulta. El objeto va a ser Long id, Long idPaciente, Long idMedico y por último LocalDateTime la fecha, que es lo que vamos a retornar. Ya con eso tenemos el controlador funcionando correctamente. Tenemos que eliminar esto acá. Ya está funcionando todo y aquí está faltando, como esto es un post, vamos a colocar unas piernas acá, @PostMapping.

[05:53] Vamos a colocarlo en Consulta. Y con eso está funcionando nuestro controlador. Lo siguiente, ya creamos los DTO, es crear la entidad @Consulta. Vamos a crear una nueva clase. Consulta. De la clase médico vamos a copiar las anotaciones, vemos que se sigue la receta, entonces esa receta se va a cumplir siempre que nosotros estemos creando nuevas entidades en nuestra base de datos utilizando Spring Framework.

[06:31] Entonces dependiendo de todo del elemento que tengamos que agregar, nosotros podríamos agregar institutos, podemos agregar más pacientes, otro tipo de personal como personal de limpieza, personal de seguridad, aquí es “consulta”. Tenemos que colocar el ID. Vamos a copiar esta parte, acá la voy a copiar, si la tengo diseñada.

[07:02] Tenemos que copiar el ID. Vamos a importar de JPA. Acá también vamos a importar de JPA. Tenemos que realizar una relación entre la entidad consulta y las tablas de médico y paciente. Entonces en el curso de JPA explico más a profundidad cómo se realizan esas relaciones entre diferentes tablas.

[07:31] Nosotros vamos a tener la tabla consulta que se encuentra relacionada a través del atributo ID con la tabla médico, que es otra entidad dentro de la base de datos. Ahora nos falta agregar el repositorio, que es el responsable de comunicarse con la base de datos. Vamos a copiar médico repository y vamos a pegarla en las consultas.

[07:55] Vamos acá a pegar. Buscamos médico, vamos a pegar y vamos a reemplazar el médico por consulta. Ahora eliminamos esto der acá y vamos a pasar en vez de médico una consulta. Entonces, como habíamos mencionado, todo repositorio también es un componente, entonces nosotros colocamos la anotación @Repository para indicar que esa interface va a representar un componente gerenciado por Spring Framework.

[08:37] Entonces, si nosotros creamos una clase que implemente esta interface, automáticamente esa clase va a heredar esta anotación y se va a encontrar instanciada y gerenciada por los componentes de Spring framework. Entonces, ya creamos la entidad, creamos el repositorio. Lo siguiente es crear la migración, entonces vamos a crear acá la migración, vamos a pegarla.

[09:07] La siguiente migración va a ser C. Vamos a crear la tabla consultas. Para eso, para evitar errores, vamos a copiar acá, porque yo tengo que realizar una restricción entre la tabla consultas_medico_id con la llave extranjera médico_id. Entonces, vamos acá, vamos a realizar otra restricción, ya que nosotros estamos relacionando la tabla consultas con la tabla médico y con la tabla pacientes.

[09:40] Vamos a pasar el atributo id, vamos a crear la columna id, la columna médico_id, la columna paciente_id para relacionarlos dentro de una nueva tabla que se va a llamar consultas. Entonces esta forma ya tenemos todo funcionando, la aplicación ya está conectada con la base de datos. En teoría debería funcionar. Vamos a ver si está funcionando todo correctamente.

[10:04] Aquí dice la base de datos no la hemos creado, creamos la base de datos. Y ejecutamos nuevamente. Entonces, luego que se ha ejecutado, el creó la sexta migración, él creó las migraciones 1, 2, 3, 4, 5 y 6. Está ocurriendo todo correctamente. Ahora aquí en el Postman nosotros vamos a realizar nuestra solicitud a nuestra API creando nuestra primera consulta.

[10:38] Entonces para eso vamos a hacer una requisición del tipo POST. Vamos a colocar la URL, cambiar paciente por consultas. Y tenemos que enviar el cuerpo, el cuerpo va a ser del tipo JSON. En cursos anteriores creo que usaron la aplicación de Insomnia.

[11:04] Aquí, para variar, vamos a usar Postman, simplemente para ver que funciona igual indiferentemente de la aplicación de test de API Rest. Acá tenemos que recordar que estamos utilizando Spring Security y vamos a tener un estado 403 si no pasamos el token. Entonces nosotros creamos esa base de datos desde cero.

[11:24] Tenemos que ir a nuestra base de datos, a los usuarios y crear un nuevo usuario. Ese nuevo usuario, tiene que tener un nombre, vamos a colocar María. Y tenemos que pasar un generador de código, de has hecho. Ese hash va a ser 1, 2, 3, 4, 5, 6. Vamos a ir la base de datos y vamos a guardar ese hash.

[11:55] Guardamos los registros y ahora sí, en el Postman vamos a ir al login, a generar ese nuevo token. Copiamos el token en nuestra nueva requisición, vamos a ir a la parte de autorizaciones, a token. Y vamos a copiar ese nuevo token. En el cuerpo que vamos a enviar, tenemos que colocar el id del paciente. Va a ser 1.

[12:41] Vamos a colocar el id del médico que también va a ser 1. Y por último, tenemos que colocar la fecha. Tiene que tener un formato del tipo LocalDateTime. Ese formato está conformado por el año, que tiene que ser el futuro, en este momento nos encontramos en el 2023. Puede ser cualquier momento futuro a partir de la fecha actual, el mes y el día.

[13:06] Entonces vamos a agendar para el mes 10, el día 10. Las horas y los minutos y los segundos se encuentran separados por la T. Entonces, de este lado vamos a tener meses, días y años, y del lado derecho vamos a tener las horas que vamos a agendar para las 10:30. Podríamos colocar los segundos, lo vamos a colocar simplemente con las horas y los minutos.

[13:35] Le colocamos la autorización al token. Ahora vamos a realizar esta requisición. Vemos que tenemos el retorno, tiene un estado de status 200, HTTP, vamos a editar el nombre de esta consulta. Vamos a llamar agendarConsulta.

[14:08] Y en nuestra aplicación vemos que se imprime en la consola los valores que recibió de Postman. Entonces recibió el valor de id 1, médico 1 y la fecha. Entonces como nosotros por ahora no estamos realizando alguna operación dentro de este método, él simplemente imprime en la consola y dio un retorno de nulo.

[14:32] Más adelante vamos a ver cómo aplicar nuestra capa de servicios. Voy a eliminar ese de System.out y ver un nuevo componente de Spring Framework, que es la anotación @Server, que nos va a permitir realizar estas operaciones dentro de nuestra aplicación.