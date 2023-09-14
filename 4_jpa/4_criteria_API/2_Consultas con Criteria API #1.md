[00:00] Hola. En la parte anterior hablamos sobre las consultas por parámetros. Construimos un método llamado consultasPorParametros donde recibíamos como atributo tres elementos. Cuando alguno de esos elementos se encontraba como nulo la consulta jpql utilizaba el único recurso que tenía para realizar su consulta.

[00:22] Si tenía más de un elemento, él realizaba esa consulta con los elementos que existieran. Entonces nosotros pasamos el nombre y el precio, él ignoraba la fecha de registro y realizaba su consulta con el nombre y el precio que estábamos pasando como parámetro.

[00:39] Utilizaba un tercer parámetro, que era el WHERE 1=1 para evitar errores de sintaxis al colocar la palabra WHERE junto a la palabra AND, ya que eso no es correcto en el lenguaje SQL.

[00:53] Ahora nosotros vamos a realizar esta consulta por parámetros utilizando la API de criteria donde nosotros no realizamos una consulta más orientada a objetos, no realizamos estas consultas JPQL y realizamos estas condiciones de filtrado una única vez, evitando la duplicación de código.

[01:18] Entonces, como vamos a utilizar este método un poco, va a ser bastante similar, vamos a llamar a este método consultarPorParametrosConAPICriteria. Los parámetros que vamos de filtrado van a ser los mismos, ya no vamos a realizar esta consulta JPQL.

[01:45] Acá ya nos vamos a realizar esta consulta jpql y estas condiciones las vamos a encontrar una única vez, vamos a dejar para el final cuál va a ser nuestro retorno. Entonces, lo primero que tenemos que hacer es llamar del EntityManager, tenemos que obtener el CriteriaBuilder que es el que nos va a permitir construir nuestras consultas a lo largo del método.

[02:16] Esa CriteriaBuilder la vamos a almacenar en una variable llamada builder, y ese builder es el que nos va a permitir crear nuestra consulta. Nosotros tenemos que indicarle cuál va a ser el contexto de la consulta, que va a ser producto.class y lo vamos a guardar en una variable llamada consulta.

[02:46] Entonces ya con eso establecemos nuestro builder, establecemos nuestra consulta que es donde el equivalente a nuestro lenguaje JPQL. Y ahora vamos a establecer el FROM. Ese FROM va a estar dentro de nuestra consulta query.from(Producto.class).

[03:10] Entonces, este from corresponde a nuestro from en nuestra consulta jpql. Lo vamos a guardar en una variable, ya que lo vamos a usar más adelante. Llamamos a from. Si nosotros quisiéramos realizar un select de otra entidad, podríamos utilizar el select del método consulta.

[03:35] Sin embargo, nosotros estamos utilizando la entidad producto con el contexto producto, no es necesario realizar ese select. Ahora vamos a introducir nuestro filtro con el builder, que es el que tiene el API de Criteria. Vamos a llamar el método and.

[03:55] Inicialmente se va a encontrar vacío, y lo vamos a almacenar en una variable con control 1 que lo vamos a llamar filtros o filtro. Entonces, ese filtro inicialmente se va a encontrar vacío y a medida que nosotros avancemos en nuestras condiciones vamos a ir reemplazando ese filtro.

[04:21] Reasignamos ese valor de filtro=builder.and y ahora va a recibir dos parámetros dentro de la restricción. El primer parámetro es el filtro anterior. Y el segundo parámetro va a ser el builder.equal. Como nosotros ya habíamos guardado el from, vamos a llamar from, le vamos a decir de dónde va a obtener el parámetro, from “nombre”. Y acá vamos a colocar el parámetro que estamos pasando a nuestro método.

[05:01] De igual forma, vamos a hacer con el precio y con la fecha. Entonces vamos a colocar precio y fecha. Aquí colocamos el nombre del atributo en la entidad “fechaDeRegistro”. Entonces sí vemos que este from corresponde al from en nuestra consulta, así como el and que corresponde a las condiciones.

[05:36] Y también tenemos la asignación de parámetros como nuestro SetParameter. Lo siguiente que vamos a hacer es establecer esos filtros, en nuestra consulta query.where(filtro). Eso lo vamos a guardar dentro de la variable query, vamos a reasignar esa variable y por último vamos a hacer el retorno, el retorno va a ser em.createQuery y vamos a pasar la consulta.

[06:15] Tenemos una lista y cerramos nuestra consulta. Ahora vamos a probar nuestro pedido de criteria. Y aquí tenemos una clase de prueba donde yo instancié el EntityManager. Tengo instanciado también un Dao para la clase producto, y llamé un elemento de consultar parámetros utilizando la API de criteria.

[06:45] Acá pasé como parámetro el nombre. Y dejé la fecha, y el precio como nulo. Obtuve el primer elemento de la lista y vemos de imprimir la descripción, vamos a ver cuál es el resultado de eso.

[07:04] Si vemos acá que él realiza un select en la entidad producto de los elementos donde 1=1, similar al método de consultar por parámetro, donde nosotros realizamos eso de forma manual. Les comparó el nombre con el nombre que nosotros pasamos en los parámetros y nos trajo la descripción que sería producto nuevo.

