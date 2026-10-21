 # Subsistema de Pase de Batalla y Personalización de Avatares 2D Modulares

## Descripción

El presente repositorio tiene como propósito abargar todos los archivos e informaciones acerca de un subsistema empresarial, que se integra a una plataforma de videojuegos en línea existente para habilitar:

- Un **Pase de Batalla** con progresión por niveles (carril gratuito y premium) y desbloqueo de activos cosméticos.
- Un **Editor de Avatares 2D** modulares por capas con tintes dinámicos y validación de compatibilidad.
- Un **Visor interactivo** con animación *idle* y exportación de imagen cuadrada 1:1 para perfil.
- Una **Consola de Administración** (backoffice) para gestionar catálogo, reglas de compatibilidad y temporadas.

El avatar se persiste como un **documento JSON inspeccionable** con referencias a IDs de activos y parámetros, lo que garantiza reconstrucción idéntica entre dispositivos y continuidad del servicio ante la desactivación de activos (*fallback*).

## Stack objetivo

| Capa | Tecnología |
|---|---|
| Backend | Java 21 · Spring Boot 3.x · Spring Security + JWT |
| Base de datos | PostgreSQL 16 (JSONB para configuraciones de avatar) |
| Frontend | TypeScript · React · Konva.js (renderizado por capas) |
| Despliegue | Railway / Render (backend) · Vercel (frontend) · Supabase / Neon (BD) |

## Documentación del proyecto

| # | Documento | Contenido |
|---|---|---|
| 01 | [Planteamiento del problema](Informe/Planteamiento.md) | Contexto, diagnóstico y formulación |
| 02 | [Propuesta y Objetivos](Informe/Propuesta-de-Sistema.md) | Arquitectura, módulos del producto y objetivos para el desarrollo del sistema|
| 03 | [Alcance del MVP](docs/04-alcance-mvp.md) | MVP, fuera de alcance y criterios de aceptación |
| 04 | [Benchmarking y arquitectura](docs/05-benchmarking-arquitectura.md) | Comparación de alternativas y motor 2D |
| 05 | [Factibilidades](docs/06-factibilidades.md) | Técnica, operativa y de tiempo |
| 06 | [Presupuesto](docs/07-presupuesto.md) | OPEX, honorarios y precio de venta |
| 07 | [Riesgos](docs/08-riesgos.md) | Análisis y mitigación |
| 08 | [Conclusiones](docs/09-conclusiones.md) | Dictamen de viabilidad |

## Estado del proyecto

**MVP congelado con un plazo máximo a una fecha aproximado a finales de Marzo 2027 (fechas exactas a definir)** Cualquier función fuera del [alcance del MVP](docs/04-alcance-mvp.md) se considera *deseable* y solo se aborda si existe holgura durante el mes 5.

## Cómo navegar en este repositorio

Cada documento en `Informe/` es autocontenido y referencia a otros cuando aplica. La sección de **Alcance del MVP** es la fuente de verdad para decisiones de producto; la sección de **Riesgos** documenta el *alcance recortable* en caso de desviación del cronograma.
