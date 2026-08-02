# Quick Start

## About 

Este repositorio es un fork del firmware que usan los teclados keychron que a su vez es un fork del repositorio del firmware QMK.

 - https://github.com/qmk/qmk_firmware 
 - https://github.com/Keychron/qmk_firmware


### QMK y VIA

QMK es el firmware open source para teclados de todo tipo.
VIA es un protocolo/apilicacion que facilita la configuración de teclados compatibles con QMK sin necesidad de recompilar ni volver a flashear el firmware.

###  Apps VIA online para chrome

 - https://launcher.keychron.com/ Aplicación VIA de keychron
 - https://usevia.app/ Aplicación VIA alternativa


## Work Guide

### Clonado del repositorio

El repositorio usa varios submodules así que habrá que clonarlo de forma que los instale. 
```sh
git clone --recurse-submodules -j4 https://github.com/Keychron/qmk_firmware.git
```

###  Keyboards y Keymaps

En el directorio `keyboards/` están todos los teclados disponibles y para cada uno, se pueden compilar diferentes keymaps (ubicados en el directorio `keymaps/` dentro del keyboard). Cuando los comandos te piden indicar un keyboard, se hace con el path relativo desde el directorio keyboards, mientas que para el keymap, sólo hay que indicar el nombre. 

Por ejemplo en mi caso:
  - Keyboard: `keychron/v1/iso_encoder` (teclado v1 iso con knob de volumen)
  - Keymap: `keychron`  (firmware por defecto de keychron con VIA activado)

### Compilar y flashear

#### Environment

Hay una guía para instalar todas las dependencias del repositorio (https://docs.qmk.fm/newbs_getting_started). 

Los pasos te guían para instalar:
  - Toolchain necesaria para trabajar (git, build-essential clang-format, clang, ...)
  - Comando CLI `qmk` a través del gestor de paquetes python uv.
  - Utilidades de flasheo
  - Reglas udev para manejar el dispositivo usb
  
**Build and flash**
```
 qmk compile -kb keychron/v1/iso_encoder -km keychron
 qmk flash   -kb keychron/v1/iso_encoder -km keychron
```

#### Docker
 
Sin embargo, la forma más sencilla de trabajar es directamente compilando y flasheando con la imagen docker proporcionada: https://docs.qmk.fm/getting_started_docker

🔨 **Build**:
```
util/docker_build.sh <keyboard>:<keymap>
# For example: util/docker_build.sh keychron/v1/iso_encoder:keychron
```

⚡️ **Flash**:
```
util/docker_build.sh keyboard:keymap:target
# For example: util/docker_build.sh keychron/v1/iso_encoder:keychron:flash
```

## Flasheo

En el momento de flasehar hay que poner el teclado en modo DFU STM32: 
 - Desconectar el teclado con `ESC` pulsado y reconectarlo mientas se mantiene `ESC` pulsado
 
 
 ## Windows
 
 Para windows existe un toolbox gráfico ejecutable que permite flashear el teclado
   - https://github.com/qmk/qmk_toolbox 
   