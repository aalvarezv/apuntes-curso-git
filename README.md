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

#### GitHub
git push -f origin HEAD^:master #Deshace el ultimo commit enviado a GitHub.