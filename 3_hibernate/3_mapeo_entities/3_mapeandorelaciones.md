[00:00] Hola. En el video anterior, nosotros hicimos el mapeamento para las dos nuevas propiedades que se agregaron en la clase producto. Nosotros agregamos el atributo fecha de registro y el atributo categoría y dentro de esta categoría nosotros teníamos tres elementos que eran SOFTWARE, los LIBROS y los CELULARES.

[00:19] Sin embargo, estos elementos eran limitados dentro de una clase del tipo de enumerador. Esto presenta el problema de que si el cliente quisiera agregar nuevas categorías o eliminar alguna de esas categorías existentes, él va a tener que llamar de nuevo a los desarrolladores, gastar de nuevo en recursos y hacer un nuevo deploy. Eso va a representar también una pérdida de tiempo.

[00:44] Entonces para darle más flexibilidad al proyecto nosotros vamos a eliminar ese numerador y vamos a crear una nueva entidad que va a ser la entidad categoría, lo que nos va a permitir guardar esta elemento de la categoría en la base de datos y permitir que el cliente almacene diversos elementos dentro de la categoría.

[01:07] Entonces ahora si nosotros vemos el diagrama, nosotros vamos a tener la tabla productos y vamos a tener la tabla categoría. Y entre esas dos tablas va a existir una relación. Esos elementos van a estar relacionados por el id, por el identificador, ya que vamos a tener el id para la tabla productos, vamos a tener el id para la tabla categoría.

[01:29] Dentro de la tabla producto, nosotros ahora vamos a tener el id de esa categoría lo que vamos a llamar una llave extranjera. Es que es el identificador que se encuentra dentro de la tabla de categoría. Entonces nosotros vamos a tener nuestra tabla producto con los atributos, id, nombre, descripción precio y el id de la categoría además de la fecha de registro.

[01:54] Entonces siempre que nosotros tenemos la relación entre dos entidades o dos tablas nosotros vamos a estar utilizando una nueva anotación de JPA que es la anotación many to one o one to one, dependiendo del tipo de tipo de relación existente entre esas entidades.

[02:13] En este caso, nosotros vamos a tener que muchos productos están relacionados con una única categoría. Ese caso es equivalente a un profesor que tiene muchos estudiantes. Entonces, nosotros vamos a ir a nuestra clase categoría. Esa clase categoría ya no va a ser un enumerador, sino que va a ser una entidad.

[02:36] Entonces, al igual que la habíamos hecho con la clase producto, vamos a colocar la anotación @Entity, vamos a colocar la anotación @Table ya que esa tabla va a tener un nombre de “categorías” en la base de datos. Vamos a eliminar estos elementos acá y vamos a agregar dos atributos para esa categoría que van a ser el id y va a tener un nombre.

[03:15] Ya con eso tenemos los dos atributos, solamente tenemos que agregar las anotaciones para el id que va a ser la anotación @Id y la anotación @GeneratedValue. La estrategia, como ya habíamos mencionado, va ser GenerationType.IDENTITY.

[03:49] Vamos a hacer todas las importaciones. Vamos a importar el Id de JPA, vamos a importar GeneratedValue y vamos a agregar los getters y los setters para esta nueva categoría. Vamos a agregar getters y setters y vamos a crear un constructor para la clase categoría.

[04:16] Generamos un constructor, únicamente vamos a pasarle como parámetro el nombre y ya con esto nosotros tenemos la entidad categoría creada. Guardamos, ahora en nuestra clase producto nosotros ya no vamos a tener más un elemento de tipo enumerador.

[04:38] Como habíamos mencionado en el diagrama, nosotros vamos a tener una relación de muchos productos, vamos a tener una única categoría. Nosotros vamos a usar la anotación @ManyToOne, que es muchos productos tienen una única categoría.

[05:01] Vamos a importar esa anotación de JPA y ya con esto se encuentra realizada la relación entre la entidad producto y la entidad categoría. Esto le va a permitir al cliente agregar diversos elementos de categorías que van a estar relacionados con la clase producto.

[05:22] Ahora en nuestra clase RegistroDeProducto nosotros tenemos que instanciar esa categoría que se va a llamar celulares. Vamos a crear un new Celulares y vamos a pasarle el nombre que va a ser celulares.

[05:45] Importamos y aquí no es celulars, aquí es categoría. Y aquí vamos a pasar esta entidad como parámetro, que sería celulares. Entonces, con eso tenemos todo funcionando, vamos a guardar y vamos a ejecutar esta aplicación para ver si está funcionando correctamente.

[06:12] Aquí genera un error. ¿Cuál es el error? Vamos a ver cuál es el error. El error dice causado por hibernateTransientPropertyValue. ¿Qué es lo que está pasando? Nosotros estamos intentando guardar un elemento que es transient.

[06:28] Hasta ahora, nosotros todavía no hemos guardado el valor de esa categoría dentro de la base datos. Como nosotros habíamos mencionado, los elementos de la tabla producto están siendo guardados en la base de datos. Y nosotros queríamos guardar los elementos de la categoría en la base de datos, por lo que nosotros tenemos que realizar el mismo proceso que hicimos para los productos con la tabla categoría.

[06:51] Entonces en la siguiente parte nosotros vamos a realizar el DAO para las categorías y vamos a ver cómo se hace esta configuración de que nosotros podamos guardar una entidad, sería la entidad categoría CELULARES, dentro del producto celular.