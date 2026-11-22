---
name: to-spec
description: Convierte la conversación actual en un documento de especificación. No entrevistes al usuario, solo sintetiza lo que ya se ha hablado en esta conversación.
disable-model-invocation: true
---

Esta skill utiliza el contexto de la conversación actual y el conocimiento de la codebase y devuelve un documento de especificación. NO entrevistes al usuario; simplemente sintetiza lo que ya sabes.

## Proceso de síntesis

1. Explora el repositorio para identificar el estado actual de la codebase, si todavía no lo has hecho.

2. Define los seams desde los que vas a testear la feature (por ejemplo: un endpoint, un comando, un componente de UI...). Reutiliza seams que ya existan antes que crear otros nuevos, y elige siempre el más externo posible, es decir, el más cercano al usuario. Si hace falta crear seams nuevos, proponlos también lo más arriba que puedas. Cuantos menos seams haya, mejor; lo ideal es uno solo. Confirma con el usuario que estos seams encajan con lo que espera.

3. Escribe el documento de especificación utilizando la siguiente plantilla:

<plantilla-especificacion>

## Problema

El problema con el que se está encontrando el usuario, desde la perspectiva del usuario.

## Solución

La solución al problema, desde la perspectiva del usuario.

## Comportamientos esperados

Escribe una lista numerada con una frase por cada comportamiento que el usuario espera de la feature.

<ejemplo-comportamiento>
  1. El cliente de la banca online puede ver el saldo de cada una de sus cuentas.
</ejemplo-comportamiento>

Esta lista debe cubrir todos los aspectos de la feature, sin repetir ni dividir comportamientos para alargarla. Tampoco omitas ninguno para acortarla.

## Decisiones de implementación

Una lista de decisiones de implementación que se han tomado. Esto puede incluir:

- Los módulos que se van a crear / modificar.
- Las interfaces de los módulos que van a ser modificados.
- Aclaraciones técnicas del desarrollador.
- Decisiones de arquitectura.
- Cambios de schema.
- Contratos de API.
- Interacciones específicas.

NO incluyas rutas ni bloques de código de archivos específicos. Acaban desactualizados rápidamente, por lo que no son un buen método.

Excepción: si un prototipo ha producido un snippet que representa una decisión de forma más precisa de lo que puede la prosa (máquina de estados, reducer, schema, forma de un tipo), insértalo dentro de la decisión relevante y anota brevemente que proviene de un prototipo. Acótalo a las partes con más peso en la decisión, no una demo funcional, solo lo importante.

## Decisiones de testing

Una lista de decisiones de testing que se han tomado. Incluye:

- Una descripción de lo que hace un buen test (que compruebe solo el comportamiento externo, no detalles de implementación).
- Qué módulos van a ser testados.
- Referencias previas para los tests (por ejemplo, tipos de test similares que ya existen en la codebase).

## Fuera de scope

Una descripción de las cosas que están fuera del scope para esta spec.

## Notas adicionales

Cualquier nota adicional acerca de la feature.

</plantilla-especificacion>
