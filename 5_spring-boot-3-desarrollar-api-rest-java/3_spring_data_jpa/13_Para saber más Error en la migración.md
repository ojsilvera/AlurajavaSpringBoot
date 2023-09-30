Como se indicó a lo largo de esta clase, es importante detener siempre el proyecto al crear los archivos de migración, para evitar que Flyway los ejecute antes de tiempo, con el código aún incompleto, lo que podría causar problemas.

Sin embargo, eventualmente puede ocurrir que nos olvidemos de detener el proyecto y se produzca un error al intentar inicializar la aplicación. En este caso, se mostrará el siguiente error al intentar inicializar la aplicación:

Exception encountered during context initialization - cancelling refresh attempt: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'flywayInitializer' defined in class path resource [org/springframework/boot/autoconfigure/flyway/FlywayAutoConfiguration$FlywayConfiguration.class]: Validate failed: Migrations have failed validationCOPIA EL CÓDIGO
Observe en el mensaje de error que se indica que alguna migración falló, lo que impide que el proyecto se inicie correctamente. Este error también puede ocurrir si el código de migración no es válido y contiene algún fragmento de SQL escrito incorrectamente.

Para solucionar este problema será necesario acceder a la base de datos de la aplicación y ejecutar el siguiente comando sql:

delete from flyway_schema_history where success = 0;
COPIA EL CÓDIGO
El comando anterior se usa para eliminar de la tabla Flyway todas las migraciones cuya ejecución falló. Después de eso, simplemente corrija el código de migración y ejecute el proyecto nuevamente.