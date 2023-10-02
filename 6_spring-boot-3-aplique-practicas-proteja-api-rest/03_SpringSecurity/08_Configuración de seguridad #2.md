[00:00] Seguido de sessionManagement, sin parámetros, porque había otro método con parámetros, no se preocupen, y aquí es donde va a ocurrir la magia de Spring, porque en este parámetro de aquí, en sessionCreationPolicy, lo que yo le voy a decir es que quiero que me póliza de creación de mi sesión sea completamente stateless.

[00:28] Finalmente para cerrar le voy a decir que .and().build(); eso sería todo lo que tengo que hacer para especificar que mi sesión va hacer stateless. Me está dando un error de compilación aquí a nivel del scrf, porque no estoy atrapado una excepción. Tengo dos opciones: o con try catch o en la firma del método.

[00:52] Yo voy a escoger la segunda, la más sencilla y listo, no tengo nada más que hacer por ahora. Voy a iniciar mi servidor, vamos a agrandar esto un poco para ver la terminal y vamos a probar los cambios. En este punto ya deberíamos tener algunos cambios en la aplicación.

[01:14] Tengo una excepción aquí y me dice que no hay propiedad username para el tipo usuario. Es por esto. Recordemos que yo estoy identificando find by username que me dejé ya por el nombre del parámetro, pero en mi entidad usuario el parámetro es login.

[01:36] ¿Entonces esto cómo debería ser? Debería ser findByLogin. Aquí le voy a hacer un refactor, voy a renombrar y le voy a decir que es un findByLoging. Enter y listo, ya está refactorizado, reviso aquí mi AutenticacionService. También está listo. Inicio nuevamente mi servidor, ese era el error que yo estaba teniendo.

[02:07] Perfecto. Aplicación inicializada correctamente y venimos a nuestro listado de médicos que me estaba dando Unauthorized hace un momento. Voy a enviar aquí mi request, y miren, ya tengo ahora sí mis accesos normales como estaban antes. ¿Por qué? Porque mi autenticación ya es stateless, es decir, ya no maneja por defecto una autenticación a nivel de Spring Security, que me cierra todo por defecto y que me da una página de login por defecto autogenerada.

[02:39] Sino que ahora yo tengo el control sobre mí autenticación, y parece que volvimos a donde comenzamos porque nuevamente tengo todos mis recursos abiertos, expuestos, en ninguna parte me piden que me loguee y no tengo digamos cómo loguearme en mi aplicación, porque no tengo dónde poner mi usuario y mi clave para generar mi token. Eso lo vamos a descubrir en el próximo video.