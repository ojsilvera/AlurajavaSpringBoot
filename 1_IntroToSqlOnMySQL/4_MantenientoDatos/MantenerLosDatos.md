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
