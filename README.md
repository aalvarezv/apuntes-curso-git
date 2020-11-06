# Apuntes Curso Git y Github.

**Notas:**
Cuando se usan dos guiones seguido el comando Git interpreta que el comando es una palabra ejemplo: --oneline, cuando se usa un guión Git interpreta que cada letra es un comando, ejemplo: git status -sb es lo mismo que git status -s -b

#### Configuración inicial.

| Comando | Descripción |
| ------ | ------ |
|git config --global user.name “nombre_usuario”|Configura el usuario.|
|git config --global user.email “mail@mail.cl”|Configura el email.|
|git config --global -e |Obtiene información de la configuración global del usuario en un editor de texto.|

#### Comandos básicos.

| Comando | Descripción |
| ------ | ------ |
|git init|Inicia el repositorio.|
|git status|Obtiene el estado actual del repositorio.|
|git status -s |Muestra el estado con menos detalles.|
|git status -s -b |Muestra el estado con menos detalles y agrega a la información la rama en cual estamos trabajando.|
|git add . | Agrega todos los archivos al stage para que Git les haga seguimiento.|
|git add index.html |Agrega solo el archivo index.html|
|git add *.txt |Agrega todos los txt en el directorio actual.|
|git add “*.txt” |Agrega todos los txt de todo el proyecto.|
|git add css/ |Agrega todos los archivos de la carpeta css.|
|git add css/*.pdf |Agrega todos los archivos .pdf de la carpeta css|
|git add —all |Agrega todos los archivos.|
|git reset *.xml |Excluye archivos .xml del commit.|
|git commit -m “Primer commit”|Crea hitos en la linea del tiempo de Git.|
|git log |Entrega el historial de los commit.|
|git log --oneline |Muestra el historial de los commit escrito de una forma mas corta, no agrega fecha hora y otros datos.|
|git log --oneline --decorate --all --graph |Muestra el historial de los commit de forma mas gráfica y entendible.|

#### Alias
| Comando | Descripción |
| ------ | ------ |
|git config --global alias.lg “log --oneline --decorate --all --graph”|Crea el alias "git lg" para ejecutar el comando: git log --oneline --decorate --all --graph|
|git config --global alias.s “status -s -b”| Crea el alias "git s" para ejecutar el comando: git status -s -b|

#### Viajes en el tiempo.
| Comando | Descripción |
| ------ | ------ |
|HEAD |Apunta al último commit.|
|HEAD^ |Apunta 1 commit antes del último.|
|git diff | Entrega las diferencias entre el ultimo commit vs lo que existe actualmente.|
|git diff --stageg | Entrega todas las diferencias solo de los archivos que están en el stage, aquellos que se les hizo un git add -A |

#### Ir al pasado.
| Comando | Descripción |
| ------ | ------ |
|git reset HEAD README.md |Para quitar un archivo del stage.|
|git checkout -- README.md | Para revertir los últimos cambios en un archivo.| 
|git commit -am “Mensaje” | Aplica el git add + git commit.|
|git commit --amend “Actualizando mensaje” | Actualiza el mensaje del ultimo commit.|
|git reset --soft HEAD^ | Deshace el ultimo commit.|
|git reset --soft a26ef2d | Elimina los commits posteriores al commit que estas apuntando mediante el hash (a26ef2d), conserva los cambios en el stage area (git add) y conserva los cambios que tengas en tus archivos (working directory).|
|git reset --mixed 1cb6d0f | Elimina los commits posteriores al commit al que estas haciendo el reset, deshace los cambios en el stage area (git add) y conserva los cambios que tengas en tus archivos (working directory). |
|git reset --hard 1cb6d0f | Elimina los commits posteriores al commit al que estas haciendo el reset, deshace los cambios en el stage area y deshace los cambios que tengas en tus archivos (working directory). |

#### Ir al presente.
| Comando | Descripción |
| ------ | ------ |
|git reflog | Incluye los reset realizados en el log, con esto se pueden obtener los hash y hacer nuevamente un git reset --hard para volver atras.|

#### Renombrar y eliminar archivos. 
Permite tener un registro en git, en caso que desee volver a tener el archivo eliminado o su nombre cambiado.

#### Mediante comandos Git
| Comando | Descripción |
| ------ | ------ |
|git mv destruir-mundo.txt salvar-mundo.txt | Cambia el nombre del archivo de destruir-mundo.txt a salvar-mundo.txt. |
|git rm salvar-mundo.txt | Elimina el archivo salvar-mundo.txt.|

#### Sin Git 
Eliminar directo desde la carpeta (explorador del sistema operativo) o desde visual studio code.
| Comando | Descripción |
| ------ | ------ |
|git add -u | Avisa a git sobre el cambio realizado, para actualizar el estado.|


#### Ramas
Se utilizan para hacer cambios en paralelo sin afectar el proyecto inicial ejemplo: agregar una funcionalidad que no se tiene claridad si será o no integrada al proyecto final.
| Comando | Descripción |
| ------ | ------ |
|git branch rama-villanos | Crea una rama.|
|git branch | Lista las ramas creadas.|
|git branch -a| Lista las ramas incluyendo las ocultas.|
|git branch -d rama-villanos | Elimina una rama.|
|git checkout rama-villanos | Mueve a la rama indicada.|
|git checkout -b rama-villano | Crea la rama y posiciona en ella.|
|git diff rama-villanos master | Entrega las diferencias entre las ramas indicadas en este caso rama-villanos y rama master.|
|git merge rama-villanos | Une los cambios que estan en la rama-villanos a la rama en la cual estoy posicionado ejemplo: master.|


**Nota:** Para unir ramas (merge) ejemplo: creo la rama rama-villanos para agregar una nueva funcionalidad del programa, esta funcionalidad no es seguro que sea implementada en el proyecto final y por ello se creó esta rama. La rama tendrá los commit que se hayan hecho hasta terminar la nueva funcionalidad. Luego deciden qué esta funcionalidad se debe pasar al proyecto final. Entonces me ubico en la rama principal para el ejemplo sería la rama master. Luego hago un merge de la rama-villanos hacia la rama master, es decir todos los cambios agregados en la rama-villanos se pasarán a la rama master. Y finalmente como buena práctica se elimina la rama-villanos ya que no seguirá siendo utilizada.

#### Merge: Fast-forward
Se produce cuando en la rama principal no ha habido ningún cambio  y por lo tanto cuando se hace la unión de ramas, se unen de manera automática sin que haya problemas (es entonces cuando los commits de la rama secundaria pasan a formar parte de la rama principal).
#### Merge: Automático
Se produce cuando en la rama principal tienes un cambio y en la rama secundaria también, dado que no hay conflicto (no se modifican los mismos archivos) se unen sin problemas de forma automática.
#### Merge: Uniones conflicto
Se produce cuando en un dos ramas se hace un commit a un mismo archivo, al hacer la union (merge) git no sabe cual de los 2 cambios del archivo se debe conservar por lo tanto se debe resolver el conflicto abriendo el archivo, modificarlo para dejar como se requiere finalmente el archivo y luego hacer un commit. 


#### TAGS 
El propósito de los tag es marcar hitos del desarrollo, ejemplo cuando creo la primera versión de producción. Android crea sus tag con nombres de dulces.
| Comando | Descripción |
| ------ | ------ |
|git tag nombreTag | Crea un tag.|
|git tag -d nombreTag | Elimina un tag.|
|git tag -a v1.0.0 -m “Versión 1.0.0” |Agrega un tag con mas información.|
|git tag -a v0.0.9 d0fa820 -m “Version alfa” | Agrega un tag al commit, usa el hash del commit.|
|git show v0.0.9 | Muestra información del tag usa el número de versión.|


#### STASH
Es como una caja donde se guarda de forma temporal todo el trabajo en progreso y que no se desea incluir en un commit, Ejemplo: Tengo avanzado el requerimiento A y me piden otro requerimiento B mas urgente, el requerimiento A lo dejo en el stash, hago el requerimiento B y le hago el commit. Y luego recupero del stash el WIP (WORK IN PROGRESS) del requerimiento A.

**Nota:** Al igual que en los merge de ramas, puede que existan problemas de conflicto al hacer el pop. Estos se resuelven igual que en las ramas, de forma manual se dejan los archivo(s) como se requieren y luego hacer un commit. En caso que existan conflictos el stash no será eliminado y para ello se debe usar el comando drop.

| Comando | Descripción |
| ------ | ------ |
|git stash save | Crea un stash.|
|git stash save “Mensaje del stash” | Agrega un stash con un mensaje de información.|
|git stash list | Permite listar todos los stashes creados.|
|git stash apply | Permite recuperar el trabajo guardado del último stash creado.|
|git stash apply stash@{1} | Permite recuperar un stash en particular del listado de stash. El id del stash a recuperar es: stash@{1}.|
|git stash pop | Permite recuperar el trabajo guardado del último stash creado y también elimina el stash. |
|git stash drop | Permite borrar el último stash creado.|
|git stash drop stash@{1} | Permite borrar un stash en particular del listado de stash. El id del stash a borrar es: stash@{1}.|
|git stash save --keep-index | Guarda todo menos los archivos en el stage o los que se les hizo git add -A.|
|git stash save --include-untracked |Incluye todos los archivos junto a los que git no les está haciendo seguimiento (aquellos que nunca se les ha hecho un git add).|
|git stash list --stat | Entrega mas información de cada una de los stash listados.|
|git show stash | Entrega información mucho mas detallada de cada stash creado. las diferencias de los archivos antes y despues de crear el stash, etc.|
|git show stash@{1} | Entrega información mucho mas detallada de un stash en particular.|
|git stash clear | Borra todas las entradas que hay en el stash, no pregunta, las borra y no hay manera de recuperarlas.|

#### Rebase

Si tengo dos ramas trabajando en paralelo, el comando rebase permite que los commit organizar los commit.

| Comando | Descripción |
| ------ | ------ |
|git checkout rama-misiones-completadas| Me ubico en la rama que queremos que sus commits queden al final de la línea de tiempo.|
|git rebase master | Los commits de la rama indicada en este caso (master) se ubicarán antes de la rama que estoy posicionado (rama-misiones-completadas).|

Luego de hacer el rebase se debe aplicar un merge para unir las ramas y queden ubicadas en el mismo punto de la linea de tiempo. Es decir en el HEAD.
| Comando | Descripción |
| ------ | ------ |
|git checkout master| Me ubico en la rama principal master.|
|git merge rama-misiones-completadas| Une los cambios desde la rama misiones-completas hacia la rama master.|
|git branch -d rama-misiones-completadas | Se elimina la rama rama-misiones-completadas en caso de ser necesario.|

#### Rebase Interactivo
**Se usa para:**
* Ordenar commits.
* Corregir mensajes en los commits.
* Unir commits.
* Separar commits.

#### Rebase Squatch
Permite unir commits. Ejemplo: Tengo dos commits donde actualicé cierta información en ciertos archivos, esta información esta relacionada pero lo hice en dos commit y quiero que estos dos commits se transformen en uno.
| Comando | Descripción |
| ------ | ------ |
|git rebase -i HEAD~4| Toma los últimos 4 commits donde se deberá indicar cual comando aplicar a cada commit.|

**Al aplicar el comando devuelve lo siguiente:**
* pick 158ba9e Se agrego a la liga: Volcán Negro
* pick df3c52a Agregamos el archivo de las misiones completadas
* pick ba0faea Actualizamos dos misiones completadas al momento
* pick eadaddd Actualizamos las misiones completadas

**Comandos:**
* p, pick <commit> = use commit
* r, reword <commit> = use commit, but edit the commit message
* e, edit <commit> = use commit, but stop for amending
* s, squash <commit> = use commit, but meld into previous commit
* f, fixup <commit> = like "squash", but discard this commit's log message
* x, exec <command> = run command (the rest of the line) using shell
* b, break = stop here (continue rebase later with 'git rebase --continue')
* d, drop <commit> = remove commit
* l, label <label> = label current HEAD with a name
* t, reset <label> = reset HEAD to a label
* m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
* .       create a merge commit using the original merge commit's
* .       message (or the oneline, if no original merge commit was
* .       specified). Use -c <commit> to reword the commit message.

**Si quiero unir los últimos dos commits:**
* pick ba0faea Actualizamos dos misiones completadas al momento
* pick eadaddd Actualizamos las misiones completadas

**En el último commit cambiamos el pick por squash, con esto se unirá el commit que tiene el squash con el commit anterior.**
* pick 158ba9e Se agrego a la liga: Volcán Negro
* pick df3c52a Agregamos el archivo de las misiones completadas
* **pick ba0faea Actualizamos dos misiones completadas al momento**
* **squash eadaddd Actualizamos las misiones completadas**

Finalmente se actualiza el mensaje que tendrá el commit.

#### Rebase Reword
Permite cambiar el mensaje de un commit utilizando el rebase.

| Comando | Descripción |
| ------ | ------ |
|git rebase -i HEAD~1| Toma el último commits.|

**Al aplicar el comando devuelve lo siguiente:**
* pick 5e6043e Unimos los commits mediante squash donde actualizamos dos misiones completadas al momento

**Comandos:**
* p, pick <commit> = use commit
* r, reword <commit> = use commit, but edit the commit message
* e, edit <commit> = use commit, but stop for amending
* s, squash <commit> = use commit, but meld into previous commit
* f, fixup <commit> = like "squash", but discard this commit's log message
* x, exec <command> = run command (the rest of the line) using shell
* b, break = stop here (continue rebase later with 'git rebase --continue')
* d, drop <commit> = remove commit
* l, label <label> = label current HEAD with a name
* t, reset <label> = reset HEAD to a label
* m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
* .       create a merge commit using the original merge commit's
* .       message (or the oneline, if no original merge commit was
* .       specified). Use -c <commit> to reword the commit message.

**Si quiero cambiar el mensaje del commit: En el commit cambiamos el pick por reword.**

* **reword 5e6043e Unimos los commits mediante squash donde actualizamos dos misiones completadas al momento**

Finalmente se actualiza el mensaje que tendrá el commit.

#### Rebase Edit

Permite editar un commit, puede ser para separarlo en dos o mas commit. Para este caso de ejemplo se modificaron 2 archivos README.md y villanos.md. Ambos se dejaron en el último commit con el mensaje "Commits".

| Comando | Descripción |
| ------ | ------ |
|git rebase -i HEAD~2| Toma los dos últimos commits.|

**Al aplicar el comando devuelve lo siguiente:**
* pick 1c466c7 Actualizamos el mensaje mediante reword dos misiones completadas al momento
* pick 1e03da6 Commits

**Comandos:**
* p, pick <commit> = use commit
* r, reword <commit> = use commit, but edit the commit message
* e, edit <commit> = use commit, but stop for amending
* s, squash <commit> = use commit, but meld into previous commit
* f, fixup <commit> = like "squash", but discard this commit's log message
* x, exec <command> = run command (the rest of the line) using shell
* b, break = stop here (continue rebase later with 'git rebase --continue')
* d, drop <commit> = remove commit
* l, label <label> = label current HEAD with a name
* t, reset <label> = reset HEAD to a label
* m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
* .       create a merge commit using the original merge commit's
* .       message (or the oneline, if no original merge commit was
* .       specified). Use -c <commit> to reword the commit message.

**Si quiero editar el último commit para separarlo en 2 (para este de ejemplo)**
* pick 1c466c7 Actualizamos el mensaje mediante reword dos misiones completadas al momento
* **edit 1e03da6 Commits**

**Luego se aplica un reset del commit para eliminarlo sin modificar los archivos.**
| Comando | Descripción |
| ------ | ------ |
|git reset HEAD^| Aplica un reset al último commit.|

**Seguido se agregan los archivos al stage y se crean los commit necesarios.**
| Comando | Descripción |
| ------ | ------ |
|git add README.md| Agrega el archivo README.md al stage.|
|git commit -m "Actualizamos el archivo README.md" | Aplica un commit para archivo README.md.|
|git add villanos.md| Agrega el archivo villanos.md al stage.|
|git commit -m "Agregamos Deadshot el archivo villanos.md" | Aplica un commit para archivo villanos.md.|

**Finalmente se cierra el rebase.**
| Comando | Descripción |
| ------ | ------ |
|git rebase --continue | Finaliza la edición del rebase|

Se puede observar la división de los commits.

#### GITHUB

[**Ir Ayuda GitHub**](https://help.github.com/es/github)

| Comando | Descripción |
| ------ | ------ |
|git remote add origin https://github.com/user/repo.git| Agrega un directorio remoto a mi repositorio.|
|git remote -v| Lista los repositorios remotos de mi repositorio local.|
|git push -u origin master| Envía los commits (confirmaciones de cambios) a un repositorio remoto.|
|git push --tags|Envía los tags de mi repositorio local al repositorio remoto.|
|git pull origin master| Trae los últimos cambios del repositorio remoto al repositorio local y realiza un merge|
|git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY| Para clonar un repositorio remoto a mi máquina.|
|git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY demo-10| Para clonar un repositorio remoto a mi máquina e indicar el nombre que debe tener la carpeta.|
|git fetch| Al contrario del git pull fetch baja los cambios sin hacerles merge localmente, los deja en una rama oculta llamada remotes/origin/master|
|git checkout FETCH_HEAD| Permite posicionarme en la rama oculta creada por el fetch para revisar los cambios antes de hacer el pull|
|git checkout origin/master| Permite posicionarme en la rama oculta creada por el fetch para revisar los cambios antes de hacer el pull|
|git push origin origin :rama-villanos| Permite eliminar una rama desde el repositorio local y remoto, generalmente son ramas que se obtienen mediante git pull.|
|git remote prune origin| Permite borrar ramas obtenidas mediante pull cuando solo tenemos la rama en nuestro repositorio local, ya que en el repositorio remoto (GitHub) la hemos borrado con anterioridad.|

##### Deshacer último commit en Github y Repositorio Local, comandos complementarios.

| Comando | Descripción |
| ------ | ------ |
|git reset HEAD^| Ubica el HEAD en el commit anterior en el repositorio local|
|git push origin +HEAD| Obliga (force-push) a que el commit donde se encuentra el HEAD en el repositorio local, sea el último commit en el repositorio remoto es decir en Github|

##### MarkDown
[**Ir Tutorial MarkDown**](https://www.markdowntutorial.com/)