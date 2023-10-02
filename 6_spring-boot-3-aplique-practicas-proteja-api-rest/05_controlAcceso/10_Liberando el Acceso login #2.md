[00:00] Porque vamos a la lógica. Aquí vamos a leer un poco lo que estamos haciendo. ¿Qué hacemos aquí? Primero obtenemos el header y después le preguntamos si el token es nulo o está vacío, que me lance esta excepción y es aquí donde estamos teniendo el error, porque este filtro se está ejecutando de todas formas.

[00:19] Porque el filtro de Spring fue el primero y ya lo dejó pasar, ahora mi filtro está siendo ejecutado y como yo valido que token no sea ni nulo ni vacío, entonces yo mando esto, este error. ¿Cómo puedo solucionarlo? Voy a invertir el orden en el que yo estoy haciendo cosas. ¿A qué me refiero con invertir?

[00:42] En lugar de preguntar si el token está nulo o vacío, lo que yo le voy a decir es que si el token, if token no está nulo entonces ahí va a ejecutar esta lógica y eso lo voy a borrar. Porque si este header no existe entonces esto va a ser nulo. Si el token no está nulo, entonces recién ahí en lugar de validar, si es que es igual a nulo, yo voy a validar que no sea nulo.

[01:16] Porque solo ahí yo voy a hacer este proceso de activar el filtro, de lo contrario, no voy a hacer nada. Vamos a ver si funciona esta implementación, vemos que ya está recargando. Recargó. Entonces venimos otra vez, enviamos a Insomnia y tenemos 200 OK.

[01:42] ¿Pero por qué no pasa? Porque no estamos haciendo el filterChain.doFilter. Entonces venimos aquí le ponemos aquí el filterChain. Esperamos que recargue un momento más. Listo. Enviamos y ya está funcionando para mi login, vemos que ya está abierto. ¿Pero qué pasará con este de aquí? Vemos que ya está prohibido.

[02:10] Porque no estoy enviando ningún token. Entonces con esto yo tengo mi login completamente abierto para cualquier request y mis demás métodos completamente forbidden. En este caso, como yo tengo el token, le voy a enviar y también me está dando forbidden.

[02:28] Entonces ahora yo tengo otro problema diferente, porque yo estoy enviando un token válido. Incluso lo que yo voy a hacer aquí es enviar en este nuevo talking que me ha devuelto yo voy a reemplazar aquí en mi listado. Vengo aquí, lo enviamos y de todas formas por más que estoy enviando un token válido, me dice que está prohibido. Y esto no está bien.

[02:52] Este es un error que estamos cometiendo. Entonces vamos al código nuevamente para saber en dónde es que está fallando. Si se fijan bien, logró hacer la query contra la base de datos. Entonces vamos a ver en qué parte es que está fallando en el TokenService, porque en la validación hay alguna cosa que no está bien hecha.

[03:14] Vamos a dar el código. Dice valida apiSecret con este issuer y verifícalo. Aquí le voy a decir getSubject. ¿Pero qué pasaría si el token no llega? Yo no valido si el token llega nulo o no. Entonces lo que yo voy a ver ahora es decirle que si el token es null, ahí yo voy a darle un throw new RuntimeException().

[03:52] Ya estoy validando primero que todo que mi token no llegue nulo. De esa forma yo me aseguro que subject no va a dar un error aquí en este punto porque yo lo estoy haciendo ya a nivel del token en sí. Eso es lo primero que quiero validar, para aplicar aquí vemos que ya recargó, voy a limpiar mi terminal y voy a enviar otra vez y vemos que me sigue retornando forbidden.

[04:16] ¿Esto por qué es? Vamos a ver aquí. Me dice que ya completó la inicialización. ¿Qué más tengo en este código? Venimos por aquí, en el securityFilter está recibiendo authorization, el token no está viniendo nulo porque yo estoy consiguiendo generar. Solo para eso yo voy a darle aquí un sout, un System.out.print, para validar.

[04:40] Validamos que token no es null. De esta forma si es que entra aquí, sabemos que el token no va a ser null. Entonces vamos a ver qué nos imprime, vemos que recargó mi servidor. Enviamos. Validamos digamos aquí y vemos que no está llegando aquí. Entonces, eso ya nos está dando un primer síntoma. ¿Por qué?

[05:04] Si yo vengo aquí, voy a decirle que “este es el inicio del filter”. Le damos salvar. Esperamos que recargue, vemos que recargó, enviamos y tampoco está siendo llamado. Vamos a hacer otra cosa porque lo que sucede es que mi filtro en este caso ya no está siendo llamado en absoluto porque ya no está imprimiendo ninguno de los valores que yo deseo que imprima aquí. Voy a tener mi servidor.

[05:46] Voy a iniciarlo otra vez en caso de ser algún problema de catching, porque de lo contrario en alguna parte yo estoy ejecutando mal mi código aquí. Entonces voy a retornar aquí y en efecto no está funcionando. Me dice que inicializó y todo eso pero no me retorna ningún tipo de error ni nada de eso.

[06:09] ¿Qué hacemos en estos casos cuando el error no está claro? Damos un paso hacia atrás, volvemos al filter y le vamos a preguntar que me imprima el token nuevamente. Voy a darle un sout. Imprime el token, guardamos.

[06:35] Ejecutamos, no me imprime nada aún, voy a probar otra vez con login. Voy a enviar. En efecto, me dice el inicio del filter el token es null. Entonces pasó por mi filtro, perfecto, y ya está. Entonces, ¿cuál es aquí el detalle? ¿Qué es lo que está sucediendo? Eso lo vamos a explorar en el próximo video.