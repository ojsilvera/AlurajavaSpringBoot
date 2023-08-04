# Definiciones

Las principales definiciones a tener en cuenta en mySQL son:

1. La estructura de una base de datos se compone de diversas entidades:

   - La entidad más importante es la tabla, que contiene columnas (campos) y filas (registros).

   - Los campos tienen un tipo de dato definido y los registros deben respetar esa definición, para evitar errores.

2. Las claves primarias evitan la duplicidad de registros:

   - Son campos únicos en una tabla que impiden que se repitan registros con el mismo valor en el campo seleccionado
   como clave.

   - Las claves externas se utilizan para relacionar tablas y garantizar la integridad de los datos.

3. Las bases de datos relacionales permiten utilizar vistas, procedimientos y funciones:

   - Las vistas facilitan obtener información de varias tablas al mismo tiempo sin crear una tabla con un gran número
   de campos.

   - Los procedimientos y funciones permiten realizar lógica estructurada y ejecutar cambios en la base de datos basados
   en condiciones y comandos SQL.

4. Otras entidades importantes en una base de datos son los esquemas y los triggers:

   - Los esquemas agrupan tablas por temas específicos para facilitar la organización y la administración.

   - Los triggers son alertas que activan funciones o procedimientos cuando ocurre una modificación específica en la
   base de datos.

## Workbench como IDE para SQL

1. Instalación y apertura del IDE MySQL Workbench:

   - Se ha instalado el MySQL Workbench, que es utilizado como un cliente para acceder a bases de datos.
   - Al abrir el IDE, se muestra la página de bienvenida con las conexiones disponibles, donde por defecto se encuentra
     a conexión local.

2. Conexiones a bases de datos:

   - Se puede agregar una nueva conexión haciendo clic en el botón "+" y proporcionando los detalles de la conexión, como
   el nombre, tipo y dirección IP del servidor.
   - El IDE funciona como un cliente y puede tener acceso a varios servidores, pero en este caso, solo se utilizará la
   instancia local.

3. Uso del área de comandos (Query1):

   - El área de comandos (Query1) es donde se ejecutan todos los comandos SQL.
   - Se utiliza el comando "use" para activar una base de datos específica antes de ejecutar comandos en ella.
   - El punto y coma se utiliza para indicar que un comando ha sido ejecutado y se puede pasar al siguiente.

4. Acceso a tablas y visualización de resultados:

   - Se puede acceder a una tabla haciendo doble clic en ella o usando el comando "use" seguido del nombre de la tabla.
   - Se pueden ejecutar comandos SELECT para obtener datos de las tablas.
   - El comando SELECT con asterisco (*) devuelve todos los registros de una tabla.
   - Al seleccionar varias líneas de comandos y ejecutarlas, se obtienen resultados para cada una en una nueva pestaña.

5. Errores en comandos SQL:

   - Es importante utilizar el punto y coma al final de cada comando SQL para evitar errores de sintaxis.
   - Si no se coloca el punto y coma, puede producirse un error al ejecutar comandos consecutivos.

6. Visualización y ejecución selectiva de comandos:

   - Se puede seleccionar y ejecutar solo un fragmento de comandos en el área de comandos.
   - Si se selecciona más de un comando y se ejecutan, el IDE los ejecutará en orden y mostrará los resultados en pesta-
     ñas separadas.

Este resumen destaca los conceptos clave y el proceso de trabajar con MySQL Workbench y ejecutar comandos SQL en el
entorno gráfico.

## Crear base de datos

1. Creación de una base de datos en MySQL:
   - Para crear una base de datos, se utiliza el comando "CREATE DATABASE" seguido del nombre de la base de datos.
   - La opción "IF NOT EXISTS" evita que se cree la base de datos si ya existe.
   - Se pueden especificar parámetros como el conjunto de caracteres (character set) y las reglas de comparación
   (collate) para organizar y comparar los datos.

2. Ejecución de comandos SQL en MySQL Workbench:
   - En MySQL Workbench, se crea un nuevo script para ejecutar comandos SQL.
   - Los comandos SQL pueden escribirse en mayúsculas o minúsculas, pero es una buena práctica usar las palabras clave
   en mayúsculas.
   - Se utiliza el punto y coma al final de cada comando SQL para indicar que está completo.

3. Visualización de la base de datos creada:
   - Después de crear la base de datos, se puede encontrar en la lista de bases de datos disponibles en MySQL Workbench.
   - Si no aparece de inmediato, se puede actualizar la lista haciendo clic derecho y seleccionando "Refresh".

4. Ubicación de los archivos de base de datos:
   - Los archivos de las bases de datos en MySQL se almacenan en una ruta específica en el sistema.
   - El archivo de inicialización (my.ini) contiene la ruta del directorio de datos (datadir) donde se almacenan las
   bases de datos.
   - La carpeta "data" contiene los archivos de las tablas de las bases de datos creadas.

Este resumen destaca el proceso de creación de una base de datos en MySQL, la ejecución de comandos SQL en MySQL
Workbench, y la ubicación de los archivos de la base de datos en el sistema.

## Crear base de datos con asistente

Resumen del texto como un DBA experto:

1. Creación de una base de datos con el asistente de MySQL Workbench:
   - En MySQL Workbench, se puede utilizar el asistente para crear una nueva base de datos.
   - Se accede al asistente haciendo clic derecho en el área de esquemas y seleccionando "create schema".
   - Se proporciona un nombre para el esquema o base de datos, y se elige un conjunto de caracteres (character set) y
     una regla de comparación (collation) adecuada para el tipo de datos que se utilizarán.

2. Uso de comillas para evitar conflictos con espacios en el nombre de la tabla:
   - El asistente utiliza comillas o acentos invertidos para envolver el nombre de la tabla si este contiene espacios o
     caracteres especiales.
   - Esto garantiza que no haya conflictos al crear la tabla.

3. Creación de la base de datos utilizando el asistente:
   - Una vez configurados los detalles en el asistente, se hace clic en "apply" para crear la base de datos con los
     parámetros especificados.
   - El asistente generará automáticamente el código SQL correspondiente y lo mostrará en la pestaña de consulta.

4. Ventajas del uso del asistente:
   - El asistente agiliza el proceso de creación de tablas, especialmente para quienes no están familiarizados con la
     sintaxis de SQL.
   - También es útil como recordatorio visual para los comandos SQL y permite adaptarlos según las necesidades específi-
     cas.

Este resumen destaca el proceso de creación de una base de datos utilizando el asistente de MySQL Workbench y las
ventajas que ofrece esta herramienta en comparación con la escritura manual de comandos SQL.
