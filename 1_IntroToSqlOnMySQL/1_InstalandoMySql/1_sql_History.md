# la historia de SQL

En los años 70, en los laboratorios de IBM en San José, California, se estaba realizando una investigación Y se quería
observar la viabilidad de la implementación de un sistema de consultas a bases de datos relacionales ideado por el
británico **Edgar Frank Codd**. Él ideó una forma sencilla de manipular y extraer no solamente los datos, sino de las
estructuras de los datos, aprovechando este modelo relacional de bases de datos,
conocido como DBMS: Data Base Management Systems.

Anteriormente, las bases de datos eran secuenciales, eran una tira de caracteres de texto que la única forma de acce-
derlos era siguiéndola, entonces no había una forma de hallar una relación entre ellos, lo que impedía que se facili-
tase, el hallar estos datos de una forma como más específica y con el modelo propuesto por Codd, entonces se vio una
salida o se vio mejor una alternativa para poder trabajar con estas bases de datos relacionales.

En los años 80 surgieron otras empresas como Oracle, como SQL Server de Microsoft, que comenzaron también a utilizar
este lenguaje SQL para trabajar con bases de datos, desde luego, y al ver este surgimiento de tantas empresas queriendo
trabajar con SQL, entonces entró el Instituto Americano Nacional de Estándares o la ANSI a crear una regulación para
este lenguaje.

Y allí surgió entonces SQL, el lenguaje SQL, que funciona siguiendo o respetando CRUD, que es Create Read Update Delete,
o sea crea, lee, actualiza y borra. Eso es como un acrónimo que nos ayuda mucho a recordar los principios básicos de SQL.

la ANSI dividió estos comandos en tres grandes grupos:

*DDL, que es Data Definition Language*, que es el que se encarga de manipular todas las estructuras de las bases de datos
en sí. Entonces, por ejemplo, allí se usa el comando create para crear una base de datos o una tabla, Create table o
drop, que sería para remover una tabla, remover una base de datos,

*DML, que es Data Manipulation Lenguaje o el lenguaje de manipulación de los datos*, que ya sería select, para sele-
ccionar unos datos, insert para insertar datos a las tablas, update, que sería actualizar estos datos o delete, que se-
ría borrarlos.

*Data Control Language, que se encarga de la administración en sí* de toda la estructura de la base de datos. Entonces,
por ejemplo, está la administración de la base de datos, la administración de los accesos a usuarios de los logs,
es toda la parte de políticas de crecimiento de la base de datos, etcétera.

SQL tiene las siguientes ventajas:

    - Costo reducido de aprendizaje, al respetar el standar puede manejarse en mysql O SQL Server
      cada uno con sus reglas

    - La portabilidad. Si eventualmente la empresa quiere migrar de base de datos, entonces no está
      restringida, sino que como trabaja con SQL entonces fácilmente puede ir de Oracle a SQL Server,
      de SQL Server a MySQL, de MySQL a Postgre.

    - La longevidad. Va a durar por más tiempo, porque como también hablan el mismo lenguaje estan-
      darizado, entonces cuando surjan nuevas actualizaciones, pues no se va a caer la base de datos,
      sino que va a permanecer activa.

    - Comunicación. habrá facilidad de integración en procesos, de diferentes bases de datos, pro-
      cedimientos de TL o integración, todo esto se facilita porque están hablando el mismo lenguaje SQL.

    - libertad de elección. las empresas no se tienen que preocupar si este lenguaje va a ser compa-
      tible con el otro, porque el lenguaje nativo es el mismo, el lenguaje nativo establecido por
      la ANSI, de modo que no hay ningún problema en ello de ir de Oracle y comenzará a utilizar
      MySQL Server, por ejemplo.
