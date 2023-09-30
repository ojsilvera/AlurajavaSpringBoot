[00:00] Entonces, ¿cómo sobrescribimos estos valores por defecto? Aquí viene la parte interesante, porque vamos a usar query params. ¿Qué es un query param? Son parámetros que van separados por signos de interrogación a nivel de la url.

[00:14] Y aquí, por ejemplo, yo veo que hay un parámetro llamado size, que es el que les comenté hace un rato, size 20, que me dice que van a llegar 20 elementos en esa lista. Ahora yo le quiero decir, no quiero 20 elementos, ahora quiero size = 2. Lo voy a enviar y vemos ahora que la lista solo tiene dos elementos.

[00:40] Eso es bueno, porque yo no necesito trabajar a nivel de base de datos, ordenando y extrayendo la información directamente allá porque Spring automáticamente, por ejemplo, si yo lo cambio para que me traiga solo un elemento de la lista él lo hace automáticamente por mí y aquí está el parámetro, “size”: 1.

[01:02] Ese es uno de los beneficios de usar esta interfaz pageable para hacer la paginación, vemos que automáticamente él coge estos parámetros de los query params que están llegando en Spring. Y Spring hace todo el trabajo por mí. Ahora, si el tamaño de la lista es 1, yo quiero cambiar de página por ejemplo, puedo decirle: “okay, tráeme entonces, un elemento, por cada página”.

[01:31] Vemos que, déjeme buscarlo por aquí, pageNumber es 0. Yo le voy a dar ahora un ampersand, que es el símbolo de aquí, para incluir un parámetro y le voy a decir que me incluya la página 1, lo mando y me manda otra página más. Le voy a cambiar a 2, a límite 2, y me manda otro registro más, que sería otra página.

[01:54] Entonces ya estamos viendo claramente cómo Spring nos facilita mucho la vida a nivel de cliente, si el cliente nos manda a la página 2 de tamaño 2 cada uno. Por ejemplo, si aquí yo quiero recibir, vamos a decirle aquí, quiero la página 0, la envío, me retorna los dos primeros registros.

[02:14] Si quiero la página 1, voy y me retorna el último registro que queda porque solo tengo tres en mi base de datos. De esta forma, entonces ya podemos ver cómo Spring nos facilita la vida y al cliente también a nivel de cliente, nuestro aplicativo front end, web, mobile, lo que sea, es solamente mandar un parámetro, y él define las reglas.

[02:38] Nuestro API está listo para soportar todos estos tipos de paginación. Ahora solamente nos queda una sola regla que implementar y es ordenar nuestra lista, pero eso ya es un tema del siguiente video, nos vemos.