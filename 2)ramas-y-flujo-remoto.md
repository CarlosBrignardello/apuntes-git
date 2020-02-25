# Flujo de trabajo



### Manejo de ramas

Las ramas son útiles para segmentar el desarrollo en distintas etapas.



**Crear rama:**

* `git branch *NOMBRE_RAMA*`

**Moverse a una rama:**

* `git checkout *NOMBRE_RAMA*`
  Tras hacer esto, al revisar el estado veremos que esta nueva rama esta completamente actualizada.

*Una vez en la rama podemos generar cambios y estos serán aplicados únicamente para la ramificación en la que nos encontramos. de tal modo que si guardamos los cambios realizados y volvemos a la rama MASTER, los archivos en nuestro directorio habrán cambiado y si ahora regresamos volverán a cambiar.*



**UNIR RAMAS**

Si son realizados cambios tanto en MASTER como en otra rama y se quiere que estas se unan se recurre al uso de un merge. Al hacer merge la rama adicional desaparece y se une a master.

> **NOTA:** si en este momento hacemos un checkout podríamos perder los archivos y los cambios realizados. Por lo que debemos guardarlos o subirlos al repositorio local de inmediato.

Para realizar un merge debemos estar en la rama master, en este caso vincularemos los cambios realizados en cabecera con lo cambios realizados en master. Si lo hacemos al revés convertiríamos la rama cabecera en la rama principal.

En estos casos pueden existir conflictos si dos elementos iguales fueron modificados en ambas versiones y eso debe ser arreglado.

**Realizar un merge:**

* `git merge *NOMBRE_RAMA* `

  Una vez hecho esto fusionamos ambas ramas y obtuvimos el contenido de ambas.



**Hostear un sitio con GitHub Pages**

1. Para hostear un sitio necesitamos generar una nueva rama denominada "gh-pages":
   * `git branch gh-pages`
2. Nos movemos a la rama generada:
   * `git checkout gh-pages`
3. realizamos una actualización al repositorio con la nueva rama:
   * `git push origin gh-pages`
4. Revisamos el sitio hosteado:
   * NOMBRE_USUARIO.github.io/NOMBRE_REPOSITORIO



### Conflictos

Los conflictos son representados con la siguiente sintaxis:

```bash
<<<<<<<<<< HEAD
...........
===============
...........
>>>>>>>>>> *NOMBRE_RAMA*
```

Afortunadamente programas como Visual Studio Code detectan estos conflictos y permiten de forma rápida decidir con que versión trabajar finalmente.



### Flujo remoto

**Obtener datos de un repositorio remoto:**

* `git clone *URL*`
  Lo que sucede al obtener los datos es que se descarga la historia del repositorio remoto y se trae la ultima versión del master. 

**Agregar un origen remoto a nuestros archivos:**

* `git remote add origin *URL*`

  El nombre "origin" es una convención para nombrar a los remotos de un repositorio. Tras hacer esto tendremos acceso a realizar fetch y push al repositorio remoto en cuestión.

**Revisar conexiones remotas:**

* `git remote -v`

**Actualizar y fusionar versión local:**:

* `git pull *NOMBRE_REMOTO* *RAMA*`

**Subir datos a un repositorio remoto:**

* `git push *NOMBRE_REMOTO* *RAMA*` 

  Permite subir la versión final de todos los cambios realizados en forma local.

**Traer actualización del repositorio remoto:**

* `git fetch`
  Obtiene la versión más nueva del repositorio remoto sin traer los archivos.

**Caso especial: Obtener pull de un repositorio con archivos pre-existentes:**

* `git pull origin master --allow-unrelated-histories`

**Ver que usuario genero un cambio:**

* `git blame *LÍNEA_CODIGO*` 

  Muestra quién escribió que línea de código en otras palabras quien es culpable de una línea de código en particular.



### LLAVES SSH

Las llaves publicas y privadas es un sistema de cifrado asimétrico basado en algoritmos matemáticos.

Es posible enviar una llave publica para que sean enviados mensajes o datos mediante ella que solo puedan ser descifrados por los usuarios que poseen la llave privada.

Al conectarse a Github las credenciales quedan guardadas en el equipo por lo que existe una brecha de seguridad en relación con los posibles código fuente que se posean en tu cuenta en caso de que el equipo sea robado.

debemos agregar una capa de seguridad más fuerte, esto permito no requerir de poner el nombre de usuario y contraseña en el equipo especifico.

En el entorno local generaremos una llave privada y una llave publica, la llave publica la enviaremos al GitHub. Debemos conectarnos mediante SSH. GitHub enviara automáticamente una llave publica de vuelta.

Por ende a partir de ahora existe una conexión bidireccional completamente cifrada y por SSH. A la llave privada poseída es incluso posible agregar una contraseña adicional.



#### Generar llaves SSH

Las llaves son generadas en cada equipo específicamente. 

**Generar llave publica y privada:**

* `ssh-keygen -t rsa -b 4096 -C "carlos.alb.brig@gmail.com"`
  Al ejecutar el comando preguntara por el lugar donde instalar la llave, para guardarlo en el lugar donde fue lanzado el comando simplemente presiona enter, adicionalmente puedes poner una contraseña extra a la llave.



**Ejecutar servicio SSH:**

Una vez generada la llave debemos ejecutar el servicio SSH en nuestro equipo.

Para verificar que ssh esta corriendo utilizamos el siguiente comando:

```bash
eval $(ssh-agent -s)
```



**Añadir la llave a SSH:**

* `ssh-add ~/.ssh/id_rsa`



#### Conexión a GitHub con SSH

Nos dirigimos a las configuraciones de la cuenta y a la opción **SSH key and GPG keys** y procedemos a otorgarle un nombre(recomendado el equipo en cuestión o la persona que tendrá acceso) y añadimos llave publica.

Una vez hecho esto nos dirigimos al repositorio y en la opción **Clone or Download** tendremos acceso a la opción **use SSH** lo que nos otorgara una llave publica de GitHub.

Dentro de Git procedemos a ingresar a nuestro repositorio local y revisamos nuestras conexiones remotas.



**Cambiar dirección de conexión remota:** 

* `git remote set-url origin git@github.com:CarlosBrignardello/Apuntes-Git-GitHub.git`
  Recordemos que origin es simplemente el nombre que se asigno a la conexión remota y que el valor puesto a continuación corresponde a la llave publica del repositorio de GitHub.



### Tags y versiones

Los tags permiten destacar un cambio y asignarle un nombre mediante un sistema de tags que posteriormente pueden ser vistos de forma ordenada desde GitHub.



**Generar un tag:**

* `git tag -a *NOMBRE_TAG* -m "Descripción" *IDENTIFICADOR*` 

**Ver tags existentes:**

* `git tag`

**Ver commits relacionados a los tags:**

* `git show-ref --tags`

**Enviar tags:**

* `git push origin --tags`

**Borrar un tag:**

* `git tag -d *NOMBRE_TAG*`



### Graficar Commits

Es posible mostrar una especie de grafico de la historia del repositorio, es posible hacerlo con dos comandos:

* `git log --all --graph`  # Muestra un grafico de todo el repositorio 
* `git log --all --graph --decorate --oneline` # Muestra un grafico resumido del repositorio



**Crear Alias**

* `alias three="git log --all --graph --decorate --oneline"`
* `alias three-full="git log --all --graph"`



### Manejo de ramas



**Enviar ramas creadas al repositorio remoto:**

* `git push origin cabecera`

**Muestra la historia de las ramas:**

* `git show-branch`

**Ver commits en forma visual:**

* `gitk`
