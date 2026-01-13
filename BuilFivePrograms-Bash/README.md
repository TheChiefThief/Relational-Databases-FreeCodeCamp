# 🐚 Bash Mastery: The Ultimate Shell Manual

![Bash Logo](https://img.shields.io/badge/Shell-Bash-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-success?style=for-the-badge)

Una guía exhaustiva y estética para dominar la terminal de Linux/Unix. Desde los conceptos básicos de navegación hasta la automatización con scripts complejos.

---

## 📑 Tabla de Contenidos
- [Navegación Básica](#-1-navegación-y-gestión-de-archivos)
- [Manipulación de Texto](#-2-visualización-y-edición)
- [Permisos y Seguridad](#-3-permisos-de-archivo)
- [Redirecciones y Pipes](#-4-tuberías-y-redirección-pipes)
- [Scripting Avanzado](#-5-scripting-y-automatización)
- [Atajos de Teclado](#-6-atajos-pro-tips)

---

## 📂 1. Navegación y Gestión de Archivos

| Comando | Acción | Ejemplo |
| :--- | :--- | :--- |
| `pwd` | Muestra la ruta actual | `pwd` |
| `ls -la` | Lista archivos (incluyendo ocultos) | `ls -la` |
| `cd ..` | Sube un nivel de carpeta | `cd ..` |
| `mkdir -p` | Crea carpetas anidadas | `mkdir -p src/assets/img` |
| `touch` | Crea un archivo vacío | `touch index.html` |
| `rm -rf` | Elimina recursivamente (¡Cuidado!) | `rm -rf carpeta_vieja/` |
| `cp -r` | Copia directorios | `cp -r original/ copia/` |
| `mv` | Mueve o renombra | `mv file.txt new_name.txt` |

---

## 🔍 2. Visualización y Edición

* **`cat <archivo>`**: Vuelca el contenido completo en la terminal.
* **`less`**: Abre un visor interactivo (ideal para archivos grandes).
* **`head` / `tail`**: Mira el principio o el final (usa `-f` en tail para seguir logs en vivo).
* **`grep`**: El buscador universal.
    * *Ejemplo:* `grep "error" server.log`
* **`find`**: Busca archivos por nombre o extensión.
    * *Ejemplo:* `find . -name "*.js"`

---

## 🛡️ 3. Permisos de Archivo

El sistema de permisos se basa en tres grupos: **Dueño (u)**, **Grupo (g)** y **Otros (o)**.

| Valor | Permiso | Letra |
| :--- | :--- | :--- |
| **4** | Lectura | `r` |
| **2** | Escritura | `w` |
| **1** | Ejecución | `x` |

> [!TIP]
> **Comando rápido:** `chmod +x script.sh` (Hace que un archivo sea ejecutable).

---

## 🚀 4. Tuberías y Redirección (Pipes)

Conecta la salida de un programa con la entrada de otro.

* `>` : Sobrescribe archivo.
* `>>` : Añade al final del archivo.
* `|` : Envía la salida al siguiente comando.
* `2> /dev/null` : Silencia los errores.

---

## 🤖 5. Scripting y Automatización

Todo script debe empezar con el shebang: `#!/bin/bash`.

### Estructura de un Script
```bash
#!/bin/bash

# Declaración de variables
USER_NAME="Admin"
DATE=$(date +%D)

echo "Iniciando sesión como $USER_NAME el día $DATE"

# Condicionales
if [ -f "config.txt" ]; then
    echo "Archivo de configuración encontrado."
else
    echo "Error: Configuración ausente."
    exit 1
fi

# Bucles (Loop)
for i in {1..5}; do
    echo "Intento número $i"
done
