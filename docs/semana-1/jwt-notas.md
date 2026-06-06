dia 3: jwt y debugging basico

.header:
la cabecera sule contar de dos partes: el tipo de token, que es un JWT, y el algoritmo de firma utilizado, como HMAC, SHA256 o RSA. ejemplo:
{
    "alg": "HMAC",
    "typ": "JWT"
}
Luego, este JSON se codifica en Base64Url para formar la primera parte del JWT.

.payload:
La segunda parte del token es la carga útil, que contiene las declaraciones. Las declaraciones son afirmaciones sobre una entidad (normalmente, el usuario) y datos adicionales. Existen tres tipos de declaraciones: registradas , públicas y privadas. un ejemplo de carga util podria ser:
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
A continuación, la carga útil se codifica en Base64Url para formar la segunda parte del token web JSON.

.signature:
Para crear la firma, hay que tomar el encabezado codificado, la carga útil codificada, un secreto, el algoritmo especificado en el encabezado y firmarlo. Por ejemplo, si desea utilizar el algoritmo HMAC SHA256, la firma se creará de la siguiente manera:
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
La firma se utiliza para verificar que el mensaje no se haya modificado durante el proceso y, en el caso de los tokens firmados con una clave privada, también puede verificar que el remitente del JWT es quien dice ser.

--Caso 2: Pérdida de sesión al refrescar la página (F5)--

Qué está pasando: Un error común de arquitectura es almacenar el JWT únicamente en una variable de estado en memoria (como un servicio de Angular). Al presionar F5, la memoria se limpia, el token se pierde y la app expulsa al usuario al login injustamente.

Acción Recomendada: Guarda el token en un almacenamiento persistente del navegador (sessionStorage si quieres que expire al cerrar la pestaña, o localStorage si deseas mantener la sesión activa). Al arrancar la app en el archivo principal, verifica si el token existe ahí antes de decidir si lo mandas a /login o a /infinity.