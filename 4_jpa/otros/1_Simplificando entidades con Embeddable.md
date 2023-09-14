[00:00] Hola. En esta parte vamos a hablar sobre otros recursos de JPA. Acá tenemos la clase cliente, donde vemos que tenemos los atributos nombre y de identidad. Adicional, los clientes pueden tener datos de dirección como la calle, la ciudad, el estado, el país donde vive, puede tener datos familiares, como el nombre de la madre, el nombre del padre, nombre de hermano y datos telefónicos como código de área, número de teléfono, número de teléfono celular.

[00:33] Así que estos atributos pueden llegar a ser bastante extensos. Podemos llegar a tener 10, 20, 50 atributos dependiendo de nuestra entidad. Entonces, una forma de organizar nuestro código es crear otra entidad, otra clase donde almacenemos esos atributos sin necesidad de generar una nueva tabla en la base de datos.

[00:56] Vamos a generar una nueva clase, una nueva entidad, una nueva clase que va a ser inyectada dentro de la clase cliente conteniendo esos atributos adicionales. Entonces vamos a hacer eso, vamos a crear una nueva clase que la vamos a llamar datos personales.

[01:16] Dentro de la clase datos personales vamos a colocar el nombre y la identidad. Nosotros, si tuviéramos más atributos, tendríamos que colocar el restante de los atributos e identificar esa clase con los atributos a los que pertenece. O sea, los datos de dirección, datos telefónicos o datos familiar.

[01:40] En esa clase vamos a colocar los getters y los setters como hemos hecho con otras clases, seleccionamos y generamos tanto el constructor default como el constructor con todos los atributos. Constructor default, vamos a constructor sin atributos, lo seleccionamos.

[02:08] Vamos a ver, vamos a eliminar acá. Y ya de esa forma queda creada nuestra clase, ahora necesitamos indicarle a JPA que esta clase va a ser inyectada dentro de la clase cliente, que puede ser una clase que puede ser inyectada dentro de la clase cliente.

[02:33] Entonces para eso vamos a utilizar la notación @Embedable de JPA. Entonces, importamos la librería y para conectarla con la clase cliente tenemos que agregar ese nuevo atributo que va a ser del tipo DatosPersonales. Pero ese atributo no es una entidad ni es un dato primitivo sino que es una clase propia.

[03:11] Entonces vamos a conectar esta clase que puede ser embutida con la clase cliente a través de la notación @Embedded. De esta forma, estamos indicando a JPA que esta clase, que esta clase de datos personales está siendo inyectada dentro del atributo datos personales. De esa forma, nosotros no creamos una nueva tabla, sino que simplemente estamos colocando los atributos de esa clase dentro de esta clase.

[03:48] Vamos viendo que ahora estamos generando un error dentro del constructor de cliente. Vamos a reemplazar esos atributos por datosPersonales y creamos una nueva instancia de datosPersonales pasando el nombre y el DNI. En los getters y los setters para la clase cliente vamos a crear el método delegue, vamos a delegar la responsabilidad de generar el nombre para el atributo de datos personales.

[04:25] Entonces sería datosPersonales.getNombre. Por eso el método se llama delegate, porque nosotros delegamos la responsabilidad de generar el nombre a otra clase que se encuentra inyectada dentro de la clase cliente. De la misma forma, con la identidad, vamos a llamar a datosPersonales y obtenemos el DNI.

[04:57] Para el nombre para los setters es bastante similar, el this.datosPersonales.setNombre y pasamos el nombre como atributo. Y para el Dni hacemos lo mismo: this.datosPersonales.setDni pasando el Dni como atributo. Las guardamos acá y se corrigen todos los errores de la clase cliente.

[05:31] Nosotros teníamos en la clase de pruebaDeDesempeño, un cliente que fue instanciado, pedido con cliente. Vamos a ver si él continúa funcionando. Efectivamente, está trayendo un elemento, el elemento nombre de la clase cliente. Estamos usando el getter y la clase cliente continúa funcionando correctamente. Entonces, en la siguiente parte nosotros vamos a ver el mapeamiento de herencias.