# MCDI504 - Machine Learning I

## Sumativa 3 - Fase 4: Evaluación y Validación del Modelo

Proyecto desarrollado para la asignatura **MCDI504 - Machine Learning I** de la Universidad Andrés Bello.

### Integrantes
- Luiskar Espinoza
- Henry Moraga
- Pablo Rodríguez

**Grupo:** 6  
**Docente:** David Ruete Zúñiga  
**Año:** 2026

---

## Descripción del proyecto

Este repositorio contiene la entrega correspondiente a la **Semana 04 - Sumativa 3: Informe final del proyecto Fase 4**, centrada en la evaluación y validación de modelos de clasificación supervisada.

El caso de estudio utiliza el dataset **Titanic**, obtenido desde OpenML. El objetivo es predecir si un pasajero sobrevivió o no a partir de variables demográficas, socioeconómicas y de viaje.

La variable objetivo es:

- `survived = 0`: no sobrevivió
- `survived = 1`: sobrevivió

La clase positiva utilizada para calcular precision, recall y F1-score corresponde a **`survived = 1`**.

---

## Dataset

El conjunto de datos contiene:

- **1.309 registros**
- **14 columnas iniciales**
- **809 pasajeros que no sobrevivieron (61,8 %)**
- **500 pasajeros que sobrevivieron (38,2 %)**

La división utilizada para la evaluación final fue:

- **1.047 registros de entrenamiento**
- **262 registros de prueba**
- División aproximada **80/20**

Durante el preprocesamiento se realizaron tareas de revisión de valores faltantes, imputación de variables, codificación de variables categóricas, escalamiento de variables numéricas y separación entre entrenamiento y prueba.

---

## Modelos evaluados

Se implementaron y compararon tres modelos de clasificación supervisada:

1. **Regresión Logística**
2. **Random Forest**
3. **Red Neuronal MLP**

La Red Neuronal utiliza una arquitectura con:

- 8 variables de entrada
- 1 capa oculta de 16 neuronas
- salida binaria
- función de activación ReLU
- optimizador Adam

---

## Métricas de evaluación

Los modelos fueron evaluados mediante:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Matriz de confusión

---

## Resultados sobre el conjunto de prueba

| Modelo | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Regresión Logística | 0,8092 | 0,7717 | 0,7100 | 0,7396 | 0,8680 |
| Random Forest | 0,7901 | 0,7273 | 0,7200 | 0,7236 | 0,8575 |
| **Red Neuronal** | **0,8397** | **0,8295** | **0,7300** | **0,7766** | **0,8711** |

La **Red Neuronal** obtuvo el mejor desempeño global en el conjunto de prueba.

### Matriz de confusión de la Red Neuronal

```text
[[147, 15],
 [ 27, 73]]
```

Interpretación:

- Verdaderos negativos: **147**
- Falsos positivos: **15**
- Falsos negativos: **27**
- Verdaderos positivos: **73**

---

## Validación cruzada

Para analizar la estabilidad de la Red Neuronal se utilizó **Stratified K-Fold Cross-Validation con k = 5**.

### Resultados promedio de validación

| Métrica | Promedio | Desviación estándar |
|---|---:|---:|
| Accuracy | 0,7899 | 0,0134 |
| Precision | 0,7848 | 0,0357 |
| Recall | 0,6275 | 0,0827 |
| F1-score | 0,6925 | 0,0390 |
| ROC-AUC | 0,8506 | 0,0139 |

Los resultados muestran buena estabilidad en Accuracy y ROC-AUC. El Recall presenta una variabilidad mayor, por lo que constituye una métrica relevante para futuras mejoras del modelo.

---

## Justificación de la técnica de validación

Se seleccionó **Stratified K-Fold con k=5** porque entrega un equilibrio adecuado entre aprovechamiento del conjunto de datos, estabilidad de las métricas, costo computacional y preservación de la proporción de las clases.

- **Hold-Out:** menor costo, pero depende de una sola partición.
- **K-Fold:** permite evaluar varias particiones y calcular promedio y variabilidad.
- **Leave-One-Out:** requiere una cantidad mucho mayor de entrenamientos y no resulta conveniente para este caso.

---

## Estructura del repositorio

```text
MCDI504_S4_GRUPO6/
│
├── MCDI504_S4_2_GRUPO6_REVISADO_FINAL.ipynb
├── MCDI504_S4_2_GRUPO6.pdf
├── README.md
└── requirements.txt
```

---

## Librerías utilizadas

```text
pandas
numpy
matplotlib
seaborn
scikit-learn
```

---

## Ejecución del notebook

El proyecto puede ejecutarse directamente en **Google Colab**.

1. Abrir `MCDI504_S4_2_GRUPO6_REVISADO_FINAL.ipynb`.
2. Seleccionar **Entorno de ejecución**.
3. Seleccionar **Ejecutar todo**.
4. Revisar la carga del dataset, preprocesamiento, métricas, matriz de confusión y validación cruzada.

---

## Consideración metodológica

El conjunto de prueba se mantiene separado del entrenamiento para evaluar el desempeño sobre datos no vistos.

Como mejora metodológica futura, se recomienda integrar completamente imputación, codificación, escalamiento y entrenamiento dentro de un único `Pipeline` de scikit-learn, de modo que todo preprocesamiento que aprenda parámetros sea ajustado exclusivamente dentro de cada fold.

---

## Conclusiones

La Red Neuronal presentó el mejor desempeño puntual entre los modelos evaluados, con Accuracy de **0,8397**, F1-score de **0,7766** y ROC-AUC de **0,8711**.

La validación cruzada permitió complementar la evaluación Hold-Out y analizar la estabilidad del modelo en diferentes particiones del conjunto de entrenamiento.

Los resultados muestran que el modelo posee una capacidad predictiva adecuada, aunque el Recall presenta mayor variabilidad y constituye una oportunidad de mejora.

---

## Archivos de entrega

- `MCDI504_S4_2_GRUPO6_REVISADO_FINAL.ipynb`
- `MCDI504_S4_2_GRUPO6.pdf`
- `README.md`

---

## Referencias principales

- Ruete, D. (2026). *Métricas de evaluación: accuracy, F1-score, curva ROC-AUC, curvas precisión-recall y matriz de confusión*. Universidad Andrés Bello.
- Ruete, D. (2026). *Técnicas de evaluación: validación cruzada (K-Fold, Leave-One-Out y Hold-Out)*. Universidad Andrés Bello.
- James, G., Witten, D., Hastie, T., & Tibshirani, R. (2021). *An Introduction to Statistical Learning*. Springer.
- Scikit-learn Developers. *Scikit-learn documentation*.

---

## Uso académico

Repositorio desarrollado con fines académicos para la asignatura **MCDI504 - Machine Learning I**, Universidad Andrés Bello.
