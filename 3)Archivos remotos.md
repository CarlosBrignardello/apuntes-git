# TRABAJANDO CON ARCHIVOS REMOTOS



### USAR GITHUB

Tras tener creada una cuenta creamos un repositorio, tras hacerlo obtendremos un URL

* https://github.com/CarlosBrignardello/Apuntes-Git-GitHub



Para ingresar los cambios realizados previamente a este repositorio utilizamos la opción "Clone or download" y obtenemos la URL destacada, en este caso:

* https://github.com/CarlosBrignardello/Apuntes-Git-GitHub.git



**Agregar un origen remoto a nuestros archivos:**

* `git remote add origin https://github.com/CarlosBrignardello/Apuntes-Git-GitHub.git`

Tras hacer esto tendremos acceso a realizar fetch y push al repositorio remoto en cuestión.



**Enviar nuestros archivos al repositorio remoto:**

* `git push origin master`



Se abrirá una ventana que solicitara nuestros datos, simplemente los ponemos. Lo más posible es que nos genere error pues vamos a subir archivos  al remoto sin tener los archivos remotos en primer lugar en local.



Para ello utilizamos un pull:

* `git pull origin master`

Nuevamente nos dara error pues las historias no coinciden, para solucionarlo lo hacemos de la siguiente forma:

* **git pull origin master --allow-unrelated-histories**



y ahora si podemos enviar nuestros archivos al repositorio remoto.



**RESUMEN:**

1. **Rastreamos los archivos:**

* `git add .`

2. **Guardamos los cambios en local:**

* `git commit -am "*MENSAJE*"`

3. **Subimos los cambios al repositorio:**

* `git push origin master`



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



**Revisar conexiones remotas:**

* `git remote -v`



**Agregar un origen remoto a nuestros archivos:**

* `git remote add origin https://github.com/CarlosBrignardello/Apuntes-Git-GitHub.git`



o



**Cambiar dirección de conexión remota:** 

* `git remote set-url origin git@github.com:CarlosBrignardello/Apuntes-Git-GitHub.git`
  Recordemos que origin es simplemente el nombre que se asigno a la conexión remota y que el valor puesto a continuación corresponde a la llave publica del repositorio de GitHub.



**Obtenemos la ultima versión del servidor:**

* `git pull origin master`



**Actualizamos el repositorio local:**

* `git commit -am "MENSAJE"`



**Enviamos el cambio:** 

* `git push origin master`



### TAGS Y VERSIONES

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



### GRAFICAR COMMITS

Es posible mostrar una especie de grafico de la historia del repositorio, es posible hacerlo con dos comandos:

* `git log --all --graph`  # Muestra un grafico de todo el repositorio 
* `git log --all --graph --decorate --oneline` # Muestra un grafico resumido del repositorio



#### Crear Alias

* `alias three="git log --all --graph --decorate --oneline"`
* `alias three-full="git log --all --graph"`



### MANEJO DE RAMAS



**Enviar ramas creadas al repositorio remoto:**

* `git push origin cabecera`

**Muestra la historia de las ramas:**

* `git show-branch`

**Ver commits en forma visual:**

* `gitk`



A partir de ahora crearemos dos ramas adicionales y las enviamos al repositorio remoto:

```bash
git branch header
git branch footer

git pull origin master

git push origin header
git push origin footer
```



### CONFIGURAR MULTIPLES COLABORADORES



#### Nuevo colaborador

0. Previamente es añadido al repositorio al colaborador mediante su correo o su nombre de usuario de GitHub. 

1. Genera una ruta de archivos ordenada en la que guardar el repositorio remoto.

2. Desde el terminal descargamos el repositorio:

* `git clone *DIR_HTTPS*`

3. Realizar cambios
4. Actualizar cambios locales:

* `git commit  -am "MENSAJE"`

5. Actualizamos el contenido remoto al contenido local:

* `git pull origin master`

6. Subimos los cambios al repositorio remoto:

* `git push origin master`

