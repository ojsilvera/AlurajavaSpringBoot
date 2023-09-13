[00:00] En el video anterior, nosotros habíamos recibido una excepción que era la excepción decía TransientPropertyValue. Esa excepción lo que significa es que nosotros estábamos intentando pasar como parámetro un elemento que aún no ha sido guardado dentro de la base de datos.

[00:17] En el video anterior nosotros creamos la nuestra nueva entidad, que es la entidad categoría, instanciamos esa categoría con el nombre de celulares y la intentamos pasar como parámetro dentro de la entidad producto.

[00:32] Nosotros habíamos construido un relacionamiento del tipo ManyToOne en la clase producto. Luego de que nosotros hicimos ese mapeamento, intentamos realizar la persistencia para ese producto y nosotros recibimos el error.

[00:49] Para corregirlo tenemos que construir un DAO para la categoría y luego de haber construido el DAO, del mismo modo que hicimos con los productos, tenemos que guardar esa entidad que sería la entidad categoría con el nombre celular y luego de eso es que nosotros podemos guardar el producto.

[01:07] Entonces, para realizar eso, nosotros vamos a copiar ese producto DAO, lo vamos a pegar acá, vamos a colocar el nombre CategoriaDao, vamos a acceder a esa clase. Y aquí donde dice producto vamos a cambiarlo por categoría y todo lo que diga producto lo vamos a cambiar acá por categoría.

[01:40] Importamos la clase y ya tenemos el DAO para la categoría. Con esto, nosotros podemos usar el método, el método guardar para persistir esa entidad. Entonces, ahora de vuelta en nuestra clase main nosotros vamos a instanciar esa categoriaDao que es la que nos va a permitir llamar al método guardar y hacer la persistencia de esa nueva categoría categoría.

[02:10] Entonces, new CategoriaDao y vamos a pasar el entityManager. Entonces, como nosotros habíamos mencionado anteriormente, nosotros mantenemos la conexión antes de los DAO para poder evitar la duplicación de código.

[02:31] Entonces nosotros iniciamos la conexión, realizamos todas las transacciones que nosotros deseamos crear en nuestro programa Y por último, nosotros cerramos esa conexión. Entonces, luego de que nosotros instanciamos la categoriaDao, nosotros ahora podemos guardar esa entidad, la entidad celulares.

[02:53] Entonces, vamos a llamar categoriaDao, vamos a llamar el método guardar y vamos a pasar la entidad celulares, dentro de ese elemento. Ahora sí guardamos y si podemos ejecutar nuestra aplicación. Ahora, dentro del registro, nosotros vemos que creó la tabla categoría, creó la tabla producto.

[03:17] Hizo una alteración dentro de la tabla productos agregando esa llave extranjera que como habíamos mencionado en el diagrama, es agregar el identificador de la tabla categorías dentro de la tabla producto.

[03:32] Entonces, si revisamos aquí que crea en la tabla, él tiene el id como tipo entero, tenemos el nombre que es varchar para la tabla categoría y dentro de la tabla producto tenemos el id del tipo entero, la descripción variar, la fecha de tipo date, el nombre varchar, el precio del tipo numérico y tenemos la categoría.

[03:56] En el video anterior nosotros hemos visto que este elemento era de tipo varchar. Ahora es el tipo bigInt. Eso es porque él está guardando el elemento del id de la tabla extranjera o de la tabla externa.

[04:14] Él luego realizó los inserts tanto para la tabla categoría, y en secuencia realizó el insert o guardó los elementos para la tabla producto. Entonces, repasando todo lo que fue realizado en este curso, nosotros creamos la entidad categoría del mismo modo que teníamos la entidad producto.

[04:38] Agregamos los atributos para esa entidad. Eran el id y el nombre. Le damos la relación entre la tabla productos y la tabla categoría, colocamos la cardinalidad, que va a ser tipo ManyToOne, recordando que muchos productos tienen una única.

[05:00] Creamos el DAO para esa nueva categoría, que es la que nos va a permitir guardar la entidad dentro de la entidad producto. Y por último, luego de haber instanciado el Dao, tanto para el producto como para la categoría, nosotros guardamos en el orden correcto la categoría y luego el Dao.

[05:27] Entonces, con eso tenemos todo sobre los mapeamentos de las relaciones y en la siguiente parte vamos a hablar sobre las transacciones y los estados.