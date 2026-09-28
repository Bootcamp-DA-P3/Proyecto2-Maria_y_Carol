# 🎬 Proyecto de Procesamiento y Limpieza de Datos: TMDB 5000 Movies

Este proyecto consiste en el procesamiento, limpieza y estructuración del dataset público de **TMDB 5000 Movies** utilizando Python y Pandas en Google Colab. El objetivo principal es transformar un conjunto de datos crudos con enlaces, metadatos irrelevantes y estructuras JSON complejas en un dataset limpio y listo para análisis de datos o proyectos de Machine Learning.

---

## 📁 Fuentes de Datos

El proyecto utiliza los datasets de Kaggle derivados de **The Movie Database (TMDB)**:
1. `tmdb_5000_movies.csv`: Contiene información sobre presupuestos, géneros, páginas web, fechas de estreno, ingresos, etc.
2. `tmdb_5000_credits.csv`: Contiene información sobre el reparto (*cast*) y el equipo de producción (*crew*).

Ambos archivos deben alojarse en Google Drive dentro de la carpeta:
`/content/drive/MyDrive/proyecto_datos/`

---

## 🛠️ Estructura del Pipeline de Limpieza

El proceso se divide en **dos partes fundamentales**:

```
[tmdb_5000_movies.csv] + [tmdb_5000_credits.csv]
                        │
                        ▼
            ┌───────────────────────┐
            │        PARTE 1        │
            │Unión, Fechas y Filtros│
            └───────────────────────┘
                        │
                        ▼
          [tmdb_estructurado_parte1.csv]
                        │
                        ▼
            ┌───────────────────────┐
            │        PARTE 2        │
            │  Parsing JSON/Listas  │
            └───────────────────────┘
                        │
                        ▼
            [tmdb_limpio_final.csv]
```

### 🔹 Parte 1: Integración, Depuración y Fechas
En esta primera fase se unifican las fuentes de datos y se realiza una limpieza estructural inicial:
* **Unión de fuentes:** Combinación de los DataFrames `movies` y `credits` haciendo uso del identificador único (`id` = `movie_id`).
* **Depuración de columnas:** Eliminación de campos no relevantes o con excesivos valores nulos (`homepage`, `tagline`, `status`).
* **Tratamiento de fechas:** 
  * Eliminación de registros sin fecha de estreno (`release_date`).
  * Conversión a formato `datetime` de Pandas.
  * Extracción del año de estreno en una nueva columna independiente (`release_year`).
* **Resultado intermedio:** Exportación de `tmdb_estructurado_parte1.csv`.

---

### 🔹 Parte 2: Parsing y Extracción de Estructuras Complejas
En la segunda fase se parsean los textos en formato JSON/literal para extraer información clave en listas legibles:
* **Extracción de atributos:**
  * `genres_list`: Extracción de la lista con los nombres de los géneros cinematográficos.
  * `keywords_list`: Extracción de las palabras clave asociadas a la película.
  * `top_cast`: Obtención de los **3 actores principales** del reparto.
  * `director`: Identificación y extracción del nombre del Director a partir del equipo técnico (`crew`).
* **Limpieza de columnas crudas:** Eliminación de los bloques de texto JSON originales (`genres`, `keywords`, `cast`, `crew`, `production_companies`, `production_countries`, `spoken_languages`).
* **Resultado final:** Exportación del dataset definitivo `tmdb_limpio_final.csv`.

---

## 🚀 Requisitos e Instalación

Para ejecutar este proyecto de manera local o en la nube necesitas:

* **Python 3.8+**
* **Librerías recomendadas:**
  * `pandas`
  * `json` / `ast`
* **Entorno:** Google Colab o Jupyter Notebook.

### Ejecución en Google Colab

1. Clona o sube el cuaderno/script a tu entorno de Google Colab.
2. Sube los archivos `tmdb_5000_movies.csv` y `tmdb_5000_credits.csv` a tu Google Drive en la carpeta `proyecto_datos`.
3. Monta tu unidad de Drive en el entorno:
   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   ```
4. Ejecuta el script de principio a fin para generar el dataset limpio.

---

## 👥 Trabajo Colaborativo

Este proyecto está diseñado para ser mantenido y actualizado en equipo a través de un repositorio centralizado de GitHub integrado con Google Colab.
