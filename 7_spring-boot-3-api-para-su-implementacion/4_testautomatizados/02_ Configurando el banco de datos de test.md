[00:00] Hola. Recapitulando el aula anterior, nosotros realizamos la documentación para nuestro proyecto, nosotros adaptamos que tenemos el proyecto corriendo en el puerto:8080 y realizamos algunas modificaciones adicionales dentro de nuestra interface, acá nosotros le agregamos alguna descripción, agregamos un título y agrupamos algunos de los elementos por tag.

[00:26] Por ejemplo la consulta está un poco mejor documentada y realizamos otras alteraciones dentro de esta API que nos permite documentar la aplicación. Ahora, de vuelta en la aplicación, vamos a realizar el commit, vamos a enviar este proyecto el repositorio para mantener la versión.

[00:43] Entonces, la versión anterior fue la versión 3, donde realizamos la documentación. Acá tenemos que colocar un mensaje, sería la tercera etapa del proyecto de clínica médica que era referente a la documentación. Acá yo voy a seleccionar todos los elementos que voy a enviar al repositorio que voy a commitar.

[01:13] Y voy a realizar el commit y el push en el repositorio. Entonces está procesando la información. Él detectó algunas advertencias que podríamos revisar y corregirlas, entonces vamos a pasarlas por alto y vamos a enviar esas alteraciones al repositorio.

[01:36] Acá me indica cuáles son los cambios que se están realizando. Yo puedo ver lado a lado las alteraciones que fueron realizadas. Aquí vemos la anotaciones que agregamos para colocar nuevas características dentro de la documentación. Luego de eso voy a realizar el push, todo eso dentro de la interfaz de IntelliJ.

[02:07] Entonces, ahora de vuelta en el proyecto en también yo adicioné un cliente. Utilizando la aplicación de White Flag, entonces nosotros podemos crear las tablas. Podemos alterar alguna tabla de esas o también podemos insertar nuevos elementos.

[02:23] Entonces, ya con la construcción de nuestra base de datos, podemos también traer valores iniciales. Ahora en esta parte, nosotros nos vamos a enfocar en la parte de testes unitarios, de testes automatizadas. Entonces, lo primero que nos viene a la mente es, cuál es la dependencia que vamos a utilizar.

[02:39] Nosotros vamos a utilizar la dependencia de JUnit. Entonces tendríamos que ir al archivo pom donde nosotros agregamos la dependencia, ¿pero cuál es la dependencia que tendríamos que agregar? Entonces, si recordamos en la parte inicial, cuando nosotros creamos el proyecto, nosotros agregamos una dependencia que nos permite realizar los testes unitarios con JUnit, con Mockito y con otras librerías como AssertJ, que permiten realizar el estado del test unitario.

[03:15] Verificar si el resultado es nulo, si el resultado tiene algún valor determinado. Entonces, cuando nosotros realizamos la creación inicial de nuestro proyecto en Spring Initializr la primera dependencia que nosotros estamos recibiendo era la dependencia de los test unitarios que es llamada Spring Boot Starter test.

[03:44] Adicional de la dependencia de Spring, nosotros estamos teniendo una dependencia para realizar los testes unitarios, entonces si nosotros vamos a la aplicación en Maven, entonces, que nosotros deberíamos tener dentro de las dependencias, las aplicaciones que nos permiten realizar los tests unitarios.

[04:03] Entonces acá en sprint test, nosotros vemos que tenemos JUnit, Mockito, tenemos algunas otras aplicaciones para realizar tests en archivos XML, en fin. Ahora vamos a comenzar a realizar los test unitarios, vamos a comenzar por los repositorios, vamos a ir al repositorio de médicos y vamos a revisar el primer método que nosotros encontramos en el repositorio.

[04:31] Entonces, el primer método que nosotros encontramos es findByActivoTrue, que sigue la estructura, el patrón de JPA para repositorio, donde Spring framework se encarga de realizar de forma automática la consulta.

[04:47] Entonces nosotros no necesitamos realizar una validación, ya que automáticamente Spring se encarga de realizar esa validación y en caso alguno de estas palabras claves, por así decirlo, no coincidan con los elementos dentro de las entidades, él va a mandar automáticamente un mensaje de error e impedir que la consulta sea realizada.

[05:12] O en caso de que el error se encuentre en tiempo de ejecución, cuando él intente ejecutar el método, vamos a recibir un error. Entonces el siguiente método que es un candidato a realizar un test automatizado es findActivoById, donde nosotros consultábamos el estatus, el atributo activo del médico a partir del id del médico.

[05:39] Entonces, como este método es bastante simple, no requerimos realizar un test automatizado, sin embargo, podemos dejarlo como como desafío realizar el test automatizado para este método. Entonces, nosotros nos vamos a enfocar en este método donde nosotros realizamos una consulta bastante extensa y nosotros realizamos una consulta, una sub consulta dentro de la consulta.

[06:08] O sea, nosotros tenemos que verificar que los valores que estamos recibiendo a través de esta consulta sean correctos. Adicional, este es un método bastante importante, ya que es el que nos permite seleccionar los médicos dentro de ese intervalo de fecha.

[06:26] Entonces, lo que voy a hacer es seleccionar el método y voy ya acá en refactorar, voy a seleccionar donde dice, acá en generar, disculpen, donde dice generar un test. Entonces, me va a dar una serie de opciones, incluso las librerías que puedo utilizar para realizar el test, en este caso voy a utilizar el texto unitario de JUnit5 y vamos a seleccionar el método que yo deseo testar.

[07:04] Podría seleccionar los otros, pero como ya habíamos mencionado findByActivoTrue es un método que ya es validado por Spring framework. Y findActivoById lo podemos dejar como desafío, pero sin embargo es un método bastante simple para testar.

[07:20] Entonces vamos a seleccionar acá OK y ya de forma automática él nos genera una clase, que se encuentra dentro de los paquetes de test. Entonces vemos que él ya crea automáticamente el nombre de la clase, que sería el médicoRepositoryTest y genera un método, un método de prueba.

[07:44] Si yo intento ejecutar inicialmente este test, esta prueba, vamos a ver qué ocurre. Entonces nosotros vamos a tener que esa prueba pasa automáticamente. Nosotros no estamos realizando ninguna operación dentro de este método de prueba, entonces él va a pasar.

[08:20] Nosotros incluso tenemos un método inicial que es generado en la construcción del proyecto, también como no tenemos nada dentro de él, él debería pasar. Nosotros vamos a eliminar ese test, ya que nosotros no lo estamos usando, método de prueba y lo siguiente que vamos a hacer, como nosotros deseamos testar el repositorio, nosotros necesitamos utilizar una anotación que nos permite testar las capas de persistencia.

[08:52] Entonces, para eso vamos a utilizar la anotación @DataJpaTest que nos va a permitir utilizar algunos métodos, algunas modificaciones relacionadas a lo que sería la capa de persistencia. De esa forma si intento ejecutar esta vez el método de prueba, vamos a ver qué ocurre.

[09:20] Entonces nosotros vemos que esta vez el método falla porque él está buscando dentro de la base de datos en memoria, y como no existe ninguna base por default spring, framework, cuando nosotros colocamos la anotación @DataJpaTest él entiende que nosotros estamos trabajando con una base de datos.

[09:40] Como nosotros no hemos configurado una base de datos externa, él va a entender que la base de datos sería una base de datos en memoria. Y dentro de las bases de datos de memoria en las dependencias yo no configuré ninguna base de datos, algunas bases de datos alternativas, pero serían por ejemplo la base de datos H2.

[10:03] Entonces, como esa base de datos no se encuentra dentro de mis dependencias, yo tendría que ir a Spring Initializr, buscar la dependencia para la base de datos H2, copiar esa dependencia, ir a mi proyecto y actualizar las dependencias.

[10:25] Sin embargo, este no es el método que nosotros vamos a utilizar, sin embargo, vamos a probarlo, vamos a actualizar las dependencias. Y ahora, una vez finalizada las actualizaciones, vamos a ejecutar este método de nuevo. Entonces lo voy a dejar ejecutada la aplicación. Vemos que tenemos un error nuevamente.

[10:48] Y eso se debe a que, a pesar de que nosotros ya tenemos la dependencia para esa base de datos en memoria, nosotros tendríamos que ir y configurar esa nueva base de datos con las configuraciones adecuadas para h2.

[11:04] Entonces, como no es lo que nosotros vamos a utilizar para este caso, una base de datos de memoria sino una base de datos externa, voy a remover esa base de datos o vamos a dejar esa base de datos, más adelante voy a dejar una indicación.

[11:21] Y lo que tendríamos que hacer es indicarle cuál es la base de datos que nosotros vamos a utilizar dentro de nuestros tests. Entonces, lo que yo quiero utilizar es utilizar una base de datos externa. Para eso voy a colocar la anotación @AutoConfigureTestDatabase.

[11:42] Dentro de esa anotación yo voy a colocar replace = @AutoConfiguredTestDatabase.Replace.NONE. Entonces, con esto yo le estoy indicando que la base de datos que yo voy a utilizar va a ser una base de datos externa y que no voy a reemplazar la base de datos que estoy utilizando previamente.

[12:10] Entonces, esa forma, si yo ejecuto de esta vez mi aplicación, ya le estoy indicando que no quiero utilizar la base de datos en memoria h2, que vamos a instalar, sino una base de datos externa. Entonces vemos que ahora si pasan nuestras pruebas, nuestros tests, porque yo he configurado para utilizar la base de datos que nosotros tenemos en MySQL.

[12:41] Sin embargo, cuando nosotros estamos utilizando base de datos de prueba, tenemos que separar la base de datos de producción de la base de datos de book o para prueba, ya que podemos tener conflictos y precisamente la base de prueba es para realizar diferentes tests que pueden tener valores equivocados o valores que podemos incluso borrar la base de datos.

[13:05] Y eso no lo queremos hacer con la base de datos real. Entonces, para nosotros configurar la base de datos de prueba, lo que tenemos que hacer es crear otro archivo, entonces, acá nosotros configuramos la base de datos, la base de datos real, la base de datos de producción, indicando la ruta, el usuario y la contraseña.

[13:30] Lo que vamos a hacer es copiar este archivo donde dice copiar. Vamos a pegar también acá y la diferencia va a ser que vamos a cambiar acá el nombre de application por application trazo test. Entonces ese patrón se tiene que cumplir el trazo y el nombre que quieren colocarle al nuevo perfil de propiedades.

[13:59] Entonces todos pueden aquí tener diversos perfiles, application-testimonio, application-production. En este caso vamos a utilizar el perfil de test. Para los que están utilizando la configuración anterior van a tener algo de este tipo. Va a tener aplication-testimonio.properties.

[14:28] Y la configuración va a ser la misma que nosotros venimos realizando en proyectos anteriores. Entonces acá yo creo que tengo un ejemplo, vamos a continuar utilizando este padrón, entonces para los que están utilizando este formato que es el formato jam, vamos a escribirlo de esta forma y para los que están utilizando el formato antiguo se escribe de forma lineal. Voy a dejar los dos.

[14:54] El formato que voy a dejar acá, voy a eliminar este archivo por ahora y vamos a mantener con el archivo del perfil de test. Acá voy a eliminar lo que no estoy utilizando, solamente voy a dejar la información para la base de datos. Acá vamos a sustituir este nombre de vollmed_api por vollmed_api_test.

[15:23] Y acá ahora en la clase de repositorio de prueba, tengo que modificar, indicarle cuál va a ser el perfil que estamos utilizando. Entonces aquí tenemos que utilizar la actuación @ActiveProfiles(“test”). Entonces de esa forma nosotros vamos a recapitular. Tenemos la anotación @DataJpaTest con la que nosotros le indicamos que vamos a estar trabajando con persistencia de base de datos.

[15:54] Es decir, la tiene que buscar dentro de una alguna de las bases de datos que esté utilizando y todo eso lo va a realizar con configuraciones internas de Spring. Lo segundo es colocar la anotación @AutoConfigureTestDatabase para realizar nuestras operaciones con una base de datos externa e indicarle que no vamos a reemplazar la base de datos que estamos utilizando.

[16:19] Y la tercera es indicarle cuál va a ser el perfil que vamos a utilizar. Entonces en este caso nosotros vamos a utilizar el perfil de test, donde estamos configurando una base de datos de prueba nueva. Acá vamos a intentar ejecutar esta aplicación para ver si de hecho consigue esa base de datos. Vamos a ver qué ocurre.

[16:45] Entonces nos ha generado un error, vamos a ver cuál es ese error. Él indica aquí lo siguiente, que la base de prueba vollmed_api_test no se encuentra, es desconocida. Entonces acá vamos a aplicar lo que yo tengo previamente copiado, una alternativa que nos va a permitir crear la base de datos de forma automática.

[17:17] Entonces, dentro de la configuración de la ruta, yo voy a colocar este patrón que va a indicarle al archivo que si no encuentra la base de datos, que la cree con la zona de horario determinada. Entonces vamos a ejecutarla de nuevo. Y ahora, una vez que ha finalizado de cargar la información, vemos que esta es sí pasa la prueba.

[17:41] Entonces ahora encontró la base de datos dentro de esta ruta y si nosotros quisiéramos utilizar la base de datos de memoria, voy a dejar acá una información. Es para saber más. Luego de haber configurado la dependencia, nosotros tenemos que colocar esta ruta. Entonces la ruta sería la base de datos de memoria con el nombre men:testdb.

[18:08] Tendríamos que usar el driver de la base de datos h2, el usuario por default es so y la contraseña por default también es password. Entonces este sería la información que ustedes necesitarían en caso de configurar la base de datos de memoria y recordando que si van a utilizar la base de datos de memoria dentro del repositorio de médicos, tenemos que eliminar de acá esta notación.

[18:36] Entonces, esta fue la configuración inicial. En la siguiente parte vamos a comenzar a construir nuestras pruebas para el repositorio de media.