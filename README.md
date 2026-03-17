# 🏠 Predicción de Precios de Vivienda en México
### XGBoost + SHAP Explainability | Datos: Properati × Kaggle

[![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=flat&logo=python&logoColor=white)](https://python.org)
[![XGBoost](https://img.shields.io/badge/XGBoost-2.0-FF6600?style=flat)](https://xgboost.readthedocs.io)
[![SHAP](https://img.shields.io/badge/SHAP-Explainability-00A86B?style=flat)](https://shap.readthedocs.io)
[![Colab](https://img.shields.io/badge/Open_in_Colab-F9AB00?style=flat&logo=googlecolab&logoColor=white)](https://colab.research.google.com/drive/12lOqzVocDn1Onu8BZDHL4cRdxtEYZ5yc#scrollTo=8woYINfxQ7Qa)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## 🎯 Problema de negocio

El mercado hipotecario en México mueve más de **300,000 millones de pesos al año**
en crédito hipotecario (SHF, 2024). Sin embargo, la valuación de propiedades sigue
siendo un proceso opaco, lento y dependiente de peritos costosos.

**¿Puede un modelo de ML estimar el precio de una vivienda en México con precisión
y explicabilidad usando datos reales de portales inmobiliarios?**

Este proyecto demuestra que sí — con datos reales de Properati y un pipeline
completo de ciencia de datos.

---

## 📊 Resultados

| Métrica | Baseline | Optimizado |
|---------|----------|------------|
| R² | 0.7363 | 0.7395 |
| MAPE | 28.87% | 26.08% |
| MAE | $813,139 MXN | $755,120 MXN |
| RMSE | $1,470,405 MXN | $1,461,415 MXN |

### 💡 ¿Por qué un MAPE de 26% es un resultado honesto?

El dataset de Properati carece de variables clave como baños, estacionamientos
y antigüedad para la mayoría de registros — exactamente los datos que los portales
inmobiliarios mexicanos no publican consistentemente.

**Eso también es un insight de negocio**: la calidad del dato es el principal
cuello de botella en la valuación automatizada de vivienda en México.

---

## 🔍 Insights principales

1. 📍 **La ubicación es el predictor #1** — el target encoding de alcaldía
   supera a la superficie en importancia (SHAP values)
2. 📐 **Superficie y coordenadas GPS** son los features físicos más relevantes
3. 🏚️ **Benito Juárez lidera en volumen** con 4,683 propiedades del dataset
4. 💰 **Precio mediano real: $2.08M MXN** — mercado medio-residencial CDMX
5. 🔴 **El segmento Premium (>6M)** tiene el mayor error de predicción —
   los inmuebles de lujo tienen variables intangibles que los datos no capturan

---

## 🗂️ Estructura del proyecto

mexico-housing-price-prediction/
│
├── 📓 mexico_housing_price_prediction.ipynb  # Notebook principal
├── 🖼️  P1.png                  
├── 🖼️  P2-2.png                    
├── 🗺️  P1-4.html            
└── 📄 README.md


---

## ⚙️ Stack tecnológico

| Herramienta | Uso |
|---|---|
| **Python 3.11** | Lenguaje base |
| **Pandas / NumPy** | Limpieza y transformación |
| **XGBoost** | Modelo predictivo principal |
| **Scikit-learn** | Preprocessing, métricas, RandomizedSearchCV |
| **SHAP** | Explainability — ¿por qué este precio? |
| **Plotly** | Visualizaciones interactivas |
| **Folium** | Heatmap geoespacial CDMX |
| **Google Sheets** | Almacenamiento de resultados |
| **Looker Studio** | Dashboard ejecutivo |

---

## 🚀 Cómo ejecutar

### En Google Colab (recomendado)
1. Abre el badge de Colab arriba ↑
2. Necesitas cuenta de Kaggle para descargar los datos
3. Ejecuta todas las celdas en orden

### Datos
- **Fuente:** [Mexico City Real Estate Dataset — Kaggle](https://www.kaggle.com/datasets/allankirwa/mexico-city-real-estate-dataset)
- **Proveedor original:** Properati
- **Registros después de limpieza:** ~17,000 propiedades
- **Cobertura:** Ciudad de México y área metropolitana

---

## 📐 Pipeline del proyecto

Datos reales Properati (Kaggle)
       ↓
  Limpieza y unión de 5 archivos CSV
  • Filtro: solo ventas en MXN
  • Imputación de superficie (covered + total)
  • Imputación de recámaras por tipo de inmueble
       ↓
  EDA + Visualizaciones (Plotly + Folium)
  • Distribución de precios por alcaldía
  • Mapa de calor geoespacial CDMX
  • Scatter precio vs superficie
       ↓
  Feature Engineering
  • Target encoding de ubicación (sin data leakage)
  • Ratio baños/recámaras
  • Features geoespaciales (lat, lon, flag CDMX)
       ↓
  XGBoost Baseline → R²=0.74, MAPE=28.87%
       ↓
  RandomizedSearchCV (30 iteraciones, CV=3)
       ↓
  Modelo optimizado → R²=0.74, MAPE=26.08%
       ↓
  SHAP: importancia global + force plots
       ↓
  Exportación → Google Sheets → Looker Studio


---

## 📈 Dashboard en Looker Studio

[🔗 Ver dashboard en vivo](https://lookerstudio.google.com/reporting/16fc6b33-e15a-4478-ab02-413b49756e63)

El dashboard incluye:
- KPIs: R², MAPE, precio mediano, total propiedades
- Precio mediano por alcaldía
- Distribución por segmento de precio
- Scatter: precio real vs predicho
- Error % por tipo de inmueble
- Precio por m² por ubicación
- Filtro global por segmento

---

## 🤖 Nota sobre el uso de IA

Este proyecto fue desarrollado con **Claude (Anthropic)** como asistente técnico:
- Generación y depuración del pipeline completo
- Troubleshooting de datos reales (superficie, recámaras, encoding)
- Documentación y estructura del README

Las decisiones clave fueron del autor: interpretación de resultados,
selección de features, análisis de insights de negocio y validación
del modelo contra datos reales.

---

## 📚 Fuentes

- [Mexico City Real Estate Dataset — Kaggle](https://www.kaggle.com/datasets/allankirwa/mexico-city-real-estate-dataset)
- [Índice SHF de Precios de la Vivienda](https://transparencia.shf.gob.mx/sitepages/IndicePV.aspx)
- [SHAP: A Unified Approach to Interpreting Model Predictions](https://arxiv.org/abs/1705.07874)
- [Portal de Datos Abiertos CDMX](https://datos.cdmx.gob.mx)

---

## 👤 Autor

**Jorge Francisco Velázquez Mirabal**
Data Scientist | Analista de Datos
📍 Tlaxcala, México

[![LinkedIn](https://www.linkedin.com/in/jorgevelazquezdata/)
[![GitHub](https://github.com/PatoTlax)

---

*Si este proyecto te fue útil, dale ⭐ al repo.*
