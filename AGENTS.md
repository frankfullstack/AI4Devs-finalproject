# AGENTS.md — CityFix

Instrucciones permanentes para agentes de código en este repositorio. Son estables y no dependen de la rama ni de la etapa del proyecto. El detalle vive en la documentación del repositorio, no aquí.

## Proyecto

CityFix es una plataforma para comunicar y gestionar incidencias en espacios públicos de España, con cuatro roles: ciudadano, gestor, operario y administrador. La visión inicial del producto está en `PROJECT_CONTEXT.md`; no se duplica aquí. Ese documento no es un PRD ni acredita diseño o implementación, y puede evolucionar mediante decisiones explícitas y revisadas.

## Guía del repositorio

- Inspeccionar el estado real del repositorio antes de actuar; no asumir que existen archivos, carpetas, herramientas o configuraciones.
- Los documentos especializados (producto, arquitectura, API) se crean cuando son necesarios y se enlazan desde `readme.md`, que es el documento principal del proyecto.
- Mantener los cambios pequeños, coherentes y limitados a lo pedido.

## Flujo de desarrollo

- Desarrollo incremental y Spec-Driven Development: especificar y decidir antes de implementar, e implementar en pasos verificables.
- Antes de implementar, consultar las especificaciones y la documentación aprobadas que apliquen. Si faltan o se contradicen, señalarlo en vez de suponer.
- El orden incremental de entrega no elimina capacidades de la visión global.
- Las decisiones relevantes de producto y arquitectura requieren aprobación humana explícita antes de darse por definitivas.
- Distinguir siempre entre requisito, propuesta, implementación y resultado verificado. No presentar trabajo futuro como hecho.
- No inventar funcionalidades, archivos, comandos, resultados de pruebas, integraciones ni decisiones. Lo no verificado se indica como supuesto o cuestión pendiente.

## Arquitectura y principios de ingeniería

- Arquitectura hexagonal y Clean Architecture aplicadas de forma pragmática: dominio separado de frameworks y proveedores externos, sin abstracciones innecesarias.
- Preferir la solución más simple; no añadir dependencias ni infraestructura sin necesidad justificada.
- Cada módulo tiene una responsabilidad clara; las dependencias apuntan hacia el dominio.

## Calidad y verificación

- Verificar los cambios con las herramientas y comandos que existan realmente en el proyecto (scripts, configuración, documentación). Si no hay ninguno aplicable, decirlo; no inventar comandos.
- Informar de los resultados tal como son, incluidos fallos y comprobaciones no realizadas.
- Mantener trazabilidad entre requisitos, implementación y pruebas.

## Seguridad y privacidad

- Aplicar autorización por rol y ámbito municipal en consultas, imágenes, operaciones y notificaciones.
- No incluir secretos, credenciales ni datos personales en el repositorio.
- El producto debe funcionar completamente sin IA. La IA es opcional y solo recomienda: las acciones oficiales las realizan el sistema y las personas autorizadas.

## Documentación

- La documentación es parte del cambio: al modificar requisitos, decisiones o comportamiento, actualizar en el mismo cambio los documentos afectados.
- Evitar duplicar contenido entre documentos; enlazar en su lugar.

## Convenciones

- Documentación y explicaciones: español.
- Código, identificadores, contratos de API y nombres de tests: inglés.
- Git:
  - Trabajar en ramas de propósito concreto cuando corresponda; no modificar directamente ramas protegidas.
  - Revisar los cambios antes de integrarlos.
  - Commits claros y coherentes, un propósito por commit.
  - Los commits, push, Pull Requests y merges los realiza exclusivamente el desarrollador. El agente puede inspeccionar Git, mostrar diffs y proponer mensajes de commit, pero no ejecuta esas operaciones, aunque se le soliciten durante una tarea ordinaria.
  - No realizar operaciones destructivas sin autorización explícita.
