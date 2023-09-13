[00:00] Hola, ¿cómo les va? Ahora que aprendimos cómo abrir una conexión, vamos a avanzar con las operaciones de base de datos en nuestra aplicación. Aquí, antes de presentarles la aplicación que había comentado, voy a enseñarles cómo importar un proyecto nuevo en el Maven.

[00:20] Vieron acá que mi workspace está vacío, o sea, pueden borrar el proyecto que tiene ahí ahora y el proyecto que bajaron, que disponibilicé el link para download, van a hacer lo siguiente, van a salir sacar el zip del proyecto, lo van a copiar en el workspace de ustedes y aquí en la opción import project vamos a buscar existing Maven projects.

[00:45] Con esta opción vamos a nuestra carpeta del workspace, aquí está. Elijo el proyecto, hago un open y ya me selecciona el pom.xml. Hago un clic acá en finish y está importando el proyecto. Y ya estamos, aquí está el proyecto de control de stock. Y ahora sí les voy a presentar nuestro proyecto, voy a hacer lo siguiente, lo voy a ejecutar.

[01:14] Con la clase main acá voy a hacer un ran as java application. Y aquí está, este es nuestro proyecto con el sistema de control de stock. Aquí va a ser donde vamos a estar administrando todos los productos que existen en nuestro depósito y en la base de datos. Esta aplicación está utilizando el Java swing para crear las pantallas.

[01:43] Este es un recurso propio del Java para el desarrollo de aplicaciones desktop. Actualmente, este tipo de aplicación es muy poco utilizada, no se ve mucho en el mercado, lo más común es ver y crear proyectos web o mobile con las tecnologías que tienen más recursos y que son más actuales.

[02:00] Por ejemplo, para una aplicación web estaríamos utilizando el HTML con CSS y Javascript. En el mercado, las aplicaciones siguen otros estándares también con el front-end desacoplado del back-end, pero el concepto básico sigue igual. Así que con el Swing vamos a aprender un poco este flujo y estructura del proyecto en donde tenemos una view acá, esta view, que es el front-end del proyecto, como una página HTML.

[02:35] Y el back-end es en donde estaremos desarrollando toda la lógica de negocio y conexión con la base de datos que tiene nuestro modelo. Aquí vamos a abstraer el desarrollo de los componentes de la pantalla, porque no es nuestro enfoque ahora. Nuestro enfoque acá es desarrollar las funcionalidades para completar esta aplicación. Vamos a revisar lo que hay en ella.

[02:57] Acá para ejecutar la aplicación vieron que vine acá en el paquete com.alura.jdbc, en la clase ControlDeStockMain hice un clic derecho y la ejecuté con run as Java application. En ella vamos a abrir aquí la clase. Estamos inicializando una clase llamada ControlDeStockFrame. Este ControlDeStockFrame está cargando todo el contenido de nuestra pantalla.

[03:30] La pantalla que abre acá cuando ejecutemos la aplicación muestra un formulario con cuatro campos, un botón de guardado, un botón de guardar los datos, un botón para limpiar el formulario, un cuadro en blanco acá que va a ser donde vamos a estar listando nuestros productos y tres botones acá abajo que indican acciones de eliminar, modificar un dato y ver el reporte del depósito.

[03:58] Esta pantalla es la que el usuario final va a tener acceso para administrar el stock de productos del depósito. Pero por ahora, él no puede hacer nada. Si intentamos agregar un nuevo producto, por ejemplo, un vaso de vidrio, cantidad 1. Y hago guardar. Me dice que el registro fue guardado con éxito, pero no pasa nada, o sea, nosotros aún no tenemos nada desarrollado en nuestra aplicación, no hay ninguna lógica, no hay conexión con la base de datos.

[04:30] Y ahora es nuestra vez de agregar vida al proyecto en el back-end para completar las funcionalidades de la aplicación. Como había dicho en el comienzo de la clase, yo voy a disponibilizar para ustedes el proyecto actualizado con la estructura inicial para que avancemos con el desarrollo de las operaciones de base de datos utilizando Java. Nos vemos en la próxima clase.