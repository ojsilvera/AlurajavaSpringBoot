[00:00] Ejecutamos este request y seguimos con el 403 forbidden que estamos teniendo aquí. ¿Cuál puede ser nuestro problema? Vamos a revisar el código en nuestro AuthenticationController que está recibiendo los datos de autenticación.

[00:14] Aquí está el detalle, no estamos recibiendo en este caso el request body que necesitamos y no está siendo validado, y el body. Guardamos esto, limpiamos nuestra terminal. El problema era este que no estábamos recibiendo ningún dato aquí para validar en contra, entonces la validación no estaba haciendo ella contra ningún objeto en mi base de datos.

[00:40] Limpio esto de aquí y ejecutamos ahora. Y listo. Vemos que ya nos está retornando un código 200 ok. Entonces mi usuario ya está logueado y se supone que yo tengo mi token aquí listo para ser usado. ¿Ahora deberíamos retornar un 200 o deberíamos retornar un token?

[01:05] Todo eso lo vamos a explorar en la siguiente clase. Por ahora yo sé que han sido muchos conceptos nuevos, sobre todo en la parte de configurar Spring, esta clase fue un poco larga, sobre todo por toda la facilidad que tiene Spring para ser personalizado. Les recomiendo practicar mucho, cualquier duda pueden ponerla en el foro y nos vemos en la siguiente clase.

