Traducido del inglés, la palabra Autowired sería ''un cable automático''. En el contexto del framework Spring, que utiliza como una de sus bases el patrón de diseño “Inyección de Dependencias”, la idea sirve para definir una inyección automática en un determinado componente del proyecto Spring, ese componente puede ser atributos, métodos e incluso constructores.

Esta anotación se permite con la ayuda de la anotación @SpringBootApplication, en el archivo de configuración de Spring, disponible cada vez que se crea un proyecto Spring.

Al marcar un componente con la anotación @Autowired le estamos diciendo a Spring que el componente es un punto donde se debe inyectar una dependencia, en otras palabras, el componente se inyecta en la clase que lo posee, estableciendo una colaboración entre componentes.

Para más información sobre la anotación, echa un vistazo a la documentación oficial: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/annotation/Autowired.html