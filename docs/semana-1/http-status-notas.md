dia 3: http

200 (ok): la solicitud ha tenido exito. 
201 (created): la solicitud ha tenido exito y se ha creado un nuevo recurso como resulatdo de ello. 
204 (no content): la peticion se ha completado con exito pero su respuesta no tiene no tiene ningun  contenido, aunque los encabezados pueden ser utiles  
400 (bad request): esta respuesta significa que el servidor no pudo interpretar la solicitud dada una sintaxis invalida.  
401 (unauthorized): es nnecesario autenticar para obtener la respuesta solicitada.
403 (forbidden): el clinete no posee los eprmisos necesarios para cierto contenido, por lo que el servidor esta rechazando otrogar una respuesta apropiada 
404 (not found): el servidor no puede encontrra el contenido solcitado 
409 (conflict): esta respueta puede ser enviada cuando una peticion tiene conflicto con el estado actual del servidor 
422 (Unprocessable Entity): la peticion estaba bien formada pero no se pudo seguir debido a errores de sematica  
500 (internal server error): el servidor ha encontrado una sitiacion que no sabe como manejarla.


--Caso : El usuario da clic en "Guardar" y el formulario no hace nada (Error 400/422)--

Qué está pasando: 
El usuario llenó un formulario de registro en portal, pero envió un formato de fecha incorrecto o un campo obligatorio vacío que el frontend no validó antes de disparar la petición. El backend rechaza el intento con un 400 Bad Request o 422 Unprocessable Entity.

Acción Recomendada: Abre la pestaña Network (Red) en las herramientas de desarrollador del navegador (F12), localiza la petición en rojo y revisa la pestaña Response. Mapea esos errores del backend para pintarlos en rojo debajo de cada input del formulario, evitando que el usuario quede a ciegas.