---
name: archival-v7
description: Analiza, sintetiza y consolida hilos de chat en NotebookLM al invocar //archival. Formato limpio integrado con telemetria en texto plano, conservacion sustantiva de ejemplos y confirmacion directa simple (1 o si).
---

# Archival: Organizador y Consolidador de Chats para NotebookLM

Skill diseñada para procesar el contenido de chats sueltos, sintetizar conocimientos clave y consolidar notas continuas dentro de NotebookLM bajo aislamiento `_archi`, con formato de texto plano integrado y aprobacion de minima friccion.

## Disparador Principal

- Comando explicito: `//archival`
- Peticiones del usuario para archivar, resumir o consolidar la conversacion actual en NotebookLM.

## Criterio de Síntesis y Nivel de Detalle (Compacidad Sustantiva)

La síntesis NO debe ser un "mega resumen" telegráfico que mutile el contexto práctico ni tampoco una transcripción literal redundante. Debe seguir una **compacidad sustantiva**:

1. **Retener Detalles Técnicos y Contextuales:**
   - Conservar comandos exactos, rutas, nombres de archivos, errores resueltos y configuraciones clave tratadas en el chat.
2. **Preservar Ejemplos y Fragmentos Representativos:**
   - Si en el chat se explicó un concepto mediante un ejemplo de código, una analogía crucial o un caso de uso práctico, el ejemplo DEBE incluirse en la nota (en un bloque de código o lista clara), nunca omitirse.
3. **Estructura Temática sin Redundancias:**
   - Desglosar por puntos tratados con viñetas explicativas completas, eliminando rodeos conversacionales, pero explicando el *por qué* y el *cómo*, no solo títulos vacíos.

## Perimetro de Seguridad y Nomenclatura Estricta

1. **Cuadernos exclusivos (`_archi`):**
   - La skill SOLO interactua con cuadernos cuyo nombre finalice en `_archi`.
   - Limite estricto: Maximo 2 a 3 palabras clave generales en mayusculas, sin contar el sufijo (e.g. `AUTOMATIZACION_IA_archi`, `REDES_CISCO_archi`).
   - Cuadernos sin `_archi` son intocables.
   - Evaluacion de renombrado: Si el contenido evoluciona, propone renombrarlo usando `update_notebook`, siempre bajo confirmacion previa.

2. **Documentos y Fuentes (`_archi.md`):**
   - Toda fuente creada DEBE llevar el sufijo `_archi.md`.
   - Limite estricto: Maximo 3 a 5 palabras clave descriptivas en minusculas unidas por guion bajo, sin contar el sufijo (e.g. `agentes_ia_autonomos_tiktok_archi.md`).
   - Solo se fusiona (`refresh_source_content`) contra fuentes `_archi.md` dentro de cuadernos `_archi`.

## Formato Visual Integrado (Sin bloques de codigo ni barras ASCII)

Al invocarse con `//archival`, la skill NUNCA debe usar bloques de codigo cercados (`plaintext /`) ni barras de carga ASCII ni pseudo-sintaxis de botones falsos (`[...](query=...)`). Presenta el estado como texto limpio:

⚡ **ARCHIVAL SYSTEM // Consolidacion de notas NotebookLM**

* **Cuaderno objetivo:** `[NOMBRE_CUADERNO]_archi`
* **Archivo destino:** `[nombre_archivo]_archi.md`
* **Accion:** `[CREACION Y CONSOLIDACION / FUSION CON EXISTENTE]`

---

## Flujo de Aprobacion y Confirmacion Minima

- Muestra el diagnostico y la sintesis sustantiva en Markdown.
- Al final, pide confirmacion directa sin botones simulados ni enlaces no funcionales:
  > **¿Deseas consolidar en NotebookLM? Responde simplemente `1` o `sí`.**
- Si el usuario envia `1`, `si`, `adelante` o cualquier afirmacion breve, la skill ejecuta inmediatamente la creacion o actualizacion en NotebookLM y notifica que el chat original ya puede eliminarse.