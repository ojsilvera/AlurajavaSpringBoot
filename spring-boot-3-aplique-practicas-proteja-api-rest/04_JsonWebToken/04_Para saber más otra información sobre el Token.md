Además del Issuer, Subject y fecha de expiración, podemos incluir otra información en el token JWT, según las necesidades de la aplicación. Por ejemplo, podemos incluir el id del usuario en el token, simplemente usando el método withClaim:

return JWT.create()
    .withIssuer("API Voll.med")
    .withSubject(usuario.getLogin())

    .withClaim("id", usuario.getId())

    .withExpiresAt(fechaExpiracion())
    .sign(algoritmo);COPIA EL CÓDIGO
El método withClaim recibe dos parámetros, el primero es un String que identifica el nombre del claim (propiedad almacenada en el token), y el segundo la información a almacenar.

