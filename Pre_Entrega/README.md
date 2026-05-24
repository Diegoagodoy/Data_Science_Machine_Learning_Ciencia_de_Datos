# Prediccion de Vida Util de Motores (Mantenimiento Predictivo)

## Descripcion del Proyecto

Este proyecto tiene como objetivo analizar datos de sensores industriales para predecir la **vida util restante de motores**, aplicando tecnicas de analisis de datos y preparando el terreno para modelos de Machine Learning.

El enfoque principal esta en comprender el comportamiento de los sensores y su relacion con el desgaste del motor.

---

## Dataset

Para el desarrollo de este proyecto se ha optado por utilizar un dataset de tipo regresion, ya que el objetivo principal es predecir una variable numerica continua.

- **Dataset:** NASA Turbofan Jet Engine Data Set
- **Origen:** https://www.kaggle.com/datasets/behrad3d/nasa-cmaps

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
* `ciclo`: número de ciclo de operacion
* `sensor_1` a `sensor_21`: mediciones de sensores
* `configuracion_operativa`: condiciones de operacion
* `vida_util`: variable objetivo

---

## Analisis Exploratorio de Datos (EDA)

### Analisis Univariado

* La **vida útil** presenta una distribución con mayor concentración en valores bajos
* Algunos sensores muestran baja variabilidad
* Otros presentan mayor dispersión y valores atipicos

---

### Analisis Bivariado

* La **vida útil disminuye progresivamente** con el ciclo
* Algunos sensores muestran cierta relación con el desgaste
* No todos los sensores reflejan claramente el deterioro del motor

---

### Analisis Multivariado

* Se utilizo una matriz de correlacion
* Se identificaron los sensores mas relacionados con la vida util
* Se filtran valores nulos para mejorar el analisis

---

### Outliers

* Se detectaron valores atipicos en varios sensores
* No se eliminaron para evitar perder informacion relevante

---

## Conclusiones del EDA

* La vida util disminuye con el uso del motor
* No todos los sensores aportan informacion relevante
* Existen sensores con mayor capacidad explicativa
* Se identificaron variables clave para el modelado

---

## Próximos pasos

* Selección de variables
* Escalado y normalizacion de datos
* Entrenamiento de modelos de Machine Learning
* Evaluacion de desempeño
* Optimizacion del modelo

---

## Tecnologías utilizadas

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn

---

## Autor

Proyecto desarrollado por Diego A. Godoy como parte de su formacion en Data Science.
