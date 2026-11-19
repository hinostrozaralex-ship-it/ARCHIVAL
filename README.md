# Archival (v8) ⚡

Agente y skill personalizada para organizar, sintetizar y consolidar flujos de trabajo técnicos y conversaciones en **NotebookLM** de forma estructurada, limpia y sin pérdida de contexto crítico, generando documentos Markdown con Frontmatter YAML listos para sincronizarse con bóvedas locales de **Obsidian**.

---

## Novedades en v8 (Trazabilidad y Obsidian Ready)

- **Trazabilidad temporal inmutable:** Cada documento registra automáticamente `created_at` (fijo desde su creación) y `updated_at` (actualizado en cada fusión), junto con un pie de historial legible.
- **Modo Delta (cero pérdida de información):** Al actualizar una fuente existente (`refresh_source_content`), conserva íntegro el contenido previo e integra únicamente los bloques nuevos sin resumir destructivamente.
- **Detector de umbral de saturación (Split inteligente):** Alerta cuando una nota supera ~2.500 palabras o acumula más de 5 fusiones y propone dividirla en dos subtemas específicos dentro del mismo cuaderno.
- **Extracción de acciones y enlaces cruzados:** Genera automáticamente bloques `## Próximos pasos` con tareas verificables (`- [ ]`) y secciones `## Conceptos relacionados` con enlaces `[[wikilinks]]` para alimentar el grafo de conocimiento en Obsidian.
- **Frontmatter YAML nativo:** Estructura metadatos (`title`, `created_at`, `updated_at`, `notebook`, `tags`) directamente en el encabezado del documento para facilitar la sincronización unidireccional hacia bóvedas locales mediante clientes MCP compatibles.

---

## Arquitectura y Nomenclatura Estricta

Para garantizar orden, compatibilidad entre sistemas de archivos y aislamiento dentro de NotebookLM, la skill opera exclusivamente bajo un perímetro controlado:

- **Cuadernos de destino (`_archi`):**
  - Formato: `[EMOJI_OPCIONAL] [PALABRAS_CLAVE]_archi` (máximo 2 a 3 palabras clave en mayúsculas).
  - **Política estricta de emojis:** Se permite un máximo de **1 emoji al inicio** del título del cuaderno *únicamente* si reemplaza una palabra de categoría o aporta contexto visual inmediato para acortar el título (ej. `🧠 AGENTES_IA_archi`). Si el texto es claro por sí solo, no se usa ningún emoji (ej. `REDES_CISCO_archi`).
  - Los cuadernos que no lleven el sufijo `_archi` son estrictamente ignorados y protegidos contra modificaciones.

- **Fuentes y Notas consolidadas (`_archi.md`):**
  - Formato: `[tema_especifico]_archi.md` (máximo 3 a 4 palabras clave descriptivas en minúsculas separadas por guion bajo).
  - **Cero emojis absolutos:** Queda prohibido el uso de emojis en nombres de archivos/fuentes para asegurar compatibilidad total entre sistemas operativos y enlaces `[[...]]` de Obsidian.
  - Ejemplo: `sync_notebooklm_obsidian_archi.md`.

---

## Criterio de Síntesis (Compacidad Sustantiva)

- **Equilibrio de síntesis:** Supera los resúmenes telegráficos ultracompactos. Mantiene un formato conciso pero conserva comandos de terminal, configuraciones, rutas de archivos y el desglose de fallos resueltos.
- **Preservación obligatoria de ejemplos:** Snippets de código clave, bloques de comandos y casos prácticos explicados en la conversación se guardan íntegros dentro de la nota.
- **Telemetría limpia en texto plano:** Eliminación total de cajas de código superfluas y barras ASCII para una integración visual directa.
- **Aprobación de mínima fricción:** Confirmación inmediata respondiendo únicamente `1` o `sí`.

---

## Estructura del Documento Generado

```markdown
---
title: Sync NotebookLM Obsidian
created_at: 2026-11-19 14:15
updated_at: 2026-11-19 14:15
notebook: 🧠 AGENTES_IA_archi
tags: [archival, obsidian, mcp, markdown]
---

# Sync NotebookLM Obsidian

[Cuerpo estructurado con compacidad sustantiva, comandos y ejemplos]

## Próximos pasos
- [ ] Configurar servidor MCP de NotebookLM en el entorno local.

## Conceptos relacionados
- [[Arquitectura MCP]]
- [[Gestion del Conocimiento]]

> Historial: Creado el 2026-11-19 14:15 | Última actualización: 2026-11-19 14:15

## Uso Rápido

1. En cualquier conversación o resolución técnica que quieras archivar, escribe:
   ```text
   //archival