[00:00] Hola. Ahora para finalizar el tema de las consultas, nosotros vamos a hablar sobre un último método, que es las consultas con filtro limitadas a un único elemento, único atributo de esa entidad.

[00:14] En este caso nosotros vamos a llamar de la tabla producto únicamente el precio y vamos a obtener como resultado un único valor en una lista de resultados. Entonces, voy a ir a mi clase DAO donde voy a crear el método que se va llamar consulta de precio por nombre de productos.

[00:37] Es un nuevo método, va a ser de tipo público, me va a retornar un elemento del tipo BigDecimal, ya que es el tipo al que fue asignado el precio en la entidad producto. Entonces llamamos nuestro método consultarPrecioPorNombreDeProducto. Tenemos que pasarle un parámetro. Ese parámetro va a ser un string, un nuevo nombre y vamos a realizar nuestra consulta.

[01:13] De la misma forma que hicimos anteriormente vamos a crear un string llamado jpql, donde vamos a crear nuestra consulta. Vamos a hacer “SELECT P FROM Producto AS P WHERE P.nombre=:nombre”; donde el nombre sea igual a ese parámetro que nosotros estamos buscando.

[01:47] De esta forma nosotros estamos trayendo toda la entidad porque nosotros estamos indicando aquí que seleccione la entidad P donde el nombre corresponda a ese parámetro que nosotros estamos buscando, para nosotros únicamente consultar el precio, nosotros aquí donde colocamos “SELECT P” vamos a colocar el precio entonces seleccionar el precio de la entidad P donde el nombre corresponda a ese parámetro.

[02:17] Y ahora sí nosotros vamos a realizar nuestro retorno. Venimos al EntityManager, creamos la consulta, con método createQuery, pasamos nuestro jpql y aquí tenemos que asignar el tipo que nos va a retornar.

[02:37] Ese tipo va a ser del tipo BigDecimal, vamos a importar. Entonces aquí tenemos BigDecimal.class, vamos a establecer nuestro parámetro, setParameter, la posición va a ser el nombre y el valor va a ser el nombre que estamos pasando como parámetro.

[03:05] Aquí ya no vamos a tener una lista de resultado, sino un resultado único, y con eso queda finalizada nuestra consulta. Nosotros vemos aquí que cuando nosotros creamos nuestra consulta, nosotros especificamos el tipo que nos va a dar como retorno que en este caso va a ser un BigDecimal.

[03:26] Y vemos que aquí nos ha estado marcando una alerta. Esa alerta es que nosotros no habíamos indicado el tipo que nos da como retorno. Aún así, él retorna el valor que es encontrado en la base de datos.

[03:40] Entonces, aquí nosotros vamos a indicar el tipo era la clase producto y de igual forma acá, producto.class, y con eso queda corregida la señal de alerta. Entonces, ahora voy a evaluar ese último método, sería consultar el precio.

[04:06] ConsultaPrecioPorNombre. ¿Cuál es el nombre del producto? Xiaomi. Vamos a colocar el nombre de producto. Aquí me va a dar un error porque el tipo no coincide, entonces a este lo vamos a llamar precio y el tipo va a ser BigDecimal. Con eso queda corregir el error, ahora donde dice precio yo voy a imprimir ese valor en la consola: System.out.println, vamos a imprimir el valor del precio.

[04:49] Vamos a ver que nos da esto como resultado, aquí me faltó punto y coma. Y en la consola va a estar el precio para ese producto que es de 800. Lo último que nos está faltando es darle un poco de organización a estas consultas. Esto es solamente por estética.

[05:15] Y en nuestra clase de persistencia, nosotros vamos agregar una nueva propiedad que va a ser la propiedad format_sql. Entonces nosotros le vamos a dar un formato para darle un poco más de estilo, y vamos a encontrar nuestra aplicación. Guardamos las alteraciones y vemos que de esta forma JPA nos presenta las consultas de una forma más organizada, que esto nos va a permitir ver cuáles son las consultas que se están realizando en la base de datos de forma organizada.

[05:50] Aquí vemos que él está rezando un insert a tabla producto, los valores, realizó el Select, realizó un outer join y aquí finalmente obtuvimos el precio. Entonces eso fue todo por las consultas. Espero que le haya gustado este curso, fue hecho con bastante cariño. Nos vemos más adelante.