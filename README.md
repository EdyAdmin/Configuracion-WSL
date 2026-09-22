# Configuración modular para ZSH (WSL / Ubuntu)

Configuración modular optimizada para Zsh orientada a desarrollo y productividad en entornos WSL/Linux. Transforma la línea de comandos integrando comportamiento interactivo moderno (estilo editor gráfico), atajos avanzados de edición y separación estricta entre configuraciones portables y rutas privadas del sistema.

---

## 📌 Módulos y funcionalidades añadidas

Esta configuración reorganiza la terminal en submódulos independientes ubicados en `~/.zsh_user/`. Tengo implementada una funcionalidad similar al seleccionado con shift + flechas de PowerShell y tengo instalados GHC (para Haskell), Bat y AstroNvim. También tengo puestos algunos aliases y plugins interesantes.

### 1. Arquitectura modular
* **`.zsh_aliases`**: Centraliza los atajos de comandos habituales (`c` para clear, utilidades de terminal como `bat`).
* **`.zsh_widgets`**: Contiene funciones y widgets propios programados para el subsistema interactivo de Zsh (ZLE - Zsh Line Editor).
* **`.zsh_keybinds`**: Mapeo completo de secuencias de escape y atajos de teclado.
* **Aislamiento local (`.zsh_local/`)**: Directorio protegido mediante `.gitignore`. Permite definir rutas personales (unidades montadas como Google Drive, particiones Windows o credenciales) sin exponerlas al subir los dotfiles a GitHub.

### 2. Selección Interactiva de Texto (Estilo GUI)
A través del plugin `zsh-shift-select` y la integración en `.zsh_keybinds`, la terminal adopta la edición de texto estándar:
* **`Shift + Flechas (Izquierda / Derecha)`**: Selecciona caracteres continuos directamente sobre la línea de comandos.
* **`Ctrl + Shift + Flechas (Izquierda / Derecha)`**: Selecciona palabras completas hacia adelante o hacia atrás.
* Sustitución y borrado automático al escribir o pulsar retroceso sobre texto seleccionado.

### 3. Navegación y Edición Ágil
* Integración fluida con editores modulares (como Neovim / AstroNvim) para manipular líneas sin salir del flujo de trabajo.
* **Atajo `reload`**: Ejecuta `daemon-reload`, remonta puntos de almacenamiento definidos en `/etc/fstab` y reinicia una sesión de Zsh completamente limpia (`exec zsh`) para aplicar cambios al vuelo sin acumular variables redundantes en memoria.

---

## 🛠️ PARTE 2: Guía de Instalación Paso a Paso

Sigue estos pasos en cualquier máquina nueva (o tras clonar el sistema) para desplegar el entorno completo con todas sus dependencias.

### Paso 1: Requisitos previos (Zsh y Oh My Zsh)
Asegúrate de contar con Zsh y el framework Oh My Zsh instalados:

```bash
# Instalar Zsh y utilidades base (en Ubuntu/Debian)
sudo apt update && sudo apt install -y zsh git curl

# Instalar Oh My Zsh (si no lo tienes aún)
sh -c "$(curl -fsSL [https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh](https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh))"
```
