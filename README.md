# Archival (v7) ⚡

Agente y skill personalizada para organizar, sintetizar y consolidar flujos de trabajo técnicos y conversaciones en **NotebookLM** de forma estructurada, limpia y sin pérdida de contexto crítico.

---

## Novedades en v7 (Compacidad Sustantiva)

- **Equilibrio de síntesis:** Supera los resúmenes telegráficos ultracompactos. Mantiene un formato conciso pero conserva comandos de terminal, configuraciones, rutas de archivos y el desglose de fallos resueltos.
- **Preservación obligatoria de ejemplos:** Snippets de código clave, bloques de comandos y casos prácticos explicados en la conversación se guardan íntegros dentro de la nota.
- **Telemetría limpia en texto plano:** Eliminación total de cajas de código superfluas y barras ASCII para una integración visual directa.
- **Aprobación de mínima fricción:** Confirmación inmediata respondiendo únicamente `1` o `sí`.

---

## Arquitectura y Nomenclatura Estricta

Para garantizar orden y aislamiento dentro de NotebookLM, la skill opera exclusivamente bajo un perímetro controlado:

* **Cuadernos de destino (`_archi`):**
  - Formato: `[PALABRAS_CLAVE]_archi` (2 a 3 palabras clave en mayúsculas).
  - Ejemplo: `SISTEMAS_ASIR_archi`, `FLUTTER_DEV_archi`.
  - Los cuadernos que no lleven el sufijo `_archi` son estrictamente ignorados y protegidos contra modificaciones.

* **Fuentes y Notas consolidadas (`_archi.md`):**
  - Formato: `[tema_especifico]_archi.md` (3 a 5 palabras clave en minúsculas separadas por guion bajo).
  - Ejemplo: `gemini_timeout_compresion_red_archi.md`.

---

## Uso Rápido

1. En cualquier conversación o resolución técnica que quieras archivar, escribe:
   ```text
   //archival