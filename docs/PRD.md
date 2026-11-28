# CityFix — Product Requirements Document (PRD)

> **Estado del documento:** Aprobado como base funcional — con cuestiones abiertas. La aprobación no implica que todos sus requisitos estén detallados ni implementados: las cuestiones OPEN-001 a OPEN-020 siguen abiertas y ninguna capacidad está implementada.
> **Alcance:** visión global del producto. No es un plan de entrega ni un MVP, y no acredita diseño, código ni funcionalidades implementadas.

## 1. Estado, propósito y fuentes

### 1.1. Propósito

Este documento recoge los requisitos de producto de CityFix: qué debe hacer la plataforma, para quién y bajo qué reglas. Es el documento principal de requisitos y la base de las épicas, historias, criterios de aceptación y tickets posteriores, que aún no existen.

No contiene arquitectura, modelo de datos, contratos API ni planificación de entrega.

### 1.2. Fuentes

| Fuente | Uso |
|---|---|
| `PROJECT_CONTEXT.md` | Visión global inicial. Se cita como «Contexto §n». No es un PRD aprobado. |
| Decisiones D01–D20 | Decisiones funcionales aprobadas por el responsable del producto durante el discovery. Se citan como «D01»–«D20». Su resumen autosuficiente está en la sección 15.1. No existe otro artefacto del repositorio que registre su aprobación ni se aporta evidencia externa: la aprobación consta por la declaración del responsable del producto. |
| Aclaraciones | Precisiones posteriores aprobadas por el responsable del producto durante la revisión del PRD. Se citan como «Aclaración» y se listan en la sección 15.1. |
| `AGENTS.md` y `.claude/rules/` | Principios permanentes del repositorio (privacidad, autorización, IA opcional). |
| Procedencia del discovery | El discovery de producto (rondas de preguntas y revisión de coherencia) dio lugar a las decisiones D01–D20 y a las cuestiones abiertas de la sección 16. Sus borradores de trabajo no son fuente de requisitos ni se citan como documentos permanentes: el contenido necesario está resumido en este PRD (secciones 15.1 y 16). |

### 1.3. Estados de las afirmaciones

| Estado | Significado |
|---|---|
| **Aprobado** | Deriva de una decisión explícita D01–D20 o de una aclaración posterior del responsable del producto. |
| **Aprobado parcialmente** | Parte de los comportamientos está decidida y parte sigue prevista o abierta. |
| **Previsto** | Capacidad de la visión global (`PROJECT_CONTEXT.md`) sin decisión de detalle. Es alcance del producto, no un requisito cerrado. |
| **Hipótesis** | Supuesto de producto sin validar. |
| **Abierto** | Cuestión sin decidir. Ver sección 16. |
| **Retirada** | Requisito cuyo identificador se conserva sin contenido activo porque duplicaba otro (RES-002 duplicaba RN-IA-001). El identificador no se reutiliza y no cuenta como requisito activo. |

Ningún requisito está implementado ni verificado. Este documento no sube de estado sin decisión humana.

### 1.4. Identificadores

Los identificadores son estables y no se reutilizan ni se renumeran.

| Familia | Uso |
|---|---|
| `RF-<ÁREA>-NNN` | Requisito funcional |
| `RN-<ÁREA>-NNN` | Regla de negocio |
| `RNF-<ÁREA>-NNN` | Requisito no funcional |
| `RES-NNN` | Restricción |
| `HIP-NNN`, `SUP-NNN`, `RIE-NNN`, `OPEN-NNN` | Hipótesis, supuesto, riesgo, cuestión abierta |

Áreas: `TER` territorio, `ROL` roles, `INC` ciclo de vida, `PUB` publicación, `FOT` fotografías, `DUP` duplicados, `IDN` identidad, `NOT` notificaciones, `CAT` categorías, `DSH` dashboard y administración, `IA`, `DAT` datos, `SEG` seguridad, `PRI` privacidad, `AUD` auditoría, `ACC` accesibilidad, `CAL` calidad, `COS` costes.

Este esquema es el vigente en este documento. Un identificador retirado se conserva con el estado «Retirada» y no se reutiliza.

### 1.5. Idioma

Documentación en español. Los identificadores técnicos, contratos y tests, en inglés (`AGENTS.md`).

## 2. Visión, problema, objetivos e hipótesis

### 2.1. Visión

CityFix es una plataforma para comunicar y gestionar incidencias en espacios públicos de España: baches, farolas averiadas, aceras dañadas, limpieza, contenedores, parques o señalización, entre otros (Contexto §1). Facilita el aviso, el seguimiento y la resolución entre ciudadanos, gestores, operarios y administradores.

### 2.2. Problema (hipótesis por validar)

Los avisos urbanos pueden quedar dispersos en distintos canales, tener ubicaciones imprecisas, duplicarse o carecer de seguimiento claro (Contexto §1). Se trata de una hipótesis, no de un hecho demostrado.

### 2.3. Objetivos de producto

Estos objetivos son cualitativos. No se definen métricas ni beneficios medidos (ver OPEN-020).

- Facilitar que un ciudadano comunique una incidencia con una ubicación confirmada y su evidencia.
- Dar a quien gestiona un lugar único para revisar, clasificar, priorizar, detectar duplicados, asignar y supervisar.
- Dar al operario lo necesario para ejecutar y documentar el trabajo asignado.
- Ofrecer al ciudadano seguimiento propio y consulta pública de la información publicada, protegiendo su identidad.
- Cubrir todo el territorio español en el catálogo y habilitar operativamente cada municipio de forma controlada.
- Funcionar completamente sin IA, que es una ayuda opcional bajo control humano.

### 2.4. Hipótesis

| ID | Hipótesis | Estado |
|---|---|---|
| HIP-001 | Los avisos urbanos están dispersos, mal ubicados, duplicados y sin seguimiento claro. | Hipótesis (Contexto §1) |
| HIP-002 | Los ayuntamientos querrían operar CityFix. No se presupone que ninguno lo haga ni que exista ninguno cliente. | Hipótesis (Contexto §1) |
| HIP-003 | Los ciudadanos adoptarían este canal para avisar y hacer seguimiento. | Hipótesis |
| HIP-004 | Los datos de INE e IGN/CNIG cubren con calidad suficiente la península, las islas, Ceuta y Melilla para validar la pertenencia municipal. | Hipótesis (Contexto §3) |

### 2.5. Principios de producto (Contexto §5)

Los principios que guían el resto del documento, todos con estado Previsto salvo que una decisión los concrete:

1. Funcionar sin IA.
2. Control humano: la IA recomienda; solo el sistema y las personas autorizadas realizan acciones oficiales.
3. Ámbito municipal y privacidad en consultas, imágenes, operaciones y notificaciones.
4. Ubicación explícita: no la sustituyen la localización del usuario ni los metadatos de una foto.
5. Trazabilidad de cambios y actuaciones.
6. Calidad y costes: accesibilidad, seguridad desde el inicio, mantenibilidad, testabilidad y coste contenido.

## 3. Actores y roles

### 3.1. Actores

| Actor | Descripción | Origen |
|---|---|---|
| Visitante | Cualquier persona sin sesión. Consulta incidencias publicadas. | D05, D12 |
| Ciudadano | Usuario autenticado que registra avisos, sigue los suyos y solicita reaperturas o desvinculaciones. | D07, D12; Contexto §2 |
| Gestor | Revisa, clasifica, prioriza, valida, rechaza, asigna y supervisa. Usa el dashboard web. | D07; Contexto §2 |
| Operario | Ejecuta y documenta intervenciones. Usa la misma app móvil que el ciudadano con una experiencia adaptada a su rol. | D07; Contexto §2 |
| Administrador global | Gestiona la plataforma, la habilitación territorial, los conflictos territoriales y la IA. | D03, D04, D16, D18 |
| Administrador municipal | Gestiona personal, equipos, permisos y configuración de sus municipios autorizados. | D04 |

La IA no es un actor: es una capacidad opcional que propone (sección 12).

### 3.2. Requisitos

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-ROL-001 | Existen cuatro perfiles funcionales principales: ciudadano, gestor, operario y administrador. | D04 | Aprobado |
| RF-ROL-002 | Existen dos alcances administrativos: administrador global de plataforma y administrador municipal con acceso limitado a sus municipios autorizados. | D04 | Aprobado |
| RF-ROL-003 | El administrador global gestiona la plataforma y la habilitación territorial. | D04 | Aprobado |
| RF-ROL-004 | Los administradores municipales gestionan personal, equipos, permisos y configuración de su ámbito. | D04 | Aprobado |
| RF-ROL-005 | El visitante sin sesión puede consultar las incidencias publicadas (RF-PUB-001). | D05, D12 | Aprobado |
| RN-ROL-001 | Un usuario puede estar asociado a varios municipios. | D04 | Aprobado |
| RN-ROL-002 | Un mismo usuario puede desempeñar roles distintos en municipios distintos. | D04 | Aprobado |
| RN-ROL-003 | Los permisos se evalúan considerando usuario, rol, municipio y operación. | D04 | Aprobado |
| RN-ROL-004 | Un usuario no adquiere permisos sobre otro municipio por trabajar en uno. | D04 | Aprobado |

La matriz exhaustiva de permisos queda pendiente (OPEN-008). La separación de funciones entre administración y gestión, también (OPEN-006).

## 4. Alcance funcional global

La tabla enumera las capacidades de la visión global y dónde se desarrollan. Ninguna está implementada. El orden de entrega se decidirá en un documento de planificación incremental separado y no elimina ninguna de ellas.

| Capacidad | Origen | Estado | Sección | Abierto |
|---|---|---|---|---|
| Cuentas, autenticación, roles y ámbitos municipales | Contexto §4; D04, D12 | Aprobado parcialmente | 3, 9 | OPEN-005, OPEN-006, OPEN-008 |
| Catálogo territorial de toda España, habilitación municipal y validación de ubicación | Contexto §3; D01–D03 | Aprobado parcialmente | 5 | OPEN-001, OPEN-010, OPEN-013 |
| Creación, consulta, clasificación, priorización, asignación, tramitación y resolución | Contexto §4; D07–D09 | Aprobado parcialmente | 6, 10 | OPEN-002, OPEN-008, OPEN-016, OPEN-017 |
| Fotografías y localización en mapa | Contexto §4; D02, D05, D06 | Aprobado parcialmente | 5, 7 | OPEN-007 |
| Visualización de límites municipales en mapas | Contexto §4 | Previsto | 5 | — |
| Historial cronológico con información pública e interna | Contexto §4; D05 | Aprobado parcialmente | 6, 7 | OPEN-009 |
| Duplicados y relaciones entre avisos | Contexto §4; D10, D11 | Aprobado parcialmente | 8 | OPEN-003, OPEN-012, OPEN-017 |
| Categorías, departamentos, equipos y operarios | Contexto §4; D04, D14 | Aprobado parcialmente | 10, 11 | OPEN-016 |
| Notificaciones (centro, push y correo) | D13 | Aprobado | 9 | — |
| Actualizaciones en tiempo real | Contexto §2, §4; D13 | Previsto | 9, 11 | — |
| Dashboard municipal con listados, filtros, mapas, métricas, administración y exportaciones | Contexto §4 | Previsto | 11 | OPEN-004 |
| Procesamiento convencional: reglas, búsqueda de proximidad y revisión humana | Contexto §4; D10 | Aprobado parcialmente | 8, 10 | OPEN-017 |
| IA opcional: propuestas, proveedores, modelos, credenciales, presupuesto y auditoría | Contexto §4; D15–D19 | Aprobado parcialmente | 12 | OPEN-014, OPEN-015 |
| Seguridad, privacidad y auditoría | Contexto §4; D05, D19 | Aprobado parcialmente | 7, 12, 14 | OPEN-007 |
| Accesibilidad, pruebas y experiencia visual profesional en web y móvil | Contexto §4 | Previsto | 14 | OPEN-019 |
| Conservación y eliminación de datos | D20 | Aprobado parcialmente | 13 | OPEN-018 |

Una capacidad figura como «Aprobado» solo si todos los comportamientos descritos en este documento están decididos. «Previsto» no reduce el alcance.

## 5. Territorio, habilitación y validación geoespacial

### 5.1. Conceptos

- **Catálogo territorial:** conjunto de municipios de España que CityFix conoce.
- **Pertenencia geográfica:** relación de un punto con la geometría administrativa de un municipio.
- **Habilitación operativa:** condición de un municipio cuyo ayuntamiento opera CityFix.

El sistema distingue las tres (RN-TER-002).

### 5.2. Catálogo y habilitación

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-TER-001 | El catálogo territorial incluye todos los municipios de España, incluidas península, Baleares, Canarias, Ceuta y Melilla. | D01; Contexto §3 | Aprobado |
| RF-TER-002 | Cada municipio se identifica mediante su identificador oficial. INE e IGN/CNIG son las fuentes de referencia consideradas. | Contexto §3 | Previsto |
| RN-TER-001 | Que un municipio esté en el catálogo no significa que esté habilitado operativamente. | D01 | Aprobado |
| RN-TER-002 | El sistema diferencia catálogo territorial, pertenencia geográfica y habilitación operativa. | D01 | Aprobado |
| RN-TER-003 | Solo pueden crearse nuevos avisos en municipios habilitados. Los municipios no habilitados no reciben nuevos avisos. | D01 | Aprobado |
| RF-TER-003 | Los municipios no habilitados pueden explorarse y seleccionarse para consultar información territorial. El alcance de esa información no está definido (OPEN-013). | D01 | Aprobado |
| RF-TER-004 | La habilitación operativa de municipios la gestiona el administrador global. | D04 | Aprobado |

### 5.3. Selección y confirmación de la ubicación

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-TER-005 | El ciudadano selecciona el contexto territorial mediante comunidad autónoma, provincia y municipio, con selectores encadenados o con búsqueda. | D02; Contexto §3 | Aprobado |
| RF-TER-006 | El código postal es opcional y sirve de ayuda para localizar. | D02 | Aprobado |
| RN-TER-004 | El código postal no determina la pertenencia municipal. | D02 | Aprobado |
| RF-TER-007 | El mapa permite localizar la incidencia mediante GPS, búsqueda de dirección o selección manual del marcador. | D02; Contexto §3 | Aprobado |
| RF-TER-008 | El ciudadano debe confirmar expresamente la ubicación. | D02 | Aprobado |
| RN-TER-005 | Ni la localización del dispositivo ni los metadatos de una fotografía sustituyen la confirmación expresa de RF-TER-008. | Contexto §5 | Previsto |
| RF-TER-009 | El sistema valida el punto frente a la geometría administrativa del municipio, incluidos los territorios discontinuos y los enclaves. | D02 | Aprobado |
| RF-TER-010 | Si el punto pertenece claramente a otro municipio, se propone la corrección al ciudadano y se solicita su confirmación. | D02 | Aprobado |
| RN-TER-006 | No se cambia silenciosamente el municipio ni se asignan incidencias por proximidad. | D02 | Aprobado |
| RF-TER-011 | Los mapas permiten visualizar los límites municipales. | Contexto §4 | Previsto |

**Consecuencia derivada (SUP-001):** si el punto pertenece claramente a un municipio no habilitado, RN-TER-003 impide registrar el aviso. El mensaje al ciudadano en ese caso no está definido.

### 5.4. Ambigüedades territoriales

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-TER-012 | Cuando no puede determinarse con certeza el municipio, se permite conservar el aviso como pendiente de validación territorial, sujeto a RN-TER-003. | D03 | Aprobado |
| RN-TER-007 | Durante la validación territorial no hay asignación operativa municipal ni publicación pública. | D03 | Aprobado |
| RF-TER-013 | El administrador global resuelve los conflictos de pertenencia territorial. | D03 | Aprobado |
| RF-TER-014 | Los gestores municipales pueden señalar discrepancias y proponer correcciones dentro de su ámbito. | D03 | Aprobado |
| RN-TER-008 | Las correcciones territoriales se justifican, se auditan y preservan la información original. | D03 | Aprobado |
| RF-TER-015 | Si falta información, puede solicitarse una corrección al ciudadano. | D03 | Aprobado |
| RF-TER-016 | Si no es posible validar el municipio tras las comprobaciones razonables, el administrador global puede finalizar motivadamente la revisión como «no tramitable por ubicación». | D03 | Aprobado |
| RN-TER-009 | La finalización «no tramitable por ubicación» no equivale a una incidencia resuelta ni genera una reparación municipal. | D03 | Aprobado |

Cuestiones abiertas: OPEN-001 (aviso que acaba perteneciendo a un municipio no habilitado), OPEN-005 (permisos sobre avisos sin municipio validado) y OPEN-010 (ciclo de vida de la habilitación).

## 6. Ciclo de vida, responsabilidades, asignaciones y reapertura

### 6.1. Estados y responsabilidades

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-INC-001 | El ciclo operativo tiene siete estados principales: Registrada, En revisión, Validada, Asignada, En curso, Resuelta y Cerrada. | D07 | Aprobado |
| RN-INC-001 | Los siete estados de RF-INC-001 son los estados operativos principales. La representación formal del rechazo administrativo, de la validación territorial y de otros resultados excepcionales (por ejemplo «no tramitable por ubicación») no está decidida: este documento no afirma ni excluye que se modele mediante estados o condiciones adicionales (OPEN-002). | D07 | Aprobado parcialmente |
| RN-INC-002 | La publicación pública no es un estado del ciclo operativo. | D07 | Aprobado |
| RN-INC-003 | No todas las transiciones son lineales e irreversibles. La matriz de transiciones está pendiente (OPEN-008). | D07 | Aprobado |
| RF-INC-002 | El ciudadano autenticado crea el aviso. | D07, D12 | Aprobado |
| RF-INC-003 | El gestor revisa, clasifica, prioriza, valida, rechaza y asigna o reasigna. | D07 | Aprobado |
| RF-INC-004 | El operario asignado ejecuta y documenta la intervención. | D07 | Aprobado |
| RF-INC-005 | El operario asignado finaliza su intervención y propone la resolución. | D07 | Aprobado |
| RF-INC-006 | El gestor valida la resolución y decide cerrar la incidencia o devolverla a intervención. El resultado de devolverla a intervención respeta las transiciones aprobadas; su matriz exhaustiva está pendiente (OPEN-008). | D07 | Aprobado |
| RN-INC-014 | El estado «Resuelta» representa que el trabajo se ha comunicado como terminado y está pendiente de validación por el gestor. | D07; Aclaración | Aprobado |
| RN-INC-004 | El rechazo exige un motivo obligatorio. | D07 | Aprobado |
| RN-INC-005 | El gestor municipal autorizado puede rechazar una incidencia mediante una decisión motivada. | D08 | Aprobado |
| RN-INC-006 | Una resolución insuficiente puede devolver la incidencia a intervención. | D07 | Aprobado |
| RF-INC-007 | El operario consulta los trabajos que se le asignan, registra actuaciones y documenta resultados desde la app móvil. | Contexto §2 | Previsto |
| RF-INC-008 | Cada incidencia tiene un historial cronológico de cambios y actuaciones, consultable según permisos. | Contexto §4, §5 | Previsto |

La relación entre el rechazo, el cierre y los resultados terminales («no tramitable por ubicación») no está formalizada (OPEN-002). SUP-003 recoge el supuesto de trabajo con el que este documento describe la validación territorial, sin decidir su representación formal.

### 6.2. Asignación y disponibilidad de personal

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-INC-015 | El gestor municipal asigna y reasigna tareas dentro de su ámbito. | D09 | Aprobado |
| RN-INC-008 | Las reasignaciones conservan la trazabilidad y las actuaciones anteriores. | D09 | Aprobado |
| RN-INC-009 | No se asignan automáticamente tareas a municipios vecinos. | D09 | Aprobado |
| RN-INC-010 | Si un municipio habilitado no tiene gestores disponibles, los avisos permanecen pendientes de revisión y se alerta a la administración correspondiente (OPEN-006). | D09 | Aprobado |
| RN-INC-011 | Si no existen operarios disponibles, las incidencias validadas permanecen pendientes de asignación. | D09 | Aprobado |
| RN-INC-012 | La falta de personal no constituye por sí sola un motivo para rechazar una incidencia. | D09 | Aprobado |
| RN-INC-013 | No se prometen plazos de atención que no puedan garantizarse. | D09 | Aprobado |

### 6.3. Reapertura

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-INC-009 | El ciudadano puede solicitar la reapertura de una incidencia propia durante los 30 días siguientes al cierre (plazo general). | D08 | Aprobado |
| RF-INC-010 | La solicitud requiere un motivo estructurado y una explicación. El ciudadano puede añadir fotografías, que son opcionales. | D08 | Aprobado |
| RF-INC-011 | El gestor acepta o deniega la solicitud de forma motivada. La solicitud no reabre automáticamente la incidencia. | D08 | Aprobado |
| RN-INC-007 | Si se acepta, se conserva el mismo expediente y todo su historial. | D08 | Aprobado |
| RF-INC-012 | La reapertura puede devolver la incidencia a la fase operativa que corresponda y se registra como evento. No es obligatorio crear un estado permanente «Reabierta». | D08 | Aprobado |
| RF-INC-013 | Pasado el plazo, el ciudadano puede crear un nuevo aviso relacionado. | D08 | Aprobado |
| RF-INC-014 | Un gestor autorizado puede realizar una reapertura excepcional fuera del plazo, con justificación y auditoría. | D08 | Aprobado |

El estado y el plazo de reapertura de los avisos vinculados están pendientes (OPEN-003). Si «cierre» incluye el rechazo, y si el ciudadano puede impugnar un rechazo, está pendiente (OPEN-002).

## 7. Visibilidad, privacidad, fotografías y moderación

### 7.1. Niveles de información y publicación

Se distinguen tres niveles: **pública**, **privada del ciudadano autor** e **interna municipal**.

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RN-PUB-001 | La identidad del ciudadano denunciante nunca es pública. | D05 | Aprobado |
| RN-PUB-002 | La información se clasifica en tres niveles: pública, privada del ciudadano autor e interna municipal. | D05 | Aprobado |
| RN-PUB-003 | Una incidencia requiere la revisión de un gestor antes de publicarse. | D05 | Aprobado |
| RN-PUB-004 | La tramitación administrativa y la publicación pública son decisiones independientes. | D05 | Aprobado |
| RN-PUB-005 | No se exponen públicamente notas internas, asignaciones, datos personales ni información sensible. | D05 | Aprobado |
| RN-PUB-006 | El texto libre de la incidencia requiere revisión del gestor antes de su publicación. | D05; Aclaración | Aprobado |
| RN-PUB-007 | El contenido que no pueda publicarse puede permanecer disponible para la tramitación interna, respetando los permisos. | D05, D06; Aclaración | Aprobado |
| RF-PUB-001 | Cualquier persona puede consultar las incidencias publicadas sin iniciar sesión. La superficie concreta de esa consulta no está definida (OPEN-004). | D05, D12 | Aprobado |
| RF-PUB-002 | El historial de cada incidencia distingue la información pública de la interna. Los criterios de qué eventos son públicos están pendientes (OPEN-009). | Contexto §4; D05 | Aprobado parcialmente |
| RNF-PRI-001 | La información privada se protege también en la API, las imágenes, las notificaciones, las exportaciones y el tiempo real. | D05 | Aprobado |

La precisión y la privacidad de las coordenadas publicadas están pendientes (OPEN-007). La visibilidad pública de incidencias rechazadas, desvinculadas o «no tramitables por ubicación» también (OPEN-009).

### 7.2. Fotografías y moderación

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-FOT-001 | El ciudadano puede adjuntar fotografías a un aviso. | Contexto §2 | Previsto |
| RN-FOT-001 | Las fotografías originales permanecen protegidas y con acceso restringido. | D06 | Aprobado |
| RN-FOT-002 | Cada fotografía requiere aprobación individual para su publicación. | D05 | Aprobado |
| RF-FOT-002 | El gestor puede aprobar versiones anonimizadas de las fotografías para su publicación. | D06 | Aprobado |
| RN-FOT-003 | Las imágenes publicadas no conservan metadatos EXIF. | D06 | Aprobado |
| RF-FOT-003 | El gestor puede ocultar contenido sensible, solicitar correcciones y publicar únicamente información apropiada. | D06 | Aprobado |
| RN-FOT-004 | Una incidencia legítima no se rechaza exclusivamente porque una fotografía o un texto contenga datos que no puedan hacerse públicos. | D06 | Aprobado |
| RN-FOT-005 | Las decisiones de moderación son trazables. | D06 | Aprobado |
| RN-FOT-006 | La moderación no depende obligatoriamente de IA. | D06 | Aprobado |

## 8. Duplicados y seguimiento

### 8.1. Detección y vinculación

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-DUP-001 | El sistema puede sugerir incidencias públicas cercanas y potencialmente relacionadas antes de que el ciudadano registre un aviso. | D10 | Aprobado |
| RF-DUP-002 | El ciudadano puede indicar una coincidencia o continuar creando un aviso independiente. El efecto de indicar una coincidencia no está definido (OPEN-012). | D10 | Aprobado |
| RN-DUP-001 | La detección básica de duplicados funciona sin IA. | D10 | Aprobado |
| RN-DUP-002 | El gestor autorizado decide la vinculación definitiva. | D10 | Aprobado |
| RN-DUP-003 | Se conserva cada aviso, su autor, sus imágenes y su historial. No se fusionan los avisos de forma destructiva. | D10 | Aprobado |
| RF-DUP-003 | Una incidencia principal concentra la gestión operativa. Los avisos vinculados conservan identidad propia y seguimiento. | D10 | Aprobado |
| RN-DUP-004 | La vinculación es reversible, motivada y auditable. | D10 | Aprobado |
| RF-DUP-004 | Un gestor puede sustituir la incidencia principal cuando corresponda. | D10 | Aprobado |
| RF-DUP-005 | Las estadísticas distinguen entre avisos recibidos e intervenciones realizadas. | D10 | Aprobado |

### 8.2. Desvinculación y excepciones

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-DUP-006 | El ciudadano puede solicitar la desvinculación de su aviso, justificando por qué considera que se trata de un problema diferente. | D11 | Aprobado |
| RF-DUP-007 | El gestor acepta o deniega la solicitud de forma motivada. También puede desvincular de oficio cuando detecte un error. | D11 | Aprobado |
| RN-DUP-005 | Si se rechaza la incidencia principal, no se rechazan automáticamente todos los avisos vinculados. | D11 | Aprobado |
| RF-DUP-008 | Tras el rechazo de la principal, el gestor revisa los avisos vinculados y puede seleccionar otra principal, desvincular o rechazar individualmente de forma motivada. | D11 | Aprobado |
| RN-DUP-006 | La reapertura de una principal no modifica automáticamente los expedientes de todos los autores (OPEN-003). | D11 | Aprobado |
| RF-DUP-009 | Cada ciudadano puede solicitar la revisión de su propio aviso vinculado dentro de las condiciones aprobadas. | D11; Aclaración | Aprobado |
| RN-DUP-008 | El ciudadano de un aviso vinculado no puede modificar directamente la incidencia principal. | D11; Aclaración | Aprobado |
| RN-DUP-007 | Las comunicaciones privadas de un autor no se propagan a otros. | D11 | Aprobado |
| RF-DUP-010 | Los ciudadanos con avisos vinculados reciben las actualizaciones públicas pertinentes de la gestión principal. | D11 | Aprobado |

Las reglas exactas de proximidad y de detección de duplicados están pendientes (OPEN-017).

## 9. Identidad y notificaciones

### 9.1. Identidad ciudadana

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-IDN-001 | La consulta de incidencias públicas no requiere autenticación (RF-PUB-001). | D12 | Aprobado |
| RF-IDN-002 | Registrar avisos, seguir incidencias propias y solicitar reaperturas o desvinculaciones requiere una cuenta autenticada. | D12 | Aprobado |
| RN-IDN-001 | Los datos de identidad son privados y solo accesibles al personal autorizado cuando sean necesarios. | D12 | Aprobado |

### 9.2. Notificaciones

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-NOT-001 | CityFix dispone de un centro permanente de notificaciones dentro de la aplicación. | D13 | Aprobado |
| RF-NOT-002 | Las notificaciones push son un canal externo disponible, configurable por el usuario (RF-NOT-004). | D13; Aclaración | Aprobado |
| RF-NOT-003 | El correo electrónico es un canal externo disponible, configurable por el usuario (RF-NOT-004). | D13; Aclaración | Aprobado |
| RN-NOT-001 | Los eventos esenciales quedan registrados en el centro de notificaciones aunque los canales externos estén desactivados. | D13; Aclaración | Aprobado |
| RF-NOT-004 | Los usuarios pueden configurar los canales externos (push y correo) y las comunicaciones opcionales de progreso. No se garantiza la entrega por un canal externo cuando el usuario lo ha desactivado o el dispositivo no lo permite. | D13; Aclaración | Aprobado |
| RN-NOT-002 | Las comunicaciones de autenticación y seguridad tienen un tratamiento independiente. | D13; Aclaración | Aprobado |
| RF-NOT-005 | Se notifican a cada destinatario los eventos relevantes: registro, validación, rechazo, solicitud de información, progreso, resolución, cierre y respuesta a solicitudes. | D13 | Aprobado |
| RF-NOT-006 | Gestores, operarios y administradores reciben avisos pertinentes a sus responsabilidades. | D13 | Aprobado |
| RN-NOT-003 | Un evento no genera notificaciones duplicadas al mismo usuario por tener varios avisos relacionados. | D13 | Aprobado |
| RN-NOT-004 | Las notas internas y la información privada no se incluyen en notificaciones públicas ni dirigidas a otros ciudadanos. | D13 | Aprobado |
| RF-NOT-007 | CityFix ofrece actualizaciones en tiempo real. | Contexto §2, §4 | Previsto |
| RN-NOT-005 | El tiempo real complementa los canales de notificación, pero no los sustituye. | D13 | Aprobado |

El catálogo de eventos por rol y las condiciones de cada notificación se detallarán en una especificación posterior.

## 10. Categorías y priorización

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-CAT-001 | CityFix dispone de un catálogo global de categorías de incidencias. | D14 | Aprobado |
| RF-CAT-002 | Los administradores municipales pueden habilitar categorías aplicables a sus servicios y configurar subcategorías locales. | D14 | Aprobado |
| RN-CAT-001 | Se mantiene una clasificación global común para informes y estadísticas. | D14 | Aprobado |
| RN-CAT-002 | La modificación o desactivación de una categoría no elimina ni invalida la clasificación histórica. | D14 | Aprobado |
| RF-CAT-003 | El ciudadano selecciona la categoría y puede utilizar «Otros» cuando no exista una adecuada. | D14 | Aprobado |
| RF-CAT-004 | El gestor puede corregir la clasificación dejando trazabilidad. | D14 | Aprobado |
| RN-CAT-003 | La clasificación y la priorización son responsabilidades diferenciadas. | D14 | Aprobado |
| RF-CAT-005 | El gestor prioriza las incidencias. La escala y las reglas de prioridad no están definidas (OPEN-016). | D07; Contexto §2 | Aprobado parcialmente |

El catálogo exhaustivo de categorías y subcategorías no se define en este documento (OPEN-016). Los ejemplos del Contexto §1 (baches, farolas, aceras, limpieza, contenedores, parques, señalización) ilustran el dominio y no constituyen el catálogo.

## 11. Dashboard, administración, métricas y exportaciones

La mayor parte de esta sección es visión global (Previsto): no hay decisiones de detalle sobre el dashboard.

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-DSH-001 | Los gestores disponen de un dashboard web municipal con listados, filtros, mapas y búsquedas. | Contexto §2, §4 | Previsto |
| RF-DSH-002 | El dashboard ofrece métricas y estadísticas. Las de incidencias distinguen avisos recibidos e intervenciones realizadas (RF-DUP-005). | Contexto §4; D10 | Previsto |
| RF-DSH-003 | El dashboard permite exportaciones autorizadas. | Contexto §4 | Previsto |
| RN-DSH-001 | Las exportaciones no incluyen información privada o interna para roles no autorizados (RNF-PRI-001). | D05 | Aprobado |
| RF-DSH-004 | La administración se ejerce según RF-ROL-002. El administrador global gestiona la habilitación municipal (RF-TER-004) y los catálogos globales (RF-CAT-001). El administrador municipal gestiona la configuración, el personal (usuarios), los equipos y los permisos de sus municipios autorizados, así como las categorías habilitadas y las subcategorías locales (RF-ROL-004, RF-CAT-002). Los administradores municipales no tienen facultades globales. | Contexto §2; D04, D14; Aclaración | Aprobado parcialmente |
| RF-DSH-005 | La plataforma contempla departamentos, equipos y operarios. | Contexto §4 | Previsto |
| RF-DSH-006 | El dashboard muestra actualizaciones en tiempo real. | Contexto §2, §4 | Previsto |
| RF-DSH-007 | Existe una app móvil única para ciudadano y operario, con una experiencia adaptada al rol. | Contexto §2 | Previsto |

La superficie del administrador y la de consulta pública no están decididas (OPEN-004).

## 12. IA opcional, credenciales centralizadas, presupuesto y auditoría

### 12.1. Terminología

El contexto inicial usaba «BYOK» (§6 y §7). Esa denominación **no describía el funcionamiento aprobado**. Las credenciales de proveedor de IA son **credenciales de proveedor configuradas centralmente**: las aporta y administra el operador de la plataforma, no cada municipio ni cada usuario (D16). La terminología histórica del contexto se ha actualizado en consecuencia (sección 16.5).

El contexto prefiere Anthropic API y OpenRouter como proveedores. Es una preferencia, no una decisión de arquitectura.

### 12.2. Funcionamiento y supervisión humana

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RN-IA-001 | CityFix funciona completamente sin IA. | D15; Contexto §5 | Aprobado |
| RF-IA-001 | La IA puede proponer clasificaciones, prioridades, duplicados, resúmenes y borradores. | D15 | Aprobado |
| RN-IA-002 | Las recomendaciones de IA no ejecutan por sí solas acciones administrativas oficiales. Un usuario humano autorizado las revisa y decide. | D15 | Aprobado |
| RN-IA-003 | El fallo, la desactivación o la indisponibilidad del proveedor no bloquea la tramitación convencional. | D15 | Aprobado |
| RN-IA-004 | La IA nunca amplía los permisos del usuario. | D15 | Aprobado |

El Contexto §4 incluye la asignación entre las propuestas de IA y D15 no la menciona (OPEN-015).

### 12.3. Credenciales y proveedores

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-IA-002 | El administrador global configura proveedores, modelos y credenciales de IA, de ámbito centralizado. | D16 | Aprobado |
| RN-IA-005 | Los administradores municipales no administran directamente las credenciales. | D16 | Aprobado |
| RF-IA-003 | La plataforma puede habilitar o deshabilitar capacidades de IA para municipios concretos conforme a su configuración central. | D16 | Aprobado |
| RNF-IA-001 | Las credenciales no se exponen en clientes, logs, respuestas ni repositorios. | D16 | Aprobado |

### 12.4. Privacidad de los datos enviados a IA

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RN-IA-006 | Se aplica minimización de datos por defecto. Se envía únicamente la información necesaria para cada función. | D17 | Aprobado |
| RN-IA-007 | Se evita enviar datos personales, fotografías y coordenadas exactas, salvo que una capacidad concreta lo requiera y tenga la autorización adecuada (OPEN-014). | D17 | Aprobado |
| RN-IA-008 | Habilitar IA no concede acceso general a todos los datos de una incidencia. | D17 | Aprobado |
| RN-IA-009 | Los controles de privacidad no se sustituyen por la aprobación humana de las recomendaciones. | D17 | Aprobado |

### 12.5. Presupuesto

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-IA-004 | El administrador global establece un único presupuesto de IA compartido. | D18 | Aprobado |
| RN-IA-010 | Los municipios habilitados consumen de ese presupuesto. No existen cuotas de gasto obligatorias por municipio. | D18 | Aprobado |
| RF-IA-005 | Puede medirse el consumo por municipio y funcionalidad con fines de supervisión. | D18 | Aprobado |
| RN-IA-011 | Al alcanzarse el límite global se suspenden las nuevas solicitudes de IA. El sistema convencional sigue operando. | D18 | Aprobado |
| RN-IA-012 | Una estimación de coste no garantiza un límite exacto. Los mecanismos de contabilización, alertas y límites técnicos se definirán después. | D18 | Aprobado |

El riesgo de que un municipio agote el presupuesto compartido consta en RIE-003.

### 12.6. Auditoría de IA

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RF-IA-006 | Se mantiene una auditoría estructurada y trazable de la IA. | D19 | Aprobado |
| RN-IA-013 | Se registra la recomendación relevante, su procedencia, la decisión humana y el resultado aplicado. Se minimizan los datos personales almacenados y no se guardan indiscriminadamente los prompts y respuestas completos. | D19 | Aprobado |
| RN-IA-014 | Los registros históricos no se alteran retrospectivamente. Las correcciones se añaden de forma trazable. | D19 | Aprobado |
| RN-IA-015 | El administrador global consulta la auditoría de toda la plataforma. Los administradores municipales y gestores acceden según rol y municipio autorizado. Los operarios solo ven los resultados aprobados necesarios para su trabajo. | D19 | Aprobado |
| RN-IA-016 | Los ciudadanos no ven las recomendaciones internas ni los detalles técnicos de la IA. | D19 | Aprobado |

## 13. Conservación de datos

Los plazos concretos no se fijan en este documento ni se presentan como validación jurídica.

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RN-DAT-001 | Se aplica minimización y conservación diferenciada por tipo de información y finalidad. | D20 | Aprobado |
| RF-DAT-001 | Se contemplan solicitudes de supresión, anonimización y retirada de contenido cuando procedan. | D20 | Aprobado |
| RN-DAT-002 | La eliminación de una cuenta no implica necesariamente destruir expedientes municipales que deban conservarse. | D20 | Aprobado |
| RN-DAT-003 | Las fotografías originales tienen acceso restringido y períodos de conservación acordes con su finalidad. | D20 | Aprobado |
| RN-DAT-004 | Los registros de auditoría requieren conservación proporcionada y controles de acceso. | D20 | Aprobado |
| RN-DAT-005 | Las copias de seguridad siguen reglas de caducidad y eliminación controlada. | D20 | Aprobado |
| RN-DAT-006 | Los plazos concretos se establecen según las obligaciones legales, administrativas y archivísticas aplicables (OPEN-018). | D20 | Aprobado |

## 14. Requisitos no funcionales y restricciones

### 14.1. Requisitos no funcionales

Se enuncian de forma cualitativa. No se definen cifras de rendimiento, disponibilidad ni escalabilidad (OPEN-019).

| ID | Requisito | Origen | Estado |
|---|---|---|---|
| RNF-SEG-001 | La autorización por rol y ámbito municipal se aplica en consultas, imágenes, operaciones y notificaciones. | Contexto §5; D04 | Previsto |
| RNF-SEG-002 | La autorización la comprueba el servidor; no se basa solo en datos enviados por el cliente ni en la interfaz. | `AGENTS.md`; `.claude/rules/security.md` | Previsto |
| RNF-PRI-002 | Las fotografías y las coordenadas se tratan como datos sensibles. | `.claude/rules/security.md` | Previsto |
| RNF-AUD-001 | Los cambios relevantes y las actuaciones quedan registrados y son consultables según permisos. | Contexto §5 | Previsto |
| RNF-ACC-001 | La experiencia web y móvil es accesible y visualmente consistente. El nivel de accesibilidad exigido no está definido. | Contexto §4, §5 | Previsto |
| RNF-CAL-001 | El producto es mantenible y testable. | Contexto §5 | Previsto |
| RNF-COS-001 | La infraestructura mantiene un coste contenido. | Contexto §5 | Previsto |
Otros requisitos no funcionales se definen en su sección: RNF-PRI-001 (sección 7.1) y RNF-IA-001 (sección 12.3). Los requisitos de funcionamiento sin IA son RN-IA-001 y RN-IA-003.

### 14.2. Restricciones

| ID | Restricción | Origen | Estado |
|---|---|---|---|
| RES-001 | La cobertura territorial de la visión es toda España, no una ciudad piloto. | Contexto §3 | Previsto |
| RES-002 | Retirada: duplicaba RN-IA-001. El identificador no se reutiliza. | — | Retirada |
| RES-003 | Las preferencias tecnológicas (Next.js, Flutter, NestJS, PostgreSQL con PostGIS, Supabase, Mapbox y otras) figuran en el Contexto §6 y no se repiten aquí. Son preferencias, no decisiones de arquitectura: su organización se justificará en la documentación técnica. | Contexto §6 | Previsto |
| RES-004 | Se prefiere un monorepo con backend monolítico modular y arquitectura hexagonal aplicada de forma pragmática. | Contexto §6; `AGENTS.md` | Previsto |
| RES-005 | No se afirma que exista implementación, prueba superada, integración municipal ni decisión técnica no verificada. | Contexto §8; `AGENTS.md` | Previsto |
| RES-006 | Las decisiones de conservación de datos no constituyen validación jurídica. | D20 | Aprobado |

## 15. Reglas de negocio y trazabilidad

Las reglas de negocio (`RN-`) figuran en la sección de su área. Esta sección enlaza cada decisión y cada parte del contexto con sus requisitos.

### 15.1. Decisiones aprobadas D01–D20

Cada fila resume la decisión aprobada y enlaza con los requisitos que la concretan. El detalle normativo está en las tablas de requisitos. Esta sección no aporta evidencia externa de la aprobación (ver 1.2).

| Decisión | Resumen aprobado | Requisitos |
|---|---|---|
| D01 Cobertura territorial | El catálogo incluye todos los municipios de España. Catálogo, pertenencia geográfica y habilitación operativa son conceptos distintos. Solo se crean avisos en municipios habilitados. Los no habilitados pueden explorarse para consultar información territorial. | RF-TER-001, RF-TER-003, RN-TER-001 a RN-TER-003 |
| D02 Selección y validación de ubicación | Contexto por comunidad autónoma, provincia y municipio. El código postal es opcional y no determina la pertenencia. Ubicación por GPS, dirección o marcador, con confirmación expresa. Validación contra la geometría municipal, incluidos territorios discontinuos y enclaves. Si el punto cae claramente en otro municipio se propone la corrección con confirmación. Sin cambios silenciosos ni asignación por proximidad. | RF-TER-005 a RF-TER-010, RN-TER-004, RN-TER-006 |
| D03 Ambigüedades territoriales | Un aviso con municipio indeterminable puede quedar pendiente de validación territorial, sin asignación municipal ni publicación. Resuelve el administrador global. Los gestores señalan discrepancias. Las correcciones se justifican y auditan conservando el original. Puede finalizarse como «no tramitable por ubicación». Pendiente: tratamiento si el aviso acaba en un municipio no habilitado. | RF-TER-012 a RF-TER-016, RN-TER-007 a RN-TER-009, OPEN-001 |
| D04 Roles y ámbitos | Cuatro perfiles. Un usuario puede tener varios municipios y roles distintos en cada uno. Permisos por usuario, rol, municipio y operación. Administrador global (plataforma y habilitación) y municipal (su ámbito). Sin permisos en otro municipio por trabajar en uno. | RF-ROL-001 a RF-ROL-004, RF-TER-004, RN-ROL-001 a RN-ROL-004, RNF-SEG-001, RF-DSH-004 |
| D05 Acceso público y privacidad | Consulta pública sin sesión. La identidad del denunciante nunca es pública. Tres niveles de información. La publicación requiere revisión del gestor y es independiente de la tramitación. Cada foto se aprueba individualmente. No se exponen notas internas, asignaciones ni datos personales. La información privada se protege en API, imágenes, notificaciones, exportaciones y tiempo real. | RF-ROL-005, RF-PUB-001, RF-PUB-002, RN-PUB-001 a RN-PUB-007, RN-FOT-002, RNF-PRI-001, RN-DSH-001 |
| D06 Fotografías y moderación | Originales protegidas. El gestor aprueba versiones anonimizadas, sin EXIF, y puede ocultar contenido sensible o pedir correcciones. Una incidencia legítima no se rechaza solo por contener datos no publicables. Moderación trazable y no dependiente de IA. | RN-FOT-001, RF-FOT-002, RN-FOT-003, RF-FOT-003, RN-FOT-004 a RN-FOT-006, RN-PUB-007 |
| D07 Ciclo de vida principal | Siete estados: Registrada, En revisión, Validada, Asignada, En curso, Resuelta y Cerrada. El ciudadano crea, el gestor revisa, clasifica, prioriza, valida, rechaza y asigna, y el operario ejecuta y propone la resolución. El gestor valida y cierra o devuelve a intervención. El rechazo exige motivo. La publicación no es un estado. Las transiciones no son necesariamente lineales. | RF-INC-001 a RF-INC-006, RN-INC-001 a RN-INC-004, RN-INC-006, RN-INC-014, RF-CAT-005 |
| D08 Rechazo, cierre y reapertura | El gestor puede rechazar de forma motivada. El ciudadano puede solicitar la reapertura en los 30 días siguientes al cierre, con motivo estructurado y explicación. El gestor acepta o deniega. Mismo expediente e historial. Se registra como evento, sin estado «Reabierta» obligatorio. Pasado el plazo, nuevo aviso relacionado. Reapertura excepcional por gestor con justificación y auditoría. | RN-INC-005, RN-INC-007, RF-INC-009 a RF-INC-014 |
| D09 Asignaciones y personal | El gestor asigna y reasigna en su ámbito conservando la trazabilidad. Sin asignación automática a municipios vecinos. Sin gestores, los avisos quedan pendientes y se alerta. Sin operarios, las validadas quedan pendientes de asignación. La falta de personal no es motivo de rechazo. Sin promesa de plazos. | RF-INC-015, RN-INC-008 a RN-INC-013 |
| D10 Duplicados | Sugerencia de incidencias públicas cercanas antes de registrar. Detección básica sin IA. El gestor decide la vinculación. Sin fusión destructiva. Una incidencia principal concentra la gestión y los vinculados conservan identidad y seguimiento. Vinculación reversible, motivada y auditable. Las estadísticas distinguen avisos de intervenciones. | RF-DUP-001 a RF-DUP-005, RN-DUP-001 a RN-DUP-004, RF-DSH-002 |
| D11 Desvinculación y excepciones | El ciudadano puede pedir la desvinculación y el gestor decide, o desvincula de oficio. Rechazar la principal no rechaza los vinculados. Reabrir la principal no modifica automáticamente los demás expedientes. Cada ciudadano puede pedir la revisión de su propio aviso. Las comunicaciones privadas no se propagan. Los vinculados reciben actualizaciones públicas pertinentes. | RF-DUP-006 a RF-DUP-010, RN-DUP-005 a RN-DUP-008, OPEN-003 |
| D12 Identidad ciudadana | Consulta pública sin autenticación. Registrar avisos, seguir los propios y solicitar reaperturas o desvinculaciones requiere cuenta. Los datos de identidad son privados. | RF-IDN-001, RF-IDN-002, RN-IDN-001, RF-ROL-005, RF-PUB-001, RF-INC-002 |
| D13 Notificaciones | Centro in-app, push y correo. Eventos relevantes por destinatario. Sin duplicados por avisos relacionados. Las notas internas y la información privada no se incluyen. El tiempo real complementa a los canales. | RF-NOT-001 a RF-NOT-006, RN-NOT-001 a RN-NOT-005 |
| D14 Categorías | Catálogo global. Los administradores municipales habilitan categorías y configuran subcategorías locales. Clasificación global común. El histórico se preserva. El ciudadano elige categoría o «Otros». El gestor corrige con trazabilidad. Clasificar y priorizar son distintos. | RF-CAT-001 a RF-CAT-004, RN-CAT-001 a RN-CAT-003, RF-DSH-004 |
| D15 IA y supervisión humana | CityFix funciona sin IA. La IA propone clasificaciones, prioridades, duplicados, resúmenes y borradores. No ejecuta acciones oficiales. Su fallo no bloquea la tramitación. Nunca amplía permisos. | RN-IA-001 a RN-IA-004, RF-IA-001 |
| D16 Credenciales de IA | Administración global de proveedores, modelos y credenciales. Los administradores municipales no las administran. La plataforma habilita o deshabilita la IA por municipio. Credenciales no expuestas. No es BYOK por municipio. | RF-IA-002, RF-IA-003, RN-IA-005, RNF-IA-001 |
| D17 Privacidad de IA | Minimización. Se evitan datos personales, fotografías y coordenadas exactas salvo capacidad concreta y autorización adecuada. Sin acceso general. La aprobación humana no sustituye los controles de privacidad. | RN-IA-006 a RN-IA-009 |
| D18 Presupuesto de IA | Presupuesto global compartido, sin cuotas por municipio. Consumo medible por municipio y funcionalidad. Al llegar al límite se suspende la IA y el sistema convencional sigue. Una estimación no garantiza un límite exacto. | RF-IA-004, RF-IA-005, RN-IA-010 a RN-IA-012 |
| D19 Auditoría de IA | Auditoría estructurada de recomendación, procedencia, decisión humana y resultado. No se guardan indiscriminadamente prompts y respuestas completos. Registros no alterables y acceso por rol y municipio. | RF-IA-006, RN-IA-013 a RN-IA-016 |
| D20 Conservación de datos | Minimización y conservación diferenciada. Supresión, anonimización y retirada cuando procedan. Borrar una cuenta no destruye expedientes que deban conservarse. Originales con acceso restringido. Auditoría y copias de seguridad con reglas de caducidad. Plazos según normativa, sin validación jurídica. | RN-DAT-001 a RN-DAT-006, RF-DAT-001, RES-006 |

### Aclaraciones posteriores a D01–D20

| Aclaración | Requisitos |
|---|---|
| El texto libre de la incidencia requiere revisión del gestor antes de publicarse. | RN-PUB-006 |
| El contenido no publicable puede permanecer disponible para la tramitación interna, respetando los permisos. | RN-PUB-007 |
| El ciudadano de un aviso vinculado puede solicitar la revisión de su aviso, pero no modifica directamente la principal. | RF-DUP-009, RN-DUP-008 |
| «Resuelta» significa trabajo comunicado como terminado y pendiente de validación del gestor. | RN-INC-014 |
| Notificaciones: canales externos configurables, eventos esenciales registrados aunque estén desactivados, sin garantía de entrega por canal desactivado, comunicaciones de autenticación y seguridad independientes. | RF-NOT-002 a RF-NOT-004, RN-NOT-001, RN-NOT-002 |
| Alcance administrativo: el administrador global gestiona habilitación y catálogos globales, y el municipal su ámbito. | RF-DSH-004 |
| El plazo general de reapertura es de 30 días desde el cierre. Su cómputo para avisos vinculados sigue abierto. | RF-INC-009, OPEN-003 |

### 15.2. Visión inicial (`PROJECT_CONTEXT.md`)

| Contexto | Requisitos |
|---|---|
| §1 Idea y problema | HIP-001, HIP-002, sección 2 |
| §2 Usuarios y experiencia | Sección 3, RF-INC-007, RF-FOT-001, RF-NOT-007, RF-DSH-001, RF-DSH-006, RF-DSH-007 |
| §3 Cobertura territorial | RF-TER-001, RF-TER-002, RF-TER-005, RF-TER-007, RES-001 |
| §4 Capacidades previstas | Sección 4 (tabla de alcance), RF-TER-011, RF-INC-008, RF-DSH-002, RF-DSH-003, RF-DSH-004, RF-DSH-005 |
| §5 Principios de producto | Sección 2.5, RN-IA-001, RN-TER-005, RNF-SEG-001, RNF-AUD-001, RNF-ACC-001, RNF-CAL-001, RNF-COS-001 |
| Reglas del repositorio (`AGENTS.md`, `.claude/rules/`) | RNF-SEG-002, RNF-PRI-002 |
| §6 Orientación tecnológica | RES-003, RES-004 |
| §7 Aspectos por descubrir | Sección 16 |

### 15.3. Trazabilidad futura

Cada requisito deberá poder rastrearse hasta las historias, los criterios de aceptación, los tickets y las pruebas que se creen. Esas columnas se añadirán cuando existan esos artefactos.

## 16. Supuestos, riesgos y cuestiones abiertas

### 16.1. Supuestos

| ID | Supuesto | Estado |
|---|---|---|
| SUP-001 | Si el punto pertenece claramente a un municipio no habilitado, no se puede registrar el aviso (consecuencia de D01 y D02). | A confirmar |
| SUP-002 | Un ayuntamiento actuará probablemente como responsable del tratamiento de los datos personales. No tiene base en el contexto ni validación jurídica. | Hipótesis; requiere validación jurídica |
| SUP-003 | Para redactar este documento, la validación territorial se describe como una condición distinta de los siete estados operativos, sin decidir su representación formal. | A confirmar (OPEN-002) |

### 16.2. Riesgos

| ID | Riesgo | Relacionado con |
|---|---|---|
| RIE-001 | Reidentificación del autor por la precisión de las coordenadas o de la hora publicadas. El texto y las fotografías pasan por revisión del gestor (RN-PUB-006, RN-FOT-002). | OPEN-007, RN-PUB-001 |
| RIE-002 | Fallos de autorización entre municipios en usuarios multimunicipio o en avisos sin municipio validado. | RN-ROL-003, OPEN-005 |
| RIE-003 | Un municipio con mucho uso puede agotar el presupuesto de IA compartido y suspender la IA para todos (decisión aceptada en D18). | RN-IA-010, RN-IA-011 |
| RIE-004 | El administrador global concentra la resolución de conflictos territoriales y la habilitación de toda España. | RF-TER-013 |
| RIE-005 | Filtración de campos internos o privados en listados, notificaciones, exportaciones o tiempo real. | RNF-PRI-001 |
| RIE-006 | Calidad insuficiente de los datos territoriales en algunas zonas. | HIP-004 |
| RIE-007 | Municipios habilitados sin gestores u operarios disponibles, con avisos sin atender. | RN-INC-010, RN-INC-011 |
| RIE-008 | Incoherencia entre estado operativo, publicación, validación territorial y resultados terminales. | OPEN-002 |

### 16.3. Cuestiones abiertas

Las siete primeras son las ambigüedades conocidas, que no se deciden en este documento.

| ID | Cuestión | Impacto |
|---|---|---|
| OPEN-001 | Tratamiento final de un aviso que entró en validación territorial y resulta pertenecer a un municipio no habilitado (pendiente explícito de D03). | Territorio, avisos |
| OPEN-002 | Representación formal del rechazo administrativo frente al cierre: en qué queda una incidencia rechazada, si «Cerrada» incluye el rechazo, cómo se representa «no tramitable por ubicación», si el plazo de 30 días aplica al rechazo y si el ciudadano puede impugnarlo. | Ciclo de vida, notificaciones, métricas |
| OPEN-003 | Estado y plazo de reapertura de los avisos vinculados: qué estado tienen, desde cuándo cuentan los 30 días para su autor y qué se reabre si un autor vinculado lo solicita. El plazo general de 30 días desde el cierre (RF-INC-009) está aprobado; su cómputo exacto para avisos vinculados sigue abierto. | Duplicados, reapertura |
| OPEN-004 | Superficie exacta de consulta pública sin autenticación (app, web pública o ambas) y superficie del administrador. | Privacidad, experiencia |
| OPEN-005 | Permisos sobre avisos sin municipio validado: quién los ve y con qué datos mientras se valida. | Autorización, privacidad |
| OPEN-006 | Separación de funciones administrativas y de gestión: si el administrador municipal puede ejercer de gestor, si una misma persona puede proponer y validar la resolución, y a qué administración se alerta cuando no hay gestores. | Roles, autorización |
| OPEN-007 | Precisión y privacidad de las coordenadas y datos temporales publicados. | Privacidad, reidentificación |

Otras cuestiones con impacto funcional real:

| ID | Cuestión | Impacto |
|---|---|---|
| OPEN-008 | Matriz de transiciones del ciclo de vida y matriz de permisos por rol, municipio y operación (pendiente explícito). | Ciclo de vida, autorización |
| OPEN-009 | Criterios de qué eventos y campos del historial son públicos, y qué se muestra públicamente de una incidencia rechazada, desvinculada o «no tramitable por ubicación». | Visibilidad |
| OPEN-010 | Ciclo de vida de la habilitación municipal: qué ocurre con las incidencias y el personal si un municipio deja de estar habilitado. | Territorio, administración |
| OPEN-011 | Tratamiento de incidencias en vías o espacios que no son de competencia municipal. | Alcance |
| OPEN-012 | Efecto de que el ciudadano «indique una coincidencia» al ver incidencias cercanas (D10). | Duplicados |
| OPEN-013 | Alcance de la «información territorial» consultable en municipios no habilitados (D01). | Territorio |
| OPEN-014 | Quién concede la «autorización adecuada» para enviar a IA datos personales, fotografías o coordenadas exactas (D17). | IA, privacidad |
| OPEN-015 | Si la asignación puede ser una propuesta de IA (el Contexto §4 la incluye y D15 no la menciona). | IA |
| OPEN-016 | Catálogo de categorías y subcategorías, y escala y reglas de prioridad. | Categorías |
| OPEN-017 | Reglas de proximidad y detección de duplicados, y plazos y umbrales de escalado. | Duplicados, operación |
| OPEN-018 | Plazos concretos de conservación y política jurídica de tratamiento de datos. | Datos |
| OPEN-019 | Objetivos cuantitativos de los requisitos no funcionales y nivel de accesibilidad exigido. | Calidad |
| OPEN-020 | Indicadores de éxito del producto. | Objetivos |

### 16.4. Decisiones aplazadas al diseño técnico

No son bloqueos del PRD:

- Detalles de implementación de la anonimización de fotografías.
- Elección de proveedores y servicios externos.
- Mecanismo de contabilización de consumo de IA, alertas y límites técnicos.
- Contratos API, modelo físico de datos e infraestructura.
- Despliegue y límites técnicos de almacenamiento.

### 16.5. Actualizaciones documentales

- **Terminología BYOK:** `PROJECT_CONTEXT.md` (§4, §6 y §7) y `.claude/rules/security.md` se han actualizado a «credenciales de proveedores de IA configuradas centralmente», conforme a D16.
- Los borradores de trabajo del discovery contenían recomendaciones no aprobadas, entre ellas BYOK por municipio, superadas por D16. No se citan como fuente.
- `readme.md` (secciones 1.1 y 1.2) y `prompts.md` (sección 1) se han actualizado con información comprobada. El resto de sus secciones sigue pendiente.
- La planificación incremental de entrega se documentará aparte, sin reducir el alcance global de este PRD.
