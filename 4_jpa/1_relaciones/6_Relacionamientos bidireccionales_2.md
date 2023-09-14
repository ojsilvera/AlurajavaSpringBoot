[00:00] Hola a todos. Hasta este punto ya nosotros hemos construido los modelos necesarios para ampliar nuestro proyecto. Alura nos solicita que creásemos un modelo que nos permitiera guardar en la base de datos tanto los clientes como los diversos productos solicitados por ese cliente en un cierto pedido.

[00:24] Entonces nosotros vamos a tener diversos clientes, que van a ser guardados en la base de datos como el restante de estas entidades. Y entonces este cliente va a realizar un pedido, y ese pedido tiene que tener una cierta cantidad de productos y esos productos los vamos a almacenar dentro de una nueva entidad que se va a llamar items_pedido.

[00:48] Adicional esos productos tienen una cierta categoría, esa categoría puede ser electrónico, puede ser libros, puede ser celulares. Y todas esas entidades, como estamos viendo, ellas se encuentran relacionadas de la forma uno a muchos o en algunos casos de muchos a muchos.

[01:12] Entonces nosotros habíamos almacenado nuestra información en la memoria, toda esa información que nosotros estamos agregando se encuentra en la base de datos H2, pero dentro de la memoria.

[01:23] Con la finalidad de nosotros tener una mejor percepción de lo que nosotros estamos haciendo, de cómo es esa construcción de las tablas, vamos a modificar la ruta de la base de datos a una dentro de un archivo local, en una carpeta local para poder mostrar las tablas que se están creando en todo momento. Entonces lo primero que voy a hacer es abrir la carpeta donde voy a almacenar esa información.

[01:52] Entonces voy a buscar acá la carpeta, sería la carpeta JPA. Voy a copiar la ruta que sería usuarios\públicos\Alura\jpa. E ir de vuelta a mi archivo de persistence.xml voy a reemplazar la parte de mem:tienda por la ruta donde voy a guardar mi archivo.

[02:17] Entonces, ya con la ruta voy a colocar la contraseña 1234 de acceso a esa base de datos. Para yo crear una base de datos, yo tengo que acceder al icono, crear una nueva base de datos que me va a colocar algo de este modelo, voy a colocar la ruta y en este caso voy a tener que colocar database.

[02:51] Aquí tengo que colocar una contraseña, confirmo la contraseña y creo la base de datos. Aquí voy a colocar base de datos 2. Así vemos que la contraseña fue creada exitosamente. Voy a cerrar acá y vamos a hacer la primera prueba.

[03:06] Nosotros teníamos una clase main donde estábamos haciendo las pruebas para los registros de productos y de categorías. Lo único que vamos a hacer es ejecutar esa clase. Vamos a ejecutar la clase de registro de producto, vemos que funciona todo correctamente y lo que vamos a hacer ahora es ejecutar la base de datos H2. Vamos a ver.

[03:37] Vamos a conectarnos y vemos que efectivamente nosotros ahora tenemos las tablas que hemos creado. La tabla categorías, la tabla clientes, la tabla items_pedido, la tabla pedidos y la tabla productos.

[03:50] Si yo selecciono select * from clientes vemos que no hay registros dentro de la tabla cliente. Si voy a la tabla pedidos, lo ejecuto, tampoco hay ningún registro. Entonces en la siguiente parte, nosotros vamos a ver cómo agregar pedidos dentro de la tabla clientes, ya que nosotros ya podemos ver cómo con esto vamos a obtener una mejor comprensión de lo que está pasando en la base de datos.

[04:29] Entonces nosotros vamos a combinar esa parte de JPA y vamos a tener una mejor visualización con la base de datos H2, nos vemos en la siguiente clase.