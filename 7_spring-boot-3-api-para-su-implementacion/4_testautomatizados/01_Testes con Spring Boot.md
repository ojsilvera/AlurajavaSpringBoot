[00:00] Hola. En la parte anterior nosotros realizamos lo que sería la documentación para nuestro proyecto de clínica médica. Aplicamos springdoc de OpenAPI y vimos que teníamos una interfaz de usuario similar a Postman donde realizamos también unas ciertas pruebas similares a las que fueron hechas para la consulta del paciente.

[00:24] Entonces, ahora el foco de este proyecto no es la parte de test automatizado, pero vamos a ver cómo funcionan los tests automatizados dentro del contexto de Spring Framework. Nosotros tenemos dos tipos de pruebas, tenemos las pruebas de caja negra, que fueron las que nosotros realizamos en Postman y tenemos también las que realizamos con swagger en la documentación de springdoc.

[00:51] También tenemos las pruebas de caja blanca, que son pruebas más enfocadas a las que vamos a cerrar ahora dentro de los testes automatizados, que son pruebas donde nosotros tenemos acceso a la configuración interna, entonces en las pruebas de caja negra nosotros vamos a imaginar que tenemos una caja negra donde simplemente realizamos una acción y nosotros vamos a recibir una acción de retorno.

[01:13] Nosotros no vamos a tener acceso a las configuraciones internas de esa caja. En las pruebas de caja blanca, si nosotros tenemos un acceso, tenemos más control sobre qué está haciendo realizado. Entonces, dentro de la estructura de nuestro proyecto, nosotros tenemos los controladores.

[01:33] Tenemos la parte de los servicios que fueron todas las validaciones y tenemos lo que serían los repositorios. Dentro de los repositorios hay un conjunto de elementos que ya han sido aprobados por el Spring framework, como es el método findByActivoTrue, findById, findAll.

[01:51] Entonces, todos esos métodos ya han sido probados, nosotros nos vamos a enfocar en cómo probar estas consultas que nosotros agregamos dentro del repositorio, que fueron consultas manuales y vamos a probar esta consulta simulando un conjunto de datos y configurando un banco de datos de prueba.

[02:12] Otro candidato a las pruebas, a realizar testes automatizados, serían las validaciones, ya que en las validaciones nosotros podemos verificar las reglas de negocio, verificar que se estén cumpliendo, el tiempo en el que se están realizando y que los datos que estamos enviando y recibiendo sean correctos.

[02:34] Sin embargo, por ser bastante simple, por no tener elementos tan complejos, nosotros vamos a dejar estas validaciones del lado. Vamos a enfocar en los repositorios y nos vamos a enfocar también en los controladores.

[02:47] Entonces vamos a ver cómo utilizando algunas librerías como Mockito y JUnit nosotros podemos probar, los controladores de la consulta o de médico y verificar que los estados que estemos recibiendo, los parámetros, el valor de los parámetros, así como nosotros realizamos acá, nosotros estamos recibiendo un tipo de parámetro que es el tipo de string que los parámetros que estamos enviando en total sean la cantidad de parámetros correctos.

[03:20] Así como el estado que nosotros recibimos cuando hacemos la petición, en este caso nosotros estamos recibiendo un Estado 403, ya que nosotros no tenemos el acceso al token, entonces tenemos que verificar ese retorno en el punto de entrada a la aplicación y punto de conexión con aplicaciones externas.

[03:43] Entonces el foco de esta parte es lo que sería los testes automatizados dentro del contexto de Spring framework. En la siguiente parte nosotros vamos a configurar nuestro ambiente de prueba, todo lo que serían las configuraciones iniciales, y luego vamos a comenzar a testar lo que sería nuestros repositorios, que todas esas consultas que nosotros realizamos manualmente estén trayendo los datos correctos.