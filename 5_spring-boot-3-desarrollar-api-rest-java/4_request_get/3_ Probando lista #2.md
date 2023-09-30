[00:00] Y creamos un constructor aquí, que ya lo tengo preparado, que reciba los datos del médico como entidad. Por ejemplo, tengo mi DatosListadoMedico, recibe médico entidad y automáticamente extrae el nombre, la especialidad a String, porque yo aquí le estoy mapeando como un simple string, no como mi enum, el documento y el email.

[00:25] Por lo tanto, ahora vemos que ya compila porque él crea automáticamente un nuevo registro aquí por cada médico que llega de la lista, él lo mapea a un datoListadoMedico, que es mi DTO y lo recolecta todo en una lista, y eso es todo lo que necesito. Guardo aquí, vemos que ya refresca mi servidor y vamos a probar qué tal está esto.

[00:52] Enviamos otra vez la request y ahora ya tenemos aquí los datos ya llegan más restringidos, vemos que solo llegan los cuatro parámetros que yo necesito que lleguen y nada más. Entonces check, tenemos el primer problema resuelto. ¿Qué es lo que falta ahora? Ahora falta la parte de orden. ¿Cómo ordenamos esta lista ascendentemente? Eso es un tema del siguiente video.

