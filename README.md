# INTRODUCCIÓN



**Descargar Git en Windows:**

* https://git-scm.com/downloads

  Durante la instalación es recomendable seleccionar la opción "**Git from the command line and also from 3rd-party software**" para poder utilizar Git desde el terminal emulado y la consola de Windows.

Una vez descargado podemos abrir el programa **Git Bash**, dentro de el podemos perfectamente navegar entre archivos de la misma forma en que se hace en Linux incluso desde Windows.

Dentro de git podemos utilizar el comando `git` para ver información acerca de los comandos que podemos utilizar.



### COMANDOS BÁSICOS GIT

**Conceptos:**

> **Staging:** Se trata de un área de preparación, un área temporal antes de enviar los cambios al repositorio, donde son guardadas todas las modificaciones.

> **Tracked/Untracked:** Es el estado en que los archivos están o no siendo rastreados, un archivo puede estar en estado tracked en staging o tracked en el repositorio.



**Generar un repositorio:**

* `git init *NOMBRE_ARCHIVO*`

  Al ejecutar el comando se crea un área en memoria RAM llamada staging(donde son agregados los cambios).



**Tracked data to staging area:**

* `git add *NOMBRE_ARCHIVO*`

  Al hacer esto cada vez que realicemos cambios en el archivo estos serán almacenados en el staging área. De esta manera hacemos que el archivo entre en un estado de **track**, es decir esta siendo rastreado.
  
* `git add .`

  Permite añadir a staging todos los archivos.



**Subir cambios al repositorio:**

* `git commit -m "*DESCRIPCIÓN DEL CAMBIO*"`

  Permite que los cambios queden guardados y pasen a un estado tracked en el repositorio mejor conocida como la rama MASTER donde son guardados todos los cambios.



**RAMAS**

Por defecto el repositorio posee una rama llamada **MASTER** donde son guardados los cambios de los archivos con `commit`, estos cambios son lineales. Llegado cierto momento se puede determinar que deseamos realizar cambios experimentales o ramificaciones adicionales a la rama principal, para por ejemplo: **separar el desarrollo de un proyecto en las tareas del equipo de desarrollo**. 

Para ello desde un commit de la rama MASTER podemos comenzar a dividir el camino en dos, simplemente añadiendo un nombre al commit. Si en la rama actual sucede un error se procede a crear una nueva rama proveniente de la versión actual llamada **bugfixing** o **hotfix**. Tras testear con diversas pruebas y solucionar el error, si se busca unir el cambio realizado con la rama MASTER es decir unir dos ramas se realiza un cambio denominado **merge**.

> **Merge:** es el proceso de fusionar los cambios de dos ramas, en general la rama de experimentos es denominada **development**.

Al realizar todos estos cambios es posible que existan conflictos entre archivos.



### Crear un repositorio y hacer un commit

1. **Desde Git Bash creamos un repositorio:**

* `git init`
  Lo hacemos dentro de la carpeta que se usara de repositorio

**Listar archivos ocultos:**

* `ls -al`
  Encontraremos el archivo .git en el directorio, el cual posee todos las configuraciones y funcionalidades de git.

2. **Generamos un cambio**.

3. **Revisamos los cambios en el repositorio:**

* `git status`

  Al hacerlo nos marcara el siguiente mensaje:

  ```bash
  On branch master
  
  No commits yet
  
  Untracked files:
    (use "git add <file>..." to include in what will be committed)
  
          texto.txt
  
  nothing added to commit but untracked files present (use "git add" to track)
  ```

  > Esto básicamente nos indica que el archivo no esta siendo trackeado.

4. **Trackear archivos a staging:**

* `git add .`

  Si revisamos los cambios nuevamente nos indicara el archivo como recientemente añadido. 

5. **Quitar archivo de staging:**

* `git rm --cached *NOMBRE_ARCHIVO*`

6. **Subir archivo al repositorio local:**

* `git commit -m "*MENSAJE*"`

  Para hacer esto es necesario tener configurado nuestro correo y usuario.



**CONFIGURAR GIT**

**Ver configuración de git:**

* `git config --list`

**Configurar cuenta:**

* `git config --global user.name "Carlos Brignardello"`
* `git config --global user.email "carlos.alb.brig@gmail.com"`



**VER LOGS**

**Ver cambios**:

* `git log`

**Ver todos los cambios de un archivo especifico**:

* `git log texto.txt`



### Analizar cambios en los archivos

**Ver cambios en un archivo:**

* `git show *NOMBRE_ARCHIVO*`

  Este comando nos permite ver los tags de los cambios realizados. Lo que nos indica es el contenido previo del archivo y los cambios nuevos al archivo.

**Comparar cambios:**

* `git diff *TAG#1* *TAG#2*`

  Esto es sumamente útil por ejemplo para comparar el primer y el ultimo cambio realizado o al revés.



### Volver en el tiempo en el repositorio

**Regresar TODO al estado anterior:**

* `git reset *TAG* --hard`

**Regresar a la versión anterior y mantener los cambios de staging:**

* `git reset *TAG* --soft`

**Comparar cambios entre staging y el estado sin guardar:**

* `git diff`

**Obtener archivo previo:**

* `git checkout *TAG* *NOMBRE_ARCHIVO*`

**Volver al archivo más reciente:**

* `git checkout master *NOMBRE_ARCHIVO*`



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

