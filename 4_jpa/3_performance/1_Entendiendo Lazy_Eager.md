[00:00] Hola. En la parte interior, nosotros hablamos sobre las consultas, hablamos sobre las consultas de agregación, que son consultas con los métodos suma, promedio, máximo, mínimo. Hablamos sobre las consultas para relatorio.

[00:14]Son consultas que obtienen entidades o propiedades o atributos de diferentes entidades y las consultas con nombres. Son consultas que se colocan dentro de la entidad y eviten que nosotros estemos colocando múltiples consultas a lo largo del código. Entonces simplemente colocamos una consulta que es necesaria dentro de la entidad e indicamos a otros desarrolladores que se está realizando esa consulta.

[00:41] Ahora en esta parte nosotros vamos a comenzar a hablar sobre el desempeño de las aplicaciones. Y acá, a la hora de nosotros realizar la aplicación es común que nos olvidemos de la consulta que se está realizando en la base de datos y se estén realizando consultas que estén trayendo valores innecesarios o consultas que sean ineficientes, sea porque traen muchos valores o porque no es la consulta más apropiada.

[01:08] Nosotros en esta parte cargamos unos registros desde unos archivos de texto, con una clase que importa utilizar instancia los Dao y lee esos archivos de texto para cargarlos en la base de datos. Nosotros creamos una clase main para realizar nuestras pruebas de desempeño, cargamos todos nuestros registros, instanciamos el EntityManager.

[01:35] Entonces vamos para realizar nuestra primera prueba de desempeño. Vamos a imprimir en consola un pedido, entonces vamos a llamar primero el pedido EntityManager em.find(Pedido.class, 3l). Vamos a asignar esto a una variable, vamos a importar la clase pedido, asignamos a una variable. Esa variable se va a llamar pedido. Y ahora vamos a imprimir lo en la consola: system.out.println.

[02:17] Y de ese periodo nosotros vamos a obtener la fecha. Vamos a tener la fecha para ver cómo está realizando la consulta. Ejecutamos la aplicación. Vemos que él importó todos los valores en la base de datos y al final el realizó un select de todas las columnas de pedido del id, cliente, fecha y valor de la entidad de la entidad pedido, pero adicional realizó un join con la entidad cliente donde el id del pedido coincide con el que nosotros pasamos. Imprimió la fecha y finalizó la aplicación.

[02:59]Entonces nosotros vamos a ver este detalle acá. ¿Por qué realizó un join con la tabla cliente? Primero nosotros vamos a ver esa base de datos a ver si se cargaron los valores correctamente. Voy a colocar acá la contraseña y vamos a ver el pedido. Vemos que se cargaron los pedidos correctamente, vamos a ver items_pedido. Se cargarán los pedidos y los clientes también se cargaron correctamente.

[03:33] Ahora vamos a ir a la clase pedido para ver por qué realizó un join. Entonces, nosotros vemos que el atributo cliente tiene la anotación ManyToOne. Todos los elementos que tengan la anotación del tipo ToOne, ya sean ManyToOne o OneToOne. tienen una estrategia de cargamento que se es del tipo eager, una estrategia de cargamento anticipada.

[04:02] Es decir, siempre que nosotros instanciemos una entidad, llamemos una tabla de la base de datos, y que uno de sus atributos, en este caso es cliente, tenga la notación del tipo ToOne, o sea, OneToOne, ManyToOne, él va a ser un join con todos los atributos que tengan esas notaciones.

[04:22] Entonces si lo tengo acá cinco atributos del tipo ManyToOne, él va a realizar un join con esas cinco entidades a pesar de que nosotros no las estemos utilizando. Si nosotros ejecutamos nuevamente, aquí tenemos que cerrar la base de datos, vamos a ejecutar nuevamente, vemos que los items no realizó item con los items del pedido, a pesar de que tienen la notación OneToMany.

[05:01] Eso es porque todas las anotaciones que sean de tipo ToMany, ya sea ManyToMany o OneToMany, tienen la estrategia de cargamentos del tipo lazy o cargamento perezoso. Nosotros vamos a traer ese recurso únicamente cuando sean solicitadas. Entonces, vamos a probar eso, en esta clase PruebaDeDesempeño.

[05:26] Vamos a colocar una notación acá, vamos a duplicar acá. Y aquí vamos a llamar de pedido, vamos a traer un elemento de item pedido. Sería getItems y vamos a ver el tamaño de esa lista. Sería size. Aquí me había faltado colocar los getters y los setters para la lista de pedidos, que sería item, vamos a ir a la clase de pedido, fuente, generar getters y setters.

[06:00] Seleccionamos, generamos los getters y setters y ahora en la PruebaDeDesempeño debería estar corriendo perfecto. Ejecutamos nuestra aplicación y vemos que él continúa haciendo un join con la entidad cliente, pero esta vez él realizó un select para la entidad items_pedido y también realizó un join con la tabla producto y un join con la tabla categoria.

[06:33] Entonces vamos a ver que en la entidad items_pedido vemos también que ellos están con la notación ManyToOne. Entonces, si yo llamo un elemento de la entidad items_pedido, y ese elemento tiene atributos que también tengan la notación del tipo ToOne, él vaya a realizar un join con esas entidades.

[07:03] Entonces imagina, cada vez que si dentro de ese producto, vamos a ejecutar de nuevo, él realizó un join con cliente, que se encuentra dentro de la tabla pedido, nosotros llamamos al atributo item para determinar el tamaño de esa lista, lo trajo de la entidad items_pedido, realizó un join con la entidad producto y un join con la entidad categoría, pero esa entidad no se encuentra en items_pedido.

[07:44] Esa entidad se encuentra en producto. Entonces sí hubiese otra, si dentro de categoría hubiese otro atributo con la anotación ManyToOne también sería instanciada, también sería llamada con un join. Entonces imagínate cuántas veces nosotros podemos extender esa cadena.

[08:08] Lo que nosotros vamos a hacer para corregir ese error, ese error de desempeño, que es una parte de las buenas prácticas es utilizar un atributo en la notación ManyToOne, que es el atributo fetch=FetchType.LAZY. Si vemos acá, nosotros tenemos dos tipos, el tipo lazy del tipo eager.

[08:36] Para las anotaciones del tipo ManyToOne, nosotros vamos a utilizar el cargamento o la estrategia de cargamento del tipo lazy o perezoso, que nos va a permitir llamar los elementos de cliente únicamente cuando sean solicitados. Ya los elementos del tipo OneToMany o ManyToMany, ellos por default ya son del tipo lazy.

[09:00] Entonces, todos los elementos del tipo ManyToMany por default son eager, trae todos los elementos y si dentro de ese tributo hay otros elementos del tipo ManyToOne también los va a traer, entonces tenemos que colocarle a ellos, vamos a ir a la tabla producto, el atributo lazy, así como en la tabla items_pedido que tenemos el atributo producto del tipo ManyToOne y el atributo pedido del tipo ManyToOne.

[09:32] Entonces de esta forma, nosotros le estamos indicando a nuestra aplicación que vamos a traer esos recursos únicamente cuando sea necesario. Vamos a ir a nuestra prueba de desempeño. Vas a anotar esta acá y vamos a realizar la primera consulta. Vamos a ejecutarla para ver si realizó un join a la hora de obtener la fecha.

[09:57] Importé todos los elementos, realicé un select de todas las columnas que existen dentro de la entidad pedido donde el pedido coincide con el ID, pero de esta vez ya no realizó un join con la entidad cliente. Si nosotros vamos a la otra consulta y obtenemos el tamaño de la lista vamos a ver que él realizó el select de la tabla pedido.

[10:31] No realizó el join y realizó el select de los atributos en la entidad items_pedido y no realizó el join con la entidad producto ni categoría. Vamos a hacer una última prueba donde nosotros traemos un cliente de esa tabla pedido. Entonces sería, vamos acá a clonar esto, quitamos esa anotación. Y esta vez nos vamos a traer el nombre del cliente. Sería getCliente().getNombre().

[11:11] Y vamos a ver qué nos responde la consulta. Él importa los valores y realiza un select de los atributos en la entidad pedido, de la tabla pedido, con el id y luego de eso realiza un select en la tabla cliente para obtener el nombre. Entonces aquí nos retorna el nombre de ese cliente dentro de la entidad pedido.

[11:44] Entonces, resumiendo, en la entidad pedido nosotros tenemos dos tipos de notaciones, tenemos la notación ManyToOne y la anotación OneToMany. Todas las anotaciones que sean del tipo ToOne, OneToOne o ManyToOne por default son del tipo eager. Quiere decir que ellos tienen un cargamento anticipado.

[12:02] Van a ser cargados a pesar de que los datos no sean requeridos en esa consulta. Y todos los elementos que sean del tipo ToMany, ManyToMany o OneToMany ellos van a ser cargados únicamente cuando sean requeridos dentro de nuestra consulta.

[12:22] Eso fue establecido así en JPA, porque generalmente los elementos del tipo ToMany son listas y para evitar que se sature la memoria, el estándar y el lazy para los elementos del tipo ToMany, como OneToMany o ManyToMany. Entonces, sin embargo, al nosotros colocar esta anotación del tipo lazy, nosotros podemos generar algunos problemas dentro de nuestra aplicación, es lo que vamos a hablar más adelante, y vamos a ver cómo se resuelven esos problemas.