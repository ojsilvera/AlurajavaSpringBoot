# Tipos de datos

1. Tipos de datos numéricos:
   - Números enteros: tinyint, smallint, mediumint, int y bigint con diferentes capacidades y rangos.
   - Números decimales: float y double para valores con y sin coma flotante, y decimal o numérico para valores fijos
     con una cantidad máxima de dígitos.

2. Tipos de datos de fecha y hora:
   - Date: almacena fechas en el formato año, mes, día.
   - Datetime: almacena fechas y horas.
   - Timestamp: similar a Datetime, pero considera el cambio horario de cada país.
   - Time: almacena horas sin la fecha.

3. Tipos de datos string:
   - Char: cadena de caracteres con valor fijo que ocupa más memoria.
   - Varchar: cadena de caracteres con valor variable que optimiza el uso de memoria.
   - Binary y Varbinary: trabajan con bits ceros y unos.
   - Blob: almacena datos binarios grandes como imágenes.
   - Text: almacena texto largo.
   - Enum: define opciones predefinidas en una lista.
   - Set y Collate: establecen el tipo de caracteres ASCII a utilizar.

4. Tipos de datos espaciales:
   - Point: almacena coordenadas geográficas exactas.
   - Geometry y Polygon: relacionados con áreas geográficas.
   - Linestring: almacena una línea en una dimensión.

5. Utilización de los tipos de datos en la creación de tablas:
   - Los tipos de datos se utilizan para definir la estructura y contenido de las tablas en una base de datos.
   - Cada tipo de dato tiene sus propias capacidades, rangos y atributos, lo que permite una gestión eficiente de los
     datos.

6. Uso de MySQL Workbench para la administración de tablas:
   - MySQL Workbench es una herramienta gráfica que facilita la administración y manipulación de tablas y datos en la
     base de datos.

Este resumen destaca los diferentes tipos de datos disponibles en MySQL y cómo se utilizan para crear tablas en una
base de datos. También se menciona la importancia de MySQL Workbench como una herramienta eficaz para la administración
de tablas y datos en la base de datos.

## Creando tabla

1. Requisitos para la tabla de clientes:
   - Se necesita crear una tabla para almacenar los registros de clientes de la empresa de jugos.
     Los campos requeridos son:

        DNI (varchar),
        nombre completo (varchar),
        dirección 1 (varchar),
        dirección 2 (varchar),
        barrio (varchar),
        ciudad (varchar),
        estado (varchar),
        código postal (varchar),
        edad (smallint),
        sexo (varchar),
        límite de crédito (float),
        volumen de compra (float),
        si ya realizó la primera compra (bit).

2. Consideraciones al definir los campos:

   - El campo DNI se define como varchar para preservar los ceros a la izquierda en el número de identificación.
   - Se utilizan varchars para los campos de texto, permitiendo la flexibilidad de almacenar solo la cantidad necesaria
     de caracteres.
   - El campo edad se define como smallint, ya que no es necesario que una persona viva más de 150 años.
   - El campo sexo se define como varchar de 1, para almacenar una sola letra.
   - El campo límite de crédito y volumen de compra se definen como float, evitando preocuparse por la presentación de
     los datos.
   - El campo de primera compra se define como bit, con valor 1 para sí y 0 para no.

3. Creación de la tabla en MySQL Workbench:
   - Se utiliza el comando CREATE TABLE para crear la tabla TBCLIENTES.
   - Se establecen los nombres y tipos de datos para cada columna de la tabla.
   - Se emplea la sintaxis adecuada para definir los campos de acuerdo con sus requisitos.

4. Consideraciones sobre la nomenclatura de la tabla:
   - Se nombra la tabla como TBCLIENTES por practicidad, pero es importante seguir las políticas y estándares establecidos
     por cada empresa.

5. Resultado y visualización de la tabla:
   - Al ejecutar el comando CREATE TABLE, se verifica que la tabla ha sido creada correctamente.
   - La tabla aparece en la base de datos jugos con todas las columnas especificadas.

En resumen, se ha creado una tabla de clientes en la base de datos jugos, cumpliendo con los requisitos y consideraciones
para cada uno de los campos. Se han utilizado los tipos de datos adecuados y se ha verificado la creación exitosa de la
tabla.

## Creando tabla con asistente

1. Requisitos para la tabla de productos:
   - Se necesita crear una tabla para almacenar los registros de los productos de jugos que la empresa desea vender.
     Los campos requeridos son:

        código del producto (varchar),
        nombre del producto (varchar),
        envase (varchar),
        tamaño (varchar),
        sabor (varchar),
        precio del producto (float).

2. Creación de la tabla utilizando MySQL Workbench:
   - Se abre MySQL Workbench y se selecciona la base de datos jugos.
   - Se crea la tabla productos utilizando el asistente de creación de tablas.
   - Se especifican los nombres y tipos de datos para cada columna de la tabla.
   - Los campos que permiten valores nulos se mantienen por defecto.

3. Consideraciones sobre los tipos de datos:
   - Se utilizan varchars para los campos que pueden tener caracteres alfanuméricos con tamaños adecuados para cada caso.
   - El campo precio se define como float para almacenar el valor del producto sin preocuparse por la presentación de los
     datos, que se ajustará posteriormente.

4. Resultado y visualización de la tabla:
   - La tabla productos se crea en la base de datos jugos con todas las columnas especificadas.

En resumen, se ha creado la tabla de productos para la empresa de jugos, siguiendo los requisitos y consideraciones para
cada uno de los campos. La tabla se ha creado exitosamente utilizando el asistente de creación de tablas en MySQL Workbench.
