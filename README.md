# 🔧 Predicción de Vida Útil de Motores — Mantenimiento Predictivo

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.x-orange?logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-2.x-red?logo=xgboost&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completado-brightgreen)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## 📋 Descripción del Proyecto

Este proyecto aplica técnicas de **Machine Learning** para predecir la **Vida Útil Restante (RUL — Remaining Useful Life)** de motores turbofan a partir de datos históricos de sensores operacionales.

El enfoque está orientado a entornos industriales reales, donde anticipar fallas permite:
- Reducir hasta un **30% los costos operativos**
- Eliminar **paradas no planificadas**
- Optimizar la toma de decisiones en mantenimiento

> 💡 A futuro, esta metodología será adaptada a la predicción de vida útil de **baterías UPS** en entornos industriales críticos.

---

## 📦 Dataset

| Campo | Detalle |
|---|---|
| **Nombre** | NASA Turbofan Jet Engine Data Set (FD001) |
| **Origen** | [Kaggle — NASA CMAPS](https://www.kaggle.com/datasets/behrad3d/nasa-cmaps) |
| **Tipo de problema** | Regresión continua |
| **Registros** | 20.631 |
| **Motores simulados** | 100 |
| **Sensores** | 21 |
| **Configuraciones operativas** | 3 |

---

## 🎯 Objetivos

### General
Desarrollar un modelo que estime la vida útil restante de motores a partir de datos de sensores, con el fin de anticipar fallas y optimizar el mantenimiento.

### Específicos
- Analizar el comportamiento de los sensores a lo largo del tiempo
- Detectar patrones asociados a la degradación de los motores
- Identificar variables relevantes para la predicción
- Construir la variable objetivo (`vida_util`)
- Entrenar y comparar modelos de Machine Learning

---

## 🗂️ Estructura del Dataset

```
train_FD001.txt
│
├── motor_id               → Identificador del motor
├── ciclo                  → Ciclo de operación acumulado
├── configuracion_operativa_1, _2, _3  → Condiciones de trabajo
└── sensor_1 ... sensor_21 → Mediciones internas del motor
```

### Variable Objetivo

```python
vida_util = ciclo_max - ciclo_actual
```

Representa los ciclos restantes hasta la falla del motor.

---

## 🔄 Pipeline del Proyecto

```
Carga de datos → Limpieza → Ingeniería de variables → EDA → Modelado → Evaluación
```

### 1. Data Wrangling
- Carga desde archivo `.txt` con separador de espacios múltiples
- Asignación manual de nombres de columnas
- Eliminación de columnas vacías y sin variabilidad (constantes)
- Sin valores nulos detectados en el dataset
- Outliers conservados: representan condiciones reales de desgaste

### 2. Ingeniería de Variables
- Cálculo de `ciclo_max` por motor (momento de falla)
- Creación de `vida_util` como variable objetivo
- Separación de features (`X`) y target (`y`)
- Escalado con `StandardScaler` para regresión lineal

---

## 📊 Análisis Exploratorio (EDA)

### Hallazgos Clave

| # | Hallazgo |
|---|---|
| 1 | La vida útil **disminuye progresivamente** con el número de ciclos |
| 2 | Ciertos sensores muestran **variaciones sistemáticas** previas a la falla |
| 3 | Existen sensores con **alta correlación** con la vida útil restante |
| 4 | Los patrones de desgaste se **repiten entre motores**, permitiendo generalizar |

### Top Sensores Correlacionados con `vida_util`

| Sensor | Correlación |
|---|---|
| sensor_11 | -0.847 |
| sensor_4  | -0.821 |
| sensor_12 | -0.813 |
| sensor_15 | +0.798 |
| sensor_7  | -0.771 |

---

## 🤖 Modelos de Machine Learning

Se entrenaron y compararon 4 modelos de regresión:

| Modelo | Descripción |
|---|---|
| **Regresión Lineal** | Modelo baseline, relaciones lineales |
| **Random Forest** | 100 árboles, relaciones no lineales |
| **Random Forest Optimizado** | GridSearchCV con cv=3 folds |
| **XGBoost** | Gradient Boosting, 200 estimadores, lr=0.05 |

### Configuración del Split

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

### Optimización de Hiperparámetros (GridSearchCV)

```python
parametros = {
    'n_estimators': [100, 150],
    'max_depth': [10, 20],
    'min_samples_split': [2, 5]
}
```

---

## 📈 Resultados

| Modelo | RMSE ↓ | MAE ↓ | R² ↑ |
|---|---|---|---|
| Regresión Lineal | 39.70 | 30.54 | 0.655 |
| Random Forest | 35.93 | 25.45 | 0.717 |
| **Random Forest Optimizado** | **35.62** | **25.27** | **0.722** |
| XGBoost | 35.64 | 25.37 | 0.722 |

### 🏆 Mejor Modelo: Random Forest Optimizado

```
RMSE : 35.62
MAE  : 25.27
R²   : 0.722  →  Explica el 72% de la variabilidad de la vida útil
```

### Validación Cruzada (5-Fold)

| Fold | R² |
|---|---|
| Fold 1 | 0.710 |
| Fold 2 | 0.730 |
| Fold 3 | 0.720 |
| Fold 4 | 0.710 |
| Fold 5 | 0.740 |
| **Promedio** | **0.722** |

> Resultados estables entre folds (σ < 0.015) — sin señales de sobreajuste.

---

## 🔍 Importancia de Variables

| Variable | Importancia |
|---|---|
| ciclo | 38% |
| sensor_11 | 18% |
| sensor_4 | 13% |
| sensor_12 | 9% |
| sensor_15 | 7% |
| sensor_7 | 5% |

> El ciclo acumulado y los sensores de temperatura y presión son los predictores más relevantes.

---

## 🧰 Tecnologías Utilizadas

```python
# Análisis y manipulación
pandas
numpy

# Visualización
matplotlib
seaborn

# Machine Learning
scikit-learn   # LinearRegression, RandomForestRegressor, GridSearchCV, métricas
xgboost        # XGBRegressor
```

---

## 📁 Estructura del Repositorio

```
📦 proyecto-mantenimiento-predictivo
 ┣ 📓 notebook.ipynb          → Análisis completo y modelos
 ┣ 📄 train_FD001.txt         → Dataset NASA Turbofan
 ┣ 📊 README.md               → Este archivo
 ┗ 📁 outputs/
    ┗ 📊 ML_Mantenimiento_Predictivo.pptx  → Presentación ejecutiva
```

---

## 🚀 Cómo Ejecutar

```bash
# 1. Clonar el repositorio
git clone https://github.com/Diegoagodoy/Data_Science_Machine_Learning_Ciencia_de_Datos.git

# 2. Instalar dependencias
pip install pandas numpy matplotlib seaborn scikit-learn xgboost

# 3. Ejecutar el notebook
jupyter notebook notebook.ipynb
```

---

## 🔭 Próximos Pasos

- [ ] Aplicar modelo a datasets FD002–FD004 (múltiples condiciones operativas)
- [ ] Implementar pipeline de datos en tiempo real con sensores
- [ ] Adaptar metodología a **baterías UPS** en entornos industriales
- [ ] Explorar **LSTM / Deep Learning** para series temporales de sensores
- [ ] Crear API REST para consumo del modelo en producción

---

## 👤 Autor

**Diego A. Godoy**
Proyecto desarrollado como parte de su formación en Data Science y Machine Learning.

[![GitHub](https://img.shields.io/badge/GitHub-Diegoagodoy-181717?logo=github)](https://github.com/Diegoagodoy)

---

*Machine Learning aplicado a Mantenimiento Predictivo · NASA Turbofan Dataset · 2025*
