# FLUJO DE TRABAJO PROFESIONAL



### FUSIONAR RAMIFICACIONES



A continuación en la ramificación header se planea agregar una imagen a un repositorio, si lo hacemos no existe ningún problema, sin embargo al momento de realizar cambios se tendrán en cuenta copias de la imagen y esto con el pasar del tiempo se volverá más y más pesado.



**Cambios desde Header en HTML**

```html
<body>
    <div class="container">
        <div class="cabecera">
                <img class="logo" src="./img/dragon.png" />
                NeoCards
                <span class="tagline">La información precisa</span>
        </div>
        <div class="posts">
            <h1>Este es el título atractivo e interesante del post</h1>
            <p>Y este es el parrafo de inicio donde vamos a explicar las cosas increéibles que se pueden hacer con ramas</p>
            <p>Los blogs son la mejor forma de compartir información y tus ideas. Mucho mas que ir a conferencias o salir en Youtube. Excepto si eres un rockstar. Pero estadísticamente no lo eres.... por ahora.</p>
            <p>Suscribete y dale like</p>
        </div>
    </div>

</body>
```



**Cambios en CSS**

```css
body
{
    background: #1e1f24;
    color: #333;
    text-align: center;
    font-family: Arial;
    font-size: 16px;
    margin: 0;
    padding: 0;
}

.cabecera
{
    background: #37488b;
    box-shadow: 0px 2px 20px 0px rgba(0,0,0,0.5);
    color: white;
    font-weight: bold;
    margin: 0;
    padding: 0.5em;
}

.cabecera .logo
{
    width: 20px;
    vertical-align: middle;
}

.cabecera .tagline
{
    padding: 0 0 0 1em;
    font-weight: normal;
    font-size: 0.8em;
}

.container
{
    width: 70%;
    padding: 0;
    text-align: left;
    border: 1px solid #DDD;
    margin: 0 auto;
}

.container h1
{
    font-size: 20px;
}
.posts
{
    background: white;
    padding: 1em;
}
```



Una vez son realizados los cambios estos son sincronizados con el repositorio remoto:

```bash
git pull origin header
git add .
git commit -m "Fue añadida una imagen y configurado el estilo(fondo y color header)"
git push origin header
```



Finalmente desde footer añadimos los siguientes cambios

```html
<div class="footer">
    Hecho con amor
</div>
```

> HTML

```css
.footer{
    background: #777777;
    color:white;
    text-align: center;
    padding: 5px;
}
```

> CSS



E integramos los cambios al repositorio remoto.



### PULL REQUEST

El Pull request es un punto intermedio en el que es revisado el código antes de ser enviado y al ser aprobado se ejecuta el merge a staying. Esta es una característica de GitHub.



Una buena practica es generar ramas especificas y desde ellas solucionar los errores de tipeo o bugs. Si en algún caso al ser enviado un cambio al repositorio remoto es posible establecerlo como un Pull request para que sea revisado por un usuario que tendrá el poder de aceptar o rechazar un trabajo.



### FORK - Contribuir a un proyecto

Al hacer un FORK se clona todo el proyecto hacia otro repositorio, en general colaboradores, una vez realizados los cambios desde GitHub es posible hacer un Pull Request que como se menciono anteriormente se aplicara al ser aprobado.



Al clonar el proyecto como colaborador se debe ir actualizando, sin embargo no se tiene acceso directo para hacer un pull. Para ello existe un procedimiento:



```bash
git remote add upstream *URL* # Generamos otra fuente para hacer pull
git pull upstream master
git commit -am "Fusión"
git push origin master
```



### .gitignore



En la raiz de los proyectos se puede crear el archivo .gitignore en el cual son indicados los archivos que serán ignorados.

```
*.jpg
```

Para poder agregar una imagen, es conveniente referenciarla desde un sitio web al subirla a sitios que permiten almacenar imágenes.



### Sitio Web publico con GitHub Pages



Podemos hostear un sitio web en GitHub, para ello debemos crear un repositorio con el siguiente indicador *nombre_usuario.github.io* y en el generar mínimo un archivo index.html



Una vez desarrollado, en settings nos dirigimos a pages e indicamos que utilizaremos la rama master. Una vez hecho esto podremos añadir páginas por cada proyecto que poseamos.



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

