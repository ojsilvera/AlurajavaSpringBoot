Hemos visto a lo largo de esta clase que podemos inyectar una propiedad declarada en el archivo application.properties en una clase administrada por Spring, usando la anotación @Value.

Suponiendo que el archivo application.properties tiene declarada la siguiente propiedad:

app.test=trueCOPIA EL CÓDIGO
¿Cuál de las siguientes es la forma CORRECTA de inyectarlo en un atributo de una clase administrada por Spring?

Seleccione una alternativa

@Value("{app.test}")


@Value("${app.test}")


@Value("app.test")

