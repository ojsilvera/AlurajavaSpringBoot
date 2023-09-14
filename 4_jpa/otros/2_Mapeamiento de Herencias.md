[00:00] Hola, en esta parte vamos a hablar sobre otro concepto, que es el concepto de herencia, y vamos a suponer que nosotros vamos a crear dos nuevas entidades que van a contener los mismos elementos, los mismos atributos y propiedades de la entidad producto.

[00:17] Entonces acá vamos de construir la entidad electrónico y la entidad libros, que va a tener tanto el nombre, descripción, precio y fecha de registro como la marca y modelo para electrónico y el autor y el número de páginas para los libros.

[00:34] En nuestra aplicación para realizar eso, nosotros vamos a crear dos nuevas clases que van a ser la clase libros y vamos a crear la clase electrónico. Y estas nuevas clases van a representar entidades en nuestra base de datos. Adicional, estas clases, estas nuevas entidades van a tener los mismos atributos y propiedades que la entidad producto.

[01:06] Eso lo vamos a lograr a través del concepto de herencia. Entonces, tanto libros como electrónicos tienen que extender de producto. Nosotros sabemos que para heredar propiedades se usa la palabra extends. Entendemos de una clase madre que en este caso sería producto.

[01:31] Como estas clases también van a representar a entidades, tenemos que colocar la notación @Entity y para modificar el nombre podemos usar la notación @Table con el parámetro name=”electrónicos”. Vas a colocar los atributos, los nuevos atributos para esta entidad que son la marca de tipo string y el modelo que también es de tipo string.

[02:09] Sabemos que es bastante simple, es el mismo concepto de entidades, simplemente estamos agregando la palabra extends para heredar los atributos de la entidad producto. De la misma forma, colocamos los constructores default. Y el constructor, con todos los atributos así como los getters y setters para esta clase.

[02:42] Seleccionamos todos los getters y setters, vamos a remover super y guardamos la clase electrónico. Acá vamos a colocar únicamente la notación @Entity. Y vamos a colocar los atributos son private, el autor es el tipo string. Y va a tener un número de páginas que hacer del tipo entero.

[03:23] Colocamos los constructores. Constructor default, colocamos el constructor con todos los atributos y los getters y setters para esa entidad. Importamos la entidad de JPA. Ya con eso tenemos configurada nuestra entidad libro y la entidad electrónico. Para conectar eso, esa entidad con la entidad producto, tenemos que utilizar una notación en la entidad producto que se llama @Inheritance.

[04:07] Con la estrategia de herencia (Strategy=InheritanceType) y aquí le vamos a decir cómo vamos a heredar: si va a ser una única tabla o si va a ser tabla separada. Inicialmente vamos a construir una única tabla, aquí sería todo en minúscula y ya con eso queda configurada nuestra entidad producto y la entidad de libro electrónico.

[04:50] Para ver cómo es la construcción, vamos a ejecutar la tabla de PruebaDeDesempeño y ver qué se está creando en la consola. Entonces para single table yo tengo lo siguiente. Tengo que está creando un producto que tiene los siguientes atributos, el ID, la descripción, la fechaDeRegistro, nombre, precio, marca y modelo vienen de electrónico, autor y número de páginas vienen de los libros, la categoría y la llave primaria.

[05:22] Ahí sí vamos a tener un nueva atributo que nos va a decir de dónde estamos instanciando, si es de libros o si es de electrónico. Entonces, cuando nosotros usamos la estrategia InheritanceType, nosotros creamos una única tabla con todos los atributos. Se vería de esta. Esto ayuda en el desempeño, el rendimiento de nuestra aplicación es más rápido.

[05:53] La única desventaja es que nosotros vamos a tener una gran cantidad de elementos en una única tabla. Eso puede llegar a ser confuso. La otra estrategia que nosotros podemos usar para heredar entidades es Join.

[06:15] Entonces con la estrategia de Join, nosotros vamos a construir tablas separadas. De esta forma disminuye el desempeño un poco más lento a la hora de realizar la carga. Pero tenemos todos los elementos de forma más organizada y vamos a tener llaves extranjeras que dentro de las entidades libros y electrónicos identifican esa llave primaria en la entidad producto.

[06:49] Entonces nosotros podemos escoger desempeño, utilizando la estrategia single table para tener valores más rápidos. O podemos obtener un mayor orden y separar las entidades con la notación @JoinTable. Entonces, vamos a ver esa segunda anotación para ver cuál es el comportamiento.

[07:12] Vamos a ejecutarlo. Entonces, vemos lo siguiente. Él creó la tabla electrónicos, que tiene un modelo, una marca y tiene su id, que son heredadas de la entidad producto. Así como tenemos la entidad libros, recordando que nosotros no colocamos el nombre, sino que este nombre es el mismo nombre de la entidad.

[07:42] Nosotros no colocamos table, name, libros, sino él tomó el nombre completo de la entidad libros. Y para producto simplemente coloco los valores de descripción, fecha de registro, nombre, el precio y la categoría. Entonces nosotros podemos escoger entre desempeño o utilizar los join, pero nos dan esa distribución entre entidades.