# 4. Alcance del MVP y criterios de aceptación

[← Volver al índice](../README.md)

> **Este documento es la fuente única de verdad para decisiones de producto.** Cualquier funcionalidad no listada aquí se considera *deseable* y solo se aborda si existe holgura durante el período final de desarrollo.

## 4.1. Alcance obligatorio garantizado (MVP Core)

| Componente | Especificaciones funcionales y técnicas comprometidas |
|---|---|
| **Usuarios y sesión** | Registro, inicio y cierre de sesión seguros. Perfil básico con estado de progresión. Uno o varios avatares guardados por usuario. |
| **Pase de Batalla** | Progresión por temporadas y niveles de XP con carril gratuito y premium. Reclamo de recompensas que desbloquean activos exclusivos en el editor. |
| **Catálogo de activos** | 7 categorías 2D modulares: cuerpo/base (con parámetro de tono de piel), rostro, peinado, ropa superior, ropa inferior, calzado y accesorios. Metadatos (id, nombre, categoría, spritesheet/capa, etiquetas, estado). Filtros por categoría y búsqueda simple. |
| **Editor de avatar** | Selección de piezas con vista previa en tiempo real (*Z-Index*). Tinte RGB y escala. Controles de Guardar y Cargar. Validación de ranuras (no dos sombreros ni dos peinados). Reglas de compatibilidad básicas (por ejemplo, ciertos lentes excluyen cierto peinado). |
| **Persistencia y versionado** | Configuración en JSON con referencias a IDs de activos y parámetros. Reconstrucción idéntica al cargar. Versionado simple: restauración de la última versión guardada. |
| **Visor en acción** | Carga de los avatares propios del usuario autenticado por ID, con animación *idle* en bucle (efecto global sobre el avatar). Botón de retorno al editor. Exportación de imagen cuadrada (PNG) para foto de perfil. |
| **Administración mínima** | CRUD de activos, categorías y reglas de compatibilidad. Gestión básica de temporadas y recompensas del Pase de Batalla. Activar/desactivar activos sin romper avatares guardados (*fallback* automático). |

## 4.2. Fuera de alcance (explícitamente NO incluido en el MVP)

| Funcionalidad | Motivo de exclusión |
|---|---|
| Procesamiento real de pagos / pasarela | El carril premium se simula mediante un *flag* administrativo, sin pasarela real. |
| Multijugador, chat o interacción social en tiempo real | No forman parte del objeto del subsistema. |
| App móvil nativa (iOS/Android) | El cliente es web responsive; una app nativa es un proyecto separado. |
| Motor 3D, física de telas o ropa deformable | Se descarta por costo técnico y de arte; el enfoque es 2D por capas. |
| Mundo abierto, niveles, enemigos o jugabilidad | El subsistema no es un juego; es una capa de identidad y progresión. |
| Galería pública de avatares | Se difiere a funcionalidades deseables. |
| Analítica avanzada o recomendador | Se difiere; solo se contemplan estadísticas simples como deseable. |

## 4.3. Módulos de valor agregado (deseables — hoja de ruta de mejora)

- Galería pública o función de compartir avatar mediante enlace o código único.
- Duplicar avatar y modo «Comparar Avatares» en pantalla dividida.
- Etiquetas múltiples y búsqueda avanzada.
- Captura de pantalla instantánea desde el visor.
- Panel de analítica con estadísticas simples (activos más utilizados).
- Animación *idle* por capa individual (mejora del efecto global del MVP).

## 4.4. Criterios de aceptación comercial (protocolo de entrega)

1. Un usuario crea un avatar, lo guarda y al recargarlo se visualiza **idéntico**.
2. El sistema **impide asignar dos ítems en la misma ranura**.
3. El sistema **impide equipar una combinación marcada como incompatible**.
4. El visor **carga un avatar propio por ID y lo muestra con animación 2D *idle* en bucle**.
5. Se **exporta correctamente una imagen cuadrada** del avatar para perfil.
6. El administrador **desactiva un activo y el sistema no se rompe**; muestra un *fallback* predeterminado.
7. La configuración del avatar **se puede inspeccionar en formato JSON**.
8. Un usuario avanza de nivel en el **Pase de Batalla**, reclama un activo cosmético y puede equiparlo en su avatar.
