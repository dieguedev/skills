---
name: to-tickets
description: Break a plan, spec, or the current conversation into a set of tracer-bullet tickets, each declaring its blocking edges.
disable-model-invocation: true
---

# To Tickets

Break a plan, spec, or conversation into a set of **tickets**: tracer-bullet vertical slices, each declaring the tickets that **block** it.

The issue tracker should be provided to you by the user.

## Process

### 1. Gather context

Work from whatever is already in the conversation context. If the user passes a reference (a spec path, an issue number or URL) as an argument, fetch it and read its full body and comments.

### 2. Explore the codebase (OPTIONAL)

If you have not already explored the codebase, do so to understand the current state of the code. Ticket titles and descriptions should use the project's domain glossary vocabulary, and respect ADRs in the area you're touching.

Look for opportunities to prefactor the code to make the implementation easier. "Make the change easy, then make the easy change."

### 3. Draft vertical slices

Break the work into **tracer bullet** tickets.

<vertical-slice-rules>

- Each slice cuts a narrow but COMPLETE path through every layer (schema, API, UI, tests). Vertical, NOT a horizontal slice of one layer
- A completed slice is demoable or verifiable on its own
- Each slice is sized to fit in a single fresh context window
- Any prefactoring should be done first

</vertical-slice-rules>

Give each ticket its **blocking edges**: the other tickets that must complete before it can start. A ticket with no blockers can start immediately.

**Wide refactors are the exception to vertical slicing.** A **wide refactor** is one mechanical change (rename a column, retype a shared symbol) whose **blast radius** fans across the whole codebase, so a single edit breaks thousands of call sites at once and no vertical slice can land green. Don't force it into a tracer bullet; sequence it as **expand–contract**. First expand: add the new form beside the old so nothing breaks. Then migrate the call sites over in batches sized by blast radius (per package, per directory), each batch its own ticket blocked by the expand, keeping CI green batch to batch because the old form still exists. Finally contract: delete the old form once no caller remains, in a ticket blocked by every migrate batch. When even the batches can't stay green alone, keep the sequence but let them share an integration branch that all block a final "integracion" ticket; green is promised only there.

### 4. Quiz the user

Present the proposed breakdown as a numbered list. For each ticket, show:

- **Título**: Nombre descriptivo corto.
- **Bloqueado por**: Qué otros tickets (si es que hay alguno) tiene que completar primero.
- **¿Qué entrega?**: El comportamiento end-to-end que este ticket entrega.

Ask the user:

- ¿La granularidad te parece adecuada? (Tickets demasiado grandes / Tickets demasiado pequeños)
- ¿Las dependencias son correctas? ¿Cada ticket depende solo de los tickets que realmente lo bloquean?
- ¿Habría que fusionar o dividir más algún ticket?

Iterate until the user approves the breakdown.

### 5. Publish the tickets to the configured tracker

Publish the approved tickets. **How** depends on the tracker the user provided. Publish one issue per ticket in dependency order (blockers first) so each ticket's blocking edges can reference real identifiers. Use the platform's native blocking relationship where it has one; otherwise set each ticket's "Blocked by" to the blocking issues, if the native blocking relationship exists, don't add it to the issue. If the source was an existing issue, make each ticket its sub-issue (tracker doc's operation).

Work the **frontier**: any ticket whose blockers are all done. For a purely linear chain that means top to bottom.

Do NOT close or modify any parent issue.

<issue-template>

**COMO** <actor>
**QUIERO** <feature>
**PARA** <benefit>

## ¿Qué construye?

El comportamiento end-to-end que este ticket resuelve y hace funcionar. Redactar desde la perspectiva del usuario, no como una implementación capa por capa.

## Reglas y ejemplos

Seguimos el método del example mapping. Añadiremos reglas según hayamos determinado.

Ejemplo del formato:

**R1**: Permitir el cambio de dirección si la pizza todavía no ha sido recogida
**R2**: La nueva dirección debe estar dentro del rango
**R3**: Sólo se aceptan direcciones válidas

**E1R1**: El pedido está esperando a ser recogido
- Pedro pide pizza a domicilio y se equivoca al meter la dirección.
- La pizza está esperando a ser recogida por el repartidor.
- Hace click en "Cambiar dirección de entrega".
- Cambia la dirección corrigiendo la errata.
- Hace submit de los cambios.
=> El sistema acepta los datos.

**E2R1**: El pedido ya ha sido recogido 
- Pedro pide pizza a domicilio y se equivoca al meter la dirección.
- La pizza ya ha sido recogida por el repartidor.
- Hace click en "Cambiar dirección de entrega".
=> Se le muestra un error que le muestra el número de teléfono para llamar al repartidor.

**E3R1**: El pedido ha sido recogido durante el proceso de cambio de dirección
- Pedro pide pizza a domicilio y se equivoca al meter la dirección.
- La pizza está esperando a ser recogida
- Hace click en "Cambiar dirección de entrega" y empieza a cambiar la dirección
- El repartidor recoge la pizza
- Pedro hace submit de los cambios
=> Se rechazan los cambios y se le muestra un mensaje de error.

Este formato ha de ser aplicado para todas las reglas, siguiendo las variantes posibles, happy path y todas las variantes tanto positivas como negativas que pueda haber de esa misma regla dentro del scope de esta tarjeta.

## Bloqueado por

- A reference to each blocking ticket, or "Nada.". ALWAYS omit this section when blockers were set as native edges.

</issue-template>

In either form, avoid specific file paths or code snippets: they go stale fast. Exception: if a prototype produced a snippet that encodes a decision more precisely than prose can (state machine, reducer, schema, type shape), inline it and note briefly that it came from a prototype. Trim to the decision-rich parts, not a working demo, just the important bits.
