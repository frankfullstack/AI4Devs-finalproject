---
paths:
  - "docs/**/*.md"
  - "readme.md"
  - "PROJECT_CONTEXT.md"
---

# Reglas de documentación

Se aplican al editar documentación. `docs/` es una convención prevista: la carpeta se crea cuando haya contenido que alojar.

## Coherencia y estados

- Antes de editar un documento, leer los que dependen de él o de los que depende, y mantener la cadena coherente: contexto → PRD → épicas e historias → criterios de aceptación → tickets → documentación técnica.
- Marcar el estado de cada afirmación relevante: propuesta, aprobada, implementada o verificada. Un documento no sube de estado sin una decisión humana o una evidencia concreta (cambio, prueba, resultado).
- Si dos documentos se contradicen, no elegir uno en silencio: señalar la contradicción y proponer cuál debe prevalecer.

## Identificadores y trazabilidad

- Cuando existan historias, criterios, tickets o decisiones con identificador, no renombrarlos ni reutilizarlos; las referencias cruzadas usan el identificador, no el texto.
- Cada historia debe poder rastrearse hasta su requisito de origen y hasta sus criterios, tickets y pruebas, en cuanto esos artefactos existan.
- No crear identificadores nuevos sin seguir el esquema ya vigente. Si aún no hay esquema, proponerlo y pedir aprobación.

## Contenido

- No inventar información ni completar requisitos, reglas de negocio o datos no decididos. Registrarlos como cuestión pendiente o supuesto, indicando quién debe decidirlos.
- Evitar duplicación: cada dato tiene un documento propietario y los demás lo enlazan. Al detectar contenido duplicado, proponer cuál es la fuente.
- Al cambiar un requisito, decisión o comportamiento, localizar con búsqueda los documentos afectados y actualizarlos en el mismo cambio, o listar los que queden pendientes.
- Redactar en español; mantener en inglés los identificadores técnicos, nombres de contratos y de tests.
- `readme.md` conserva la estructura de su plantilla. Completar una sección solo con información verificable.
