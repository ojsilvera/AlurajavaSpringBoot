[00:00] Hola. Bienvenidos a su curso de Spring Boot 3, creando un API Rest en Java. Yo soy su instructor Diego Argüelles Rojas, quizás algunos ya me conozcan porque ya he dictado algunos cursos aquí en Alura en la formación básica de Java. Y ahora vamos a ver lo que es Spring Boot la versión 3 y cómo crear un API Rest.

[00:21] En los objetivos este curso, bueno, valga la redundancia, es la creación de una API Rest. Para aquellos que de repente no están muy familiarizados con lo que es una API, con lo que son Rest services, no se preocupen, vamos a repasar todos esos conceptos aquí desde lo más básico hasta un nivel intermedio y quizás algunos tópicos más avanzados.

[00:42] Después vamos a ver lo que es un CRUD, las operaciones básicas de todo API: create, read, update and delete para respectivamente crear, leer, actualizar y eliminar objetos o componentes de nuestra aplicación. Lo que son validaciones que, técnicamente ¿qué es una validación? Es verificar que el tipo de dato que yo quiero guardar, que yo quiero enviar a mi servicio web, a mi Rest service es el tipo de dato que mi base de datos acepta.

[012:12] Por ejemplo, digamos que quiero guardar un número de teléfono, tengo que validar que lleguen solo números, no letras. Bueno, eso es también lo que vamos a ver aquí en este curso, paginación y orden, dicho sea de paso, por ejemplo cuando tú quieres mostrar una gran cantidad de datos no siempre vas a mostrar todos los datos en una sola vista.

[01:36] Quizás es mucho mejor mostrarlos de 10 en 10, de 20 en 20, para que puedan entrar a la pantalla, la experiencia de usuario sea un poco más amena, más amigable y puedes ordenarlo también alfabéticamente, por número, por algún tipo de orden especial que quieras definir. Todo eso es posible también hacerlo aquí, a nivel de nuestro servicio web.

[02:00] Y en la parte de tecnología, que es a lo que vinimos, quizá lo más importante, lo más interesante, Spring Boot 3 es la última versión, la última versión estable. Hay algunos releases después de esta versión, pero la versión 3 es una de las más usadas en el mercado.

[02:17] Así como Java 17. Si bien ya tenemos una versiones más recientes de Java, Java 17 se está convirtiendo rápidamente en la más adoptada, muchas empresas están migrando de Java 11 a 17 directamente por el tipo de soporte a largo plazo que brinda. Entonces es la versión ideal para poder iniciar este curso.

[02:36] También vamos a usar Lombok. Para quienes nunca han escuchado de Lombok, es una herramienta, una librería muy útil que te ayuda, por ejemplo, a abreviar código. Estás cansado de escribir getters y setters, estás cansado o aburrido de repetir constructores, de implementar el patrón builder por ti mismo, todo eso, Lombok va a ser tu mejor aliado para reducir tu escritura de código puesto que Lombok lo va a autogenerar.

[03:04] Si no eres familiar con esto aun, no te preocupes, lo vamos a explorar muy bien en este curso y lo vas a amar después de esto. Después tenemos MySQL como base de datos, donde vamos a guardar todas nuestra información. Y Flyway.

[03:16] Para quienes no son tan familiares con esto, Flyway es digamos un gestor de base de datos a nivel de la estructura y las tablas, declarar tus tablas como Scribd de SQL y el motor de Flyway lo ejecuta y va a crear tu estructura de datos en MySQL de tal forma que es mantenible en el futuro, es versionable y bueno puedes habilitar colaboración entre muchos desarrolladores.

[03:44] Nuevamente si nunca lo han escuchado no se preocupen porque en este curso lo vamos a explorar muy bien. Para la capa de persistencia, cómo guardamos los datos, cómo interactuamos entre aplicación y base de datos, vamos a usar JPA y Hibernate.

[03:57] JPA es la especificación de Java para lo que es persistencia y Hibernate es la implementación de esta especificación. Por ejemplo, ya no vas a tener que escribir todo tu prepare statement para ejecutar cualquier consulta en la base de datos, simplemente con Hibernate te vas a reducir unas cuantas líneas de código y lo vas a hacer de una forma un poco más óptima, también lo vamos a explorar en este curso.

[04:20] Y Maven es un gestor de dependencias, al igual que Gradle. Con esto tú declaras tus dependencias en el archivo pom.xml, quizás algunos ya son familiares con esto y puedes controlar mejor las versiones, actualizar y no tienes que necesariamente tener el archivo jar y pegarlo en tu proyecto.

[04:40] Y finalmente Insomnia. Dado que hasta ahora hemos hablado solo de tecnologías backend, necesitamos algo con que probar nuestra API. Y como este curso es sobre un API, es sobre backend, no vamos a enfocarnos para nada en lo que es una capa cliente, una capa web. ¿Entonces con qué probamos nuestra aplicación? Con Insomnia, que es una herramienta para este tipo de casos.

[05:05] ¿Qué proyecto vamos a desarrollar? Vamos a ver lo que es una clínica médica. Nuestra Voll clinic. Como ustedes saben, en una clínica médica intervienen muchas cosas: pacientes, doctores, consultas, historias clínicas, etcétera y hay interacciones interesantes entre estos, por ejemplo, un paciente puede tener muchos doctores así como un doctor puede tener muchos pacientes.

[05:32] Este tipo de relaciones y mapeamientos lo vamos a ver con Hybernate, por ejemplo. Podemos listar las historias clínicas, podemos listar los pacientes, podemos registrar nuevos pacientes, entonces va a ser un proyecto muy, muy interesante para implementar y por supuesto totalmente fiel a un proyecto que se pueden topar profesionalmente en la vida real. Me ha tocado. ¿Entonces qué dicen? ¿Vamos a comenzar? Nos vemos.