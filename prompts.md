> Detalla en esta sección los prompts principales utilizados durante la creación del proyecto, que justifiquen el uso de asistentes de código en todas las fases del ciclo de vida del desarrollo. Esperamos un máximo de 3 por sección, principalmente los de creación inicial o  los de corrección o adición de funcionalidades que consideres más relevantes.
Puedes añadir adicionalmente la conversación completa como link o archivo adjunto si así lo consideras


## Índice

1. [Descripción general del producto](#1-descripción-general-del-producto)
2. [Arquitectura del sistema](#2-arquitectura-del-sistema)
3. [Modelo de datos](#3-modelo-de-datos)
4. [Especificación de la API](#4-especificación-de-la-api)
5. [Historias de usuario](#5-historias-de-usuario)
6. [Tickets de trabajo](#6-tickets-de-trabajo)
7. [Pull requests](#7-pull-requests)

---

## 1. Descripción general del producto

**Prompt 1:**

````text
Actúa como Senior Product Manager y Product Engineer especializado en discovery de productos digitales y Spec-Driven Development.

Estamos comenzando la definición funcional de CityFix, un producto greenfield cuya visión inicial está documentada en `PROJECT_CONTEXT.md`.

## Objetivo

Identificar y aclarar las decisiones de producto necesarias antes de redactar un PRD completo, coherente y verificable.

No queremos reducir la visión global del producto ni seleccionar todavía un MVP.

## Fuentes

1. Lee `PROJECT_CONTEXT.md` completamente.
2. Consulta las instrucciones del repositorio y la documentación existente que resulte relevante.
3. Distingue los requisitos explícitos de las preferencias, hipótesis y decisiones pendientes.

El documento de contexto define la visión inicial, pero no debe tratarse como un PRD aprobado.

## 1. Comprensión del producto

Resume brevemente:

- Problema y propuesta de valor.
- Usuarios y necesidades principales.
- Recorrido completo de una incidencia: ciudadano → gestor → operario → seguimiento.
- Principios y restricciones que no debemos perder.
- Capacidades funcionales globales previstas.

No repitas extensamente el contexto ni propongas todavía una arquitectura.

## 2. Identificación de incertidumbres

Analiza las decisiones funcionales aún abiertas.

Presta especial atención a:

- Selección de municipios de toda España y diferencia entre municipios del catálogo y municipios operativamente habilitados.
- Permisos de gestores y operarios sobre uno o varios municipios.
- Visibilidad pública, privada e interna de incidencias, fotografías y eventos.
- Estados, transiciones, responsabilidades, rechazo, resolución, cierre y reapertura.
- Validación de ubicación dentro del término municipal y tratamiento de puntos en límites administrativos.
- Gestión de incidencias duplicadas.
- Captura, publicación y privacidad de fotografías.
- Procesamiento convencional sin IA.
- Uso opcional de agentes IA, aprobación humana y BYOK.
- Notificaciones y seguimiento del ciudadano.
- Conservación y eliminación de datos.

No inventes decisiones para cerrar estas cuestiones.

## 3. Preguntas de discovery

Formula una única ronda de entre cinco y ocho preguntas de alto impacto.

Cada pregunta debe:

- Resolver una incertidumbre real del contexto.
- Explicar brevemente por qué importa.
- Presentar alternativas razonables cuando ayuden a decidir.
- Identificar tu recomendación como propuesta, no como decisión.
- Evitar repetir aspectos que ya estén definidos.

Prioriza las preguntas que afecten a varias capacidades del producto.

No preguntes ahora por nombres de tablas, endpoints, estructura de carpetas, librerías adicionales o detalles de implementación.

## 4. Riesgos y supuestos

Identifica brevemente:

- Hipótesis de producto que todavía no han sido validadas.
- Dependencias funcionales relevantes.
- Riesgos de privacidad, autorización o incoherencia.
- Decisiones que pueden esperar al diseño técnico.

No presentes hipótesis como hechos demostrados.

## 5. Restricciones

- No crees ni modifiques archivos.
- No redactes todavía el PRD.
- No generes historias, tickets ni criterios de aceptación.
- No diseñes arquitectura, modelo de datos ni API.
- No instales dependencias ni generes código.
- No modifiques `PROJECT_CONTEXT.md`, `readme.md` ni `prompts.md`.
- No ejecutes commits, push, Pull Requests ni merges.
- No selecciones un MVP ni elimines capacidades de la visión global.
- No tomes decisiones de producto en mi nombre.

## Resultado esperado

Devuélveme:

1. Resumen breve de tu comprensión de CityFix.
2. Principales incertidumbres funcionales.
3. Entre cinco y ocho preguntas priorizadas, con alternativas y recomendaciones claramente identificadas.
4. Riesgos y supuestos que debamos vigilar.
5. Decisiones que pueden aplazarse.

Espera mis respuestas antes de redactar cualquier documento.
````

**Prompt 2:**

````text
# CityFix — Redacción del primer borrador del PRD

Actúa como Senior Product Manager y Product Engineer especializado en Spec-Driven Development.

Hemos aprobado las decisiones funcionales D01–D20 de CityFix y realizado su revisión de coherencia.

Ahora debes crear el primer borrador completo del Product Requirements Document (PRD).

## Fuentes

Lee y utiliza:

- `AGENTS.md` y las instrucciones aplicables.
- `PROJECT_CONTEXT.md` como visión global inicial.
- Las decisiones aprobadas D01–D20 proporcionadas anteriormente en esta conversación.
- `DISCOVERY_CONSOLIDACION.md`, si existe, como revisión de coherencia.
- `readme.md` y `prompts.md`, únicamente para conocer su estructura.

Si no tienes acceso a las decisiones originales D01–D20, detente y solicítamelas. No las reconstruyas únicamente a partir de un resumen.

## Objetivo

Crear `docs/PRD.md` como documento principal de requisitos de producto de CityFix.

Debe reflejar la visión completa del producto y las decisiones humanas aprobadas, sin reducir el alcance a un MVP ni confundir capacidades previstas con funcionalidades implementadas.

## Contenido

Utiliza la estructura propuesta durante la consolidación, adaptándola para evitar apartados redundantes:

1. Estado, propósito y fuentes del documento.
2. Visión, problema, objetivos e hipótesis.
3. Actores y roles.
4. Alcance funcional global.
5. Territorio, habilitación y validación geoespacial.
6. Ciclo de vida, responsabilidades, asignaciones y reapertura.
7. Visibilidad, privacidad, fotografías y moderación.
8. Duplicados y seguimiento.
9. Identidad y notificaciones.
10. Categorías y priorización.
11. Dashboard, administración, métricas y exportaciones.
12. IA opcional, credenciales centralizadas, presupuesto y auditoría.
13. Conservación de datos.
14. Requisitos no funcionales y restricciones.
15. Reglas de negocio y trazabilidad.
16. Supuestos, riesgos y cuestiones abiertas.

Adapta esta estructura si mejora la claridad, sin perder capacidades de `PROJECT_CONTEXT.md`.

## Reglas de redacción

- Identifica requisitos funcionales, requisitos no funcionales y reglas de negocio mediante IDs estables.
- Mantén trazabilidad con D01–D20 o con la sección correspondiente del contexto inicial.
- Distingue entre requisitos aprobados, capacidades previstas, hipótesis y cuestiones abiertas.
- Utiliza formulaciones verificables cuando existan decisiones suficientes.
- No inventes cifras, plazos, contratos API, estados adicionales ni reglas de autorización.
- No afirmes que existen ayuntamientos clientes, funcionalidades implementadas o integraciones operativas.
- Mantén la IA como capacidad opcional, con funcionamiento convencional independiente.

## Ambigüedades conocidas

Documenta explícitamente, sin decidir unilateralmente:

- Representación formal del rechazo administrativo frente al cierre.
- Estado y plazo de reapertura de avisos vinculados.
- Tratamiento definitivo de avisos territoriales que acaban perteneciendo a municipios no habilitados.
- Superficie exacta de consulta pública sin autenticación.
- Permisos sobre avisos sin municipio validado.
- Separación de funciones administrativas y de gestión.
- Precisión y privacidad de coordenadas publicadas.

Incluye únicamente otras cuestiones abiertas que tengan un impacto funcional real.

## Terminología de IA

Respeta la decisión aprobada:

Las credenciales de proveedores de IA se administran globalmente y el presupuesto es global compartido, sin cuotas municipales.

No describas el funcionamiento como BYOK por municipio o por usuario.

Utiliza una terminología precisa como «credenciales de proveedor configuradas centralmente» y señala que la terminología histórica de BYOK en el contexto inicial necesita actualización posterior.

## Documentación

- Crea únicamente `docs/PRD.md`.
- No crees un documento separado de decisiones D01–D20.
- No copies íntegramente `PROJECT_CONTEXT.md` ni `DISCOVERY_CONSOLIDACION.md`.
- No generes historias de usuario, tickets, modelos de datos ni contratos API todavía.
- No modifiques `PROJECT_CONTEXT.md`, `AGENTS.md`, `CLAUDE.md` ni `.claude/`.
- No actualices todavía `readme.md` ni `prompts.md`: los actualizaremos cuando revisemos el PRD.
- No hagas commits, push, PRs ni merges.

## Verificación

Después de crear el documento:

1. Comprueba que se reflejan correctamente las 20 decisiones aprobadas.
2. Comprueba que ninguna recomendación descartada aparece como requisito.
3. Verifica que no se han perdido capacidades de la visión original.
4. Identifica contradicciones, ambigüedades y puntos sin soporte.
5. Comprueba que los identificadores de requisitos son únicos.
6. Muestra un resumen de las secciones creadas y el estado Git.

No marques el PRD como aprobado: debe permanecer en estado «Borrador — pendiente de revisión».

Detente al terminar y espera mi revisión.
````

**Prompt 3:**

````text
# CityFix — Revisión adversarial del primer PRD

Quiero revisar el borrador `docs/PRD.md` antes de aprobarlo.

Utiliza el subagente `adversarial-reviewer` del repositorio para realizar una revisión crítica e independiente.

## Fuentes

- `docs/PRD.md`
- `PROJECT_CONTEXT.md`
- `AGENTS.md`
- Las instrucciones aplicables del repositorio

El PRD contiene las decisiones funcionales D01–D20 aprobadas durante el discovery.

## Objetivo

Identificar defectos reales de calidad, coherencia, trazabilidad y seguridad.

Prioriza:

1. Contradicciones entre requisitos.
2. Requisitos marcados como aprobados sin respaldo suficiente.
3. Ambigüedades que impiden verificar un comportamiento.
4. Errores de permisos por rol y ámbito municipal.
5. Incoherencias entre los siete estados operativos, el rechazo, la reapertura y la validación territorial.
6. Incoherencias entre duplicados, incidencia principal y avisos vinculados.
7. Riesgos de exposición de datos personales, imágenes y ubicaciones.
8. Referencias de trazabilidad incorrectas o inexistentes.
9. Capacidades de la visión global que se hayan perdido.
10. Redundancias que dificulten mantener el PRD.

Comprueba también si las cuestiones abiertas están correctamente diferenciadas de los requisitos aprobados.

## Criterios

- No inventes nuevos requisitos.
- No conviertas preferencias de diseño en defectos.
- No reabras decisiones explícitamente aprobadas por el responsable del producto.
- No consideres un defecto que un detalle técnico esté pendiente cuando pueda resolverse más adelante.
- No exijas definir un MVP ni una arquitectura técnica.
- No propongas nuevos documentos como solución predeterminada.

## Resultado

Presenta únicamente hallazgos con evidencia:

- Severidad: crítica, alta, media o baja.
- Identificador del requisito o sección afectada.
- Descripción del problema.
- Evidencia concreta en los documentos.
- Impacto.
- Corrección recomendada.

Separa los defectos comprobados de los riesgos hipotéticos.

Al finalizar, proporciona una valoración de si el PRD puede pasar a aprobación tras correcciones menores o requiere una revisión funcional mayor.

No modifiques archivos.

No ejecutes operaciones Git de escritura.

No generes informes adicionales.

Espera mi revisión.
````

---

## 2. Arquitectura del Sistema

### **2.1. Diagrama de arquitectura:**

**Prompt 1:**

**Prompt 2:**

**Prompt 3:**

### **2.2. Descripción de componentes principales:**

**Prompt 1:**

**Prompt 2:**

**Prompt 3:**

### **2.3. Descripción de alto nivel del proyecto y estructura de ficheros**

**Prompt 1:**

**Prompt 2:**

**Prompt 3:**

### **2.4. Infraestructura y despliegue**

**Prompt 1:**

**Prompt 2:**

**Prompt 3:**

### **2.5. Seguridad**

**Prompt 1:**

**Prompt 2:**

**Prompt 3:**

### **2.6. Tests**

**Prompt 1:**

**Prompt 2:**

**Prompt 3:**

---

### 3. Modelo de Datos

**Prompt 1:**

**Prompt 2:**

**Prompt 3:**

---

### 4. Especificación de la API

**Prompt 1:**

**Prompt 2:**

**Prompt 3:**

---

### 5. Historias de Usuario

**Prompt 1:**

**Prompt 2:**

**Prompt 3:**

---

### 6. Tickets de Trabajo

**Prompt 1:**

**Prompt 2:**

**Prompt 3:**

---

### 7. Pull Requests

**Prompt 1:**

**Prompt 2:**

**Prompt 3:**
