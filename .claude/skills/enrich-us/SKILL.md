---
name: enrich-us
description: Evalúa una historia de usuario existente de CityFix según INVEST y propone criterios de aceptación Given/When/Then, señalando ambigüedades, contradicciones y dependencias. Úsala solo cuando el desarrollador la invoque con el identificador de la historia.
argument-hint: "<story-id>"
disable-model-invocation: true
---

# Enriquecer una historia de usuario

Historia a enriquecer: `$ARGUMENTS`

Esta skill **propone**; no modifica ningún archivo hasta que el desarrollador apruebe de forma explícita.

## Procedimiento

1. **Identificador.** Si `$ARGUMENTS` está vacío, pedir el identificador y detenerse.
2. **Localizar fuentes.** Buscar el PRD y el backlog vigentes en el repositorio (convención prevista: `docs/product/`). Si no existen, o hay varios candidatos, informar y preguntar cuál es el vigente. No continuar sin ellos.
3. **Comprobar la historia.** Buscar el identificador exacto. Si no existe, indicarlo, listar los identificadores cercanos y detenerse. No crear la historia.
4. **Recuperar contexto.** Leer la historia, sus requisitos y reglas de negocio de origen, los criterios ya existentes y las historias o tickets que la referencian. Citar documento y ubicación de cada dato.
5. **Evaluar con INVEST** (Independiente, Negociable, Valiosa, Estimable, Pequeña, Testeable). Para cada letra: cumple, cumple parcialmente o no cumple, con evidencia. Si no es Pequeña, proponer cómo dividirla.
6. **Proponer criterios Given/When/Then** que cubran, cuando apliquen:
   - camino principal;
   - errores y validaciones;
   - permisos por rol y ámbito municipal, y visibilidad pública o interna;
   - casos límite (por ejemplo ubicación fuera del término municipal, municipio no habilitado, fotos ausentes o excesivas, concurrencia, funcionamiento sin IA).
7. **Separar origen.** Marcar cada criterio como *confirmado* (respaldado por requisito del PRD o backlog, con su referencia) o *propuesto* (inferido por esta skill).
8. **Listar hallazgos:** ambigüedades, contradicciones con otros documentos, dependencias con otras historias o decisiones pendientes, y preguntas concretas para el desarrollador.

## Reglas para los criterios

- Describir comportamiento observable desde la perspectiva del usuario o del sistema.
- No prescribir endpoints, clases, campos de base de datos, códigos HTTP ni tecnologías.
- Un comportamiento por escenario; lenguaje de dominio del producto; sin inventar reglas de negocio no decididas: convertirlas en preguntas.
- Redactar en español.

## Salida

Presentar en la conversación, sin escribir archivos:

1. Resumen de la historia y sus fuentes.
2. Evaluación INVEST.
3. Criterios Given/When/Then (confirmados y propuestos, diferenciados).
4. Ambigüedades, contradicciones, dependencias y preguntas.
5. Cambios concretos que se propondrían a la historia.

Terminar preguntando qué cambios aprueba el desarrollador. Solo después de su aprobación explícita, aplicar exactamente los cambios aprobados, con los permisos normales de Claude Code, y mostrar el diff.
