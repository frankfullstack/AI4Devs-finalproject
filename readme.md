## Índice

0. [Ficha del proyecto](#0-ficha-del-proyecto)
1. [Descripción general del producto](#1-descripción-general-del-producto)
2. [Arquitectura del sistema](#2-arquitectura-del-sistema)
3. [Modelo de datos](#3-modelo-de-datos)
4. [Especificación de la API](#4-especificación-de-la-api)
5. [Historias de usuario](#5-historias-de-usuario)
6. [Tickets de trabajo](#6-tickets-de-trabajo)
7. [Pull requests](#7-pull-requests)

---

## 0. Ficha del proyecto

### **0.1. Tu nombre completo:**

### **0.2. Nombre del proyecto:**

CityFix

### **0.3. Descripción breve del proyecto:**

CityFix es una plataforma, actualmente en fase de definición, para comunicar y gestionar incidencias en espacios públicos de España (baches, farolas averiadas, aceras dañadas, limpieza, contenedores, parques o señalización), facilitando su aviso, seguimiento y resolución entre ciudadanos, gestores, operarios y administradores.

### **0.4. URL del proyecto:**

> Puede ser pública o privada, en cuyo caso deberás compartir los accesos de manera segura. Puedes enviarlos a [alvaro@lidr.co](mailto:alvaro@lidr.co) usando algún servicio como [onetimesecret](https://onetimesecret.com/).

### 0.5. URL o archivo comprimido del repositorio

https://github.com/frankfullstack/AI4Devs-finalproject

> Puedes tenerlo alojado en público o en privado, en cuyo caso deberás compartir los accesos de manera segura. Puedes enviarlos a [alvaro@lidr.co](mailto:alvaro@lidr.co) usando algún servicio como [onetimesecret](https://onetimesecret.com/). También puedes compartir por correo un archivo zip con el contenido


---

## 1. Descripción general del producto

> Describe en detalle los siguientes aspectos del producto:

### **1.1. Objetivo:**

CityFix busca facilitar que los avisos ciudadanos sobre espacios públicos de España se registren con una ubicación confirmada, se revisen, se asignen y se resuelvan, con seguimiento para quien avisa y respetando su privacidad.

La idea parte de una hipótesis por validar: los avisos urbanos pueden quedar dispersos en distintos canales, tener ubicaciones imprecisas, duplicarse o carecer de un seguimiento claro. No se presupone que ninguna administración pública utilice la plataforma ni se afirman beneficios medidos.

**Para quién:** ciudadanos, que avisan y siguen sus incidencias; gestores municipales, que las revisan y supervisan; operarios, que ejecutan y documentan los trabajos; y administradores, que gestionan la plataforma o su ámbito municipal.

**Estado:** el proyecto está en fase de definición. Los requisitos de producto están recogidos en [`docs/PRD.md`](docs/PRD.md), aprobado como base funcional con cuestiones abiertas. No hay ninguna funcionalidad implementada ni verificada.

### **1.2. Características y funcionalidades principales:**

Capacidades **previstas** de CityFix. Ninguna está implementada; el detalle y su estado de decisión se encuentran en [`docs/PRD.md`](docs/PRD.md).

- **Territorio:** catálogo de todos los municipios de España, habilitación operativa municipal y validación de la ubicación confirmada por el ciudadano.
- **Avisos y seguimiento:** registro de incidencias por ciudadanos autenticados y seguimiento de las propias.
- **Tramitación:** revisión, clasificación, priorización, asignación y resolución por gestores y operarios, con historial y reapertura.
- **Publicación y privacidad:** consulta pública de incidencias publicadas, revisión del gestor antes de publicar y protección de la identidad, las fotografías y las ubicaciones.
- **Duplicados:** sugerencia de avisos cercanos y vinculación decidida por el gestor.
- **Notificaciones:** centro de notificaciones, push y correo configurables, y actualizaciones en tiempo real.
- **Gestión municipal:** categorías, dashboard con listados, filtros, mapas, métricas y exportaciones autorizadas, y administración de usuarios y configuración.
- **IA opcional:** propuestas supervisadas por personas, con credenciales de proveedores de IA configuradas centralmente y presupuesto global compartido. CityFix debe funcionar íntegramente sin IA.
- **Datos:** conservación diferenciada, supresión y anonimización cuando procedan.

Las cuestiones pendientes de decidir figuran en la sección 16 del PRD.

### **1.3. Diseño y experiencia de usuario:**

> Proporciona imágenes y/o videotutorial mostrando la experiencia del usuario desde que aterriza en la aplicación, pasando por todas las funcionalidades principales.

### **1.4. Instrucciones de instalación:**
> Documenta de manera precisa las instrucciones para instalar y poner en marcha el proyecto en local (librerías, backend, frontend, servidor, base de datos, migraciones y semillas de datos, etc.)

---

## 2. Arquitectura del Sistema

### **2.1. Diagrama de arquitectura:**
> Usa el formato que consideres más adecuado para representar los componentes principales de la aplicación y las tecnologías utilizadas. Explica si sigue algún patrón predefinido, justifica por qué se ha elegido esta arquitectura, y destaca los beneficios principales que aportan al proyecto y justifican su uso, así como sacrificios o déficits que implica.


### **2.2. Descripción de componentes principales:**

> Describe los componentes más importantes, incluyendo la tecnología utilizada

### **2.3. Descripción de alto nivel del proyecto y estructura de ficheros**

> Representa la estructura del proyecto y explica brevemente el propósito de las carpetas principales, así como si obedece a algún patrón o arquitectura específica.

### **2.4. Infraestructura y despliegue**

> Detalla la infraestructura del proyecto, incluyendo un diagrama en el formato que creas conveniente, y explica el proceso de despliegue que se sigue

### **2.5. Seguridad**

> Enumera y describe las prácticas de seguridad principales que se han implementado en el proyecto, añadiendo ejemplos si procede

### **2.6. Tests**

> Describe brevemente algunos de los tests realizados

---

## 3. Modelo de Datos

### **3.1. Diagrama del modelo de datos:**

> Recomendamos usar mermaid para el modelo de datos, y utilizar todos los parámetros que permite la sintaxis para dar el máximo detalle, por ejemplo las claves primarias y foráneas.


### **3.2. Descripción de entidades principales:**

> Recuerda incluir el máximo detalle de cada entidad, como el nombre y tipo de cada atributo, descripción breve si procede, claves primarias y foráneas, relaciones y tipo de relación, restricciones (unique, not null…), etc.

---

## 4. Especificación de la API

> Si tu backend se comunica a través de API, describe los endpoints principales (máximo 3) en formato OpenAPI. Opcionalmente puedes añadir un ejemplo de petición y de respuesta para mayor claridad

---

## 5. Historias de Usuario

> Documenta 3 de las historias de usuario principales utilizadas durante el desarrollo, teniendo en cuenta las buenas prácticas de producto al respecto.

**Historia de Usuario 1**

**Historia de Usuario 2**

**Historia de Usuario 3**

---

## 6. Tickets de Trabajo

> Documenta 3 de los tickets de trabajo principales del desarrollo, uno de backend, uno de frontend, y uno de bases de datos. Da todo el detalle requerido para desarrollar la tarea de inicio a fin teniendo en cuenta las buenas prácticas al respecto. 

**Ticket 1**

**Ticket 2**

**Ticket 3**

---

## 7. Pull Requests

> Documenta 3 de las Pull Requests realizadas durante la ejecución del proyecto

**Pull Request 1**

**Pull Request 2**

**Pull Request 3**

