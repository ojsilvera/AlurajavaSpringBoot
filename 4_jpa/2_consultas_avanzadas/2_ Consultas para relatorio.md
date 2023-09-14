[00:00] Hola. En la clase anterior nosotros hablamos sobre las funciones de agregación y vimos cómo utilizar la función sumatoria para calcular el valor total de todos los pedidos existentes en la tabla pedido. También utilizamos la función average dentro de las funciones de agregación, que nos da como retorno un elemento del tipo double.

[00:21] Ahora en esta parte, nosotros vamos a utilizar esas funciones de agregación en una consulta que nos mandaron a realizar para un relatorio de ventas. Entonces vamos a suponer que el cliente nos mandó a implementar una nueva funcionalidad donde nosotros pudiéramos extraer los productos, el nombre de los productos, la cantidad vendida por producto y la fecha de última venta para ese producto.

[00:53] Entonces nosotros vamos a tener elementos de la entidad producto, vamos a tener elementos de la entidad items_pedido y vamos a tener elementos de la entidad pedido. Y todos esos los tenemos que retornar en una única consulta. Nosotros vamos a tener una lista de elementos combinados que provienen de la entidad items_pedido y de la entidad pedido.

[01:21] ¿Cómo vamos a realizar eso? Vamos a ir a nuestra clase pedidoDao, vamos a construir un nuevo método que se va a llamar relatorioDeVentas. Por ahora no vamos a saber cuál es el retorno de ese método. Vamos a saber que se va a llamar relatorioDeVentas y vamos a comenzar a construir nuestra consulta.

[01:48] Entonces para construir la consulta creamos un string, vamos a llamar jpql y comenzamos a realizar la consulta. Lo primero que tenemos que hacer es seleccionar las columnas que deseamos extraer, entonces “SELECT”. Primer elemento va a ser el producto. Colocamos el token producto.nombre.

[02:23] El segundo elemento que nosotros queremos traer va a ser la sumatoria, vamos a ir acá en el relatorio. Nosotros queremos la sumatoria de las cantidades vendidas que se encuentran en la entidad items_pedido, entonces vamos a colocar sumatoria de items_cantidad y el último elemento que nosotros vamos a traer es la columna MAX, la máxima fecha. ¿Dónde se encuentra esa fecha?

[02:54] En la entidad pedido. Entonces, la máxima fecha de la entidad pedido. Si nosotros revisamos en la entidad producto, tenemos el elemento nombre, ese nombre tiene que corresponder al que nosotros estamos colocando acá. Este elemento de acá, el elemento de la izquierda va a ser un auxiliar o un token, y el elemento de la derecha va a ser el nombre del atributo en la clase items_pedido tengo el atributo cantidad. Y en la clase pedido en la entidad pedido yo voy a tener el atributo fecha.

[03:34] Ahora tengo que indicarle de dónde voy a traer esos elementos, entonces vamos a colocar ahora FROM. La primera entidad que nos permite relacionar eso sería pedido. Entonces yo voy a ir a la entidad pedido y la segunda, yo voy a ir a la entidad pedido se encuentra relacionada con la entidad items_pedido entonces de la entidad pedido, voy a ir a la entidad items_pedido y en la entidad items_pedido, yo puedo acceder a los elementos de producto.

[04:13] Entonces vamos a hacer ese recorrido, sería FROM Pedido. Recordando que tenemos que colocar el mismo nombre de la entidad y el nombre que estamos utilizando para el auxiliar. Y ahora vamos a realizar un join, nosotros vamos a concatenar esa entidad pedido con la entidad items_pedido. Entonces vamos a realizar un JOIN de pedido.

[04:45] ¿Qué elemento existe en pedidos que nos permite concatenar esas entidades? Sería la entidad y items_pedido que se llama items. Entonces en la entidad pedidos vamos a concatenarlo de ítems con el atributo item que estamos utilizando, con el token item que estamos utilizando para la sumatoria.

[05:09] Ahora voy a concatenar la última entidad que sería item. ¿Qué elemento está faltando? El producto. Vamos a revisar en la entidad items_pedido yo puedo concatenarlo con el atributo producto. Entonces vamos a ir al Dao, realizamos esa consulta item.producto con el token producto.

[05:42] Entonces, con eso queda finalizada la unión entre mis entidades, ahora solamente falta indicarle que los agrupe. Vamos a agrupar esa consulta por nombre, ya que en el relatorio de ventas, yo tengo todos los elementos. Es la cantidad vendida para todos los elementos por un determinado nombre entonces quiero agrupar por producto.nombre.

[06:16] Y quiero ordenarlos. Vamos a ordenarlo por la cantidad de elementos vendidos, entonces vamos a ordenar por item.cantidad. Lo vamos a ordenar de forma descendente. Con eso ya tenemos nuestro relatorio de ventas construido. Ahora solamente falta darle el retorno para ese método, entonces vamos a ver qué es lo que vamos a retornar.

[06:49] Nosotros vimos en la imagen que tenemos una lista de elementos, entonces ya podemos ir colocando que es una lista de cuál elemento. Eso es lo que vamos a ver ahora. Entonces vamos a retornar EntityManager. Vamos a crear la consulta. Aquí sería createQuery.

[07:16] Vamos a pasar la consulta que realizamos y el retorno. Entonces, como nosotros vamos a tener elementos del tipo nombre, entonces el nombre en producto es del tipo string para el elemento cantidad, es del tipo long y para el elemento fecha es del tipo localDate. Entonces nosotros tenemos dos formas de realizar esta consulta.

[07:43] Tenemos una forma utilizando un arreglo de objetos, que el objeto es la clase raíz de la que derivan todas las demás clases, o podemos construir un VO que es una clase, un tipo de entidad que nos sirve para transferir información dentro de nuestra aplicación.

[08:04] Vamos a aplicar la primera estrategia, que es como una regla de objetos, una regla de objetos. Y aquí vamos a colocar .class. Lo último sería, vamos a obtener getResultList(). Y finalizamos. Entonces, tengo que importar object. Aquí me falta colocar esto en este signo de interrogación para saber que el retorno de mi lista va a ser del tipo arreglo de objetos.

[08:47] Entonces, con esto queda finalizada la primera estrategia para dar un retorno de un relatorio que está compuesto por múltiples atributos de múltiples entidades. Entonces, vamos a ejecutar eso en la clase de registro de pedido. Entonces de pedidoDao vamos a llamar relatorio de ventas.

[09:13] Vamos a apretar control 1 para asignar ese valor en una variable. Vamos a llamarlo relatorio. Y ahí vamos a imprimir lo que se encuentra en ese relatorio. Sería aplicar un for. Ese for es del tipo object arreglo de objetos. Lo vamos a llamar obj, y un arreglo, vamos a instalar en la lista de relatorio.

[09:41] Entonces, yo quiero imprimir todos los elementos existentes en todas las posiciones. Como tengo tres posiciones, yo tengo que imprimir los elementos en la primera posición que va a hacer obj en la posición 0, la primera posición. Y lo mismo para la posición 1 y la posición 2.

[10:09] Entonces, de esa forma, yo ya puedo comenzar a imprimir los elementos, vamos a ver en qué retorna. Ejecuto mi aplicación. Y vemos que efectivamente, él está realizando un select en las columnas nombre, la cantidad de la fecha, realizó la función de agregación, él trae de la tabla pedido y realizó un join con la entidad item pedido y la entidad producto.

[10:43] Agrupó por el nombre de producto y los ordenó por la cantidad de forma descendiente. También tenemos la forma ascendente que sería ASC. Imprimimos en la consola el nombre de esos elementos. Entonces, en la siguiente parte nosotros vamos a ver la segunda estrategia, que es a través de la construcción de una clase llamada VO.