# 📐 Matemáticas Avanzadas — Actividades

Este repositorio es una colección de actividades prácticas y ejercicios resueltos para la asignatura de **Matemáticas Avanzadas**, diseñados para el primer semestre. El enfoque principal es el aprendizaje mediante visualizaciones interactivas y programación en Python.

Cada actividad del curso se guarda de forma independiente siguiendo esta lógica:

1.  Un **Jupyter Notebook** (`.ipynb`) con el desarrollo teórico y el código de los ejercicios.
2.  Una **carpeta de gráficas** dedicada donde se extraen todas las figuras generadas por el notebook.

## 📓 Actividades Disponibles

### 1. Series de Taylor

- **Archivo**: [`Series_Taylor_Actividad.ipynb`](Series_Taylor_Actividad.ipynb)
- **Carpeta de Gráficas**: `series_taylor_graficas/`
- **Contenido**:
  - Aproximación lineal de $\sin(x)$ con análisis de cota del error.
  - Implementación de la serie de Taylor para $e^{x^2}$.
  - Estudio comparativo de precisión entre diferentes métodos algebraicos de expansión.

### 2. Diferencias Finitas y Métodos Numéricos

- **Archivo**: [`Series_finitas_actividad_2.ipynb`](Series_finitas_actividad_2.ipynb)
- **Carpeta de Gráficas**: `diferencias_finitas_graficas/`
- **Contenido**:
  - Aproximación de $\cos(0.2)$ con polinomios de Taylor de 4to orden.
  - Derivación y verificación de fórmulas de diferencias finitas para derivadas.
  - Análisis del error de truncamiento $O(h^2)$ y $O(h)$ en esquemas forward y central.
  - Estudio del error máximo en la derivada numérica de $\cos(x)$ para distintos $h$.
  - Demostración de exactitud de la diferencia central para $f(x)=x^2$.

## 🚀 Instalación y Configuración (UV)

El proyecto utiliza [**uv**](https://github.com/astral-sh/uv), una herramienta de nueva generación para gestionar entornos virtuales de Python de forma rápida y eficiente.

### ¿Se debe crear el Kernel cada vez?

**No es necesario crear manualmente el kernel cada vez**, pero el entorno virtual (`.venv`) **no se exporta** (no se sube al repositorio) porque contiene archivos específicos de tu ordenador.

Para que el proyecto funcione en cualquier sitio, solo necesitas clonar los archivos de configuración (`pyproject.toml` y `uv.lock`) y recrear el entorno localmente una vez:

1.  Abre la terminal de **Visual Studio Code** en la carpeta raíz del proyecto.
2.  Ejecuta el siguiente comando para recrear el entorno y descargar todas las librerías:
    ```bash
    uv sync
    ```
    _Esto creará la carpeta `.venv` de forma local y todas las librerías necesarias._

## 🛠️ Cómo ejecutar en Visual Studio Code

1.  Abre el notebook de la actividad que desees (ej: [`Series_Taylor_Actividad.ipynb`](Series_Taylor_Actividad.ipynb)).
2.  En la esquina superior derecha del editor de VS Code, haz clic en **"Select Kernel"** (Seleccionar Kernel).
3.  Elige la opción **"Python Environments..."** y selecciona el kernel que apunta a tu carpeta **`.venv/bin/python`**.
4.  Ya puedes ejecutar todas las celdas del documento.

---

_Repositorio mantenido para las actividades del 1er semestre de Matemáticas Avanzadas._
