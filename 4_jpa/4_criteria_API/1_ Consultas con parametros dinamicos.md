[00:00] En esta parte vamos a hablar sobre consultas, utilizando parámetros y sobre las consultas utilizando la API de criterio. Aquí nosotros realizamos consultas, utilizando los parámetros en algunas aulas anteriores donde obtuvimos los elementos en la tabla, productos que tuvieran un determinado nombre, eso nos daba como retorno una lista de productos.

[00:22] Para esa consulta, nosotros teníamos que el nombre era de carácter obligatorio y teníamos un único parámetro. Ahora, nosotros vamos a construir nuestro método, que va a tener más de un parámetro de filtrado y va a reconocer cuando uno de esos elementos existe o no, y de esa forma lo va a ignorar para permitirle ya obtener los parámetros restantes.

[00:49] Entonces, nosotros ya vemos que a la hora de realizar nuestra consulta, más de un elemento puede coincidir con ese determinado parámetro con el que vamos a buscar, entonces nos va a dar como el retorno una lista de la entidad producto. El nombre de esa entidad va a ser consultarPorParametros. Y vamos a buscar cuáles son los parámetros que vamos a escoger.

[01:18] Nosotros vamos a buscar por el nombre, por el precio y por la fecha de registro. Entonces puede existir que encontremos en la base de datos más de un atributo, más de un producto con determinado nombre, con determinado precio o con determinado nombre y fecha de registro.

[01:37] Vamos a colocar los parámetros que serían nombre, el precio, que es el tipo BigDecimal, precio y la fecha, que es del tipo LocalDate, fecha. A partir de acá, nosotros comenzamos a realizar nuestra consulta, que es un string al que llamamos jpql y seleccionamos los elementos de la tabla producto, recordando que tenemos que colocar el mismo nombre de la entidad donde coinciden con nuestra condición de filtrado.

[02:18] Entonces vamos a colocar where. La primera condición de filtrado es que el nombre sea igual al parámetro que estamos pasando. La segunda, que el precio sea igual, el precio que estamos pasando y por último, que la fecha sea igual fechaDeRegistro, recordando que tiene que ser el nombre del atributo registro, del atributo que existe en la entidad producto y del lado derecho tiene que ser el nombre que estamos pasando como parámetro.

[03:03] Sin embargo, aquí vemos que si alguno de estos elementos llegase a ser nulo, él va a buscar los elementos en la entidad producto que tengan ese nombre nulo y el precio que nosotros indicamos y la fecha que indicamos. O que busque si el precio se encuentra nulo, él va a buscar el nombre que nosotros estamos indicando como parámetro, las fechas que estamos indicando como un parámetro y el precio que sea nulo.

[03:31] Entonces, de esa forma es obligatorio y eso no es lo que queremos. Nosotros queremos que a la hora de que uno de esos elementos no se encuentre, él simplemente lo ignore, entonces nosotros vamos a colocar acá que él ignore ese elemento y que coloque dónde el precio sea igual al parámetro y la fecha de registro sea igual a ese otro parámetro.

[03:58] Acá vemos que si el precio tampoco existe él va a tener la palabra de SQL WHERE y la palabra AND coincidiendo en la misma línea, entonces yo voy a usar acá un pequeño truco, que 1=1 me va a permitir construir mi consulta de esta forma, seleccionar los elementos de la entidad producto donde 1=1, cierto.

[04:24] Entonces, aquí va a ser true y va a continuar con mi consulta. Y que la fecha de registro sea igual a esa fecha. Entonces, esta va a ser mi consulta base. Como yo voy a ir aumentando el tamaño de mi consulta, vamos a utilizar un StringBuilder y aquí vamos a instanciar ese nuevo StringBuilder. Abro paréntesis.

[04:54] Recordamos que los elementos del tipo string son inmutables y los elementos del tipo StringBuilder son mutables. Nosotros los podemos ir modificando a la hora que vamos construyendo nuestro código. Entonces, ahora nosotros vamos a comenzar a construir nuestros if, que nos van a permitir modificar y ampliar esa consulta.

[05:16] El primero sería que el nombre no sea nulo, para eso colocamos nombre diferente de nulo y nombre que no sea vacío. Nosotros vemos si es vacío y retornamos la condición contraria. Ahora vamos a llamar a esa consulta jpql y le vamos a agregar el siguiente parámetro que sería “AND”, que el nombre coincida con el parámetro que estamos indicando.

[05:57] Cerramos acá. Y vamos a hacer lo mismo con el precio y con la fecha. Para el precio nosotros tenemos que colocar la condición de que el precio no sea nulo y que el precio sea diferente de cero por ejemplo, no vamos a tener ningún elemento que tenga como precio cero.

[06:24] Aquí vamos a colocar new BigDecimal(0). Y para la fecha, simplemente aquí es precio. Aquí estoy en la segunda parte. Vamos a colocar a cada precio, solamente por orden, podrían haberlo dejado en la parte de abajo. Pero por orden, vamos a dejarlo nombre, precio y acá fecha, entonces que la fecha no sea nula.

[07:05] Podrían colocar una otra condición como que la fecha sea mayor a tal fecha o menor a tal fecha. Del mismo modo, para el precio. Pueden consultar por el precio que sea mayor a tal valor o que los nombres tengan tanta cantidad de sílabas o de vocales. Vamos aquí, vamos a colocar fechaDeRegistro=fecha.

[07:40] Ya de esta forma queda elaborada nuestra consulta. Ahora vamos a con el EntityManager vamos a crear nuestra consulta. Vamos a pasar esa consulta que estamos pasando que estamos escribiendo, la vamos a transformar a string y le vamos a indicar cuál va a ser nuestro retorno. Va a ser producto del tipo class.

[08:07] Ahora nosotros vamos a establecer los parámetros. Para establecer los parámetros, voy a utilizar las mismas condiciones anteriores, y voy a colocar esto acá, lo voy a almacenar en una variable que va a ser del tipo typeQuery y lo voy a llamar consulta. Entonces, si el nombre no es nulo él va fijar esa consulta, va a ser query.setParameter, el primer nombre, sería nombre. Y el valor, “nombre”.

[08:53] De la misma forma lo vamos a hacer para el precio y para la fecha. Fijamos el parámetro precio con el valor de precio y la fecha sería “fechaDeRegistro”. Recordando de nuevo que el nombre del atributo en entidad y acá el nombre del parámetro. Ahora si vamos a darle el retorno, a EntityManager query. Ya nosotros realizamos la consulta, fijamos los parámetros.

[09:36] Y vamos a indicarle getResultList. Vamos a obtener la lista. De esa forma queda. Aquí tenemos un error. Establecimos el parámetro, no indicamos el retorno. Ahora, nosotros queremos una lista de todos los elementos que coincidan con un determinado parámetro, entonces ese parámetro puede ser el nombre, el precio y la fecha, o si nosotros no colocamos el nombre, va a buscar todos los elementos en la tabla producto que tengan ese precio y la fecha.

[10:14] Sin embargo, si ese nombre se encuentra nulo, él buscaría los elementos que tengan el nombre nulo, el precio que indicamos y la fecha. Para evitar eso, nosotros vamos a establecer una condición que él va a permitir ir construyendo esa consulta a medida que eso parámetros existan o no.

[10:35] Entonces si el nombre no existe, él no va a agregar ese valor en la consulta. Va a saltar al siguiente valor, que sería el precio, si el precio existe, entonces va a agregar un AND. Nosotros aplicamos aquí este pequeño truco. Y va a construir la consulta y el precio sea igual al precio. Y por último, si la fecha también existe, la agrega el valor de la fecha.

[10:59] Dejando un espacio en blanco, ya que a la hora de nosotros construir nuestra consulta, él va a ir agregando esos espacios en blanco también. Va a crear el espacio en blanco y a partir de ahí colocamos el AND. Un error común que ocurra es que nosotros acá podemos colocar acá, entonces va a establecer una sola palabra, entonces eso no es lo que queremos.

[11:27] Vamos a ver que eso se está ejecutando correctamente. Vamos a ir aquí a una clase main, donde yo cargue unos elementos de prueba, y vamos a instanciar el EntityManager con la clase de JPAUtils.getEntityManager. Vamos a asignar eso a una variable y vamos a instanciar el Dao.

[11:54] El Dao para la clase de producto, productoDao va a ser igual a productoDao. Instanciamos un nuevo Dao con el EntityManager para realizar ese pequeño experimento. Entonces, vamos a utilizar el método consultarPorParametros, productoDao.consultarPorParametros y el nombre, que aquí dentro de los productos que ya registré, coloqué un celular, que sería un iPhone x, un FIFA del año 2000 y una memoria de 30 gigas.

[12:37] Ahora entonces, vamos a suponer que pasamos el nombre FIFA, el precio es nulo. Y la fecha también la colocamos como nula. Vamos a ver cuál va a ser el resultado de esto. Vamos a guardar esto dentro de una variable. Como yo sé que me va a dar como retorno un único valor, yo voy a imprimir en la consola. Vamos a ponerle acá un nombre como resultado. Y vamos a imprimir.

[13:13] System.out.println. El resultado es una lista, vamos a tener el primer elemento get(0), y de ahí vamos a obtener la descripción para ese de FIFA.