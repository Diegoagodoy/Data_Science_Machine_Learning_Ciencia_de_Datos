# Predicción de Vida Util de Motores Mantenimiento Predictivo)

## Descripción del Proyecto

Este proyecto tiene como objetivo analizar datos de sensores industriales para predecir la **vida útil restante de motores**, aplicando técnicas de análisis de datos y preparando el terreno para modelos de Machine Learning.

El enfoque principal está en comprender el comportamiento de los sensores y su relación con el desgaste del motor.

---

## Dataset

Para el desarrollo de este proyecto se ha optado por utilizar un dataset de tipo regresión, ya que el objetivo principal es predecir una variable numérica continua.

- **Dataset:** NASA Turbofan Jet Engine Data Set
- **Origen:** https://www.kaggle.com/datasets/behrad3d/nasa-cmaps

Este dataset simula el comportamiento de motores a lo largo del tiempo, permitiendo estimar su vida útil restante a partir de múltiples sensores.

Esta elección se encuentra alineada con aplicaciones reales en entornos industriales, particularmente en la empresa donde actualmente trabajo.

A futuro, se busca aplicar este enfoque en la predicción de mantenimiento predictivo, específicamente en la estimación de la vida útil de equipos críticos como baterías de UPS (Sistemas de Alimentación Ininterrumpida).

---

## Objetivos

* Analizar el comportamiento de los sensores
* Comprender la variable objetivo (**vida_util**)
* Detectar patrones de desgaste
* Identificar variables relevantes
* Preparar los datos para modelado

---

## Estructura del Dataset

El dataset contiene las siguientes variables principales:

* `motor_id`: identificador del motor
* `ciclo`: número de ciclo de operación
* `sensor_1` a `sensor_21`: mediciones de sensores
* `configuracion_operativa`: condiciones de operación
* `vida_util`: variable objetivo (Remaining Useful Life)

---

## Análisis Exploratorio de Datos (EDA)

### Análisis Univariado

* La **vida útil** presenta una distribución con mayor concentración en valores bajos
* Algunos sensores muestran baja variabilidad
* Otros presentan mayor dispersión y valores atípicos

---

### Análisis Bivariado

* La **vida útil disminuye progresivamente** con el ciclo
* Algunos sensores muestran cierta relación con el desgaste
* No todos los sensores reflejan claramente el deterioro del motor

---

### Análisis Multivariado

* Se utilizó una matriz de correlación
* Se identificaron los sensores más relacionados con la vida útil
* Se filtran valores nulos para mejorar el analisis

---

### Outliers

* Se detectaron valores atípicos en varios sensores
* No se eliminaron para evitar perder información relevante

---

## Conclusiones del EDA

* La vida útil disminuye con el uso del motor
* No todos los sensores aportan información relevante
* Existen sensores con mayor capacidad explicativa
* Se identificaron variables clave para el modelado

---

## Próximos pasos

* Selección de variables (Feature Selection)
* Escalado y normalización de datos
* Entrenamiento de modelos de Machine Learning
* Evaluación de desempeño
* Optimización del modelo

---

## Tecnologías utilizadas

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn

---

## Autor

Proyecto desarrollado por Diego A. Godoy como parte de su formación en Data Science.
