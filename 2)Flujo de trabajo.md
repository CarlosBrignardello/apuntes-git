# FLUJO DE TRABAJO

Al trabajar en equipo se requiere de un repositorio remoto, las alternativas existentes son (GitHub, GitLab, etc).

**Obtener datos de un repositorio remoto:**

* `git clone *URL*`
  Lo que sucede al obtener los datos es que se descarga la historia del repositorio remoto y se trae la ultima versión del master. 



**Subir datos a un repositorio remoto:**

* `git push` 

  Permite subir la versión final de todos los cambios realizados en forma local.



**Traer actualización del repositorio remoto:**

* `git fetch`
  Obtiene la versión más nueva del repositorio remoto sin traer los archivos.



**Fusionar versión actualizada y versión local:**

* `git merge`
  Integra los archivos locales con la versión más nueva del MASTER remoto.



**Actualizar y fusionar versión local:**

* `git pull`
  Obtiene una copia actualizada de lo ultimo que sucedió en el repositorio remoto.



### MANEJO DE RAMAS

Creamos los siguientes archivos en una carpeta llamada SITIO WEB.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="./styles.css">
    <title>Document</title>
</head>
<body>
    <h1>Este es header del proyecto</h1>
    <p>Este es el parrafo del proyecto</p>
</body>
</html>
```

> index.html



```
body{
    text-align: center;
    color: deeppink;
    font-family: Arial;
}
```

> css.html



Añadimos el archivo a staging y lo subimos al repositorio local.

```bash
git add SITIO WEB
git commit -m "Se agrega la base del sitio"
```



#### Crear rama

Cambiamos los dos archivos de la siguiente forma:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="./styles.css">
    <title>Document</title>
</head>
<body>
    <div class="container">
        <div class="posts">
            <h1>De regalo un poco latin</h1>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. 
                Ullam ipsam quo impedit ratione consequatur! Fuga, aliquid 
                totam molestiae pariatur eum, eaque obcaecati incidunt id 
                tempore iste earum tempora laborum laudantium.</p>
        </div>
    </div>

</body>
</html>
```

> index.html



```css
body{
    text-align: center;
    color: #333;
    font-family: Arial;
    font-size: 16px;
    margin: 0;
    padding: 0;
}

.container{
    width: 70%;
    padding: 1em;
    text-align: left;
    border: 1px solid #DDD;
    margin: 0 auto;
}

.container h1{
    font-size: 20px;
}
```

> style.css



**Ahora añadimos los cambios al repositorio local:**

* `git commit -am "Se envian las actualizaciones al sitio web"`



**Crear rama:**

* `git branch *NOMBRE_RAMA*`



**Moverse a una rama:**

* `git checkout *NOMBRE_RAMA*`
  Tras hacer esto, al revisar el estado veremos que esta nueva rama esta completamente actualizada.



*Una vez en la rama podemos generar cambios y estos serán aplicados únicamente para la ramificación en la que nos encontramos. de tal modo que si guardamos los cambios realizados y volvemos a la rama MASTER, los archivos en nuestro directorio habrán cambiado y si ahora regresamos volverán a cambiar.*



### UNIR RAMAS

Actualmente se dispone de dos ramas: MASTER y cabecera. A continuación serán realizados cambios tanto en MASTER como en cabecera para posteriormente hacer uso de un merge. Es decir vincular las dos ramas.

Al hacer merge la rama cabecera desaparece y se une a master.



**Cambios en la rama cabecera:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="./styles.css">
    <title>Document</title>
</head>
<body>
    <div class="container">
        <div class="cabecera">
                NeoCards
                <span class="tagline">La información precisa</span>
        </div>
        <div class="posts">
            <h1>Git & GitHub</h1>
            <p>Este es el cambio realizado en la ramificación cabecera.</p>
        </div>
    </div>

</body>
</html>
```

> index.html



```css
body{
    text-align: center;
    color: #333;
    font-family: Arial;
    font-size: 16px;
    margin: 0;
    padding: 0;
}

.cabecera{
    background: #33A;
    box-shadow: 0px 2px 20px 0px rgba(0,0,0,0.5);
    color:white;
    font-weight: bold;
    margin: 0;
    padding: 0.5em;
}

.cabecera .tagline{
    margin: 1em 0 0 0;
    font-weight: normal;
    font-size: 0.8em;
}

.container{
    width: 70%;
    padding: 0;
    text-align: left;
    border: 1px solid #DDD;
    margin: 0 auto;
}

.container h1{
    font-size: 20px;
}

.posts{
    padding: 1em;
}
```

> styles.css



**NOTA:** si en este momento hacemos un checkout podríamos perder los archivos y los cambios realizados. Por lo que debemos guardarlos o subirlos al repositorio local de inmediato.



Nos pasamos a la versión master y modificamos aleatoriamente alguno de nuestros archivos (CSS Y HTML).



#### Realizar un merge

Para realizar un merge debemos estar en la rama master, en este caso vincularemos los cambios realizados en cabecera con lo cambios realizados en master. Si lo hacemos al revés convertiríamos la rama cabecera en la rama principal.

En estos casos pueden existir conflictos si dos elementos iguales fueron modificados en ambas versiones y eso debe ser arreglado.

```bash
git merge cabecera
```



Una vez hecho esto fusionamos ambas ramas y obtuvimos el contenido de ambas.



### CONFLICTOS CON MERGE

Los conflictos son representados con la siguiente sintaxis:

```
<<<<<<<<<< HEAD
...........
===============
...........
>>>>>>>>>> *NOMBRE_RAMA*
```

Afortunadamente programas como Visual Studio Code detectan estos conflictos y permiten de forma rápida decidir con que versión trabajar finalmente.

Finalmente al solucionar el conflicto esto se guarda con commit.

