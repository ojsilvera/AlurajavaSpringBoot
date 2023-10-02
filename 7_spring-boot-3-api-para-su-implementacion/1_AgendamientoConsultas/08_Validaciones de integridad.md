[00:00] Hola. En el video anterior nosotros comenzamos a construir nuestro método de agendar, que es el que nos va a permitir agregar nuevos elementos en la base de datos.

[00:07] Dentro de ese método nosotros estamos recibiendo los datos con el ID del paciente, el ID del médico y la fecha con hora de la consulta. Sin embargo, nosotros tenemos que verificar que esos datos que estamos recibiendo en nuestro proyecto sean válidos.

[00:24] Si esos elementos son nulos o no se encuentran en la base de datos, nosotros tenemos que enviar un mensaje de error al elemento que esté consumiendo nuestra API. Puede ser el front end o puede ser directamente alguna otra API. Entonces, para eso yo voy a construir una serie de validaciones de integridad, a partir de la construcción de algunos if.

[00:49] Entonces, el primer elemento que tengo que checar es el ID del paciente. Para eso tengo que comunicarme con la base de datos a través del pacienteRepository y vamos a usar primero el findById que me retorna un optional. En ese option voy a pasar el ID del paciente.

[01:06] Y ese optional tiene algunas opciones como es el get, que me retorna un elemento del tipo paciente y tiene isPresent que retorna un evento booleano, que es true en caso de que sea encontrado y falso en caso de que no haya sido encontrado.

[01:22] Voy a usar ese método. Entonces, en caso de que no haya sido encontrado el ID del paciente en la base de datos y voy a arrojar una nueva sección, entonces yo tengo algunas excepciones que ya fueron prediseñadas, sin embargo, acabamos de mostrar cómo crear una excepción que puede seguir reglas de negocio un poco diferentes.

[01:44] Entonces vamos a llamar esta excepción validaciónDeIntegridad. Dentro de ella vamos a enviar un mensaje que se llama “id de paciente”. Vamos a colocar esto mejor. “Este id para el paciente no fue encontrado”. Entonces tenemos que crear esa nueva excepción, vamos a apretar al enter y vamos a crearla en el infra en la parte de error. Pueden colocarla en una clase de excepciones y lo voy a colocar en este paquete.

[02:33] Entonces esa clase de validación de integridad está extendiendo, está heredando de la clase throwable. Entonces nosotros tenemos la clase throwable y tenemos la clase RunTimeException. La diferencia entre una y otra es que la clase throwable responde ante errores y excepciones, y RunTimeException solo responde ante excepciones.

[02:55] Cuando nosotros usamos el Throwable, tenemos que agregar dentro del método un throw. Entonces, ahora, acá en este constructor, déjame mostrar ese throwable. Entonces, si coloco acá, voy a enviar ese mensaje a la clase madre utilizando la palabra super. Y acá vamos a ver lo que estoy diciendo del throwable.

[03:28] Entonces, aquí si vemos me dice que tengo que agregar el throw dentro del método. Para evitar eso, como nosotros no vamos a responder a errores, vamos a cambiar el throwable por RunTimeException. Y de esa forma queda, no necesitamos agregar el throw. Sin embargo, es importante recordar que en caso de que queramos responder a errores, podemos usar el throwable.

[03:55] Entonces ya con esto realizamos la validación de integridad para el paciente. Ahora, en las tarjetas de Trello, nosotros tenemos lo siguiente en caso de que la elección del médico es opcional y en caso de no se encuentre, el sistema de elegir aleatoriamente un médico que se encuentre disponible para la fecha y hora de ingresar.

[04:18] Entonces esto no quiere decir que el ID del médico puede ser nulo o puede que en caso de que sea ingresado y no existe en la base de datos, él va a buscar médico que corresponda a las necesidades de ese paciente. Entonces, de vuelta en el proyecto, nosotros tenemos que colocar esas condiciones.

[04:40] Vamos a agregar un if indicando primero que los datos, el ID del médico tiene que ser diferente de nulo. En caso de que sea nulo, yo puedo continuar y buscar un médico dentro de la base de datos. Y la segunda condición es que en la base de datos de médicoRepository vamos a usar ahora directamente el método existsById.

[05:12] La diferencia entre este y el findById es que el findById retorna un optional. Nosotros del opcional usamos el método isPresent. Acá directamente estamos usando datos de ID médicos que me retornan un booleano. En caso que es true en caso de que se encuentren y es falso en caso de que no se encuentren.

[05:32] Caso de que no se encuentren vamos a retornar una excepción y este ID para el médico no fue encontrado. Ahora nosotros habíamos colocado acá que en caso de que nosotros estuviésemos recibiendo el ID del médico, lo buscábamos en la base de datos con el optional y lo teníamos con el get.

[05:56] Ahora vamos a modificar esto un poco y vamos a colocar acá un método que se va a llamar escogerMedico o seleccionarMedico. Acá vamos a colocar los datos. Entonces ahora vamos con “Alt + enter”, vamos a crear ese método dentro de nuestra clase.

[06:24] Y ahora, en la siguiente parte, nosotros vamos, acá estamos recibiendo un error, nosotros tenemos que retornar acá un médico, y por ahora vamos a retornar null. En la siguiente parte, nosotros vamos a ver el cuerpo de este método que nos va a permitir crear el algoritmo para seleccionar un médico que sea aleatorio y que se encuentre disponible en la fecha y que atienda las necesidades de ese paciente.