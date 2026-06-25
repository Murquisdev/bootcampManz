# Control de proyecto
[Youtube](https://www.youtube.com/watch?v=Pvjs0h306pI) | [Diapostivias](https://bootcamp.manz.dev/slides/control/) |

Se recomienda utilizar PNPM como gestor de paquetes.

```bash
# Instalamos pnpm
curl -fsSL https://get.pnpm.io/install.sh | sh -
pnpm --version

# Instalamos Node (LTS)
pnpm env use --global lts
node --version

# Otros posibles lenguajes a  instalar
# Instalación de dependencias necesarias
# Descarga del instalador de Rust e instalación
sudo apt install curl build-essential -y
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Comprobación de la versión del instalador de Rust
cargo --version
rustc --version

# Ejemplo de instalación
cargo install nuls

# Instalación de dependencias de Python
sudo apt install python3-full python3 python3-pip

# Crear un entorno virtual para Python
python3 -m venv ~/.python

# Activar el entorno
. ~/.python/bin/activate.fish
```
## Estructura de carpetas

📁 project-name                  # Carpeta del proyecto
 ├── 📁 src                      # Código fuente editable
 │    ├── 📁 assets              # Ficheros estáticos
 │    │    ├── 📁 fonts          # Tipografías
 │    │    └── 📁 images         # Imágenes
 │    ├── 🟧 index.html          # Nuestro HTML
 │    ├── 📁 css                 # Carpeta de estilos
 │    │    └── 🟪 global.css     # Archivo CSS
 │    ├── 📁 modules             # Carpeta de modulos Javascript
 │    └── 🟨 main.js             # Javascript principal
 ├── 📄 README.md                # Instrucciones o comentarios del proyecto
 ├── 📄 .gitignore               # Ficheros o carpetas a ignorar (lo que no nos interesa)
 └── 📄 package.json             # Fichero de información del proyecto

 ## Trabajar con un servidor local
 ```bash
pnpm add servor

pnpx servor src/ index.html 1234 --reload
```

## Iniciar un proyecto con pnpm

```bash
# Inicializa. Crea `package.json`. ESM.
pnpm init
pnpm pkg set type=module

# Instala dependencias en node_modules/
pnpm add -D servor # -D modo desarrollo

# Desinstala dependencias
pnpm remove servor
```
```js
{
  "name": "project-name",
  "description": "My pet project",
  "type": "module",
  "author": "ManzDev",
  "devDependencies": {
    "servor": "^4.0.2",
  }
}

pnpm add servor             # ^4.x.x
pnpm add -E servor@4.0.2    # 4.0.2 (exacta)
pnpm add -D servor          # De desarrollo
pnpm add -g servor          # Global (evitar)
pnpx npm-check -u           # Actualizaciones

# Truco: añade siempre versiones exactas
echo "save-exact=true" >>.npmrc
```
Se pueden automatizar scripts en el ```package.json```
```json
{
  "scripts": {
    "test": "echo \"Error...\" && exit 1",      <- Puedes eliminar esta linea
    "dev": "servor src/ index.html 1234 --reload",
    "lint": "oxlint src/",
    "format": "oxfmt src/"
  }
}
```
```bash
# Para ejecutar un script
pnpm run dev
```

## Linters
Herramientas que revisan el código, formatean y evitan problemas.

```bash
# Instalación de linter + formateador
pnpm add -D oxlint oxfmt

# Crea reglas de configuración
pnpx oxlint --init
echo "node_modules/" >.eslintignore

# Ejecutamos
pnpx oxlint
```

En VSCode hay una [extensión](https://open-vsx.org/extension/oxc/oxc-vscode)
y la configuración de las propiedades (CTRL + SHIFT + P) son:
```json
{
  "css.validate": false, // Desactiva el linter nativo de CSS
  "javascript.validate.enable": false, // Desactiva el linter nativo de JS
  "editor.formatOnSave": true, // Activa formatear al guardar
  "editor.defaultFormatter": "oxc.oxc-vscode", // Usa OXC como formateador por defecto
  "editor.codeActionsOnSave": {
    "source.fixAll.oxc": "always" // Cuando guardas, corrige código
  },
}

// Es posible configurar a nivel del lenguaje:
{
  "editor.defaultFormatter": "oxc.oxc-vscode", ❌
  "[javascript]": {
    "editor.defaultFormatter": "oxc.oxc-vscode"
  },
  "[css]": {
    "editor.defaultFormatter": "oxc.oxc-vscode"
  },
}
```

## Git

### Instalación
```bash
sudo apt install git
git --version

git config --global user.name "usuario"                   # Aunque no es necesario 100%, intenten
git config --global user.email "usuario@dominio.com"      # que coincidan con los de GitHub
git config --global init.defaultBranch main # Para cambiar el nombre de maestro a principal
git config --global --list

# Necesario si usas HTTPS
git config --global credential.helper \
  "/mnt/c/Program\ Files/Git/mingw64/bin/git-credential-manager.exe"
```

### Comandos básicos

```bash
# Vamos a la carpeta del proyecto
cd workspace/project-name

# Inicializamos repositorio git local
git init

# Comprobamos el estado
git status

# Añadimos nuevos ficheros
git add index.html
git add index.css

git status

git reset index.css # lo quita
# Guardamos los cambios
git commit -m "Add first files"

# Consultar commits
git log --oneline

# Clonar con HTTPS
git clone https://github.com/ManzDev/gallinerica
```

### Deshacer commits

|Comando|	Modifica último commit|	Descripción|
|-------|-----------------------|------------|
|`git commit --amend`|	✅ Sí	|Reescribe último commit añadiendo lo nuevo
|`git reset HEAD~1`|	✅ Sí |Mantiene los cambios en la carpeta (sin vigilar)|
|`git reset --soft HEAD~1`|	✅ Sí	|Mantiene los cambios en la carpeta (vigilando)|
|`git reset --hard HEAD~1`|	✅ Sí	|Se pierden los cambios en la carpeta|
|`git revert`|	❌ No|	Añade nuevo commit deshaciendo el último|

* `HEAD~1` significa «el commit anterior al que estás ahora»

## GitHub

Cuando se crea un repositorio en GitHub es necesario traerlo a local.

```bash
# Añadimos origin (repo remoto) a main (rama principal local)
git remote add origin https://github.com/ManzDev/gallinerica

# Si hay gente trabajando en el proyecto, traete siempre los cambios
git pull

# Subimos los cambios del repo local al remoto
# (las siguientes simplemente `git push`, pero la primera vez es obligatorio)
git push -u origin main
```

### SSH
```bash
ssh-keygen -t ed25519 -C "usuario@dominio.com"

# (Clave privada 🔑) -> Tu PC:
# /home/usuario/.ssh/id_ed25519

# (Clave pública 🔒) -> GitHub:
# /home/usuario/.ssh/id_ed25519.pub

cat /home/usuario/.ssh/id_ed25519.pub
ssh-ed25519 ############################ Usuario@dominio.com

# A partir de ahora, mejor así:
git remote add origin git@github.com:ManzDev/gallinerica.git
git clone git@github.com:ManzDev/gallinerica.git
```

### Automatizar con GitHub CLI
```bash
# Crea un repositorio público de la carpeta actual, usando el origin
gh repo create --public ManzDev/nombre-de-repo --source . --remote origin

# Ver si existen PR (pull request)
gh pr view

# Echa un vistazo al repositorio
gh repo view
```

### Ramas

```bash
# Saltar a una rama concreta (para revisar)
git log
git checkout <id-commit>

git switch main  # Vuelve a la rama principal

git switch -c nombre-nueva-rama <id-commit>
git branch -d nombre-rama  # Borra rama local
git push origin --delete nombre-rama # remota
 # Crea nueva rama desde donde estás
git switch -c nombre-rama

# Vamos a main y traemos cambios remotos
git switch main
git pull origin main

# Mezclamos la rama con nuestro main
git merge nombre-rama
```

### GitHub Pages

Código fuente: github.com/user/repo, GitHub Pages (webs alojadas): user.github.io/repo

```bash
# Instalamos comando para desplegar
pnpm add -D gh-pages

# Despliegue en la rama `gh-pages`
gh-pages -d src

# Buena idea: añadirlo en package.json (en scripts)
{
  "deploy": "gh-pages -d src/"
}
```
