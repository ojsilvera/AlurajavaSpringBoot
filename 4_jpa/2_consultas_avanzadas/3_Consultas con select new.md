[00:00] Hola. En la parte anterior nosotros construimos un relato de venta con elementos provenientes de diferentes entidades. Entonces, para ese relatorio de ventas, nosotros realizamos una consulta del nombre de los productos en la tabla producto, la cantidad en la tabla, items_pedido y de la fecha en la entidad pedido.

[00:23] Adicional, utilizamos funciones de agregación en esa consulta, nosotros utilizamos función de agregación para calcular la cantidad de productos vendidos y la máxima fecha en la que fueron vendidos a esos productos. Utilizamos una estrategia en la que retornamos elementos del tipo objeto, pero ese retorno no es el más específico.

[00:46] Nosotros tenemos que tratar de dejar nuestra aplicación bastante tipeada para indicarle cuál es el elemento de retorno que deseamos. Entonces nosotros vamos a utilizar la segunda estrategia, que es a través de la construcción de un VO, que significa value object. Vamos a colocar aquí relatorio de ventas VO.

[01:08] Y el retorno de ese método va a ser, se va a llamar relatorioDeVenta. El relatorioDeVenta va a tener tres atributos, vamos a colocar dentro del paquete que no pertenece a la clase Dao, un paquete en particular, y va a tener tres atributos. Va a tener string. Va a ser de tipo privado y vamos a tener el nombre del producto, nombreDelProducto.

[01:50] El segundo atributo o propiedad va a ser el tipo long o sea la cantidad de producto que existe. Y por último, un último atributo que va a ser del tipo localDate que va a ser fecha de última venta: FechaDeUltimaVenta.

[02:17] Entonces, es importante realizar el constructor para esta clase, la clase VO, ya que el constructor es el que nos va a permitir realizar la consulta en nuestro método de relatorio de venta, entonces vamos a colocar aquí crear un constructor con todos los atributos, vamos a eliminar la palabra clave super y vamos a colocar los getters y setters para esta entidad.

[02:53] Seleccionamos todo. Adicional, voy a colocar el método ToString que nos va a permitir imprimir los atributos, ya que de lo contrario vamos a imprimir únicamente la posición de memoria en la que se encuentra esa entidad. Nosotros queremos imprimir el valor que tienen esos atributos.

[03:11] Entonces nosotros vamos a imprimir el valor del nombre de producto para esa entidad instanciada. Ahora en la clase pedidoDao, nosotros vamos a reemplazar este objeto acá también por un elemento del tipo relatorioDeVenta. Y aquí tenemos que utilizar la palabra clave new, que es un recurso de JPA que nos permite utilizar el lenguaje de Java dentro de nuestras consultas de SQL.

[03:45] SELECT new RelatorioDeVenta. Vamos a abrir paréntesis, como si estuviéramos realizando un constructor y vamos a pasar los atributos producto.nombre, suma de la cantidad de items y el máximo pedido de fecha, y cerramos el constructor.

[04:08] El resto de la consulta va a permanecer igual, pues va a través de la entidad de pedido para realizar los JOIN y los va a agrupar por el nombre y ordenarlos por la cantidad. Una cosa que está faltando acá es indicar la ruta correcta de esa relatorio. De esta forma, él no va a saber de dónde traerlo.

[04:28] Vamos a dejar eso ahí. Vamos a dejar ese error ahí presente. Ahora vamos a colocar relatorioDeVentasVO y el tipo ya no va a ser del tipo objeto, sino que va a ser del tipo RelatorioDeVenta. Acá vamos a colocar RelatorioDeVenta, importamos la clase.

[04:54] Aquí vamos a eliminar esto y vamos a colocar Relatorio. Vamos a realizar un forEach(System.out::println) e imprimimos todos los elementos que existen en ese relatorio. Vamos a ejecutar. Deberíamos obtener un error. Vamos a ver. Y, en efecto, él dice que es incapaz de localizar la clase. Vas a ir al pedido de Dao.

[05:25] Vamos a ir al velatorioDeVentas, copiamos la ruta. Y en registro de pedido en pedidoDao tengo que colocar acá la ruta exacta de donde esta provenía. Sería com.latam.alura.tienda.vo.RelatorioDeVenta. Ahora sí podemos ejecutar nuestra aplicación y vemos que él no mudó la consulta.

[05:57] Él realizó un select de la entidad pedido, realizó los join con items_pedido y con la entidad producto, agrupó por nombre, ordenó por la cantidad y nos imprimió en la consola la clase, esa entidad de relatorioDeVentas, que es un VO con sus respectivos atributos a través del método ToString.

[06:21] Entonces, esas son las dos estrategias que nosotros tenemos para imprimir relatorios de elementos que provienen de múltiples entidades, incluso usando funciones de agregación. Para tener relatorios, nosotros podemos aquí agregar más columnas, más o menos columnas, pero tenemos que tener cuidado con la consulta y ver de dónde vamos a traer esos elementos cómo van a rehacer los join.

[06:49] Entonces, en la siguiente parte nosotros vamos a hablar sobre otro recurso de JPA, que son las consultas con nombres, que son consultas que pueden ser agregadas dentro de nuestra entidad.