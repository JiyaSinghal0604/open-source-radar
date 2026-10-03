# 4. Encuentra un issue que puedas completar

Un buen primer issue es pequeño, está claramente descrito, se puede reproducir y no está siendo trabajado por otra persona. Este último punto es donde la mayoría de los principiantes pierde tiempo.

## Dónde buscar

* **El [índice de issues](../issues/README.md) de este repositorio** y el [sitio web](https://tanbirramim.github.io/open-source-radar/): issues abiertos etiquetados para principiantes, ya filtrados para excluir aquellos que tienen una persona asignada o un pull request abierto vinculado.
* **El propio gestor de issues del proyecto**, filtrado por sus etiquetas para principiantes.
* **La búsqueda de GitHub**, por ejemplo:

```text
is:issue is:open no:assignee -linked:pr label:"good first issue" language:python
```

`no:assignee` oculta los issues asignados y `-linked:pr` oculta los issues que ya tienen un pull request asociado. Añade `updated:>2026-06-01` (usa una fecha reciente) para omitir los que estén obsoletos.

## Etiquetas que verás

| Etiqueta                                                      | Normalmente significa                                                                 |
| ------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| `good first issue`, `first-timers-only`, `beginner`, `E-easy` | Los mantenedores creen que un principiante puede hacerlo, normalmente con orientación |
| `help wanted`, `PR welcome`, `up-for-grabs`                   | Los mantenedores quieren que otra persona lo haga; no siempre es pequeño              |
| `bug`, `confirmed`, `has: repro`                              | Un defecto real; `confirmed` significa que un mantenedor lo ha reproducido            |
| `needs-triage`, `needs-info`, `question`                      | No está listo: el problema todavía no se entiende                                     |
| `design`, `rfc`, `discussion`, `blocked`                      | No está listo para un pull request; hay una decisión pendiente                        |

Cada proyecto define sus propias etiquetas. Consulta las descripciones de las etiquetas en la página **Issues → Labels** del proyecto.

## ¿Alguien ya está trabajando en ello?

Antes de escribir una sola línea de código, comprueba todo lo siguiente:

1. **Personas asignadas.** Si alguien está asignado, el issue ya está ocupado.
2. **Pull requests vinculados.** Mira la barra lateral derecha ("Development") y la línea de tiempo en busca de eventos como "linked a pull request" o "mentioned this issue" procedentes de PR. Un PR abierto significa que el issue está ocupado; uno cerrado y no fusionado puede significar que el enfoque fue rechazado, así que lee el motivo.
3. **Comentarios.** Busca frases como "I'd like to work on this" o "working on it". Si la reclamación es reciente (un par de semanas) y la persona no ha desaparecido, elige otro issue.
4. **Busca pull requests abiertos** usando el número del issue o palabras clave del título. No todos los PR vinculan correctamente el issue.

Si una reclamación es antigua y la persona ha dejado de responder, normalmente está bien preguntar educadamente: "Hola @name, ¿sigues trabajando en esto? Si no, estaré encantado de encargarme de ello." Después, espera unos días.

## ¿Puedes completarlo?

Haz una estimación honesta. Un buen primer issue para ti:

* **Tiene un comportamiento esperado claro.** Puedes decir en una frase qué debería ocurrir en su lugar.
* **Se puede reproducir.** El issue contiene pasos, un fragmento de código o un comando que falla. Si no es así, reproducirlo es tu primera tarea, y publicar la reproducción ya es una contribución.
* **Es local.** Puedes imaginar qué archivo o función está involucrado. Busca en el código base el mensaje de error o el nombre de la función mencionados en el issue.
* **No necesita una decisión de diseño.** Si los mantenedores todavía están discutiendo *cómo* debería funcionar, espera.
* **Funciona en tu máquina.** Evita errores exclusivos de Windows si estás en macOS, errores de GPU si no tienes una GPU, y situaciones similares.

## Una forma rápida de calcular el tamaño de un issue

Dedica entre 20 y 30 minutos antes de comprometerte con él:

1. Clona el proyecto y ejecuta su conjunto de pruebas una vez (capítulo 5).
2. Reproduce el error o encuentra el lugar del código correspondiente a la funcionalidad.
3. Encuentra el archivo de pruebas existente para esa parte.

Si completaste los tres pasos, probablemente el issue tenga un tamaño adecuado. Si después de 30 minutos sigues perdido, prueba con otro issue o haz una pregunta específica en el issue (capítulo 7).

## Lista de comprobación

* [ ] No hay ninguna persona asignada, ningún PR abierto vinculado ni ninguna reclamación reciente en los comentarios.
* [ ] Puedo explicar el comportamiento esperado en una sola frase.
* [ ] Reproduje el problema o sé exactamente dónde realizar el cambio.
* [ ] Los mantenedores no siguen debatiendo el enfoque.

Siguiente: [Tu primer pull request, paso a paso](05-first-pull-request.md)
