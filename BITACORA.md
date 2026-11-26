# Bitácora del laboratorio de rescate

## Reto 1. Ver el historial

**Enunciado.** ¿Qué muestra cada comando?

**Respuesta.** `git log` muestra el autor, la fecha y el mensaje de cada commit. `git log --oneline` resume cada commit en una línea. `git log --oneline --graph --all` muestra el historial de todas las ramas con un gráfico que permite ver cómo se conectan.

**Enunciado.** ¿Qué es el código que aparece al inicio de cada commit?

**Respuesta.** Es el identificador del commit. Sirve para localizarlo en el historial.

## Reto 2. Ver qué cambió antes de guardar

**Enunciado.** ¿Por qué el segundo `git diff` no mostró nada?

**Respuesta.** Porque ya había preparado el cambio de `notas.txt` con `git add`. `git diff` muestra los cambios que todavía están sin preparar.

**Enunciado.** ¿Qué muestra `--staged`?

**Respuesta.** `git diff --staged` mostró el cambio de la línea 2 que había preparado para el siguiente commit.

## Reto 3. Borré un archivo por error

**Enunciado.** ¿Qué hace `git restore`?

**Respuesta.** `git restore notas.txt` recuperó mi archivo borrado usando la versión que Git tenía en el área de preparación.

**Enunciado.** ¿Funcionaría si nunca hubieras hecho commit de ese archivo?

**Respuesta.** Si tampoco lo hubiera agregado con `git add`, Git no tendría una copia para recuperarlo. Si ya lo había agregado, podría recuperarlo desde el área de preparación.

## Reto 4. Agregué un archivo que no debía subir

**Enunciado.** ¿Qué diferencia hay entre `git restore` y `git restore --staged`?

**Respuesta.** `git restore` cambia la copia de trabajo. `git restore --staged secreto.env` sacó el archivo del área de preparación y lo dejó en mi carpeta. Agregué `*.env` a `.gitignore` para que Git lo ignore.

## Reto 5. Escribí mal el mensaje del commit

**Enunciado.** ¿Cómo corregiste el mensaje del último commit antes de subirlo?

**Respuesta.** Usé `git commit --amend -m "docs: agrega línea 4 a notas"` para reemplazar el mensaje `cambios`. Revisé el nuevo mensaje con `git log --oneline` antes de subirlo.

## Reto 6. Subí un commit que dañó el proyecto

**Enunciado.** ¿`git revert` borró el commit equivocado o creó uno nuevo?

**Respuesta.** `git revert HEAD` creó un commit nuevo que recuperó las líneas de `notas.txt`. El commit que las borró sigue en el historial.

**Enunciado.** ¿Por qué es la opción segura cuando ya se hizo push?

**Respuesta.** Porque la corrección se agrega al historial que ya compartimos. Los demás pueden descargarla sin perder el historial que tenían.

## Reto 7. Hice un commit antes de tiempo

**Enunciado.** ¿Qué diferencia hay entre `git reset --soft` y `git revert`?

**Respuesta.** `git reset --soft HEAD~1` quitó el último commit de mi rama y dejó el borrador preparado. `git revert` agrega un commit que deshace los cambios de otro.

**Enunciado.** ¿Cuándo se usa cada uno?

**Respuesta.** Uso `git reset --soft` cuando el commit todavía es local y quiero conservar los cambios para completarlos. Uso `git revert` cuando el commit ya se compartió y quiero corregirlo sin cambiar el historial publicado.

## Reto 8. Tengo trabajo a medias y debo cambiar de tarea

**Enunciado.** ¿Para qué sirve `git stash`?

**Respuesta.** `git stash` guardó temporalmente el cambio de `notas.txt`. Así pude cambiar a la rama `fix/urgente` con la carpeta de trabajo limpia.

**Enunciado.** ¿Qué hace `git stash pop`?

**Respuesta.** Al volver a `main`, `git stash pop` recuperó la línea 5 de `notas.txt` y quitó el guardado temporal de la lista.

## Historial antes del commit de cierre

```text
* 13cb81b docs: agrega línea 5 a notas
* e44b320 feat: agrega borrador completo
* a28ce7a Revert "fix: limpia notas"
* 9e4bbf3 fix: limpia notas
* a5ad5f5 docs: agrega línea 4 a notas
* db5620f chore: agrega .gitignore para archivos .env
* d141e34 docs: modifica línea 2 de notas
* d4dd999 feat: agrega notas y bitácora
* e768460 Initial commit
```
