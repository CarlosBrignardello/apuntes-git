### Comandos para terminal

**Listar archivos**:

* ls

**Moverse entre carpetas**: 

* cd

**Retroceder entre carpetas**:

* cd ..

**Crear una carpeta**:

* mkdir *NOMBRE*

**Crear un archivo**:

* touch *NOMBRE*

**Conocer donde estoy**:

* pwd



### Comandos git

**Iniciar git en un directorio**:

* git init

**Añadir archivos a staging**:

* git add .

**Realizar un commit**:

* git commit -m "MENSAJE"

**Clonar repositorio**:

* git clone *URL | SSH*

**Vincular repositorio remoto**:

* git remote add *NOMBRE* *URL|SSH*

**Obtener actualización**:

* git pull *NOMBRE* master

**Enviar actualización**:

* git push *NOMBRE* master



**Generar un repositorio y actualizarlo mediante git**

1. Creamos un repositorio en github, en mi caso se llama "git-talento-digital".
2. Obtenemos la URL del repositorio, en mi caso "https://github.com/CarlosBrignardello/Git-Talento-Digital.git".
3. Ingresamos a una carpeta donde queremos generar el proyecto, **DEBEN SER ORDENADOS **,  abrimos git en la carpeta dando botón derecho y haciendo clic en la opción "**Git Bash Here**". Iniciamos el repositorio en nuestro equipo con el comando `git init`.
4. Realizamos cambios en nuestro proyecto, una vez hemos avanzado suficiente procedemos a realizar commits de nuestro avance:
   * **Añadimos los archivos a staging:**
     * `git add .`
   * **Realizamos un commit:**
     * `git commit -m "MENSAJE"`
   * Utilizamos `git status` para entender el estado/contexto de git en el momento, si nos aparecen archivos en rojo significa que no hemos añadido los archivos (git add .), si nos aparece en verde significa que nos falta hacer un commit y si aparece en blanco no necesitamos realizar nada.
5. Una vez hecho esto tenemos nuestros cambios guardados en local, para subirlos al repositorio necesitamos generar un vinculo remoto, para ello utilizamos el siguiente comando:
   * `git remote add origin master`
     * origin es el nombre por defecto, puede ser cualquiera y master hace referencia a la rama en la que nos encontramos.
6. Podemos revisar si tenemos nuestra conexión remota bien hecha con:
   * `git remote -v`
7. Luego realizamos un pull request que consiste simplemente en obtener la ultima version del repositorio (Como el repositorio esta vacio no hacemos nada).
   * `git pull origin master`
8. Finalmente enviamos los cambios realizando un push:
   * `git push origin master`



**Hostear un sitio con GitHub Pages**

1. Para hostear un sitio necesitamos generar una nueva rama denominada "gh-pages":
   * `git branch gh-pages`
2. Nos movemos a la rama generada:
   * `git checkout gh-pages`
3. realizamos una actualización al repositorio con la nueva rama:
   * `git push origin gh-pages`
4. Revisamos el sitio hosteado:
   * NOMBRE_USUARIO.github.io/NOMBRE_REPOSITORIO



**CONSEJO**: Lean las advertencias que el programa les arroja cuando hacen add, commit, pull y push.



**Comandos adicionales**



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





**.gitignore**

Para ignorar archivos debes crear un archivo llamado .gitignore que puede poseer la siguiente sintaxis:

```bash
# ignora cualquier archivo llamado "secret.txt"
secret.txt
# ignora cualquier directorio llamado "secrets"
secrets/
# ignora un archivo llamado "hidden.txt" ubicado en la raíz de tu directorio de trabajo
/hidden.txt
# ignora un directorio llamado "node_modules" ubicado en la raíz de tu directorio de trabajo
/node_modules/
# ignora cualquier archivo con extensión .png
*.png
# ignora cualquier archivo o directorio que comienza con "cache", como cache-file-01, cached_assets/, etc.
cache*
# ignora cualquier archivo o directorio que termine con "data", como project_data/, big_file_of_data
*data
```



**Haciendo merg**

La rama master debe estar libre de errores, las ramas **develop** o **production** son las ramas desde las que se trabaja principalmente. Un merge consiste en mezclar el contenido de dos ramas.

* **Generar una rama de desarrollo**: git branch develop
* **Moverse a una rama**: git checkout develop
* **Hacer pull a la rama**: git pull origin develop
* **Nos movemos a la rama final**: git checkout master
* **Hacemos la fusión**: git merge develop



**Concepto de versiones**

**Master**: es una rama en la que no existen errores y es la del producto final.

**Beta**: un poco más avanzada que master, presenta una versión casi lista, que sera probada con ciertos usuarios.

1. **Usuarios entusiastas**:

**QA(Quality assurage)**: Un poco más avanzada, se asegura que los desarrollos de dev funcionen correctamente.

1. **Especialistas tester**:

**Dev**: rama donde trabaja el equipo de desarrollo, repleto de errores y desarrollo experimental

1. **Arquitectos de software**:

**Sales_histories**

1. **Jefe de proyectos**: pueden existir varios, son los que conocen bien la empresa y su operación.

2. **Scrum master**: se encarga de que el equipo de desarrollo este feliz y cumpla sus objetivos, existen cursos de capacitación para esto.

> **Agustin Vilena** promotor de metodologias agiles.

3. **Desarrollador**: son operados mediante el scrum master, se incluyen UI/UX.



**Corregir colisiones**

Eliminamos las líneas especiales y comparamos con que código nos quedamos.