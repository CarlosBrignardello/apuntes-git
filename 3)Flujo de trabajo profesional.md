# FLUJO DE TRABAJO PROFESIONAL



### FORK - Contribuir a un proyecto

Al hacer un FORK se clona todo el proyecto hacia otro repositorio, en general colaboradores, una vez realizados los cambios desde GitHub es posible hacer un Pull Request que como se menciono anteriormente se aplicara al ser aprobado.



Al clonar el proyecto como colaborador se debe ir actualizando, sin embargo no se tiene acceso directo para hacer un pull. Para ello existe un procedimiento:



```bash
git remote add upstream *URL* # Generamos otra fuente para hacer pull
git pull upstream master
git commit -am "Fusión"
git push origin master
```



### Git Rebase



En el caso de crear una rama denominada bugfix en la que realizamos varios cambios y posteriormente buscamos fusionarla con la rama master mediante un merge. Sin embargo existen ocasiones en las que se persigue fusionar tambien la historia de los cambios de bugfix y desaparecer la rama bugfix.



**Rebase:** Tomar una rama completa e integrarla a la historia de master. Solo se usa en repositorios locales pues reescribe la historia del repositorio, puede llegar a ser una mala practica pues es usada solo para solucionar pequeños errores.



Primero se debe hacer rebase donde existieron los cambios que queremos modificar y posteriormente a la rama donde se desea que queden los cambios. Quedara finalmente indicada la existencia de la rama bugfix, para solucionarlo podemos simplemente eliminarla.

```bash
git commit -am "Cambio master 1"
git branch bugfix
git checkout bugfix
git commit -am "cambio bugfix 1"
git commit -am "cambio bugfix 2"
git checkout master
git commit -am "cambio master 2"
git checkout bugfix
git rebase master
git checkout master
git rebase experimento

git branch -D bugfix # Eliminamos la rama
```



### Git Stash



Con `git stash` podemos restaurar los cambios recientemente realizados y además guardarlos en memoria.



**Listar cambios guardados:**

* `git stash list`



Si ahora por ejemplo pasáramos a otra rama y queremos poner los cambios que guardamos en stash lo podemos hacer con:

* `git stash pop`



Si los cambios realizados no son los deseados simplemente presionamos `Ctrl + Z` .



**Crear una rama con los cambios guardados en temporal:**

* `git stash branch *NOMBRE_RAMA*`



**Borrar cambios guardados en temporal:**

* `git stash drop`



### Git Clean



En ocasiones podemos por error crear un montón de archivos que no necesitamos en el proyecto y que solo ocupan espacio extra.



**Ver archivos que probablemente fueron añadidos por error:**

* `git status`



**Ver archivos que serán borrados:**

* `git clean --dry-run`



**Nota:** Los archivos dentro de nuevas carpetas tienen problemas para ser rastreados con este sistema.



**Borrar definitivamente los archivos:**

* `git clean -f`



### Git cherry-pick



**Permite agregar cambios previos a la historia de una rama:**

* `git cherry-pick *HASH*`



**Nota:** debemos estar en la rama en que buscamos que la historia sea añadida.



### COMANDOS PARA CASO DE EMERGENCIA



**Añadir nuevos cambios a un commit previo:**

* `git commit --amend`



**Encontrar cambios eliminados:**

* `git reflog`

**En caso de cometer un error masivo, con ramas, archivos, etc, nos devuelve una posición previa:**

* `git reset --HARD *HASH*`



**Buscar palabras en los archivos y commits:**

* `git grep *PALABRA*`
* `git grep -n *PALABRA*` # Buscar línea.
* `git grep -c *PALABRA*` # Buscar cantidad de veces.

* `git log -S "PALABRA"` # Buscar palabras en commits.



### COMANDOS Y RECURSOS COLABORATIVOS



Ver cantidad de commits realizados por los miembros del equipo:

* `git shortlog` # Muestra los commits del equipo
* `git shortlog -sn` # Muestra los commits resumidos
* `git shortlog -sn --all` # Muestra TODOS los commits resumidos
* `git shortlog -sn --all --no-merges` # Muestra todos los commits a exepción de los merges

* **Crear ALIAS:**
  * `git config --global alias.stats "git shortlog -sn --all --no-merges"`



**Ver modificaciones por usuario:**

* `git blame *ARCHIVO*`
* `git blame *ARCHIVO* -LX,Y`



**Ver ramas remotas:**

* `git branch -r`
* `git branch -a` # Ver TODAS



**Recomendación probar y aprender Travis, Jenkins y GitLab.**

