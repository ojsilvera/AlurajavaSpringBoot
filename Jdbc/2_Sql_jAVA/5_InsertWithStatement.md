[00:00] Hola, seguimos con el desarrollo de la aplicación. Ya estamos recuperando la conexión y listando los productos de la base de datos en la pantalla. Pero estos datos fueron insertados en la base desde la consola de MySQL en el inicio del curso. Y ahora nosotros vamos a desarrollar la funcionalidad que guarda un nuevo producto en la base de datos desde nuestra aplicación.

[00:22] Y para eso vamos a estar utilizando este formulario acá, combinado con el botón de guardar para poder guardar un nuevo producto a la base de datos. Vamos a ver en el código el camino que el botón guardar realiza. Vamos a entrar aquí en el ControlDeStockFrame y vamos a ver el método configurarAccionesDelFormulario.

[00:42] Aquí, en el configurarAccionesDelFormulario tenemos varias acciones, y la primera de ellas es sobre el botón guardar. Tenemos un listener de acción de acá y el listado de métodos que son ejecutados son guardar, limpiar tabla y cargar tabla, que ya conocemos, nosotros vamos a entrar en el método guardar.

[01:05] Aquí en el método guardar nosotros estamos tomando los datos del formulario, estamos acá ejecutando algunas validaciones, para ver si está en blanco el campo, tomamos la cantidad también para ver si está todo bien y tenemos una parte acá de to do, que es en donde nosotros reformamos el formulario en un objeto de producto y nosotros enviamos la información para el método guardar.

[01:34] Aquí en el método guardar nosotros tenemos que darle vida, entonces tenemos que agregar toda esta lógica para hacer el insert en la tabla de productos. Pero antes de eso, vamos a cuidar de esta parte acá que dice que estamos recibiendo un objeto de producto, un object y en lugar de hacer un new object acá, nosotros vamos a seguir un poco el modelo que hicimos con el listar de producto, por ahora vamos a estar utilizando, trabajando con el Maip.

[02:03] Entonces vamos a hacer lo siguiente acá. En el new object, en lugar de estar haciendo así, vamos a hacer que el producto sea un new hashmap de String, String(); y en lugar de new Object, vamos a estar haciendo el producto.put y ahí decimos ("NOMBRE", recibe este valor como parámetro, como un valor, punto y coma.

[02:37] Ahí tenemos otra vez producto.put. Ahí ponemos la clave como "DESCRIPCIÓN", ahí está, coma el texto, ahí guardamos. Y por último hacemos un producto.put de la "CANTIDAD". Y esta cantidad, como ella es del tipo entero, vamos a estar haciendo un String.valueOf(cantidadInt); y acá punto y coma. Bueno, ahí falta un paréntesis acá y ahora sí, estamos enviando el producto.

[03:26] Vamos a importar acá el hashMap, ahora sí, importamos el hashMap y el producto lo estamos enviando al método guardar. Y acá el guardar cuando entremos acá al método guardar. Presioné el botón equivocado, perdón. Ahora sí, en el guardar vamos a estar esperando en lugar de un object, que todas las clases son de objeto, vamos a recibir un Map del tipo string.

[03:57] String. Ahí está. Bueno, ahora en el método guardar lo primero que vamos a hacer es tomar la conexión de la ConnectionFactory, entonces vamos a hacer Connection con = new ConnectionFactory(). ahí está, punto recuperaConexión(). Listo, ya tenemos la conexión, ahí está.

[04:22] Ahora, nosotros vamos a trabajar con la lógica de crear un statement, entonces de la conexión hacemos un con.createStatement. Ahí está, y vamos a llamar el método execute, entonces hacemos, perdón, primero hacemos acá, asignamos a una variable, ahora sí, statement, y el statement, voy a bajar un poquito acá, statement.execute y acá vamos a tener nuestra lógica del insert.

[04:59] Entonces acá para escribir la query de insert, nosotros, si queremos insertar algo en la tabla, tenemos que escribir una query de insert. Entonces, para agregar los valores, vamos a hacer lo siguiente, vamos a escribir: ("INSERT INTO PRODUCTO y ahí vamos a declarar las columnas, (nombre, descripción y cantidad)".

[05:22] Recuerden que no necesitamos estar poniendo acá el valor de id porque el id es AUTO_INCREMENT. Entonces tenemos acá la cantidad, voy ahora a crear otro string acá que va a ser "VALUES", que vamos a estar declarando qué valores vamos a estar agregando acá. Entonces en los values vamos a estar concatenando los valores de producto.get, la clave ("NOMBRE"), ahí está. A ver, un paréntesis más acá, ahí está.

[05:59] Lo concatenamos siguiendo acá la, ahora sí. Faltó un + acá, perdón. Ahora sí, concatenamos "VALUES"( + producto.get("NOMBRE") + ",", vamos siguiendo acá y vamos a agregar ahora, ¿qué otro valor? Ponemos producto.get("DESCRIPCION") concatenamos acá con otra coma y por último, ponemos el valor de producto.get("CANTIDAD");

[06:52] Perfecto. Ya está nuestra query de insert. "INSERT INTO PRODUCTO (nombre, descripción, cantidad)" con los valores, nombre, descripción y cantidad también, pero acá tenemos que tener atención en una cosa que dejé pasar. Como estamos agregando el producto.get("NOMBRE") y producto.get("DESCRIPCIÓN"), que son valores del tipo string, nosotros tenemos que poner comillas simples acá.

[07:14] Entonces en el VALUES tenemos la comilla simple para señalar que es un string adentro del string de SQL. Y las comillas simples en SQL señalan un string, y acá en Java son las comillas dobles que señala un string. Entonces no tenemos mucho problema acá, pero ahí estamos con comilla simple, abrí, cerré para nombre, ahora abrí acá también arriba y cerré acá abajo para la descripción y para la cantidad no es necesario, porque la cantidad en la tabla es un valor numérico.

[07:50] Anteriormente, nosotros vimos que el método execute devuelve un valor de tipo boolean, para señalar cuando el resultado de la query es un resultSet que es un listado, devuelve true, y si el resultado no es un resultSet, devuelve un false. O sea, en el caso del insert, el retorno no va a ser un listado, entonces su valor será false.

[08:15] Igualmente, este valor no es útil para nosotros. ¿Entonces qué vamos a hacer con este valor false? Sería mejor si tuviéramos un resultado que nos dijera cuál es el producto que fue insertado luego de la creación, tipo el id del producto. Acá con JDBC y todas sus clases y métodos, tenemos cómo saberlo, y ya lo veremos.

[08:35] Este método execute tiene una sobrecarga, un parámetro adicional para señalar si alguna clave autogenerable fue creada, o sea, el id es una clave autogenerable. Entonces nosotros podemos utilizar este parámetro y para utilizarlo nosotros podemos utilizar las constantes que existen en la clase statement y este valor sería el RETURN_GENERATED_KEYS.

[09:04] Con este valor acá en este parámetro de la sobrecarga de execute, nosotros podemos tomar el id que fue creado como el resultado de la ejecución de la query de insert. Entonces aquí estamos diciendo que cuando se ejecuta un insert, yo quiero tener de vuelta la clave generada, o sea, el id que fue generado en la tabla.

[09:25] Así que luego que ejecutamos este statement, nosotros podemos tomar la clave generada con el método statement.getGeneratedKeys(); ¿Este método va a retornar qué? Algo que ya conocemos: el resultSet. O sea, tenemos acá un resultSet tiene el listado de ids que fueron creados porque nosotros podemos en un insert insertar más de un valor.

[09:54] O sea, acá tenemos un listado con todos los ids que fueron generados en la ejecución de esta query. Entonces nosotros podemos hacer que con eso, iterarlo con un while: while(resultSet.next()) Y acá, dentro de este método, de este loop, perdón, nosotros podemos tomar el valor del id que fue generado. Bueno. Y para tomar el valor nosotros ya sabemos cómo se hace también. ¿Cómo es?

[10:27] Es resultSet.getInt. Como es un id, nosotros estamos tomando el valor entero. Y acá, para cambiar un poco, voy a tomar como habíamos dicho. Son devueltas filas como resultado, por ejemplo, en el select fue una fila acá con cuatro posiciones. Acá tenemos una fila con una sola posición, entonces el getInt va a ser de la posición 1 para saber cuál fue el id que fue generado.

[11:00] ¿Y acá nosotros qué vamos a hacer con eso? Por ahora, vamos a estar imprimiendo este valor en la consola para ver cuál fue el id que fue generado. Entonces voy a hacer acá un system.out.println. Ahora sí. A ver. Bueno, ahí no está ejecutando, pero system.out.println y vamos a agregar el siguiente valor en este comando.

[11:33] "Fue insertado el producto de ID" y voy a poner acá un %d y va a ser así. String.format, para quedar un poco más lindo, en lugar de salir concatenando strings, va a ser el String.format, y tomamos este resultSet acá, dejame arreglar un poquito este código. Ahí está y tenemos el resultSet.getInt.

[12:07] Para finalizar acá tenemos que hacer el throws de SQLException. Ahora sí el método deja de quejarse pero tenemos que tratarlo acá en el ControlDeStockFrame. Entonces el método guardar lo voy a agregar adentro de un bloque de try catch, que vamos a hacer igual como hicimos con el método de cargar tabla, que en lugar de imprimir el StackTrace, vamos a hacer un throw new RuntimeException, la excepción encapsulada.

[12:46] Ahí está, guardamos todo y ahora sí vamos a ejecutar una vez más la aplicación. Voy a parar acá, la que estaba ejecutando y la voy a ejecutar una vez más para ver cómo va a funcionar nuestro formulario. Bueno, acá está la aplicación. Nosotros tenemos el formulario, y siguiendo la lógica del botón guardar cuando ya tenemos el formulario y hagamos clic en guardar, nosotros vamos a ejecutar el comando insert en la base de datos después de tomar la conexión con ella.

[13:14] Vamos a ver, vamos a agregar acá un vaso. Entonces vaso, vaso de cristal, y vamos a agregar 10 vasos. Hagamos un clic en guardar y tenemos un error. Bueno, vamos a ver qué pasa. Dice que tenemos un error de sintaxis. Vamos a ver acá qué pasa con la sintaxis. Volviendo acá, vamos al productoController, tenemos INSERT INTO PRODUCTO, voy a dar un espacio acá para ver.

[13:52] Nombre, descripción, cantidad, valores. Abro comillas, producto.get("NOMBRE"), cierra la comilla. Abro una comilla más, producto.get("DESCRIPCION"), cierro la comilla. O sea. Ya vi, ya vi qué pasó, me olvidé de cerrar el paréntesis de la query, mira. Entonces hago un + acá y pongo el string con el paréntesis cerrado.

[14:22] Ahora voy a parar la aplicación y la voy a ejecutar una vez más. Ahora vamos a ver si funciona, vamos una vez más. Vaso, vaso de cristal 10. Haga un clic en guardar y registrado con éxito, ahí apareció un tercer producto acá, ID 3, vaso, vaso de cristal, con 10 cantidades y acá en la consola tenemos el "Fue insertado el producto de ID 3". Perfecto.

[14:52] Entonces finalizamos una funcionalidad más de nuestra aplicación y cuando insertamos un nuevo producto acá en nuestra aplicación, la consola de Eclipse nos va a informar que el ID del nuevo producto fue generado y nos está mostrando acá también tanto en la consola como en el frame de la aplicación el número 3, o sea muy bien.

[15:15] Para la próxima clase vamos a aprender cómo borrar un registro guardado en la base de datos.