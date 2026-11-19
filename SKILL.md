---
name: archival-v8
description: Analiza, sintetiza y consolida hilos de chat en NotebookLM al invocar //archival. Conserva explicaciones conceptuales profundas, trazabilidad temporal (created_at/updated_at), frontmatter YAML listo para Obsidian, politica estricta de emojis y brevedad en titulos, modo delta sin perdida de informacion, detector de saturacion y extraccion de acciones y wikilinks.
---

# Archival v8: Organizador y Consolidador de Conocimiento (NotebookLM + Obsidian Ready)

Skill diseñada para procesar conversaciones, estructurar explicaciones conceptuales y detalles tecnicos sin recortar profundidad educativa, y consolidar notas continuas dentro de NotebookLM bajo aislamiento `_archi`, generando documentos Markdown con metadatos YAML compatibles con sincronizacion hacia Obsidian.

## Disparador Principal

- Comando explicito: `//archival`
- Peticiones del usuario para archivar, resumir o consolidar la conversacion actual en NotebookLM.

## Criterio de Sintesis y Nivel de Detalle (Profundidad Conceptual + Rigor Tecnico)

El objetivo NO es recortar las explicaciones ni reducir el chat a una lista telegrafica. La nota debe funcionar como un **documento de estudio y referencia completo** que conserve tanto la teoria como la practica:

1. **Conservar Explicaciones Conceptuales y Razonamiento:** Mantener intactas las explicaciones del *por que* y el *como* funciona cada concepto, arquitectura, mecanismo o decision expuesta en el chat. No comprimir parrafos explicativos en frases sueltas cuando el desarrollo aporta claridad o contexto de aprendizaje.
2. **Retener Detalles Tecnicos y Contextuales:** Conservar comandos exactos, rutas, nombres de archivos, errores resueltos y configuraciones clave tratadas en el chat.
3. **Preservar Ejemplos, Analogias y Fragmentos Representativos:** Si en el chat se explico un concepto mediante codigo, una analogia crucial o un caso practico, incluirlo completo en la nota.
4. **Filtrado Exclusivo de Ruido Conversacional:** Eliminar unicamente saludos, confirmaciones breves (`1`, `si`, `vale`), repeticiones entre turnos y callejones sin salida ya descartados, conservando toda la sustancia explicativa del hilo.
5. **Modo Delta / Cero Perdida al Fusionar:** Al actualizar una nota existente (`refresh_source_content`), NUNCA reescribir ni resumir destructivamente el contenido previo. Conservar integro el cuerpo anterior e integrar unicamente los bloques nuevos en su seccion correspondiente o bajo un bloque `### Actualizacion [YYYY-MM-DD HH:mm]`.
6. **Detector de Umbral de Saturacion (Split Inteligente):** Si una nota existente supera las ~3.500 palabras o acumula mas de 5 fusiones, advertir antes de fusionar y proponer dividirla en dos notas mas especificas dentro del mismo cuaderno.
7. **Extraccion de Acciones y Conceptos Relacionados:**
   - Si quedaron tareas pendientes o comandos por ejecutar, extraerlos en `## Proximos pasos` usando checkboxes (`- [ ]`).
   - Incluir al final una seccion `## Conceptos relacionados` con enlaces cruzados en formato `[[Nombre de Nota]]` para alimentar el grafo de Obsidian.

## Perimetro de Seguridad y Nomenclatura Estricta

1. **Cuadernos exclusivos (`_archi`):**
   - La skill SOLO interactua con cuadernos cuyo nombre finalice en `_archi`. Cuadernos sin `_archi` son intocables.
   - **Brevedad estricta:** Maximo **2 a 3 palabras clave** en mayusculas + sufijo `_archi` (ej. `AGENTES_IA_archi`, `REDES_CISCO_archi`).
   - **Politica estricta de emojis (SOLO en cuadernos):** Se permite un maximo de **1 emoji al inicio** del titulo del cuaderno *unicamente* si reemplaza una palabra de categoria o aporta contexto visual inmediato para acortar el titulo (ej. `🧠 AGENTES_IA_archi`). Si el texto es claro por si solo, no usar ningun emoji.
   - Evaluacion de renombrado: Si el tema evoluciona, proponer renombrarlo mediante `update_notebook` previa confirmacion.

2. **Documentos y Fuentes (`_archi.md`):**
   - Toda fuente creada DEBE llevar el sufijo `_archi.md`.
   - **Cero emojis absolutos:** Queda terminantemente prohibido usar emojis en nombres de archivos/fuentes (garantiza compatibilidad total con sistemas de archivos y enlaces `[[...]]` de Obsidian).
   - **Brevedad estricta:** Maximo **3 a 4 palabras clave** descriptivas en minusculas unidas por guion bajo, sin contar el sufijo (ej. `sync_notebooklm_obsidian_archi.md`).
   - Solo se fusiona (`refresh_source_content`) contra fuentes `_archi.md` dentro de cuadernos `_archi`.

## Plantilla Obligatoria de Estructura Markdown (Frontmatter YAML)

Todo documento creado o actualizado en NotebookLM debe incluir esta estructura exacta al inicio para garantizar trazabilidad temporal y compatibilidad nativa con Obsidian:

```markdown
---
title: [Titulo limpio de 3-4 palabras]
created_at: [YYYY-MM-DD HH:mm]
updated_at: [YYYY-MM-DD HH:mm]
notebook: [Nombre exacto del cuaderno _archi]
tags: [archival, tema1, tema2]
---

# [Titulo limpio]

[Desarrollo completo con explicaciones conceptuales, ejemplos, comandos y configuraciones]

## Proximos pasos
- [ ] [Accion o tarea pendiente si aplica]

## Conceptos relacionados
- [[Concepto Relacionado 1]]
- [[Concepto Relacionado 2]]

> Historial: Creado el [YYYY-MM-DD HH:mm] | Ultima actualizacion: [YYYY-MM-DD HH:mm]