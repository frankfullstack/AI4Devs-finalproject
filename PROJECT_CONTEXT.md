# CityFix — Contexto inicial del proyecto

> **Estado:** idea y visión de producto para iniciar un proyecto desde cero (*greenfield*). No es un PRD ni acredita diseño, código o funcionalidades implementadas.
> **Propósito:** ofrecer a Claude Code el contexto mínimo para realizar el discovery y elaborar progresivamente la documentación del proyecto, sin anticipar sus resultados.

## 1. Idea y problema

CityFix será una plataforma para comunicar y gestionar incidencias en espacios públicos de España: baches, farolas averiadas, aceras dañadas, problemas de limpieza, contenedores, parques o señalización, entre otros.

La idea nace de una **hipótesis por validar**: los avisos urbanos pueden quedar dispersos en distintos canales, tener ubicaciones imprecisas, duplicarse o carecer de un seguimiento claro. CityFix pretende facilitar su comunicación y seguimiento y ayudar a quienes deben gestionarlos y resolverlos. No se presupone que ninguna administración pública utilice la plataforma ni se afirman beneficios medidos.

## 2. Usuarios y experiencia general

- **Ciudadano:** registra una incidencia desde el móvil, indica qué ocurre y dónde, puede adjuntar fotografías y consulta su evolución y la información pública disponible.
- **Gestor:** usa un dashboard web para revisar, clasificar, priorizar, detectar posibles duplicados, asignar incidencias y supervisar su resolución.
- **Operario:** utiliza la **misma app móvil**, con una experiencia adaptada a su rol, para consultar trabajos asignados, registrar actuaciones y documentar resultados.
- **Administrador:** gestiona usuarios, permisos, municipios habilitados, catálogos, configuración general y capacidades opcionales de IA.

El recorrido principal buscado es: **aviso ciudadano → revisión → asignación → intervención → resolución → seguimiento**. Se prevén mapas, fotografías, historial de cambios, actualizaciones en tiempo real, búsquedas, filtros, estadísticas y notificaciones.

## 3. Cobertura territorial

CityFix está concebido para **toda España**, incluidas península, Baleares, Canarias, Ceuta y Melilla; no se limita a una ciudad piloto como visión de producto.

El usuario debe poder buscar y seleccionar un municipio o término municipal, situar la incidencia mediante GPS, búsqueda de dirección o marcador manual y confirmar su ubicación. La plataforma deberá distinguir los municipios por sus identificadores oficiales y comprobar que el punto corresponde al término municipal seleccionado.

**Disponer de un municipio en el catálogo no significa que su ayuntamiento opere CityFix.** Las reglas de recepción de avisos en municipios no habilitados se decidirán durante la definición de requisitos. Se consideran INE e IGN/CNIG como fuentes de referencia para los datos territoriales.

## 4. Capacidades previstas

El producto completo contempla, sin definir todavía sus requisitos detallados:

- Cuentas, autenticación, roles y permisos, incluidos los ámbitos municipales autorizados.
- Creación, consulta, clasificación, priorización, asignación, tramitación y resolución de incidencias.
- Categorías, departamentos, equipos, operarios y relaciones entre posibles avisos duplicados.
- Fotografías, localización geográfica, mapas y visualización de límites municipales.
- Historial cronológico de cada incidencia, distinguiendo información pública e interna.
- Actualizaciones en tiempo real y notificaciones relevantes.
- Dashboard municipal con listados, filtros, mapas, métricas, administración y exportaciones autorizadas.
- Procesamiento convencional de incidencias mediante reglas, búsqueda de proximidad y revisión humana.
- Agentes de IA **opcionales** para proponer clasificación, posibles duplicados, prioridad y asignación; configuración de proveedores, modelos, claves y costes.
- Seguridad, privacidad, accesibilidad, auditoría, pruebas y una experiencia visual profesional en web y móvil.

Estas capacidades definen la **visión global**, no el contenido que ya está desarrollado ni un compromiso de entregarlas todas a la vez. El trabajo se ordenará incrementalmente por valor, riesgo y dependencias, sin eliminar el alcance global por defecto.

## 5. Principios de producto

1. **Funcionar sin IA:** la tramitación convencional debe seguir operativa sin claves, con fallos del proveedor o con presupuesto agotado.
2. **Control humano:** la IA recomienda; solo el sistema y las personas autorizadas realizan acciones oficiales.
3. **Ámbito municipal y privacidad:** las consultas, imágenes, operaciones y notificaciones deben respetar roles, permisos y límites territoriales.
4. **Ubicación explícita:** la localización del usuario o los metadatos de una foto no sustituyen la confirmación del lugar de la incidencia.
5. **Trazabilidad:** los cambios relevantes y las actuaciones deben quedar registrados y ser consultables según permisos.
6. **Calidad y costes:** diseño accesible y consistente, seguridad desde el inicio, mantenibilidad, testabilidad e infraestructura de coste contenido.

## 6. Orientación tecnológica inicial

Se parte de las siguientes **preferencias y restricciones tecnológicas**, cuya organización concreta se justificará en la documentación de arquitectura:

| Área | Tecnología prevista |
|---|---|
| Dashboard web | Next.js, React, TypeScript, Tailwind CSS y shadcn/ui |
| App Android/iOS | Flutter y Dart; una app para ciudadano y operario |
| Backend | NestJS y TypeScript, API REST y Socket.IO |
| Datos y geografía | PostgreSQL, PostGIS y Prisma |
| Identidad y archivos | Supabase Auth y Supabase Storage |
| Mapas y geocodificación | Mapbox |
| Datos administrativos | INE e IGN/CNIG como referencias |
| IA opcional | Anthropic API y OpenRouter mediante BYOK |

Se prefiere un **monorepo con backend monolítico modular**, aplicando arquitectura hexagonal y principios de Clean Architecture de forma pragmática en backend y clientes. El dominio debe estar separado de frameworks y proveedores sin crear abstracciones innecesarias. No se buscan microservicios ni infraestructura adicional salvo necesidad justificada.

## 7. Aspectos que debemos descubrir y decidir

Antes de cerrar los requisitos y el diseño, hay que concretar, entre otros: política de municipios no habilitados; permisos sobre uno o varios municipios; visibilidad pública e interna; reglas de clasificación, asignación, estados, reapertura y cierre; tratamientos de duplicados y fotografías; manejo de límites territoriales; notificaciones; comportamiento y revisión de la IA; configuración BYOK y límites de coste; retención de datos y despliegue.

Estas cuestiones **no están decididas por este contexto**. Se resolverán mediante discovery, PRD y decisiones arquitectónicas, distinguiendo decisiones aprobadas, propuestas y supuestos.

## 8. Cómo utilizar este documento

Este archivo es el **punto de partida**, no el lugar para redactar el PRD, historias, criterios de aceptación, tickets, modelos de datos, endpoints, diagramas definitivos o ADRs. Dichos artefactos se crearán y revisarán en sus propios documentos y podrán desarrollar las ideas aquí resumidas.

La documentación de producto será en **español**. Código, nombres de identificadores, contratos y tests se escribirán en **inglés**. No se afirmará que existe implementación, una prueba superada, una integración municipal ni una decisión técnica que no se haya verificado o aprobado.

Este documento describe **CityFix como producto**. Las exigencias académicas, las fechas y el registro de uso de IA se gestionarán por separado en la documentación de la entrega.
