[00:00] Hola, bienvenidos una vez más a la tercera parte del desarrollo de la API de clínica médica con Java y Spring Boot en la versión 3. En esta parte vamos a dar continuidad al desarrollo de la aplicación que veníamos trabajando en los dos cursos anteriores.

[00:14] Entonces en los cursos anteriores nosotros vimos cómo desarrollar una API Rest, vimos qué es una API Rest y cuáles son los componentes que en los que se estructura. Vimos que realizamos peticiones y recibimos respuestas a través de una API de la de API Insomnia. En esta parte usaremos la API de Postman.

[00:33] Realizamos un CRUD donde permitía crear una entidad, una nueva entidad que era la entidad de médicos, así como la de pacientes, leer los registros existentes en la base de datos, actualizar los registros para alguno de esas entidades como médico paciente y eliminar de forma lógica o de forma permanente, utilizando los métodos internos de repositorio.

[00:56] Realizamos validaciones para los campos ingresados, utilizando BIM Validation y acá nosotros al ingresar campos tenemos que verificar que esos campos no sean nulos, que no se encuentren vacíos o que contengan un cierto formato, ya sea como un formato numérico, un formato del tipo email.

[01:14] Realizamos la paginación y el ordenamiento para el modo cómo íbamos a recibir los resultados de la lectura de la base de datos cuando nosotros realizamos una petición. Nosotros vamos a recibir ese resultado y lo podemos ordenar e indicarle a Sprint cuál va a ser la cantidad de valores que vamos a recibir por página.

[01:36] Apliquemos las buenas prácticas en el desarrollo de API Rest, realizamos el tratamiento de errores, ya que cuando nosotros ingresamos un valor que no corresponda al formato deseado, nosotros tenemos que indicarle mediante un mensaje capturar ese error e indicarle al cliente que está enviando los datos de forma errónea, ya sea como nulo o un formato inadecuado.

[02:05] Y por último, realizamos el control de acceso con Jason Web Token, lo que nos va a permitir darle más seguridad a nuestra aplicación al colocarle un acceso de usuario a todos estos endpoints o estas rutas de acceso.

[02:22] Ahora, en esta nueva parte, nosotros vamos a agregar una nueva entidad que va a ser la entidad de consulta, la que nosotros vamos a permitir registrar una consulta con los médicos y pacientes existentes dentro de la base de datos, entonces nosotros vamos a agregar un nuevo componente que se va a relacionar internamente con esos elementos que ya existen dentro de la aplicación.

[02:49] Ahora vamos a realizar una agendamiento de consulta y vamos a crear la documentación para esa nueva aplicación, eso lo vamos a realizar utilizando la API de Spring Doc, con la que nosotros vamos a poder entregar un formato agradable a la vista al cliente que nos está solicitando la API de forma que él no tiene necesidad de entender cuál es el desarrollo del código o puede que alguno de los que va a trabajar con la API no tenga conocimiento de Java con Spring.

[03:19] Y esta documentación le va a facilitar cuál va a ser los parámetros y cuáles son las diferentes rutas con las que va a trabajar. Vamos a trabajar también con los tests automatizados, ya que al trabajar con Spring framework tenemos que vamos a tener una forma diferente de trabajar con JUnit.

[03:43] Ahora nosotros vamos a simular estas entidades, estos componentes que existen en Spring framework y que son auto instanciadas, entonces vamos a ver cómo realizar estos tests unitarios con JUnit y Mockito dentro de El ambiente de Spring frame. Y por último, vamos a realizar el build del proyecto.

[03:59] Nosotros ya hemos construido proyectos con Java, ahora vamos a ver cómo realizar ese build del proyecto con el Java Spring Framework y cómo hacer el deploy o cómo ejecutar ese archivo final dentro de un servidor externo o dentro de la nube.

[04:19] Por último, vamos a continuar trabajando con la API de clínica médica, entonces vamos a disponibilizar una aplicación mobile donde vamos a ver los diferentes componentes de registro tanto para médicos como para pacientes y nos vamos a enfocar en la parte de consulta. Entonces, sin más que mencionar, vamos a darle continuidad al curso y nos vemos en la siguiente aula.