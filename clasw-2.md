**git blame ____** - muestra quién escribió que línea de código en otras palabras quien es culpable de una línea de código en particular.

**Comparar una versión con otra**: 

* `git diff --stat HASH`

**Comparar códigos anteriores**:

* `git log -p`

**Moverse al pasado**:

* `git checkout HASH`

**Revertir un commit**: Para revertir varios commits solo ejecuta múltiples veces el comando *git revert* con el parámetro -*n* y Git agregara al staging todos los cambios y esperará que tú hagas el commit.

* `git revert -n HEAD`

**Hacer un reset**: El reset permite reiniciar a un commit en especifico.

* `git reset 6c77676 --hard`

**Hacer un reset a un archivo**:

* `git reset <commit hash> <filename> --hard`