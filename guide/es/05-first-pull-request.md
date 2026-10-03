# 5. Tu primer pull request, paso a paso

Este es el flujo de trabajo completo, desde hacer fork hasta abrir un pull request. Reemplaza `OWNER/REPO` con el proyecto y `your-username` con tu nombre de usuario de GitHub.

## 1. Haz fork y clona el repositorio

Un **fork** es tu propia copia del repositorio en GitHub. Haces push a tu fork y luego pides al proyecto original (llamado **upstream**) que incorpore tus cambios.

```bash
gh repo fork OWNER/REPO --clone
cd REPO
git remote -v
# origin    https://github.com/your-username/REPO.git  (tu fork)
# upstream  https://github.com/OWNER/REPO.git          (el original)
```

Sin GitHub CLI: haz clic en **Fork** en la página del repositorio y luego:

```bash
git clone https://github.com/your-username/REPO.git
cd REPO
git remote add upstream https://github.com/OWNER/REPO.git
```

> ¿Repositorio grande? `git clone --filter=blob:none URL` descarga el contenido de los archivos solo cuando es necesario, lo que es mucho más rápido.

## 2. Crea una rama

Nunca trabajes en la rama predeterminada de tu fork. Comienza cada cambio desde el código más reciente de upstream:

```bash
git fetch upstream
git switch -c fix-empty-username upstream/main   # usa el nombre de la rama predeterminada del proyecto
```

Nombra las ramas según el cambio, como `fix-empty-username` o `docs-install-windows`.

## 3. Compílalo y ejecuta las pruebas antes de cambiar nada

Sigue el `CONTRIBUTING.md` o `DEVELOPMENT.md` del proyecto. Las [guías rápidas por lenguaje](../languages/README.md) muestran los comandos habituales. Ejecuta primero las pruebas con el código sin modificar:

* Si pasan, tienes una línea base funcional.
* Si algunas ya fallan, anota cuáles. Esos fallos no son tuyos y deberías mencionarlos en tu PR si son relevantes.

## 4. Reproduce el problema

Antes de solucionarlo, demuestra que el error existe en tu máquina utilizando los pasos del issue. Anota qué ocurre y qué debería ocurrir en su lugar. Si no puedes reproducirlo, dilo en el issue (indicando tu versión y entorno) en lugar de adivinar una solución.

## 5. Escribe una prueba que falle

Encuentra el archivo de pruebas correspondiente al código que estás modificando y añade una prueba que muestre el error. Ejecútala y observa cómo falla. Esto te indica a ti y al revisor que tu prueba realmente cubre el error.

No todos los cambios necesitan una prueba (por ejemplo, las correcciones de documentación), pero casi todas las correcciones de errores sí. Muchos proyectos no aceptarán una corrección sin una prueba.

## 6. Haz el cambio más pequeño que lo solucione

* Cambia únicamente lo que necesita el issue. No hagas refactorizaciones, cambios de nombre ni reformateos de código no relacionados: hacen que tu pull request sea más difícil de revisar.
* Sigue el estilo del código que te rodea, incluso si tú lo escribirías de otra manera.
* Vuelve a ejecutar la prueba del paso 5. Ahora debería pasar.

## 7. Ejecuta todas las comprobaciones localmente

Ejecuta las mismas comprobaciones que ejecuta el CI del proyecto, al menos para la parte que modificaste:

* el conjunto de pruebas (o la parte relevante)
* el formateador (por ejemplo `prettier`, `black`/`ruff format`, `cargo fmt`, `gofmt`)
* el linter (por ejemplo `eslint`, `ruff`, `clippy`, `go vet`)
* la comprobación de tipos si el proyecto la utiliza (`tsc`, `mypy`)

Algunos proyectos también requieren una entrada en el registro de cambios o un archivo de "changeset". La guía de contribución lo indicará.

## 8. Haz commit

```bash
git add path/to/changed/files
git commit
```

Escribe un mensaje claro. Sigue la convención del proyecto (consulta `git log --oneline -20`). Un formato habitual es:

```text
parser: handle empty username in login prompt

An empty username made the prompt loop forever because validation
rejected it without telling the user. Show the validation error and
ask again instead.

Fixes #1234
```

* Primera línea: resumen breve, a menudo con el área o con un tipo de [Conventional Commits](https://www.conventionalcommits.org) como `fix:` o `docs:`.
* Cuerpo: qué estaba mal y por qué este cambio lo soluciona.
* `Fixes #1234` cierra el issue automáticamente cuando se fusiona el PR.
* Si el proyecto requiere la firma DCO, utiliza `git commit -s` (consulta el capítulo 6).

## 9. Haz push y abre el pull request

```bash
git push -u origin fix-empty-username
gh pr create --repo OWNER/REPO --fill   # o abre en tu navegador el enlace que se muestra
```

Completa la plantilla de pull request del proyecto si existe. El capítulo 7 explica cómo debe ser una buena descripción. En resumen: qué estaba mal, qué cambiaste, cómo lo probaste y qué issue soluciona.

## 10. Mantén tu rama actualizada

Si la rama upstream cambia antes de que tu PR se fusione y aparecen conflictos, actualiza tu rama:

```bash
git fetch upstream
git rebase upstream/main
# resuelve cualquier conflicto y luego: git add <files> && git rebase --continue
git push --force-with-lease
```

`--force-with-lease` es la forma segura de actualizar una rama que has reescrito; se niega a sobrescribir commits que no tienes localmente. Algunos proyectos prefieren fusionar `upstream/main` en tu rama en lugar de hacer rebase; sigue su guía.

## Lista de comprobación

* [ ] Rama creada a partir de la rama predeterminada de upstream más reciente.
* [ ] Las pruebas pasaron antes de mi cambio (o anoté los fallos existentes).
* [ ] Reproduje el error y escribí una prueba que fallaba antes de la corrección.
* [ ] El diff contiene únicamente los cambios necesarios para este issue.
* [ ] Las pruebas, el formateador y el linter pasan localmente.
* [ ] El mensaje del commit sigue la convención del proyecto y hace referencia al issue.
* [ ] La plantilla del PR está completada.

Siguiente: [Reglas que debes comprobar antes de empezar](06-rules-before-you-start.md)
