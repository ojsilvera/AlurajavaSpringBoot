# Incluyendo datos en una tabla

1. Introducción al comando SELECT:
   - Se explica el uso del comando SELECT para visualizar registros en una tabla y filtrarlos según las necesidades.

2. Acceso al archivo SQL:
   - Se menciona que se proporciona un archivo SQL adjunto para usar en la lección.

3. Creación de tablas:
   - Se remueven las tablas existentes tbclientes y tbproductos.
   - Se crean nuevamente las tablas tbcliente y tbproducto con campos específicos y una clave primaria en tbcliente.

4. Visualización de registros con SELECT:
   - Se muestra cómo seleccionar todos los campos usando "SELECT * FROM tbcliente".
   - Se explican los campos de la tabla tbcliente.
   - Se ejemplifica seleccionar campos específicos usando "SELECT DNI, nombre FROM tbcliente".
   - Se ilustra el uso de alias para renombrar campos usando "SELECT NOMBRE AS Nombre_Completo, SEXO AS Género, EDAD AS
     Años, DIRECCION1 AS Domicilio".
   - Se demuestra el uso de LIMIT para limitar el número de filas mostradas con "LIMIT 6".

Script de SQL basado en el resumen:

```sql
-- Creación de la tabla cliente con clave primaria en DNI
CREATE TABLE tbcliente (
    DNI VARCHAR(20) PRIMARY KEY,
    nombre VARCHAR(100),
    direccion1 VARCHAR(200),
    direccion2 VARCHAR(200),
    barrio VARCHAR(50),
    ciudad VARCHAR(50),
    estado VARCHAR(50),
    cp VARCHAR(10),
    fecha_nacimiento DATE,
    edad SMALLINT,
    sexo VARCHAR(10),
    limite_credito FLOAT,
    volumen_compra VARCHAR(50),
    primera_compra BIT
);

-- Creación de la tabla producto con clave primaria en código
CREATE TABLE tbproducto (
    codigo VARCHAR(20) PRIMARY KEY,
    nombre VARCHAR(100),
    descripcion VARCHAR(200),
    precio_unitario FLOAT,
    existencias INT
);

-- SELECT para visualizar todos los campos de la tabla tbcliente
SELECT * FROM tbcliente;

-- SELECT para visualizar campos específicos de la tabla tbcliente con alias
SELECT DNI, nombre AS Nombre_Completo, sexo AS Género, edad AS Años, direccion1 AS Domicilio
FROM tbcliente;

-- SELECT para limitar la visualización a 6 filas de la tabla tbcliente
SELECT * FROM tbcliente LIMIT 6;
```

Nota: El script crea las tablas tbcliente y tbproducto con campos específicos y ejecuta SELECT para visualizar los
registros. El archivo completo contiene más líneas de código para configurar la base de datos y cargar datos, pero aquí
solo se incluyó el resumen relevante para el texto seleccionado.

## filtrado de registros

1. Introducción al filtrado de registros:
   - Se explica el uso del comando SELECT con el filtro WHERE para seleccionar registros específicos basados en ciertos
     valores de campo.

2. Filtrado en la tabla de productos:
   - Se muestra cómo usar SELECT * FROM tbproducto WHERE SABOR = 'maracuyá' para seleccionar los registros con sabor
     "maracuyá".
   - Se ejemplifica SELECT * FROM tbproducto WHERE envase = 'Botella de vidrio' para seleccionar registros con envase
     "Botella de vidrio".

3. Actualización de registros:
   - Se menciona cómo cambiar el valor del campo "sabor" de "limón" a "cítrico" usando el comando UPDATE con WHERE.
   - Se destaca que los cambios con UPDATE son in place y afectan los registros directamente.

Script de SQL basado en el resumen:

```sql
-- SELECT para filtrar registros de la tabla tbproducto con sabor "maracuyá"
SELECT * FROM tbproducto WHERE SABOR = 'maracuyá';

-- SELECT para filtrar registros de la tabla tbproducto con envase "Botella de vidrio"
SELECT * FROM tbproducto WHERE envase = 'Botella de vidrio';

-- UPDATE para cambiar el valor del campo "sabor" de "limón" a "cítrico"
UPDATE tbproducto SET SABOR = 'cítrico' WHERE SABOR = 'limón';
```

Nota: El script contiene solo las líneas de código relevantes para el resumen del texto. El archivo completo del texto
incluye más ejemplos y detalles sobre el filtrado y actualización de registros.

## filtrando usando mayor que, menor que y diferente

1. Introducción a filtros avanzados:
   - Se explica cómo crear filtros utilizando condiciones como mayor que (>), menor que (<), igual (=) o
     diferente de (!=) para seleccionar registros específicos basados en valores numéricos y alfanuméricos.

2. Filtros numéricos:
   - Se muestra el uso de SELECT * FROM tbcliente WHERE EDAD > 27 para seleccionar clientes mayores de 27 años.
   - Se ejemplifica SELECT * FROM tbcliente WHERE EDAD < 27 para seleccionar clientes menores de 27 años.
   - Se destaca la sintaxis para utilizar menor o igual (<=) y mayor o igual (>=) en las consultas.

3. Filtros alfabéticos:
   - Se demuestra cómo usar SELECT * FROM tbcliente WHERE NOMBRE > 'Erica Carbajo' para seleccionar nombres alfabéticamente
     mayores que "Erica Carbajo".
   - Se indica que se pueden utilizar los operadores menor o igual (<=) y mayor o igual (>=) con nombres alfabéticos.

4. Filtros con coma flotante:
   - Se muestra el problema de precisión al buscar registros con coma flotante exactos.
   - Se introduce el uso del comando BETWEEN para establecer un rango y seleccionar registros con precisión.

Script de SQL basado en el resumen:

```sql
-- Filtros numéricos
SELECT * FROM tbcliente WHERE EDAD > 27;
SELECT * FROM tbcliente WHERE EDAD < 27;
SELECT * FROM tbcliente WHERE EDAD <= 27;
SELECT * FROM tbcliente WHERE EDAD >= 27;

-- Filtros alfabéticos
SELECT * FROM tbcliente WHERE NOMBRE > 'Erica Carbajo';
SELECT * FROM tbcliente WHERE NOMBRE >= 'Erica Carbajo';

-- Filtros con coma flotante
SELECT * FROM tbproducto WHERE PRECIO_LISTA BETWEEN 28.48 AND 28.52;
```

Nota: El script contiene solo las líneas de código relevantes para el resumen del texto. El archivo completo del texto
incluye más ejemplos y detalles sobre el uso de filtros avanzados.

## filtrando fechas

Resumen del texto como un DBA experto:

1. Introducción a filtros con fechas:
   - Se explica cómo realizar filtros utilizando fechas en una tabla.
   - Se muestra la sintaxis para seleccionar registros que coincidan con una fecha específica utilizando el operador
     igual (=).

2. Filtros de fecha:
   - Se demuestra cómo usar SELECT * FROM tbcliente WHERE FECHA_NACIMIENTO < '1995-01-13' para seleccionar personas que
     nacieron antes del 13 de enero de 1995.
   - Se ejemplifica SELECT * FROM tbcliente WHERE FECHA_NACIMIENTO >= '1995-01-13' para seleccionar personas que nacieron
     el mismo día o después de Marcos Rosas.

3. Filtros con partes específicas de la fecha:
   - Se muestra cómo utilizar la función YEAR() en la consulta para seleccionar registros de un año específico,
     como SELECT * FROM tbcliente WHERE YEAR(FECHA_NACIMIENTO) = 1995 para obtener a las personas que nacieron en el año
     1995.
   - Se utiliza la función DAY() para seleccionar registros de un día específico,
     como SELECT * FROM tbcliente WHERE DAY(FECHA_NACIMIENTO) = 20 para obtener a las personas que nacieron el día 20 de
     cualquier mes.

Script de SQL basado en el resumen:

```sql
-- Filtros de fecha
SELECT * FROM tbcliente WHERE FECHA_NACIMIENTO = '1995-01-13';
SELECT * FROM tbcliente WHERE FECHA_NACIMIENTO < '1995-01-13';
SELECT * FROM tbcliente WHERE FECHA_NACIMIENTO >= '1995-01-13';

-- Filtros con partes específicas de la fecha
SELECT * FROM tbcliente WHERE YEAR(FECHA_NACIMIENTO) = 1995;
SELECT * FROM tbcliente WHERE DAY(FECHA_NACIMIENTO) = 20;
```

Nota: El script contiene solo las líneas de código relevantes para el resumen del texto. El archivo completo del texto
incluye más ejemplos y detalles sobre el uso de filtros con fechas.
