# Bitera Bio | Identidad Digital Soberana

> **Repositorio Maestro de Desarrollo**
> *Plataforma SaaS para la generación de identidades digitales estáticas bajo normativa de Soberanía Digital.*

---

## 1. Visión y Alcance del Proyecto
Este repositorio aloja el código fuente y la inteligencia operativa de **Bitera Bio**. El software aquí contenido está diseñado para operar en un entorno de **Infraestructura Soberana (On-Premise)**, aislado de dependencias de terceros para garantizar la privacidad absoluta del usuario final.

### Referencias Normativas (Documentación Vinculante)
Antes de escribir código, todo agente debe consultar la documentación oficial en el directorio `docs/`:
* **Definición del Producto:** `docs/01-producto/BIO-001-Definicion-Maestra.md`
* **Procedimiento de Despliegue:** `docs/02-procedimientos/SOP-BIO-01-Despliegue-Cliente.md`
* **Arquitectura de Red:** `docs/03-arquitectura/BIO-ARQ-01-Topologia-y-Flujo.md`

---

## 2. Directivas Técnicas por Rol Especializado

### ROL: FRONTEND DEVELOPER (UI/UX)
**Objetivo:** Rendimiento extremo (TTFB < 50ms) y cero dependencia externa.

1.  **Política de Activos Locales (Strict Local-Only):**
    * Está **prohibido** el uso de CDNs (Google Fonts, FontAwesome, JSDelivr).
    * Todas las fuentes, iconos, estilos y scripts deben residir físicamente en `src/template-bio/assets/`.
    * Las imágenes deben ser formato WebP optimizado.

2.  **Arquitectura de Estilos:**
    * Motor CSS: Nativo (Vanilla CSS3). No se permite SASS/LESS en tiempo de ejecución.
    * Personalización: Uso obligatorio de **CSS Custom Properties** definidas en el `:root` para la gestión de temas de color.
    * Metodología: BEM (Block Element Modifier) estricto para evitar colisiones de estilo.

3.  **JavaScript:**
    * Límite de peso: 3KB (Gzipped).
    * Restricción: Solo para manipulación del DOM (UI). Prohibido frameworks SPA (React/Vue) o librerías de rastreo.

### ROL: SECOPS ENGINEER (Seguridad)
**Objetivo:** Garantizar la integridad del código y la privacidad por diseño.

1.  **Hardening de Cabeceras:**
    * El código debe ser compatible con una política CSP estricta: `default-src 'self'`.
    * No se permiten estilos o scripts en línea (`unsafe-inline`) salvo excepciones documentadas en el bloque `<head>` para inyección de variables.

2.  **Privacidad:**
    * El software es **Stateless**. No debe configurar cookies en el navegador del cliente.
    * Verificar ausencia total de píxeles de seguimiento (Meta, Google Analytics, LinkedIn Insight).

### ROL: INFRASTRUCTURE ENGINEER (DevOps)
**Objetivo:** Despliegue atómico y configuración de servidor web.

1.  **Servidor Web:**
    * Optimizado para **Nginx**. No incluir archivos `.htaccess` o `web.config`.
    * La estructura de URLs depende del sistema de archivos: `dominio.com/slug` mapea a `.../slug/index.html`.

2.  **Estrategia de Despliegue:**
    * El despliegue se realiza moviendo el artefacto generado a la DMZ y asignando permisos al usuario `www-data`.
    * Seguir estrictamente el `SOP-BIO-01`.

---

## 3. Stack Tecnológico Aprobado

| Capa | Tecnología | Especificación Técnica |
| :--- | :--- | :--- |
| **Generación** | SSG Manual | HTML5 Semántico pre-renderizado. |
| **Estilos** | CSS3 | Variables Nativas + Flexbox/Grid. |
| **Fuentes** | WOFF2 | Alojamiento local con `font-display: swap`. |
| **Imágenes** | WebP / SVG | Optimización Lossy 85% para fotos, Vectorial para iconos. |
| **Servidor** | Nginx | Terminación TLS 1.3 y Cache-Control agresivo. |

---

## 4. Estructura del Sistema de Archivos

```text
/
├── docs/                       # Base de Conocimiento (SGI)
│   ├── 01-producto/            # Especificaciones Funcionales (BIO-001)
│   ├── 02-procedimientos/      # Manuales de Operación (SOPs)
│   └── 03-arquitectura/        # Mapas de Red y Flujos
│
├── src/                        # Código Fuente
│   └── template-bio/           # PLANTILLA MAESTRA (Golden Image)
│       ├── assets/             # Recursos estáticos locales
│       │   ├── css/            # core.css
│       │   ├── fonts/          # Archivos de tipografía
│       │   ├── img/            # Placeholders y Sprites SVG
│       │   └── js/             # Lógica de UI mínima
│       └── index.html          # Esqueleto HTML semántico
│
└── config/                     # Infraestructura como Código
    └── nginx/                  # Snippets de configuración de servidor
