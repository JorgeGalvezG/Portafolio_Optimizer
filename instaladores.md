# 🛠️ Guía de Instalación Local y Despliegue en la Nube

Esta guía detalla el proceso paso a paso para configurar el entorno de desarrollo local mediante la terminal de Windows (`winget`) y el proceso de despliegue oficial requerido por la especificación del curso.

---

## 💻 1. Instalación y Configuración Local por Terminal

Sigue estos comandos ordenadamente desde la terminal de tu sistema o de IntelliJ (`Alt + F12`):

### Paso 1: Instalar Python 3.11 con Winget
Ejecuta el siguiente comando para descargar e instalar Python de manera automática:
```powershell
winget install Python.Python.3.11
```
> [!IMPORTANT]
> Una vez finalizada la instalación de Python, **reinicia tu terminal** o el IDE para que se actualicen las variables de entorno del sistema y reconozca los nuevos comandos.

### Paso 2: Crear el Entorno Virtual (`venv`)
Crea un entorno de ejecución aislado en la raíz de tu proyecto ejecutando:
```powershell
python -m venv venv
```

### Paso 3: Activar el Entorno Virtual
Para activar el entorno según tu terminal en Windows:

* **En PowerShell (Terminal por defecto en IntelliJ):**
  ```powershell
  .\venv\Scripts\Activate.ps1
  ```
  *Nota: Si PowerShell te arroja un error de directiva de ejecución (Execution Policy), ejecuta primero `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process` y luego vuelve a intentar la activación.*

* **En Command Prompt (CMD):**
  ```cmd
  .\venv\Scripts\activate.bat
  ```

*(Sabrás que el entorno está activo porque verás el prefijo `(venv)` al inicio de la línea de comandos).*

### Paso 4: Instalar Dependencias
Instala todas las librerías necesarias especificadas en `requirements.txt`:
```powershell
pip install -r requirements.txt
```

### Paso 5: Ejecutar la Aplicación
Corre el servidor de desarrollo local de Streamlit para probar el sistema:
```powershell
streamlit run app.py
```

---

## ☁️ 2. Guía de Despliegue en la Nube (GitHub + Streamlit Cloud)

> [!WARNING]
> **Nota sobre Vercel:** Vercel está diseñado para sitios web estáticos y funciones Serverless (stateless). Como **Streamlit** es una aplicación con estado persistente basada en conexiones continuas por **WebSockets**, no se puede desplegar directamente de forma nativa en Vercel. 
> Además, **el profesor califica específicamente el despliegue en Streamlit Community Cloud (URL con formato `.streamlit.app`), lo cual equivale al 15% de tu nota final.**

Sigue estos pasos para subir tu código a GitHub y desplegarlo en la nube calificada:

### Fase A: Subir el Código a GitHub (Por Terminal)

1. **Inicializar el repositorio local:**
   ```powershell
   git init
   ```
2. **Crear archivo `.gitignore`:**
   Crea un archivo `.gitignore` para evitar subir carpetas temporales pesadas e innecesarias (como el entorno virtual o configuraciones del IDE). Ejecuta en terminal:
   ```powershell
   echo "venv/" >> .gitignore
   echo ".idea/" >> .gitignore
   echo "__pycache__/" >> .gitignore
   echo ".streamlit/config.toml" >> .gitignore
   ```
3. **Agregar archivos y hacer el primer commit:**
   ```powershell
   git add .
   git commit -m "feat: setup inicial del optimizador de portafolios"
   ```
4. **Vincular con tu repositorio remoto de GitHub:**
   Crea un repositorio público vacío en tu cuenta de GitHub y vincúlalo ejecutando (reemplaza con tu URL):
   ```powershell
   git branch -M main
   git remote add origin https://github.com/TU_USUARIO/TU_REPOSITORIO.git
   git push -u origin main
   ```

---

### Fase B: Desplegar en Streamlit Community Cloud

Una vez subido a GitHub, realiza el despliegue en la nube gratuita de Streamlit:

1. Ingresa a **[Streamlit Share / Community Cloud](https://share.streamlit.io/)**.
2. Regístrate o inicia sesión vinculando tu cuenta de **GitHub**.
3. En tu panel de control de Streamlit Cloud, haz clic en el botón **"Create app"** (o **"New app"**).
4. Configura los campos del formulario:
   * **Repository:** Selecciona tu repositorio de GitHub recién subido.
   * **Branch:** Selecciona `main`.
   * **Main file path:** Escribe `app.py`.
5. Haz clic en el botón **"Deploy!"**.
6. Streamlit Cloud leerá el archivo [requirements.txt](file:///D:/Tareas_momentaneas/Ciclo%205/ADA/portfolio_optimizer/requirements.txt), instalará todas las dependencias y levantará el servidor automáticamente.
7. Copia la URL pública resultante para incluirla en el informe Word de entrega del curso (la URL oficial del Grupo 1 es: [https://grupo1-optimizador-portafolio.streamlit.app/](https://grupo1-optimizador-portafolio.streamlit.app/)).
