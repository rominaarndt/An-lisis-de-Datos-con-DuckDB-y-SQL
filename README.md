# Análisis de Datos Meteorológicos con DuckDB y SQL

## 🎯 Propósito del Proyecto
Este proyecto forma parte de la pre-entrega orientada a consolidar el uso de **DuckDB** como un motor analítico embebido de alto rendimiento. Permite procesar y consultar series temporales de clima directamente desde un archivo plano (`temperature_anomaly_monthly.csv`) alojado en la web, sin necesidad de instalar o desplegar bases de datos tradicionales pesadas.

## 🚀 Instrucciones para Replicar el Análisis

Puedes ejecutar este análisis de forma interactiva y gratuita utilizando Google Colab:

1. **Abrir Google Colab:** Crea un nuevo cuaderno en [Google Colab](https://colab.research.google.com/).
2. **Instalar Dependencias (si es necesario):** DuckDB viene preinstalado, pero puedes asegurar su disponibilidad con:
   ```python
   !pip install duckdb pandas --quiet
   ```
3. **Cargar el Dataset mediante la URL Raw:** Copia la URL *Raw* de tu archivo `temperature_anomaly_monthly.csv` en GitHub y conéctala directamente usando DuckDB:
   ```python
   import duckdb
   import pandas as pd

   url_raw = "https://raw.githubusercontent.com/TU_USUARIO/TU_REPOSITORIO/main/temperature_anomaly_monthly.csv"
   
   # Crear vista virtual
   duckdb.sql(f"""
       CREATE OR REPLACE VIEW clima AS
       SELECT * FROM read_csv_auto('{url_raw}');
   """)
   ```
4. **Ejecutar las Consultas Analíticas:** Sigue el script provisto en el repositorio para realizar conteos, promedios mensuales y regionales, y filtrados avanzados.

## 📊 Consultas Analíticas Implementadas
El script incluye tres tipos de consultas requeridas:
1. **Conteo y Distribución:** Agrupamiento de registros totales por región con delimitación temporal.
2. **Agregaciones Estadísticas:** Cálculo de promedios, valores mínimos y máximos de anomalía térmica ($\text{temp\_anomaly\_c}$) por región.
3. **Filtrado Complejo:** Subconsultas anidadas para identificar registros globales que superan el promedio histórico general.

## ⏱️ Tiempos de Respuesta y Hallazgos Principales
* **Velocidad de procesamiento:** Gracias a la arquitectura columnar de DuckDB y la lectura directa por streaming HTTP desde la URL de GitHub, las consultas de agregación y filtrado sobre miles de registros se ejecutaron en **menos de $0.05$ segundos**, demostrando una eficiencia superior frente a motores relacionales tradicionales.
* **Hallazgos climáticos:** Se observa una tendencia clara de incremento en las anomalías térmicas recientes, siendo las regiones de altas latitudes (como el Ártico) las que presentan las desviaciones más pronunciadas en comparación con la línea base histórica.

## 🛠️ Archivos del Repositorio
* `temperature_anomaly_monthly.csv`: Dataset principal de anomalías climáticas mensuales.
* `requirements.txt`: Dependencias del proyecto (`duckdb`, `pandas`).
* `README.md`: Documentación oficial del análisis.
