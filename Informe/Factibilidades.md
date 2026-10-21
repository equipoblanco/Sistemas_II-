# 3. Estudio de factibilidad

## 3.1. Factibilidad operativa

La solución está diseñada para integrarse al portal del cliente sin exigir cambios profundos en su operación actual.

- **Integración transparente.** El subsistema se entrega documentado con contratos **OpenAPI (Swagger)**, de modo que el equipo del cliente pueda conectarlo con el portal principal mediante servicios REST.
- **Autonomía de gestión.** El personal del cliente podrá subir activos, crear reglas de exclusión, lanzar temporadas del Pase y desactivar ítems antiguos desde una interfaz gráfica (backoffice), sin tocar código ni interrumpir el servicio.
- **Continuidad del servicio.** El protocolo de *fallback* garantiza que, al desactivar un activo, los avatares que lo tuvieran equipado se sustituyan automáticamente por una pieza predeterminada, evitando errores de renderizado y datos corruptos.
- **Bajo requerimiento de infraestructura.** Al ser una aplicación web con cliente liviano (Canvas), no se requiere hardware especializado en el lado del usuario; basta con un navegador moderno.

## 3.2. Factibilidad técnica

La solución se construye sobre tecnologías empresariales consolidadas, lo que garantiza escalabilidad, mantenibilidad e integración.

### 3.2.1. Stack tecnológico

| Capa | Tecnología | Justificación |
|---|---|---|
| Backend | Java 21 + Spring Boot 3.x | Servicios REST, seguridad con JWT y control transaccional (ACID), indispensable para validar incompatibilidades, evitar reclamos duplicados de XP y gestionar el versionado JSON. |
| Frontend | TypeScript + React + Konva.js | Tipado estático para validar las 7 ranuras en el cliente, reactividad en el editor y soporte de Canvas para la composición por capas y la exportación PNG. |
| Base de datos | PostgreSQL 16 | Integridad relacional (usuarios, catálogo, reglas, temporadas) y almacenamiento JSONB para las configuraciones y versiones de los avatares. |
| Despliegue | Railway/Render (backend), Vercel (frontend), Supabase/Neon (base de datos) | Infraestructura cloud de bajo costo, con CI/CD y respaldos administrados. |

### 3.2.2. Cumplimiento estricto del stack exigido

| Capa | Requisito | Implementación | Estado |
|---|---|---|---|
| Backend | Java + Spring Boot | Java 21 + Spring Boot 3.x | Cumplido |
| Frontend | TypeScript (Angular / React / Vue) | TypeScript + React | Cumplido |
| Base de datos | MySQL o PostgreSQL | PostgreSQL 16 | Cumplido |

**Konva.js** es una librería de renderizado 2D sobre HTML5 Canvas, no un framework. Se integra con React mediante `react-konva` y cuenta con equivalentes para Angular (`ng2-konva`) y Vue (`vue-konva`). Por tanto, el frontend sigue siendo TypeScript + framework permitido, y Konva solo resuelve la composición por capas y la exportación PNG. Como plan de respaldo, el motor gráfico puede implementarse con la API nativa de `Canvas` de HTML5, con mayor costo de desarrollo pero mismo resultado funcional.

**PostgreSQL sobre MySQL:** se elige PostgreSQL por el soporte nativo de JSONB, que permite indexar y consultar configuraciones de avatar de forma eficiente. La decisión es reversible a MySQL 8 (tipo `JSON`) sin cambios arquitectónicos.

### 3.2.3. Aceleración con asistentes de IA

El equipo integra asistentes de código (Codex, Google Gemini y Claude Code) en el flujo de desarrollo para automatizar pruebas unitarias, generar esquemas SQL y optimizar algoritmos de validación. Su uso es una decisión interna de productividad y no forma parte del producto entregado.

### 3.2.4. Riesgo técnico controlado

El único componente con curva de aprendizaje es la composición por capas en Canvas. Para reducirlo, el equipo ejecutará un **technical spike** (un pico técnico para resolver una tecnología) de aproximado una semana: renderizar una pieza por cada una de las 7 categorías con Konva y exportar un PNG cuadrado. Si el spike falla, se activa el plan de respaldo con Canvas nativo, sin afectar el cronograma.

## 3.3. Factibilidad económica

El presupuesto cubre los **5 meses de ejecución (octubre-febrero)** y se divide en (A) costos operativos de infraestructura e IA (**OPEX**) y (B) honorarios profesionales de ingeniería.

### A. Costos operativos (OPEX)

| Rubro | Justificación | Costo unitario (USD) | Cantidad / tiempo | Total (USD) |
|---|---|---|---|---|
| Licencias de IA de ingeniería | Aceleración de código, motor de reglas y pruebas. 3 desarrolladores × $20/mes. | $60,00/mes | 5 meses | $300,00 |
| Herramientas gráficas / IA de arte | Generación asistida y vectorización de piezas de las 7 categorías y recompensas del Pase. | $30,00/mes | 3 meses | $90,00 |
| Servidor cloud backend | Instancia para la API Spring Boot (2 vCPU, 4 GB RAM) con CI/CD. | $20,00/mes | 5 meses | $100,00 |
| Base de datos administrada | PostgreSQL con respaldos diarios, cifrado y soporte JSONB. | $15,00/mes | 5 meses | $75,00 |
| CDN y hosting frontend | Distribución de capas gráficas, almacenamiento de imágenes exportadas y despliegue web. | $12,00/mes | 5 meses | $60,00 |
| Dominio, DNS y SSL | Registro anual y certificados HTTPS. | $15,00/año | 1 año | $15,00 |
| Conectividad y servicios del equipo | Telecomunicaciones y energía de las 3 estaciones de trabajo. | $30,00/mes | 5 meses | $150,00 |
| Fondo de contingencia técnica | Reserva del 10 % sobre costos directos ($790) para picos de tráfico o tokens adicionales. | 10 % | Única | $79,00 |
| **Subtotal OPEX** | **Promedio: ~$173,80 USD/mes (~$57,93 por desarrollador).** | — | 5 meses | **$869,00** |

### B. Honorarios profesionales y precio de venta

| Concepto | Detalle del cálculo | Monto (USD) | Proporción |
|---|---|---|---|
| Honorarios de desarrollo | 3 desarrolladores × 30 h/mes × 5 meses = 450 horas a $12,22 USD/hora (≈ $366,67/mes por desarrollador). | $5.500,00 | 86,36 % |
| **Precio total de venta (llave en mano)** | **Inversión total por desarrollo, despliegue y garantía del MVP (5 meses).** | **$6.369,00** | **100,00 %** |

### C. Retorno de inversión para el cliente

1. **Potencial de monetización directa:** el carril premium del Pase de Batalla y el catálogo de activos 2D generan ingresos recurrentes por microtransacciones y suscripciones de temporada, con potencial de recuperar la inversión en los primeros trimestres de operación, sujeto a la base de usuarios del cliente.
2. **Ahorro por uso de asistentes de IA:** el equipo estima una reducción interna de horas de codificación y depuración. Esta cifra es una **estimación del equipo** y no constituye una garantía contractual. El compromiso verificable es el precio de venta de **$6.369 USD**.

## 3.4. Factibilidad de tiempo (complemento)

Aunque la cátedra solicita las factibilidades operativa, técnica y económica, se incluye el cronograma por ser condición indispensable del MVP.

La ejecución se distribuye entre **4 desarrolladores** (Especialista Backend/BD, Especialista Frontend/Editor y Especialistas Full-Stack/QA) en un lapso estimado de **20 semanas**.

| Mes / Fase | Semanas | Entregables comprometidos |
|---|---|---|
| **Noviembre** — Arquitectura y base de datos | 01 – 04 | DER en PostgreSQL, contratos de API REST, proyecto Spring Boot base, estructura del JSON y plantillas gráficas con puntos de anclaje de las 7 categorías. |
| **Diciembre** — Usuarios, catálogo y backoffice | 05 – 08 | Registro, sesión (JWT) y perfil multi-avatar. API del catálogo (7 categorías, estados, filtros y búsqueda). CRUD administrativo y motor de *fallback*. |
| **Enero** — Motores de reglas y Pase de Batalla | 09 – 12 | Validador de ranuras y motor de reglas de compatibilidad. Motor del Pase (niveles, XP, carril Free/Premium y reclamo de recompensas). |
| **Febrero** — Editor, versionado y perfil | 13 – 16 | Editor en TypeScript (capas Z-Index, tinte y escala, guardar/cargar, versionado e inspector JSON). Módulo de perfil con exportación PNG 1:1 e interfaz del Pase. |
| **Marzo** — QA, aceptación y entrega | 17 – 20 | Pruebas unitarias y de integración, validación de los criterios de aceptación y puesta en producción. Funciones deseables solo si existe holgura. |

**Nota de riesgo:** 20 semanas con 3 estudiantes que cursan otras materias exige disciplina sostenida. Por ello se declara un **alcance recortable** (ver documento de alcances del MVP) y se congela el catálogo de activos a fines de enero.
