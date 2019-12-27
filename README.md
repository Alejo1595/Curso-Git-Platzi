# Curso-Git-Platzi

Es una introducción al mundo de git para aprender a dominarlo de manera profesional.

Para poder entender git hay que tener en cuenta que tiene tres estados basicos

- Directorio de trabajo: Lugar donde se guardaran los archivos de trabajo.
- Area de preparacion (Stagen): Lugar en memoria RAM que guardara los archivos modificados (Cambios) que esten listo para pasar a ser un commit.
- Commit: Es un historial de los cambios realizados del proyecto.

Con git podemos tener archivos que no han sido rastreados, es decir archivos que git **no** sabe de su existencia. Por otro lado podemos tener archivos que si han sido rastreados, es decir archivos de los cuales git **si** conoce su existencia.

El trabajo en git se basa en ramas, es decir crear lineas de trabajo en el cual cada uno tendra su propio destino.

## Comandos

### Comando para trabajar de forma local

- git init: Inicia un repositorio en git.
- git status: Permite saber el estado del repositorio.
- git add [Nombre del archivo]: Añade un archivo en espeficico al area de preparación.
- git add .: Añade todos los archivos al area de preparación.
- git commit: Crea un commit con los archivos que estan en el area de preparación. Abre un editor de texto de la consola para colocarle un mensaje al commit.
- git commit -m"mensaje del commit": Crea un commit con los archivos del area de preparacion y le coloca un mensaje.
- git commit -am"mensaje del commit": Añade los archivos que ya han sido rastreados al area de preparacion y crea un commit con colocandole un mensaje.
- git log [--all][--oneline] --[graph] --[decorate]: Permite ver el historial de cambios.
- git diff [commit antiguo][commit actual]: Es la forma de ver los cambios entre dos commits.
- git branch [Nombre de la rama]: Permite crear ramas.
- git checkout [commit] || [rama] || [tags]: Permite cambiar a un commit, rama o un tag.
- git checkout -b [branch]: Permite crear y cambiar a una rama.
- git merge [rama]: Permite unir dos ramas. Creara un commit automatico si no hay conflictos. En caso de haber conflictos se deberan resolver primeros y de ahi hacer un commit para terminar el merge.
- git merge --abort: Permite cancelar una fusion de ramas.
- git rm --cached: Permite eliminar los archivos de staging y del proximo disco duro pero los mantiene en el disco duro.
- git rm --force: Permite eliminar los archivos de git y del disco duro. Git guardara un registro de esos archivos pero para recuperarlos se necesitan comando mas avanzados.
- git reset --hard [Commit]: Borrara los archivos que estan en staging y los commits que hay por encima del commit establecido.
- git reset --soft [Commit]: tomara los commit que esten por encima del commit establecido y los añadira al area de preparacion.
- git reset HEAD: Sacara los archivos que estan en al staging y los añadira al area de preparacion.

Con estos comando podremos trabajar de forma local. pero si queremos trabajar de forma remota tenemos que hacer lo siguiente:

En primer lugar debemos que git es una base de datos que se crea de manera local en nuesto ordenador. Para poder trabajar de manera remota debemos vincular git con un servicio en la nube como github o gitlab. Estos servicios permiten tener una copia de nuestro repositorio en la nube.

Despues de crear una cuenta en github o gitlab y de crear nuestro repositorio se debe vincular nuestro repositorio local con el remoto.

### Comando Para trabajar de manera remota

git remote add [url-repositorio]: Permite vincular un repositorio local con uno remoto.
git remote set-url [url-repositorio]: Permite cambiar el link del repositorio remoto.
git remote: Mostrara la rama remota.
git remote -v:Mostrara los link para hacer fetch y push.
git push origin [nombre-rama]: Permnite subir los cambios de local a remoto.
git fetch: Traera las ramas remotas al repositorio local.
git pull origin [rama]: Permitira fusionar los cambios remotos con los locales, en caso de NO haber conflictos se realizara un merge de la rama remota con la rama local y si llega a ver conflictos primero se deberan solucionar y despues hacer un commit para concluir el pull.

## Llaves publicas y llaves privadas

Uno de los temas mas importantes en git es mantener secreta la comunicación entre git y nostros. Para poder efectuar esa operacion de manera segura se usaran las llaves publicas y las llaves privadas.

- Llave publica: Es una llave que es de dominio publico y permite cifran un mensaje.
- Lave privada: Es una llave por la cual podemos decifrar un mensaje, esta llave debe ser secreta.

Crear una llave publica y privada:

```git
ssh-keygen -t rsa -b 4096 -C "alejo15san95@gmail.com"
```

- -t rsa: Indicara el tipo de algoritmo que usara.
- -b: Indicara la complejidad del algoritmo.
- -C: Sera el correo al cual se le asiganara esa clave.

Despues de ejecutar el comando se creara una llave publica y privada en nuestro ordenador, por defecto (y es recomendado) se creara en el home.

Luego de crear la llave se debe configurar github o gitlab para que reconozca nuestra llave publica. Despues de eso se debera configurar la url del repositorio para que sea de tipo SSH, para ello se usa el comando:

```git
git remote set-url [url-SSH]
```

Con esta configuracion se añade una capa mas de seguridad a nuestro repositorio ademas de que ya no sera necesario ingresar usuario y contraseña cada vez que se quiera hacer un comando remoto de git.

## Creacion de tags

Un tag nos ayuda a llevar el versionamiento de nuestro app, ademas de poder recodar de manera mas facil un punto en especifico del historial de commit.

- git tag: Permite ver los tags creados.
- git tag -a [nombre tag] -m [mensaje del tag][commit]: permite crear un tag con un mensaje en un commit en especifico.
- git tag -d [nombre tag]: Permite eliminar un tag de manera local.
- git push origin :refs/tags/[nombre tag]: Permite eliminar tags de manera remota.
- git show-ref --tags: Mostrara los tags y a que commit estan unidos.
