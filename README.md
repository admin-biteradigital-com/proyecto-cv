# Bitera Bio | Identidad Digital Soberana

> **Proyecto SaaS de Bitera Digital**
> *Infraestructura de Identidad Profesional y Currículum Vitae Web Estático.*

## 1. Visión del Proyecto
**Bitera Bio** es un servicio de Software as a Service (SaaS) diseñado para proveer identidades digitales profesionales, minimalistas y de alta velocidad.

A diferencia de las soluciones de mercado convencionales, este proyecto opera bajo una arquitectura de **Soberanía Digital Total**. La infraestructura, el código y los datos residen en el **Bitera Home Datacenter** (Uruguay), garantizando:
* **Privacidad por Diseño:** Sin rastreadores externos ni venta de datos.
* **Resiliencia Forense:** Alojado en infraestructura HEDT con redundancia 3-2-1-0.
* **Velocidad de Borde:** Entrega optimizada vía Nginx DMZ y Cloudflare Edge.

## 2. Marco de Gobierno (SGI)
Este proyecto se ejecuta bajo el cumplimiento estricto del **Sistema de Gestión Integrado (SGI v12.0)** de Bitera Digital, alineado con:
* **ISO 9001:2015:** Calidad y estandarización de despliegues.
* **ISO/IEC 27001:2022:** Seguridad de la información y control de accesos (Zero Trust).
* **ISO 22301:2019:** Continuidad del negocio y recuperación ante desastres.
* **Ley 18.331 / GDPR:** Protección de Datos Personales y Soberanía.

Cualquier desviación de los estándares definidos en los documentos maestros (`GOV-01`, `SEC-01`, `ARQ-01`) constituye una No Conformidad.

## 3. Arquitectura Técnica
El servicio corre sobre una infraestructura virtualizada de alta densidad:

| Capa | Tecnología / Activo | Función |
| :--- | :--- | :--- |
| **Borde Global** | Cloudflare Enterprise | WAF, DDoS Protection, Ofuscación de IP. |
| **Perímetro** | pfSense (`vm-pfsense-01`) | Segmentación de VLANs, IDS/IPS Suricata. |
| **Entrega Web** | Nginx DMZ (`vm-nginx-dmz-01`) | Terminación SSL (TLS 1.3), Routing Estático. |
| **Frontend** | HTML5 + CSS3 (Vanilla) | Sitios estáticos ligeros (<500KB), sin frameworks JS. |
| **Identidad** | FreeIPA (`vm-freeipa-01`) | Control de acceso administrativo (Kerberos/LDAP). |

## 4. Estructura del Repositorio
Este repositorio actúa como la Fuente Única de Verdad (SSOT) para el código y la documentación operativa del producto.

* `/docs`: Documentación normativa, procedimientos (SOPs) y definiciones de producto.
* `/src`: Código fuente de las plantillas maestras (HTML/CSS).
* `/config`: Archivos de configuración de referencia para Nginx y CI/CD.

---
**Propiedad de Bitera Digital**
*Mantenedor Principal: Zelmar Velazquez (CEO & Lead Architect)*
*Estado: En Desarrollo (Fase MVP)*
