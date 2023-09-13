[00:00] Hola. Continuando con el desarrollo de nuestra aplicación, hasta este punto ya nosotros tenemos nuestro código organizado y hemos realizado la primera persistencia para un producto.

[00:09] Ahora el cliente nos solicitó agregar dos nuevas propiedades para ese producto, que sería la fecha de registro y la categoría a la que pertenece ese producto. Entonces, para eso nosotros vamos a ir a la clase producto, nuestra aplicación y vamos a agregar esa propiedad.

[00:27] Propiedad va a ser private, vamos a colocar aquí LocaDate, que va a ser el tipo, fechaDeRegistro va a ser el nombre del atributo y vamos a un asignar el valor de una vez.

[00:44] El método estático LocalDate.now, entonces con eso nosotros aseguramos que al ser instanciado el producto se esté guardando la fecha actual en la que se está instanciando.

[00:57] El tipo que va a ser guardado en la base de datos va a ser el tipo date o Time stamp, dependiendo de la base de datos. Y la siguiente propiedad que nosotros vamos a agregar en la clase producto va hacer la categoría. Esa categoría va a ser privada y no va a ser un elemento del tipo de string ni del tipo entero, sino va a ser del tipo categoría.

[01:23] Ese atributo se va a llamar categoría. Entonces el cliente nos mencionó que tenemos unos elementos, unas categorías limitadas, nosotros vamos a tener software, vamos a tener libros y vamos a tener celulares.

[01:35] Entonces para eso es recomendable cuando nosotros tenemos elementos limitados conocidos, es recomendable utilizar el numerador, entonces nosotros vamos a construir el enumerador a partir de esa categoría dentro del paquete modelo.

[01:51] Vamos a finalizar acá, ya tenemos nuestro enumerador creado y ahora vamos a agregar los elementos de ese enumerador. Los elementos van a ser como ya mencionamos SOFTWARES, LIBROS y CELULARES. Ya tenemos nuestra categoría configurada.

[02:10] Vamos a guardar acá y de vuelta en la clase producto nosotros podríamos haber colocado aquí un string pero eso permitiría múltiples opciones para el usuario que está guardando, los elementos del producto y eso permitiría que él se equivoque y daría paso a errores, entonces para evitar eso nosotros nos mantenemos con el enumerador.

[02:33] Pero usando el numerador como ya nosotros habíamos mencionado, a la hora de guardar en la base de datos, el nombre va a ser un elemento de tipo varchar la descripción va a ser varchar, el precio de hacer un elemento del tipo decimal y el id va a ser un elemento de tipo entero.

[02:48] Pero esta categoría no pertenece a ninguna de esas conocidas. Entonces nosotros vamos a colocar acá constructor para pasar esos parámetros nuevos. Vamos a ir a fuentes, generar constructor y vamos a desmarcar el id y la fecha de registro.

[03:10] Ya que el id es generado automáticamente en la base de datos y la fecha de registro y que nosotros le asignamos un valor. Generamos ese constructor guardamos aquí los cambios, nos aseguramos que hayamos guardado aquí la categoría y nos está generando un error, ya que nosotros hemos generado un constructor como parámetro.

[03:31] Vamos a instanciar ese producto nuevamente con los nuevos parámetros, entonces sería producto celular y aquí vamos a instanciar un producto con el nombre que sería “Samsung”, la descripción que sería teléfono usado, el precio que se tira un elemento del tipo bigDecimal y el precio sería 1000.

[04:04] Y por último, nos está faltando la categoría. La categoría va a ser categoría.CELULARES. Guardamos, faltando un punto y coma acá y ya con eso tenemos instanciado nuestro producto. Entonces vamos a ejecutar esta aplicación para ver que se está guardando en la base de datos.

[04:28] He creado la tabla producto, tenemos el id que ese tipo entero y la categoría es del tipo integer o del tipo entero. Entonces el valor que se está guardando para esa categoría es el elemento en el que se encontraría esta categoría si estuviese un arreglo entonces en este caso se está guardando, nosotros estamos guardando celulares, él está guardando el número 3.

[04:56] Esto daría paso a errores ya que si se alteran las posiciones, si nosotros ahora colocamos los celulares acá arriba esos números ahora pasarían a ser 1, 2 aquí 3. Pero anteriormente nosotros habíamos guardado el número 3 como celular y ahora el número 3 pertenece a la clase LIBROS.

[05:18] Entonces por eso no es recomendable guardar los números o un valor numérico en la base de datos ya que estos pueden ser alterados. Entonces, para nosotros darle más significancia a lo que está haciendo persistir, nosotros vamos a guardar la palabra como string. Para eso, nosotros aquí vamos a guardar y vamos a ir a la clase producto donde usar una anotación de JPA que es la anotación @Enumerate.

[05:53] Esa anotación tiene un parámetro (EnumType) del tipo string. Ella una serie de valores y nosotros vamos a usar el string, que nos va a permitir guardar la palabra que está siendo registrada en el enumerador.

[06:15] Guardamos ese enumerador, importamos la clase y vamos a ejecutar de nuevo nuestra aplicación. Si nosotros ejecutamos la aplicación nuevamente vemos que se creó la tabla producto, el id es de tipo entero y la categoría de esta es del tipo varchar. Eso quiere decir que él guardo la palabra y no la posición en la que se encuentra en ese arreglo.

[06:45] Vemos la descripción que también es varchar, la fecha de registro que es el tipo date y el nombre varchar y el precio numérico. Entonces, con esto concluimos la parte de la solicitud de ese cliente de agregar las nuevas propiedades y en la siguiente parte nosotros vamos a continuar con los mapeamentos y vamos a hacer una extensión de la categoría para convertirlo a una tabla.