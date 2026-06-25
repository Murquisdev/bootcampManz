# Terminal
[Youtube](https://www.youtube.com/watch?v=x28OvdVBegU) | [Diapostivias](https://bootcamp.manz.dev/slides/terminal/) |

Se recomienda el uso de Windows Terminal en Windows y el sistema WSL (Windows Subsystem for Linux)

```bash
# Instaladas
wsl --list

# Para descargar e instalar
wsl --list --online

# Instalar Debian
wsl --install -d Debian
```

## Personalizar Shell

Se recominda utilizar Fish.

```bash
# Actualizar repositorios
sudo apt update

# Instalar curl + fish
sudo apt install curl fish

# Establecer fish por defecto
chsh -s $(which fish)`

# Instalar fisher (instalador de complementos de fish)
curl -sL https://raw.githubusercontent.com/jorgebucaran/fisher/main/functions/fisher.fish | source
fisher install jorgebucaran/fisher

# Instalar tide (framework de fish)
fisher install IlanCosman/tide@v6
```

## Comandos
[Cheatsheet de comandos de terminal](https://terminaldelinux.com/terminal/cheatsheets/)
```bash
# Muestra la dirección actual
pwd

# Mover de forma absoluta
cd /
cd /home/manz
cd /etc

# Mover de forma relativa
cd ..
cd home && cd manz
cd .. && cd .. && cd etc

# Crea carpetas y ficheros
mkdir carpeta
mkdir -p carpeta/subcarpeta
touch file

# Mostrar archivos y carpetas
ls -lh
eza --icons --tree -lh // requiere instalación

# Renombrar/Mover, copiar y eliminar
mv origen destino
cp origen destino
rm fichero

# ¿Donde está un ejecutable?
which file

# Buscar ficheros
find -name *png
fdfind fragmento // requiere instalación

# File managers requieren instalación
ytree
broot
lf

# Mostrar el contenido de un fichero
cat file.txt

# Muchas veces, se usa con paginador
# Opciones: more, less, most
cat file.txt | more

# Bat: Mejora de `cat`
batcat file.txt // requiere instalación

# Buscar coincidencias en un fichero
grep "texto" file.txt

# Buscar lineas que no coincidan
grep -v "texto" file.txt

# Filtrar con fzf Requiere instalación
fzf
ls -lh | fzf

# Editores básicos
nano file.txt
nvim file.txt
echo "contenido" >file.txt

# Editores más complejos
micro file.txt
fresh file.txt // Recomendado, requiere instalación
```

## Visual Studio Code
Es el editor recomendado.
Panel de VSCode: CTRL + SHIF + P
[Open User Settings (JSON) de Manz](https://gist.github.com/ManzDev/8038b009b2243a9108cf8c2876372278)

```bash
#En la carpeta a editar, abrir VSCode desde terminal
code .
```

## Crear Scripts
Guarda o mueve los scripts a ```/usr/local/bin```

```bash
nano saludo

#!/bin/bash
echo "╭────────╮" | lolcat
echo "│ ◕ ‿  ◕ │ ¡Saludos, Manz!" | lolcat
echo "╰───┬─┬──╯" | lolcat

chmod +x saludo
./saludo

#Scripts en Fish utilizando funciones:
# Creamos alias
funced take
take> function take
           mkdir -p $argv && cd $argv
      end

# Si funciona bien, guardamos de forma permanente
funcsave take

# Se puede editar con fresh por ejemplo:
fresh /home/{user}/.config/fish/functions/{nombreFuncion}.fish

#Ejemplo
fresh /home/murquisdev/.config/fish/functions/newProject.fish
```
