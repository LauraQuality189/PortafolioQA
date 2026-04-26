## System Benhavior:
- La API permite crear bookings
- Devuelve un ID único al crear un booking
- Los datos se almacenan correctamente
- Se puede consultar un booking por ID
- Permite actualizar bookings existentes
- Permite eliminar bookings existentes

## Real Flow:
- POST /booking → Crea un booking y devuelve bookingid
- GET /booking/{id} → Recupera un booking específico
- PUT /booking/{id} → Actualiza completamente un booking existente
- DELETE /booking/{id} → Elimina un booking existente
- POST /auth → Genera token de autenticación

## Real Observations
- La API genera los ID's automáticamente
- Tras el POST, cuando se crea un nuevo booking, los datos se generan correctamente. El ID siempre aparece en el listado de bookings de la ruta principal
- POST devuelve 500 "Internal server error" si el JSON está incompleto
- En GET, cuando consulto un ID exitente desde el Postman, me muestra los datos registrados correctamente
- En GET, cuando el ID no existe devuelve 404 "Not Found"
- PUT requiere token válido
- En PUT, actualiza corretamente los datos, siempre que el Json esté completo y los el token auth esté en el header
- En PUT, Si el token es inválido o no autorizado, devuelve 403 Forbidden. Si el método o payload es incorrecto, puede devolver 405 Method Not Allowed
- En DELETE, permite eliminar un Booking siempre que el token esté vigente y la sesión del ID a eliminiar esté activa, si no está activa la sesión o el token está vencido devuelve error 403
- El PUT y el DELETE Funcionan con token en header. El token se crea correctamente con las credenciales del admin

## QA Risks
- Permite crear bookings sin validación. De hecho, permite crearlos enviando campos vacíos
- La respuesta del GET del ID en el navegador no devuelve nada más que la frase “I’m a teapot”, por más que el ID existe. En el postman se comporta de la manera correcta
- PATCH está declarado como disponible en OPTIONS, pero no está completamente implementado. Al intentar usarlo, por más que se envían los datos correctos, devuelve 405 "Method Not Allowed"
- En la actualización de los datos tampoco valida campos vacíos
