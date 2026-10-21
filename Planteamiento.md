# 1. Planteamiento del problema

[← Volver al índice](../README.md)

## 1.1. Contexto y diagnóstico

En la industria actual de plataformas digitales de videojuegos, la retención de usuarios y la monetización recurrente dependen del sentido de pertenencia, la identidad digital y los sistemas de progresión continua. La experiencia del sector muestra que los pases de temporada y la personalización cosmética de avatares prolongan el tiempo de permanencia del usuario y generan ingresos sostenidos sin alterar la jugabilidad ni ofrecer ventajas competitivas pagadas.

Sin embargo, la plataforma central del cliente opera con **perfiles planos, basados en fotografías estáticas y sin mecanismos de recompensa**, lo que reduce la frecuencia de visita, limita la expresión individual del usuario y deja sin explotar una fuente de ingresos por microtransacciones.

Resolver esta brecha no consiste en añadir una función aislada: se requiere **integrar a la plataforma existente un subsistema especializado, desacoplado e interoperable**, capaz de transformar perfiles planos en un ecosistema de personalización y fidelización sin comprometer la estabilidad del portal actual.

### Diagnóstico técnico: cinco puntos críticos

1. **Baja retención y ausencia de economía de progresión.** No existe un motor de recompensas por temporadas (*Pase de Batalla*) basado en niveles y puntos de experiencia (XP) que premie la recurrencia con activos cosméticos exclusivos.

2. **Identidad visual estática y sin soporte multi-avatar.** Las fotografías fijas impiden coleccionar, construir y alternar avatares expresivos. Un sistema 2D modular con capas (*Z-Index*) y tintes dinámicos ofrece versatilidad estética sin el peso de motores 3D.

3. **Errores gráficos por colisión de piezas y duplicidad de ranuras.** Sin un motor de validación, el usuario puede superponer ítems de la misma categoría (dos sombreros o dos peinados) o combinar piezas incompatibles (por ejemplo, lentes que cortan un peinado específico).

4. **Riesgo operativo al desactivar activos del catálogo.** Al retirar una prenda, los perfiles que la tienen equipada sufren fallos de renderizado o datos corruptos por falta de un protocolo de sustitución automática (*fallback*).

5. **Falta de persistencia estandarizada y visualización dinámica.** Sin manifiestos serializables (JSON) con control de versiones ni un visor animado (animación *idle* en bucle y exportación cuadrada 1:1), el avatar no se reconstruye de forma idéntica entre dispositivos ni alimenta cabeceras y rankings.

## 1.2. Formulación del problema central

> ¿Cómo diseñar, desarrollar y desplegar en producción un subsistema empresarial bajo arquitectura cliente-servidor (Java Spring Boot, TypeScript y PostgreSQL) que integre un **Motor de Pase de Batalla** con un **Editor de Avatares 2D Modulares por Capas** (con animación *idle* y tintes dinámicos) y un **Visor Interactivo**, garantizando validación de ranuras y compatibilidad, persistencia serializable en JSON con *fallback* administrativo, y la entrega de un MVP 100 % operativo en marzo?

## 1.3. Sistematización del problema

- ¿Qué modelo de progresión (XP, niveles, carril gratuito y premium) fideliza al usuario y desbloquea activos cosméticos?
- ¿Qué técnica de renderizado 2D por capas ofrece alta expresividad con bajo costo computacional?
- ¿Cómo garantizar la validación de ranuras y la compatibilidad entre piezas?
- ¿Cómo asegurar la persistencia fiel de los avatares y la continuidad del servicio ante la desactivación de activos?
- ¿Es el proyecto viable técnica, operativa, temporal y económicamente en un plazo de cinco meses?

## 1.4. Justificación

El proyecto se justifica:

- **Comercialmente**, por abrir una vía de ingresos recurrentes y mejorar la retención.
- **Técnicamente**, por aplicar tecnologías empresariales consolidadas con una arquitectura desacoplada y de bajo peso en el cliente.
- **Académicamente**, por integrar el ciclo completo de formulación y evaluación de un proyecto de software: diagnóstico, objetivos, alcance, factibilidades y presupuesto.