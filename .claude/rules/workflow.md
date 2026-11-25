# Reglas de flujo de trabajo

## Antes de modificar

- Inspeccionar el estado real: archivos existentes, `git status`, rama actual y configuración del proyecto. No dar por hechos ficheros, herramientas ni scripts.
- Consultar las especificaciones y documentos aprobados que afecten a la tarea. Si no existen o no cubren el caso, decirlo y preguntar en lugar de suponer.
- Limitarse al alcance pedido. Si surge trabajo adicional útil, proponerlo aparte y no hacerlo.

## Durante el trabajo

- Hacer cambios pequeños, coherentes y fáciles de revisar; un propósito por cambio.
- Antes de decidir algo relevante de producto o arquitectura, presentar la propuesta con sus alternativas y esperar aprobación. No registrar como decidido lo que solo se ha propuesto.
- Si aparece una contradicción con instrucciones o documentos existentes, informar antes de modificarlos.

## Al terminar

- Revisar el propio diff antes de darlo por terminado y comprobar que solo contiene lo pedido.
- Ejecutar solo las comprobaciones que existan realmente en el proyecto e informar de lo que se ejecutó, lo que falló y lo que no se pudo verificar.

## Git

- Claude Code puede consultar el estado Git, mostrar diffs, el historial y proponer mensajes de commit.
- Los commits, push, Pull Requests y merges son responsabilidad exclusiva del desarrollador: no ejecutarlos, aunque el desarrollador los pida de pasada; ofrecer en su lugar el mensaje o el comando para que los ejecute él.
- No ejecutar operaciones destructivas (reset duro, borrado de ramas, limpieza forzada, reescritura de historial) ni añadir al staging archivos que no se hayan pedido.
