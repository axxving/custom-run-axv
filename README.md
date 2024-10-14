# Guía de configuración y ejecución de scripts

Este proyecto incluye scripts para abrir dos terminales de forma automática, cada una ejecutando un proceso necesario:
- **El servidor de desarrollo de Django**.
- **El entorno de desarrollo de Node.js utilizando `npm run dev`**.

## Configuración y ejecución en Windows

### Requisitos previos:
- **Python** y un entorno virtual deben estar configurados correctamente.
- **Node.js** debe estar instalado y el proyecto debe tener un script definido como `npm run dev`.

### Pasos:
1. **Crea un archivo `.bat`** en la raíz del proyecto (por ejemplo, `iniciar_proyectos.bat`).

2. **Contenido del archivo**:

    ```batch
    @echo off
    
    REM Activar el entorno virtual de Python y ejecutar el servidor de Django
    start cmd.exe /k "cd {ruta-al-directorio-del-entorno-virtual} && envTADV\Scripts\activate.bat && cd {ruta-al-directorio-django} && python manage.py runserver"
    
    REM Iniciar npm run dev en otra ventana
    start cmd.exe /k "cd {ruta-al-directorio-del-proyecto-node} && npm run dev"
    ```

3. **Explicación del archivo**:
    - **`{ruta-al-directorio-del-entorno-virtual}`**: Reemplaza esta ruta con la ubicación de tu entorno virtual de Python.
    - **`{ruta-al-directorio-django}`**: La ubicación donde se encuentra el archivo `manage.py` de tu proyecto Django.
    - **`{ruta-al-directorio-del-proyecto-node}`**: La ubicación del directorio raíz de tu proyecto Node.js, donde se encuentra el archivo `package.json`.
    
    Este script abrirá dos ventanas de `cmd.exe`. Una ejecutará el servidor de Django tras activar el entorno virtual, y la otra iniciará el entorno de desarrollo de Node.js con `npm run dev`.

4. **Ejecución**:
    - Guarda el archivo `.bat` y ejecútalo con doble clic. Las dos ventanas de terminal se abrirán y los procesos se ejecutarán de forma paralela.

---

## Configuración y ejecución en macOS

### Requisitos previos:
- **Python** y un entorno virtual deben estar configurados correctamente.
- **Node.js** debe estar instalado y el proyecto debe tener un script definido como `npm run dev`.

### Pasos:
1. **Crea un archivo bash** (por ejemplo, `iniciar_proyectos.sh`).

2. **Contenido del archivo**:

    ```bash
    #!/bin/bash

    # Abrir nueva ventana para ejecutar npm run dev
    osascript -e 'tell application "Terminal" to do script "cd {ruta-al-directorio-del-proyecto-node} && npm run dev"'

    # Abrir nueva ventana para activar el entorno virtual y ejecutar Django
    osascript -e 'tell application "Terminal" to do script "cd {ruta-al-directorio-del-entorno-virtual} && source envTADV/bin/activate && cd {ruta-al-directorio-django} && python manage.py runserver"'
    ```

3. **Explicación del archivo**:
    - **`{ruta-al-directorio-del-proyecto-node}`**: Reemplaza con la ubicación del directorio raíz de tu proyecto Node.js.
    - **`{ruta-al-directorio-del-entorno-virtual}`**: Reemplaza con la ubicación de tu entorno virtual de Python.
    - **`{ruta-al-directorio-django}`**: La ubicación del directorio donde se encuentra `manage.py` en tu proyecto Django.
    
    Este script abrirá dos nuevas ventanas en la terminal de macOS. Una ejecutará `npm run dev` y la otra activará el entorno virtual de Python y ejecutará el servidor de Django.

4. **Hacer el archivo ejecutable**:
    - Navega a la carpeta donde guardaste el script y ejecuta el siguiente comando en la terminal:

      ```bash
      chmod +x iniciar_proyectos.sh
      ```

5. **Ejecución**:
    - Ejecuta el script con el siguiente comando en la terminal:

      ```bash
      ./iniciar_proyectos.sh
      ```

---

## Notas adicionales:
- **Entorno virtual**: Asegúrate de que el entorno virtual esté correctamente configurado y que el comando para activarlo funcione adecuadamente (en Windows, `activate.bat`, en macOS, `source bin/activate`).
- **npm run dev**: Verifica que el archivo `package.json` de tu proyecto de Node.js esté configurado correctamente con el script de desarrollo adecuado, normalmente bajo `"scripts": { "dev": "tu-comando" }`.
