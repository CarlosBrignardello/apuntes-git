# INTRODUCCIÓN



[TOC]

**APUNTES DE:**

* **Platzi**



### INSTALACIÓN

**Descargar Git en Windows:**

* https://git-scm.com/downloads

  Durante la instalación es recomendable seleccionar la opción "**Git from the command line and also from 3rd-party software**" para poder utilizar Git desde el terminal emulado y la consola de Windows.

 **Descargar Git en Linux:**

* `apt-update`
* `apt-upgrade`
* `apt-get install git`

Una vez descargado podemos abrir el programa **Git Bash**, dentro de el podemos perfectamente navegar entre archivos de la misma forma en que se hace en Linux incluso desde Windows.

Dentro de git podemos utilizar el comando **git** para ver información acerca de los comandos que podemos utilizar.

#### Pruebas con archivos

Abriendo un archivo **.doc** desde un editor de código:

+ Presenta complicaciones para hacerlo, una vez dentro se ven símbolos y garabatos, internamente el documento esta estructurada en 0s y 1s es decir de forma binaria.



Abriendo un archivo **.rtf** desde un editor de código:

* Posee códigos internos algo así como lo que sucede con un archivo .md al ser visualizado y editado por un procesador como Typora.



### COMANDOS BÁSICOS GIT

**CONCEPTOS:**

**Staging:** Se trata de un area de preparación, un area temporal antes de enviar los cambios al repositorio, donde son guardadas todas las modificaciones.

**Tracked/Untracked:** Es el estado en que los archivos están o no siendo rastreados, un archivo puede estar en estado tracked en staging o tracked en el repositorio.



**Generar un repositorio:**

* `git init *NOMBRE_ARCHIVO*`

  Al ejecutar el comando se crea un área en memoria RAM llamada staging(donde son agregados los cambios).



**Tracked data to staging area:**

* `git add *NOMBRE_ARCHIVO*`

  Al hacer esto cada vez que realicemos cambios en el archivo estos serán almacenados en el staging area. De esta manera hacemos que el archivo entre en un estado de **track**, es decir esta siendo rastreado.



**Subir cambios al repositorio:**

* `commit -m "*DESCRIPCIÓN DEL CAMBIO*"`

  Permite que los cambios queden guardados y pasen a un estado tracked en el repositorio mejor conocida como la rama MASTER donde son guardados todos los cambios.



**Obtener un cambio de otro miembro del equipo:**

En caso de que sea necesario obtener el cambio de otro desarrollador que no posees en local es posible obtenerlo dirigiéndose a la ramificación MASTER y lo obtenemos con:

* `checkout`



#### CREAR RAMIFICACIONES

Por defecto el repositorio posee una rama llamada MASTER donde son guardados los cambios de los archivos con `commit`, estos cambios son lineales.

<<<<<<< HEAD
Llegado cierto momento se puede determinar que deseamos realizar cambios experimentales o ramificaciones adicionales a la rama principal, para por ejemplo: separar el desarrollo de un proyecto en las tareas del equipo de desarrollo.
=======
Llegado cierto momento se puede determinar que se deseamos realizar cambios experimentales o ramificaciones adicionales a la rama principal, para por ejemplo: separar el desarrollo de un proyecto en las tareas del equipo de desarrollo.
>>>>>>> 91a7376ccfc19ff81f8f4ed261d7f7028782c76d

Para ello desde un commit de la rama MASTER podemos comenzar a dividir el camino en dos simplemente añadiendo un nombre al commit.

Si en la rama actual sucede un error se procede a crear una nueva rama proveniente de la versión actual llamada **buxfixing** o **hotfix**. Tras testear con diversas pruebas y solucionar el error, si se busca unir el cambio realizado con la rama MASTER es decir unir dos ramas se realiza un cambio denominado **merge**.

**Merge:** es el proceso de fusionar los cambios de dos ramas, en general la rama de experimentos es denominada **development**.

Al realizar todos estos cambios es posible que existan conflictos entre archivos.



### PRUEBA #1 - Crear un repositorio y hacer un commit

**Desde Git Bash creamos un repositorio:**

* `git init`
  Lo hacemos dentro de la carpeta que se usara de repositorio

**Listar archivos ocultos:**

* `ls -al`
  Encontraremos el archivo .git en el directorio, el cual posee todos las configuraciones y funcionalidades de git.

Generamos un archivo de texto con el nombre texto.txt con el siguiente texto en su interior:

```
Juventud divino tesoro ya te vas para no volver, 
cuando quiero llorar no lloro y aveces lloro sin querer :C
```



**Revisar cambios en el repositorio:**

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

Esto básicamente nos indica que el archivo texto.txt no esta siendo trackeado.



**Trackear archivo a staging:**

* **git add texto.txt**



Si revisamos los cambios nuevamente nos indicara el archivo texto.txt como recientemente añadido. Si deseamos cancelar el estado tracked hacemos lo siguiente:



**Quitar archivo de staging:**

* `git rm --cached texto.txt`



**Subir archivo al repositorio:**

* `git commit -m "Ese es el primer archivo texto.txt"`

  Para hacer esto es necesario tener configurado nuestro correo y usuario.



**Ver configuración de git:**

* `git config --list`

  Cambiar nombre de usuario:

  * `git config --global user.name "Carlos Brignardello"`
  * `git config --global user.email "carlos.alb.brig@gmail.com"`



Una vez subido el archivo podemos modificarlo de la forma que se nos ocurra y revisamos el estado del repositorio. Nos indicara que fue modificado, para arreglarlo debemos trackear el archivo a staging y luego subirlo al repositorio.


Si por ejemplo poseemos más muchos archivos que queremos añadir al repositorio podemos utilizar el siguiente comando:

**Añadir varios archivos en git:**

* `git add .`



**Ver todos los cambios de un archivo:**

* `git log texto.txt`



### ANALIZAR CAMBIOS EN LOS ARCHIVOS

**Ver cambios en un archivo:**

* `git show texto.txt`

  Este comando nos permite ver los tags de los cambios realizados.



El resultado en este caso es:

```
-Juventud divino tesoro ya te vas para no volver,
+Juventud divino tesoro ya te vas para SI volver,
 cuando quiero llorar no lloro y aveces lloro sin querer :C
\ No newline at end of file
```

Lo que nos indica es el contenido previo del archivo y los cambios nuevos al archivo.



**Comparar cambios:**

* `git diff *TAG#1* *TAG#2*`

  Esto es sumamente útil por ejemplo para comparar el primer y el ultimo cambio realizado o al reves.



### VOLVER EN EL TIEMPO EN EL REPOSITORIO

**Regresar TODO al estado anterior:**

* `git reset *TAG* --hard`



**Regresar a la versión anterior y mantener los cambios de staging:**

* `git reset *TAG* --soft`



**Comparar cambios entre staging y el estado sin guardar:**

* `git diff`



**Obtener archivo previo:**

* `git checkout *TAG* historia.txt`



**Volver al archivo más reciente:**

* `git checkout master historia.txt`
