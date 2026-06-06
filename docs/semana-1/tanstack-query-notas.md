Dia 4:  Notas de TanStack Query (Estado del Servidor)

TanStack Query se encarga de gestionar las peticiones HTTP, el almacenamiento en caché, la sincronización y la actualización del estado del servidor en el frontend, reduciendo drásticamente el código repetitivo.

Conceptos Clave
-queryKey: Un arreglo único (ej. [users, userId]) que actúa como la llave de identificación para almacenar y buscar los datos en la caché.
-Caché: Almacenamiento temporal en memoria de las respuestas de la API para evitar peticiones duplicadas e innecesarias.
-Invalidación (invalidateQueries): Comando para decirle a la caché que ciertos datos ya son viejos (stale) y obligar a la app a volver a pedirlos al servidor.
-staleTime: El tiempo en milisegundos que los datos se consideran "frescos" antes de requerir una actualización automática en segundo plano.


