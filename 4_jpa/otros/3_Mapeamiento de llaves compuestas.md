[00:00] En esta parte vamos a hablar de unos recursos de JPA que nos va a permitir hacer referencia a una entidad, a través de llaves compuestas. Entonces, nosotros aquí en la clase de categoría, cuando nosotros queremos obtener una fila, que se encuentra en la base de datos, nosotros utilizamos el Id que corresponde a esa fila.

[00:23] Sin embargo, a veces eso no es suficiente y nosotros queremos identificar esa fila con múltiples elementos, entonces serían llaves compuestas. Para eso esta notación no nos va a servir. Nosotros tenemos que crear una nueva clase que va a contener esos atributos que van a servir de referencia para esa fila en la entidad.

[00:48] Entonces, acá, cuando yo quiero llamar un elemento de la clase categoría, por ejemplo, yo llamo al EntityManager, uso el método find y coloco la clase que quiero instanciar, sería categoria.class. Acá el Id que nosotros colocamos, que es de tipo long, vamos a pasar el número 1, haciendo referencia a que es el primer elemento en la base de datos.

[01:16] Si ya ejecutó esta aplicación, vamos a ver que él realiza un select en la base de datos pasando el Id. Ahora yo quiero crear una llave que sea compuesta con el nombre y una contraseña. Para eso, vamos a generar una nueva clase, se va a llamar categoriaId y la vamos a colocar dentro del paquete modelo.

[01:52] De la misma forma que hicimos con los datos personales, nosotros tenemos que colocar la notación @Embeddable para indicarle a JPA que este no es una nueva tabla, sino que es una clase que va a contener atributo a ser inyectado en una entidad. ¿Y cuáles van a ser esos atributos? El nombre que va a ser del tipo string y una contraseña que también va a ser del tipo string.

[02:24] Vamos a generar los constructores, tanto el default como el constructor con los atributos. Generamos los constructores que son requisitos indispensables de JPA y generamos los getters y setters para esa entidad.

[02:50] Seleccionamos el nombre y la contraseña. Adicional, todos los elementos que sean del tipo embeddable tienen que implementar la interfaz serializable. Ya que son elementos que van a ser serializados en bits para transitar en nuestra aplicación. Entonces, importamos la interfaz serializable y para identificar que son elementos únicos, tenemos que implementar el método hashcode.

[03:28] Entonces, ahora nuestra clase categoriaId nos está reclamando de que no hay un atributo de llave primaria definida. Entonces, vamos a definir nuestra categoriaId como llave primaria a través de la notación @EmbeddedId. Importamos de JPA. Aquí vamos a ver, vamos a guardar, se corrige ese error.

[03:57] Como ya no tenemos el nombre, tenemos que hacer como hicimos para los datos personales en la entidad cliente, hacer categoriaId y vamos a crear una nueva instancia de categoriaId, donde pasamos el nombre y una llave que en esta parte la vamos a colocar como fija pero ustedes pueden colocar acá el atributo contraseña para que sea variable.

[04:28] Como ya no estamos utilizando el id, este método ya no es necesario y vamos a utilizar el método delegate para delegar la responsabilidad de asignar el nombre a la categoría Id. Entonces sería categoriaId.getNombre y de la misma forma para el setter: this.categoriaId.setNombre pasando el nombre como atributo.

[05:03] Aquí tenemos un error. Vamos a ver, nueva CategoriaId. A ver cuál es el error. Aquí, no guardé los elementos acá. Entonces, ya que se guardó, ahora a la hora de nosotros instanciar un elemento en la base de datos, voy a llamar el EntityManager, voy a usar el método find pasando entidad categoría y ahora nuestra llave primaria va a ser el elemento de tipo CategoriaId con el nombre que va a ser “CELULARES” y la contraseña que es 456, como definimos.

[05:57] Importamos y ejecutamos esa aplicación. Vemos que el realizó un select en la entidad categoría, en la tabla categoría donde coincide con el nombre y la contraseña. Para ver qué eso está funcionando, nosotros vamos a asignar ese valor a una variable, la clave, podemos dar como find. Y vamos a realizar un System.out para imprimir ese valor.

[06:40] Entonces sería find, nos da un elemento del tipo categoría y nosotros vamos a imprimir el nombre. Vamos a ver cuál es el retorno de esa aplicación. Y efectivamente, nos está dando un elemento de la entidad categoría con el nombre celulares. Entonces, es importante mencionar que todos los elementos del tipo Embeddable como CategoriaId y datos personales tienen que implementar la interfaz serializable.

[07:19] Importamos acá. Y ya con eso queda culminado todo sobre las clases embutidas.