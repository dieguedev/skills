---
name: to-spec
description: Turn the current conversation into a spec. No interview, just synthesis of what you've already discussed.
disable-model-invocation: true
---

This skill takes the current conversation context and codebase understanding and produces a spec. Do NOT interview the user; just synthesize what you already know.

## Process

1. Explore the repo to understand the current state of the codebase, if you haven't already. Use the project's domain glossary vocabulary throughout the spec, and respect any ADRs in the area you're touching.

2. Sketch out the seams at which you're going to test the feature. Existing seams should be preferred to new ones. Use the highest seam possible. If new seams are needed, propose them at the highest point you can. The fewer seams across the codebase, the better, the ideal number is one.

Check with the user that these seams match their expectations.

3. Write the spec using the template below:

<spec-template>

## Problema

El problema con el que se está encontrando el usuario, desde la perspectiva del usuario.

## Solución

La solución al problema, desde la perspectiva del usuario.

## User Stories

Una lista LARGA y numerada de User Stories. Cada User Story debería estar en el siguiente formato:

1. COMO <actor>, QUIERO <feature>, PARA <benefit>

<user-story-example>
1. COMO cliente de la banca online, QUIERO ver el dinero de mis cuentas, PARA realizar mejores decisiones de gasto.
</user-story-example>

Esta lista de historias de usuario debe ser extremadamente extensiva y cubrir todos los aspectos de la feature.

## Decisiones de implementación

Una lista de decisiones de implementación que se han hecho. Esto puede incluir:

- Los módulos que se van a crear / modificar.
- Las interfaces de los módulos que van a ser modificados.
- Aclaraciones técnicas del desarrollador.
- Decisiones de arquitectura.
- Cambios de schema.
- Contratos de API.
- Interacciones específicas.

NO incluyas rutas ni bloques de código de archivos específicos. Acaban desactualizados rápidamente, por lo que no son un buen método.

Excepción: Si un prototipo ha producido un snippet que representa una decisión de forma más precisa de lo que puede la prosa (máquina de estados, reducer, schema, forma de un tipo), insértalo dentro de la decision relevante y anota brevemente que proviene de un prototipo. Acótalo a las partes con más peso en la decisión, no una demo funcional, sólo lo importante.

## Decisiones de testing

Una lista de decisiones de testing que se han hecho. Incluye:

- Una descripción de lo que hace un buen test (solo comportamiento externo al test, no detalles de implementación).
- Qué módulos van a ser testados.
- Referencias previas para los tests (por ejemplo, tipos de test similares que ya existen en la codebase).

## Fuera de scope

Una descripción de las cosas que están fuera del scope para esta spec.

## Notas adicionales

Cualquier nota adicional acerca de la feature.

</spec-template>
