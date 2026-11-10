# 🚦 Movilidad Urbana y Productividad Económica en Ciudades Latinoamericanas

Análisis de datos que explora la relación entre la **congestión vehicular** (TomTom Traffic Index) y la **productividad económica** (OECD Cities) en las principales ciudades de Latinoamérica durante 2024, con el fin de identificar en qué ciudades conviene priorizar la inversión en infraestructura de transporte.

![Python](https://img.shields.io/badge/Python-3.9-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-data%20wrangling-150458?logo=pandas&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-visualization-4c72b0)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)

---

## 📌 Pregunta de negocio

> ¿Qué relación existe entre la movilidad urbana (congestión y tiempos de viaje) y la productividad económica (PIB per cápita)? ¿Qué ciudad es prioritaria para invertir en infraestructura de transporte?

## 📂 Datos

| Dataset | Fuente | Contenido | Tamaño |
|---|---|---|---|
| `tomtom_traffic.csv` | TomTom Traffic Index | Congestión, longitud de embotellamientos, tiempos de viaje y retrasos por ciudad (registros en tiempo real) | ~1,004,464 filas × 12 columnas |
| `oecd_city_economy.csv` | OECD Cities | PIB per cápita, desempleo, PM2.5 y población por ciudad y año | 30 filas × 7 columnas |

**Dataset final:** `ladb_mobility_economy_2024_clean.csv`, con una fila por ciudad para 2024 y variables de tráfico y economía integradas.

## 🛠️ Metodología

1. **Carga y exploración:** revisión de estructura, tipos de datos y valores nulos con `.info()` y `.head()`.
2. **Estandarización:** renombrado de columnas a `snake_case` en ambos datasets.
3. **Limpieza de formatos:**
   - Conversión de fechas a `datetime` (con `errors='coerce'` para evitar fallos).
   - Limpieza de formatos numéricos europeos en `eco` (separador de miles `.` y decimal `,`), eliminación del símbolo `%` y creación de la columna `population` en unidades absolutas.
4. **Filtrado temporal:** extracción del año con `.dt.year` y filtrado del período **2024**.
5. **Agregación:** promedios de las métricas de tráfico por `city`, `country` y `year` con `groupby` + `agg`.
6. **Integración:** `merge` tipo **inner** entre tráfico y economía usando `city` y `year` como claves.
7. **Visualización:** boxplot de `jams_delay`, histograma de `city_gdp_capita` y gráfico de barras comparativo por ciudad.
8. **Exportación:** guardado del dataset limpio en CSV (`index=False`).

## 📊 Hallazgos principales

- **No hay una relación lineal clara** entre el PIB per cápita y la congestión: el nivel de riqueza por sí solo no explica el tráfico.
- Las ciudades más congestionadas (**Ciudad de México, São Paulo, Bogotá**) son megaciudades de alta densidad y gran extensión urbana, lo que sugiere que factores como población, infraestructura vial y tasa de motorización pesan más.
- Ciudades con PIB per cápita alto, como **Buenos Aires** y **Montevideo**, presentan niveles de congestión comparativamente bajos.
- **Bogotá** destaca como caso relevante: combina un PIB per cápita relativamente bajo con congestión considerablemente alta.
- En el conjunto global de ciudades, **Ciudad de México** registra el mayor `jams_delay` promedio en 2024.

## ✅ Recomendaciones

- **Priorizar a Bogotá** para un análisis más profundo de inversión en infraestructura de transporte.
- Validar la relación con un **análisis de correlación estadística** (Pearson o Spearman) antes de decidir.
- Incorporar variables adicionales: desempleo, densidad poblacional y contaminación (PM2.5).
- **Ampliar la cobertura temporal** más allá de 2024 para confirmar que el patrón se mantiene.

## 📁 Estructura del repositorio

```
├── everpeak_analysis.ipynb                  # Notebook con todo el análisis
├── ladb_mobility_economy_2024_clean.csv     # Dataset final limpio
├── datasets/
│   ├── tomtom_traffic.csv                   # Datos originales de tráfico
│   └── oecd_city_economy.csv                # Datos originales de economía
└── README.md
```

## 🚀 Cómo reproducirlo

```bash
# 1. Clonar el repositorio
git clone https://github.com/<tu-usuario>/<tu-repositorio>.git
cd <tu-repositorio>

# 2. Instalar dependencias
pip install pandas numpy seaborn matplotlib jupyter

# 3. Abrir el notebook
jupyter notebook everpeak_analysis.ipynb
```

> **Nota:** el notebook lee los datos desde `/datasets/`. Si lo ejecutas en local, ajusta las rutas en la celda de carga según la ubicación de tus archivos.

## 🧰 Librerías utilizadas

`pandas` · `numpy` · `seaborn` · `matplotlib`

## 👤 Autor

**Edinson**
Proyecto de análisis de datos desarrollado como parte de un bootcamp de Data Analytics.

---

⭐ Si te resultó útil, ¡déjale una estrella al repositorio!
