Elegir entre el método HTTP PUT o PATCH es una pregunta común que surge cuando estamos desarrollando APIs y necesitamos crear un endpoint para la actualización de recursos. Comprendamos las diferencias entre las dos opciones y cuándo usar cada una.

PUT
El método PUT reemplaza todos los datos actuales de un recurso con los datos enviados en la solicitud, es decir, estamos hablando de una actualización completa. Entonces, con él, hacemos la actualización completa de un recurso en una sola solicitud.

PATCH
El método PATCH, a su vez, aplica modificaciones parciales a un recurso. Por lo tanto, es posible modificar solo una parte de un recurso. Con PATCH, entonces, realizamos actualizaciones parciales, lo que flexibiliza las opciones de actualización.

¿Cuál elegir?
En la práctica, es difícil saber qué método usar, porque no siempre sabremos si un recurso se actualizará parcial o completamente en una solicitud, a menos que lo verifiquemos, algo que no se recomienda.

Entonces, lo más común en las aplicaciones es usar el método PUT para las solicitudes de actualización de recursos en una API, que es nuestra elección en el proyecto utilizado a lo largo de este curso.