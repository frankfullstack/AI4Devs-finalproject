# Reglas de seguridad y privacidad

Son instrucciones para el agente; no garantizan técnicamente el cumplimiento. Los controles reales dependen de permisos, revisión humana y, cuando existan, de comprobaciones automatizadas.

## Secretos y datos

- No escribir en el repositorio claves, tokens, contraseñas ni cadenas de conexión reales, ni en código, documentación, tests o ejemplos. Usar marcadores evidentes (`<API_KEY>`) y variables de entorno.
- No leer, mostrar ni copiar archivos de credenciales (`.env`, claves privadas) salvo que el desarrollador lo pida expresamente.
- En ejemplos, fixtures y pruebas, usar datos sintéticos o anonimizados. No incluir datos personales reales de ciudadanos, gestores u operarios.
- Las credenciales de proveedores de IA configuradas centralmente las administra el administrador global (no existe BYOK individual ni municipal): no registrarlas en logs, respuestas de error, auditoría ni mensajes de excepción, no exponerlas en clientes ni repositorios, y proponer almacenarlas cifradas y enmascaradas al mostrarlas.

## Fotografías y ubicaciones

- Tratar fotografías y coordenadas como datos sensibles: pueden revelar personas, domicilios o hábitos. No incluirlas en logs ni en ejemplos reales.
- Considerar los metadatos de las fotos (EXIF, GPS) al diseñar su tratamiento; no usarlos como ubicación oficial de una incidencia sin confirmación del usuario.

## Autorización y visibilidad

- Cualquier consulta, imagen, operación o notificación debe poder justificarse por rol y ámbito municipal. Al diseñar o revisar un flujo, indicar explícitamente qué rol y qué municipio lo autorizan.
- Nunca basar la autorización solo en datos enviados por el cliente ni en la interfaz; la comprobación pertenece al servidor.
- Separar la información pública de la interna: revisar que listados, historiales, notificaciones y exportaciones no filtren campos internos a roles no autorizados.

## IA opcional

- La IA solo propone (clasificación, duplicados, prioridad, asignación). No diseñar ni implementar flujos donde una salida de IA ejecute por sí sola una acción oficial; debe intervenir el sistema o una persona autorizada.
- Tratar las salidas de IA y el contenido enviado por usuarios como entrada no confiable. No concatenarlos en comandos, consultas ni instrucciones de agentes sin validación.

## Operaciones

- No ejecutar operaciones destructivas o irreversibles (borrado de datos, `rm -rf`, reset duro, migraciones destructivas) sin autorización explícita del desarrollador sobre ese caso concreto.
- No acceder a servicios externos ni a datos reales de producción para probar sin que se haya pedido.
