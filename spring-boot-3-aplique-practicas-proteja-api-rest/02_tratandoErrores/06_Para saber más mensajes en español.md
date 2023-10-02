Por defecto, Bean Validation devuelve mensajes de error en inglés, sin embargo, hay una traducción de estos mensajes al español ya implementada en esta especificación.

En el protocolo HTTP hay un encabezado llamado Accept-Language, que sirve para indicar al servidor el idioma preferido del cliente que activa la solicitud. Podemos utilizar esta cabecera para indicarle a Spring el idioma deseado, para que en la integración con Bean Validation pueda buscar mensajes según el idioma indicado.

En Insomnia, y también en otras herramientas similares, existe una opción llamada Header en la que podemos incluir cabeceras a enviar en la petición. Si agregamos el encabezado Accept-Language con el valor es, los mensajes de error de Bean Validation se devolverán automáticamente en español.

Nota: Bean Validation solo traduce los mensajes de error a unos pocos idiomas.