Proyectos que utilizan Spring Boot generalmente usan el formato jar para empaquetar la aplicación, como se demostró durante esta lección. Sin embargo, Spring Boot brinda soporte para empaquetar la aplicación en formato war, que era ampliamente utilizado en aplicaciones Java antiguas.

Si desea que el build del proyecto empaquete la aplicación en un archivo en formato war, deberá realizar los siguientes cambios:

1) Agregue la etiqueta <packaging>war</packaging> al archivo pom.xml del proyecto, y esta etiqueta debe ser hija de la etiqueta raíz <project>:

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
<modelVersion>4.0.0</modelVersion>
<parent>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-starter-parent</artifactId>
<version>3.0.0</version>
<relativePath/> <!-- lookup parent from repository -->
</parent>
<groupId>med.voll</groupId>
<artifactId>api</artifactId>
<version>0.0.1-SNAPSHOT</version>
<name>api</name>
<packaging>war</packaging>COPIA EL CÓDIGO
2) En el archivo pom.xml, agregue la siguiente dependencia:

<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-tomcat</artifactId>
  <scope>provided</scope>
</dependency>COPIA EL CÓDIGO
3) Cambie la clase principal del proyecto (ApiApplication) para heredar de la clase SpringBootServletInitializer, y sobrescriba el método configure:

@SpringBootApplication
public class ApiApplication extends SpringBootServletInitializer {
@Override
protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
return application.sources(ApiApplication.class);
}
public static void main(String[] args) {
SpringApplication.run(ApiApplication.class, args);
}
}COPIA EL CÓDIGO
¡Listo! Ahora, al realizar el build del proyecto, se generará un archivo con la extensión .war en el directorio target, en lugar del archivo con la extensión .jar.