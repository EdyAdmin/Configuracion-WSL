# Configuración modular para ZSH (WSL / Ubuntu)

Configuración modular optimizada para Zsh orientada a desarrollo y productividad en entornos WSL/Linux. Transforma la línea de comandos integrando comportamiento interactivo moderno (estilo editor gráfico), atajos avanzados de edición y separación estricta entre configuraciones portables y rutas privadas del sistema.

---

## 📌 Módulos y funcionalidades añadidas

Esta configuración reorganiza la terminal en submódulos independientes ubicados en `~/.zsh_user/`. Tengo implementada una funcionalidad similar al seleccionado con shift + flechas de PowerShell y tengo instalados GHC (para Haskell), Bat y AstroNvim. También tengo puestos algunos aliases y plugins interesantes.

### 1. Arquitectura modular
* **`.zsh_aliases`**: Centraliza los atajos de comandos habituales (`c` para clear, utilidades de terminal como `bat`).
* **`.zsh_widgets`**: Contiene funciones y widgets propios programados para el subsistema interactivo de Zsh (ZLE - Zsh Line Editor).
* **`.zsh_keybinds`**: Mapeo completo de secuencias de escape y atajos de teclado.
* **Aislamiento local (`.zsh_local/`)**: Directorio protegido mediante `.gitignore` para definir rutas personales (unidades montadas como Google Drive, particiones Windows o credenciales).

### 2. Selección interactiva de texto
A través del plugin `zsh-shift-select` y la integración en `.zsh_keybinds`, la terminal adopta la edición de texto propia de PowerShell:
* **`Shift + Flechas (Izquierda / Derecha)`**: Selecciona caracteres continuos directamente sobre la línea de comandos.
* **`Ctrl + Shift + Flechas (Izquierda / Derecha)`**: Selecciona palabras completas hacia adelante o hacia atrás.
* Sustitución y borrado automático al escribir o pulsar retroceso sobre texto seleccionado.

### 3. Navegación y edición ágil
* Integración fluida con editores modulares (como Neovim / AstroNvim) para manipular líneas sin salir del flujo de trabajo.
* **Atajo `reload`**: Ejecuta `daemon-reload`, remonta puntos de almacenamiento definidos en `/etc/fstab` y reinicia una sesión de Zsh completamente limpia (`exec zsh`) para agilizar un reinicio sin necesidad de cerrar la terminal.

---

## 🛠️ Guía de instalación paso a paso

Si estás interesado en instalar esta configuración, sigue estos pasos para desplegar el entorno completo con todas sus dependencias.

### 1. Clonar la configuración modular
Clona el repositorio directamente dentro de tu carpeta personal con el nombre `.zsh_user`:

```bash
git clone https://github.com/EdyAdmin/Configuracion-WSL.git ~/.zsh_user
```

---

### 2. Instalar los plugins
Descarga los complementos externos dentro de la carpeta custom de Oh My Zsh (`git` ya viene incluido en el framework):

```bash
# 1. Selección de texto con Shift
git clone https://github.com/jirutka/zsh-shift-select.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-shift-select

# 2. Sugerencias automáticas
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# 3. Portapapeles del sistema
git clone https://github.com/kutsan/zsh-system-clipboard.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-system-clipboard

# 4. Resaltado de sintaxis
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

# 5. Integración con Bat
git clone https://github.com/fdellwing/zsh-bat.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-bat

# 6. Recordatorio de aliases
git clone https://github.com/MichaelAquilina/zsh-you-should-use.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/you-should-use
```

---

### 3. Configurar ~/.zshrc
Abre tu archivo `~/.zshrc`:

```bash
nvim ~/.zshrc
```

a. Activa los plugins:
```zsh
plugins=(
    git
    zsh-shift-select
    zsh-autosuggestions
    zsh-system-clipboard
    zsh-syntax-highlighting
    you-should-use
    zsh-bat
)
```

b. Carga los módulos añadiendo esto al final:
```zsh
source ~/.zsh_user/.zsh_aliases
source ~/.zsh_user/.zsh_widgets
source ~/.zsh_user/.zsh_keybinds

if [ -f ~/.zsh_user/.zsh_local/.zsh_local ]; then
    source ~/.zsh_user/.zsh_local/.zsh_local
fi
```

---

### 4. Aplica los cambios
```bash
exec zsh
```
