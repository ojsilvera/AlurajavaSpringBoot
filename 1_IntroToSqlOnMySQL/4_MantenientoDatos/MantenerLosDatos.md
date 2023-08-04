# Insertar registros

1. Introducción a la inserción de datos:
   - Se procederá a insertar datos en la tabla de productos utilizando un archivo de Excel con la información requerida.

2. Preparación para la inserción:
   - Se asegura que la base de datos "jugos" esté seleccionada utilizando el comando "USE jugos".

3. Comando de inserción:
   - Se utiliza el comando "INSERT INTO tbproductos" para insertar datos en la tabla "tbproductos".
   - Se especifican las columnas (producto, nombre, envase, volumen, sabor y precio) a las que se insertarán valores.

4. Inserción de valores:
   - Se insertan los valores correspondientes a cada columna utilizando el comando "VALUES".
   - Los valores de tipo VARCHAR (producto, nombre, envase y sabor) se colocan entre comillas sencillas.
   - El valor de tipo FLOAT (precio) se escribe sin comillas, utilizando punto en lugar de coma decimal.

5. Verificación de la inserción:
   - Se utiliza el comando "SELECT * FROM tbproductos" para verificar que el registro ha sido insertado correctamente en
     la tabla.
   - Se muestra el registro insertado con su respectiva información.

En resumen, se ha demostrado cómo insertar datos en la tabla de productos utilizando comandos SQL en MySQL Workbench, y
se ha verificado que la inserción fue exitosa mediante una consulta SELECT. Este proceso de inserción se puede repetir
para agregar más registros a la tabla.

## Registros multiples

1. Introducción a la inserción de múltiples registros:
   - Se explicó que se procederá a insertar varios registros en la tabla de productos de forma manual.

2. Preparación para la inserción:
   - Se copia el script que contiene los comandos SQL con los valores de los nuevos registros desde una planilla de Excel.

3. Inserción de múltiples registros:
   - Se pegan los comandos SQL en un nuevo script vacío.
   - Se modifica cada comando SQL con los valores correspondientes para los nuevos registros.
   - Los valores de tipo VARCHAR se colocan entre comillas sencillas y los de tipo FLOAT se escriben sin comillas,
     utilizando punto en lugar de coma decimal.

4. Ejecución de la inserción:
   - Se ejecuta el script con los comandos SQL utilizando el botón de "rayo" en MySQL Workbench.
   - Se verifica que la inserción fue exitosa y se muestran los 4 registros insertados en la tabla de productos.

En resumen, se ha mostrado cómo insertar múltiples registros en la tabla de productos utilizando comandos SQL en MySQL
Workbench. Los registros se ingresan manualmente en un nuevo script y luego se ejecuta para realizar la inserción en la
base de datos. Se muestra que los registros fueron insertados correctamente en la tabla.

## Alterando registros

1. Introducción a la alteración de registros:
   - Se explica que se procederá a corregir errores en algunos registros de la tabla de productos.

2. Preparación para la alteración:
   - Se copia el script desde un archivo adjunto (SQL4.3) que contiene los comandos SQL para la actualización de registros.
   - Se ejecuta un SELECT para visualizar la tabla antes de realizar las correcciones.

3. Corrección de registros:
   - Se utiliza el comando UPDATE para modificar los campos de los registros con errores.
   - Se establecen los nuevos valores para los campos que se deben corregir.

4. Uso de filtro para la actualización:
   - Se utiliza el WHERE para filtrar los registros que se deben actualizar.
   - Se explica la necesidad de desactivar el "modo seguro de actualización" en las preferencias del MySQL Workbench para
     permitir la ejecución del UPDATE sin una clave primaria definida.

5. Reinicio del MySQL Workbench:
   - Se reinicia el MySQL Workbench para aplicar la configuración de "modo seguro de actualización" desactivado.

6. Ejecución de la actualización:
   - Se ejecuta nuevamente el script de UPDATE para corregir los registros de la tabla de productos.

7. Verificación de los cambios:
   - Se realiza un SELECT para visualizar la tabla actualizada y se comprueba que los cambios se hayan realizado correctamente.

En resumen, se ha explicado cómo corregir registros con errores en la tabla de productos utilizando el comando UPDATE en
MySQL Workbench. Se realiza una actualización de los campos incorrectos y se utiliza un filtro con el WHERE para aplicar
los cambios solo a los registros específicos. Luego de desactivar el "modo seguro de actualización", se ejecuta el script
de UPDATE y se verifica que los registros hayan sido corregidos exitosamente.

## Excluyendo registros

1. Introducción a la eliminación de registros:
   - Se explica que se utilizará el comando DELETE para remover registros de la tabla.

2. Distinción entre DROP y DELETE:
   - Se aclara la diferencia entre los comandos DROP y DELETE: DROP se utiliza para objetos más relevantes como columnas
     o tablas completas, mientras que DELETE se refiere a registros individuales.

3. Uso del comando DELETE:
   - Se muestra el comando DELETE FROM tbproductos para borrar registros de la tabla "tbproductos".
   - Se advierte sobre la importancia de utilizar un filtro (WHERE) para evitar eliminar toda la tabla accidentalmente.

4. Realización de la eliminación:
   - Se ejecuta el comando DELETE con un filtro específico para borrar un registro con el producto 773912.
   - Se muestra cómo el registro ha sido eliminado y se verifica que ya no aparece en la tabla.

5. Precaución en el uso del comando DELETE:
   - Se advierte que el comando DELETE puede ser peligroso si se utiliza sin un filtro adecuado, ya que podría eliminar
     toda la tabla.
   - Se menciona que se aprenderá a crear una llave primaria en el próximo video para proteger los registros.

-- Script para eliminar el registro con producto = '773912' de la tabla 'tbproductos'

```sql

    DELETE FROM tbproductos
    WHERE producto = '773912';
```

## Incluyendo Claves primarias

Resumen del texto como un DBA experto:

1. Introducción a la importancia de las llaves primarias:
   - Se menciona la importancia de establecer una llave primaria en las tablas para mantener la integridad de los datos
     y evitar duplicidad de registros.

2. Restauración del registro eliminado:
   - Se restaura un registro previamente eliminado en la tabla "tbproductos" utilizando el comando INSERT INTO con el
     valor "773912".

3. Creación de una llave primaria:
   - Se utiliza el comando ALTER TABLE para agregar una llave primaria a la columna "producto" de la tabla "tbproductos"
     mediante el comando "ADD PRIMARY KEY (producto)".

4. Demostración de la función de la llave primaria:
   - Se intenta insertar nuevamente el registro "773912" en la tabla, pero el sistema muestra un error debido a la
     duplicidad del valor en la columna que se ha establecido como llave primaria.

5. Importancia de establecer llaves primarias:
   - Se reitera la importancia de establecer una llave primaria al momento de crear una tabla para evitar duplicidad y
     mantener la integridad de los datos.

-- Insertar el registro con producto = '773912' (este registro debería generar un error debido a la llave primaria)

```sql

    INSERT INTO tbproductos (producto, nombre, envase, volumen, sabor, precio)
    VALUES ('773912', 'clean', 'lata', '350 ml', 'naranja', '2.81');

```

Nota: El script intenta insertar nuevamente el registro con producto = '773912', pero como este producto ya es una clave
primaria en la tabla, se generará un error indicando que ya existe una entrada duplicada. Esto demuestra cómo la llave
primaria evita la duplicidad de registros en la tabla.

## Manipulando fechas y campos logicos

1. Creación de una llave primaria en la tabla de clientes:
   - Se utiliza el comando ALTER TABLE para agregar una llave primaria a la tabla tbclientes con el campo "DNI" como
     clave primaria.

2. Adición de una nueva columna:
   - Se utiliza el comando ALTER TABLE para agregar una nueva columna llamada "fecha de nacimiento" del tipo DATE a la
     tabla tbclientes.

3. Inserción de un nuevo registro en la tabla de clientes:
   - Se utiliza el comando INSERT INTO para agregar un nuevo cliente a la tabla tbclientes con valores específicos para
     cada campo.

4. Consideraciones sobre la sintaxis y formato de fecha:
   - Se menciona que el formato de fecha en MySQL es año-mes-día, para evitar confusiones con diferentes formatos de fecha.

Script de SQL basado en el resumen:

```sql

    -- Agregar la llave primaria (DNI) a la tabla de clientes (tbclientes)
    ALTER TABLE tbclientes
    ADD PRIMARY KEY (DNI);

    -- Agregar una nueva columna (fecha de nacimiento) a la tabla de clientes (tbclientes)
    ALTER TABLE tbclientes
    ADD COLUMN fecha_nacimiento DATE;

    -- Insertar un nuevo registro en la tabla de clientes (tbclientes)
    INSERT INTO tbclientes (DNI, nombre, direccion, direccion2, barrio, ciudad, estado, cp, edad, sexo, limite_credito,
    volumen_compra, primera_compra, fecha_nacimiento)
    VALUES ('456789548', 'Pedro el Escamoso', 'Calle del Sol, 25', '', 'Los Laureles', 'CDMX', 'Estado de México', '65784',
    55, 'Masculino', 1000000.0, '2000 litros', 0, '1971-05-25');

```

Nota: El script realiza la creación de la llave primaria, la adición de la nueva columna "fecha de nacimiento" y la
inserción de un nuevo registro en la tabla tbclientes. Se asume que la estructura completa de la tabla tbclientes ya ha
sido creada previamente con las demás columnas mencionadas en el texto.
