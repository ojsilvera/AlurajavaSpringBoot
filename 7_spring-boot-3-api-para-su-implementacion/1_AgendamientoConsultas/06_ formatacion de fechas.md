Como se demostró en el video anterior, Spring tiene un patrón de formato para campos de tipo fecha cuando se asignan a atributos de tipo LocalDateTime. Sin embargo, es posible personalizar este patrón para utilizar otros formatos que prefiramos.

Por ejemplo, imagine que necesitamos recibir la fecha/hora de la consulta en el siguiente formato: dd/mm/yyyy hh:mm. Para que esto sea posible, debemos indicar a Spring que este será el formato en el que se recibirá la fecha/hora en la API, lo que puede hacerse directamente en el DTO utilizando la anotación @JsonFormat:

@NotNull
@Future
@JsonFormat(pattern = "dd/MM/yyyy HH:mm")
LocalDateTime dataCOPIA EL CÓDIGO
En el atributo pattern indicamos el patrón de formato esperado, siguiendo las reglas definidas por el estándar de fechas de Java. Puede encontrar más detalles en esta página del JavaDoc.

Esta anotación también se puede utilizar en las clases DTO que representan la información que devuelve la API, para que el JSON devuelto se formatee de acuerdo con el patrón configurado. Además, no se limita solo a la clase LocalDateTime, sino que también se puede utilizar en atributos de tipo LocalDate y LocalTime.