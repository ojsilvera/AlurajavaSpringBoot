Lo ideal sería proporcionar documentación para que los equipos puedan leer y entender cómo funciona el back-end y construir sus soluciones integradas correctamente.

No lo haremos manualmente para enviarlo como un PDF, por ejemplo, porque es laborioso y, si tenemos algún cambio en la API, tendríamos que actualizar constantemente el documento.

Es decir, nuestra idea es usar alguna herramienta que lo haga de forma automatizada, y existen varias que pueden leer el código de la aplicación del back-end para ponerlo a disposición de los equipos de front-end y móviles, que aún pueden usar automatizaciones en la integración.

En nuestro caso, como estamos usando Java con Spring Boot, tendremos que usar una herramienta compatible, que será SpringDoc. En el navegador, buscaremos "springdoc" para buscar la biblioteca y entender cómo funciona. Como resultado, encontraremos la documentación de SpringDoc en este enlace https://springdoc.org/.

En la página, tendremos explicaciones sobre lo que es, cómo funciona y cómo aplicar la biblioteca en el proyecto. En la sección "Introduction" o introducción, tendremos más información sobre las tecnologías involucradas que soporta, conteniendo una parte destacada por una alerta de "importante":

Para soporte de spring-boot v3, asegúrese de usar springdoc-openapi v2 https://springdoc.org/v2/

Es decir, si estamos usando spring-boot en la versión 3, se recomienda usar la versión 2 de springdoc-openapi, que es nuestro caso.

Haciendo clic en el enlace de springdoc-openapi v2 aquí, tendremos la documentación según la versión correcta que necesitaremos.

Más adelante, tendremos la sección "Getting Started" o "Dando inicio" en portugués, donde tenemos las instrucciones para usar la biblioteca, comenzando con la descarga de la dependencia de Maven con el siguiente código:

<dependency>
  <groupId>org.springdoc</groupId>
  <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
  <version>2.0.2</version>
</dependency>COPIA EL CÓDIGO
Copiaremos el bloque y lo agregaremos a nuestro proyecto.

Abriendo IntelliJ, abriremos el archivo pom.xml y navegaremos hasta la última dependencia que es la de java-jwt para pegar el código a continuación antes del cierre de </dependencies>.

<dependency>
    <groupId>com.auth0</groupId>
    <artifactId>java-jwt</artifactId>
    <version>4.2.1</version>
</dependency>

<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
        <version>2.0.2</version>
</dependency>COPIA EL CÓDIGO
Guardaremos y habremos descargado la biblioteca. Cada vez que incluyamos una nueva, es interesante detener el proyecto haciendo clic en el icono "pausa" representado por un cuadrado rojo en la esquina superior derecha de la pantalla, y luego hacer clic en la pestaña central "Maven" en el extremo derecho. Ampliándolo, seleccionaremos "Dependencies" y luego, en la esquina superior izquierda de esta pestaña, haremos clic en el icono "reload" representado por dos flechas circulares para recargar las dependencias y ver si se descargaron correctamente al final de la lista. Para usar la biblioteca, volveremos a la documentación y, justo después del bloque de código, nos dice que al instalar la dependencia en el proyecto, se crearán dos direcciones en la API: http://server:port/context-path/swagger-ui.html y http://server:port/context-path/v3/api-docs. El primero es una documentación en una página web que podemos navegar y hacer pruebas, similar a lo que hacemos en Postman. La segunda URL genera un JSON con la documentación, y podemos usar herramientas que automatizan la creación del cliente de esta API basado en este JSON. Sin embargo, como estamos usando Spring Security, por defecto bloquea todas las URLs que tenemos en el proyecto, y necesitaremos estar logeados para acceder a ellas, excepto la URL de inicio de sesión. En este caso, queremos que ambas URL sean públicas y estén disponibles sin necesidad de iniciar sesión. Haremos esta configuración en el proyecto. Abriendo IntelliJ, cerraremos el pom.xml y abriremos "src > main > java", y en el paquete med.voll.api, accederemos a "infra > security" y abriremos la clase SecurityConfigurations.java que contiene las configuraciones de seguridad del proyecto. En el método securityFilterChain() donde configuramos las URLs del proyecto, encontraremos la línea de requestMatchers() con .permitAll() que permite la URL de inicio de sesión. Al copiarlos, abriremos una nueva línea debajo y colocaremos las dos direcciones, eliminando el método HttpMethod.POST de los paréntesis de la copia, ya que en este caso la URL será para cualquier método, no necesitaremos filtrar por esto. Cambiaremos la URL a /v3/api-docs seguida de /** con los subdirecciones que también deben ser liberadas. Después de cerrar las comillas de la cadena, colocaremos otra en la misma línea con la segunda URL "/swagger-ui.html" en la documentación. También hay otra dirección de Swagger, que es la página HTML que tiene algunos CSS y JavaScript que deben descargarse para cargar la página correctamente. Entonces escribiremos "/swagger-ui/**" para que lo que está después de esta dirección sea liberado.

//código omitido

@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    return http.csrf().disable()
        .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS)
        .and().authorizeHttpRequests()
        .requestMatchers(HttpMethod.POST, "/login").permitAll()
        .requestMatchers("/v3/api-docs/**", "/swagger-ui.html", "/swagger-ui/**").permitAll()
        .anyRequest().authenticated()
        .and().addFilterBefore(securityFilter, UsernamePasswordAuthenticationFilter.class)
        .build();
}
//código omitidoCOPIA EL CÓDIGO
De esta forma, guardaremos y tendremos las tres direcciones que necesitaremos dejar públicas para acceder a la documentación generada por SpringDoc.

Ejecutaremos el proyecto haciendo clic en el icono de "play" representado por un triángulo verde en la esquina superior derecha de la pantalla y veremos si aparece algún error.

Si se inicia correctamente, accederemos a la documentación directamente desde el navegador. En el navegador, abrimos una nueva pestaña, accederemos a la dirección de nuestro proyecto "localhost:8080/v3/api-docs" para ver la respuesta.

Recibiremos un JSON que describe todos los endpoints de nuestra API. En el tema llamado paths: en la lista lateral izquierda, tendremos cada uno de ellos.

"Detrás de escena", la biblioteca y los controladores, los métodos y toda la información se utilizan para crear un JSON que describe las funcionalidades.

Este documento de API puede ser utilizado por equipos y clientes para automatizar la generación del código que consumirá la API.

En una nueva pestaña del navegador, accederemos a "localhost:8080/swagger-ui/index.html" y abriremos la versión web como un sitio que representa la API.

Es lo mismo que el JSON, pero en una página HTML más agradable y organizada, de modo que más personas puedan comprenderlo fácilmente.

Ya hemos generado la documentación, pero aún no podemos "disparar" la solicitud enviando el encabezado con el token JWT.

Deberemos crear un @Bean con la configuración y anotar los métodos y controladores que queremos proteger con el encabezado bearer. Crearemos una clase de configuración de estructura que recibirá el código proporcionado.

En este nuevo paquete, crearemos una nueva clase Java llamada "SpringDocConfigurations" para contener las configuraciones de SpringDoc.

public class SpingDocConfigurations {
}COPIA EL CÓDIGO
Es una clase Java desconocida, por lo que no podemos cargarla.

Crearemos una anotación @Configuration para dejar claro que la clase hará configuraciones. Dentro de ella, pegaremos el código que copiamos de la documentación.

@Configuration
public class SpingDocConfigurations {

    @Bean
     public OpenAPI customOpenAPI() {
         return new OpenAPI()
                        .components(new Components()
                            .addSecuritySchemes("bearer-key",
                            new SecurityScheme().type(SecurityScheme.Type.HTTP).scheme("bearer").bearerFormat("JWT")));
    }
}
COPIA EL CÓDIGO
Este método está exponiendo el objeto @Bean del tipo OpenAPI que será cargado por SpringDoc y seguirá las configuraciones definidas.

Después de instanciar OpenAPI, llamamos al método que configura componentes que contiene .addSecuritySchemes() pasando el parámetro "bearer-key" y especificando que es del protocolo HTTP del esquema "bearer" en formato "JWT".

Por lo tanto, es una configuración de acuerdo con la biblioteca, que contiene un encabezado para pasar la clave del token. Pero todavía no hemos dicho qué controladores también necesitamos pasar.

Volviendo a la documentación, veremos que hay @Operation() en la que vamos a la operación donde queremos restringir y colocamos la anotación @SecurityRequirement(name = "bearer-key").

La copiaremos y volveremos a IntelliJ para colocar la anotación en los controladores.

Abriendo el paquete de controladores, accederemos a PacienteController.java y la colocaremos encima de un método para hacerlo restringido.

Si todos lo son, para evitar mucha repetición en cada uno, podemos colocar la anotación encima de la clase para que se considere que todos los métodos necesitan "bearer-key".

En el caso de PacienteController, todos los métodos deben tener autenticación.

@RestController
@RequestMapping("pacientes")
@SecurityRequirement(name = "bearer-key")
public class PacienteController {

//código omitido
}
COPIA EL CÓDIGO
//código omitido

@RestController
@RequestMapping("medicos")
@SecurityRequirement(name = "bearer-key")
public class MedicoController {

//código omitido
}
COPIA EL CÓDIGO
//código omitido

@RestController
@RequestMapping("consultas")
@SecurityRequirement(name = "bearer-key")
public class ConsultaController {

//código omitido
}COPIA EL CÓDIGO
No haremos esto en AutenticationController.java porque no tiene token, ya que es el controlador para iniciar sesión. Notaremos que en autenticacao-controller no hay un ícono de candado porque no hay un encabezado en el token. Ejecutaremos nuevamente la solicitud de inicio de sesión haciendo clic en "Try Out". Pasaremos "maria@voll.med" y la contraseña 123456 que ya tenemos registrada. Haciendo clic en el botón azul "Execute", ejecutaremos y enviaremos la solicitud. Copiaremos el valor del token que aparece en el cuerpo de la respuesta y lo pegaremos en el ícono de candado de "/pacientes" en paciente-controller. También podemos hacer clic en el botón "Authorize" en la esquina superior derecha encima de paciente-controller, antes de todas las solicitudes. Al completar y guardar el campo "value", guardaremos el token y, en la solicitud GET de "/pacientes", haremos clic en "Try Out" y no tendremos que ingresar el token nuevamente, ya que ya está guardado y se enviará automáticamente por Swagger.

{
"page": 0,
"size": 20
}COPIA EL CÓDIGO
Al hacer clic en "Execute", veremos que devuelve el código 200 con todos los pacientes registrados en la base de datos.