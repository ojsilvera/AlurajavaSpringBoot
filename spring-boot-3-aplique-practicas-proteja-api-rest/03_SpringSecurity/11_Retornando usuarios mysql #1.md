[00:00] Ahora lo que vamos a ver es cómo guardar nuestro usuario en la base de datos, y ahora sí en efecto disparar nuestro request y hacer la validación de mi login contra mi base de datos. Para esto lo primero que yo voy a hacer es abrir mi base de datos con el cliente de base datos que ustedes estén usando, voy a abrirlo aquí y voy a agregarle un registro nuevo.

[00:26] Para esto voy al más, el id va a ser autogenerado, mi nombre usuario va a ser el que yo marqué anteriormente: diego.rojas y mi clave, aquí entra algo curioso, porque mi clave yo te estoy mandando aquí como número del 1 al 6. Entonces hubiera guardado del 1 al 6 aquí, pero esto es muy inseguro.

[00:48] Las claves normalmente se guardan en algún formato encriptado o hasheado. Nosotros vamos a usar el formato de Hash Bcrypt. Entonces por ejemplo en esta página web que yo entré internet, si yo quiero saber cuál es el hash en Bcrypt, en algoritmo Bcrypt del 1 al 6, me va a dar este hash aquí.

[01:11] No vamos a entrar aun en detalle sobre lo que es has hecho y lo que es encriptación, pero lo que yo voy a hacer es copiar este string grande de aquí, que es el hash de este string de aquí del 1 al 6. Regreso aquí y es lo que yo voy a guardar aquí en mi base datos.

[01:29] Le voy a dejar a guardar y listo, todavía tengo mi usuario y tengo mi clave guardada en mi base datos. Como bien tengo guardado entonces yo debería ser capaz de acceder ahora sí a mi login. Vamos a dispararlo, y ahora recibo 403 forbidden. ¿Por qué? Aquí entra otro dato curioso.

[01:50] Vemos que de todas formas Hybernate lanzó la query para intentar descubrir cuál es mi usuario. Pero tampoco lo encontró, ahora lo debería encontrar porque mi login es el mismo, “diego.rojas” y aquí es “diego.rojas”, pero las claves no son las mismas. ¿Y eso es por qué?

[02:12] Voy a cerrar esto aquí. Y aquí entra una cosa también interesante yo tengo aquí mi entidad usuario. ¿Pero ustedes se han preguntado como Spring sabe el campo clave, significa que aquí está la clave? Lo que quiero decir es para comenzar Spring está escrito en inglés y nosotros no estamos especificando nada de password o algo así, esta es nuestra clave y este es nuestro login. Son nombres completamente diferentes a lo que Spring pueda conocer.

[02:46] Y esto es porque si bien Spring puede sonar a que es mágico, no lo es. Spring por dentro necesita que nosotros le digamos cuál es el atributo que él va usar como username, cuál es el atributo que él va a usar para comparar la clave, y también necesita saber cuál es el algoritmo de hashing que hemos usado para que él sea capaz de comparar el tipo de contraseña que le hemos mandado.

[03:18] Entonces son dos cosas que tenemos que hacer. Perdón, tres cosas que tenemos que hacer. Indicarle el tipo de encriptación de nuestra clave, indicarle nuestro campo user, indicarle nuestro campo password. Vamos a comenzar primero por la configuración. Venimos aquí a la configuración de Spring y lo que necesitamos aquí es un password encoder: PasswordEncoder.

[03:47] Y esto va a retornar BCryptPasswordEncoder. Nada más. Vamos a decirle esto, olvidé de declararlo. Listo. Y recuerden como siempre. @Bean para que esté disponible en mi contexto de Spring y listo, ya tengo mi BCryptPasswordEncoder. ¿Qué más necesito ahora?

[04:16] Ahora necesito decirle a mi usuario, que este es un usuario de Spring. Para esto implemento una interfaz llamada UserDetails, esta de aquí abajo. UserDetails me va a pedir que yo implemente una serie de métodos, que son todos estos de aquí.

[04:37] Ustedes saben que en una interfaz yo debo implementar todos, pero no se preocupen, porque no tiene nada del otro mundo como quien dice. Si vemos aquí, por ejemplo lo que me dice es por defecto si la credencial está expirada, si la cuenta está bloqueada, si el usuario está habilitado. Entonces por defecto yo le voy a decir que sí.

[04:54] Copio aquí, veo que sí, la cuenta no está bloqueada, es verdad, la cuenta no está bloqueada, la cuenta no está expirada, es verdad, no estamos expirados. Y aquí entra lo que es la implementación mediante la cual nosotros le decimos que el username es el campo login y el password es mi campo clave. De esta forma yo ya le digo a Spring internamente por si acaso cuando valides la clave hazlo con este campo y usando este PasswordEncoder.

[05:28] Aquí no este de aquí, aquí es PasswordEncoder. Entonces, guardamos y vamos a ver qué tal va ahora. Es por eso que si se dan cuenta, aquí en el repositorio, si alguno de ustedes se dio cuenta que yo estaba retornando un objeto diferente al que yo declaré aquí inicialmente, y pensó que iba a saltar de un error, mis felicitaciones porque estás muy atento.

[05:53] En efecto este findByLogin nunca me iba a recordar un usuario porque lo que él busca es un objeto del tipo UserDetails, que es exactamente el que yo le estoy dando aquí a UserDetails en este momento, a mi usuario.

[06:10] Mi usuario ahora es un objeto del tipo UserDetails. Acabo de ver un campo que yo olvidé actualizar y es este de aquí, que es el GrantedAuthority. ¿Por qué? Lo vamos a dejar venir primero en null, porque quiero ver qué es lo que Spring me va a dar ahora que yo aún no implemento esto.

[06:28] Yo ya le dije dónde está la clave, dónde está el nombre de usuario, pero por alguna razón no le estoy especificando el Authority, estos roles que tiene. Le vuelvo a dar y me sigue dando 403 en efecto. ¿Por qué? Porque Authorities significa el rol que va a tener este usuario dentro de mi aplicación.

[06:49] Si no tiene ningún rol asignado automáticamente Spring le bloquea el acceso y me dice: “no puedes entrar porque tú no tienes ningún tipo de rol asignado para ti.” ¿Qué debo hacer ahora? Lo que yo voy a hacer una lista, una lista de SimpleGrantedAuthority y esta lista va a ser de “ROLE_USER” y voy a inicializarlo obviamente.

[07:27] Ahora sí. Perfecto. Entonces lo que le estoy diciendo aquí es que este rol de usuario va a ser el que tenga por defecto mis usuarios que entren aquí. Voy a darle guardar. Voy a limpiar mi terminal. Esperamos que reinicie mi servicio porque tengo el web tools activado y me da una excepción. Me dio un exception primero, pero ahora no. Vamos a ver, quizás fue un reload tardío. Vamos a entrar.

[07:55] Y sigue con el 403 aquí a pesar de que yo le estoy dando mi nombre usuario y mi clave. ¿Cuál es el error que estoy teniendo? Vamos a ver aquí y de todas formas no es posible que encuentre mi usuario. ¿Esto por qué es? Vamos a explorar un poco más lo que tenemos aquí.