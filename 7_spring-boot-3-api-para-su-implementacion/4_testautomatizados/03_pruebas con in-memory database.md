Como se mencionó en el video anterior, es posible realizar pruebas de interfaces de repositorio utilizando una base de datos en memoria, como H2, en lugar de utilizar la misma base de datos de la aplicación.

Si desea utilizar esta estrategia para ejecutar las pruebas con una base de datos en memoria, será necesario incluir H2 en el proyecto, agregando la siguiente dependencia en el archivo pom.xml:

<dependency>
  <groupId>com.h2database</groupId>
  <artifactId>h2</artifactId>
  <scope>runtime</scope>
</dependency>
También debe eliminar las anotaciones @AutoConfigureTestDatabase y @ActiveProfiles en la clase de prueba, dejándola solo con la anotación @DataJpaTest:
@DataJpaTest
class MedicoRepositoryTest {
//resto del código permanece igual
}COPIA EL CÓDIGO
También puede eliminar el archivo application-test.properties, ya que Spring Boot realiza la configuración de la URL, el nombre de usuario y la contraseña de la base de datos H2 de manera automática.