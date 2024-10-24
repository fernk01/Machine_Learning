# Introduction to Machine Learning

## Aprendizaje Supervisado

| Modelo | Clasificación | Regresión |
| --- | --- | --- |
| Regresión Lineal |  | ✅ |
| Regresión Polinómica |  | ✅ |
| [Regresión Ridge](https://www.youtube.com/watch?v=ETyIMqHoP9g) |  | ✅ |
| Regresión Lasso |  | ✅ |
| Regresión Logística | ✅ |  |
| K-Nearest Neighbors (k-NN) | ✅ | ✅ |
| Árboles de Decisión | ✅ | ✅ |
| Bosques Aleatorios | ✅ | ✅ |
| Máquinas de Vectores de Soporte (SVM) | ✅ | ✅ (SVR) |
| Elastic Net |  | ✅ |
| XGBoost | ✅ | ✅ |
| Gradient Boosting Machine (GBM) | ✅ | ✅ |
| AdaBoost | ✅ | ✅ |
| Redes Neuronales | ✅ | ✅ |
| LightGBM | ✅ | ✅ |
|Tree Gradient Boosting | ✅ | ✅ |

## Aprendizaje No Supervisado

| Modelo | Agrupamiento | Reducción de Dimensionalidad |
| --- | --- | --- |
| K-Means | ✅ |  |
| DBSCAN | ✅ |  |
| Jerárquico | ✅ |  |
| PCA (Análisis de Componentes Principales) |  | ✅ |
| t-SNE (t-Distributed Stochastic Neighbor Embedding) |  | ✅ |
| Autoencoders (Redes Neuronales) | ✅ | ✅ |

## Arbol de Decision

| algoritmo | clasificacion | regresion |
| --- | --- | --- |
| ID3 | ✅ |  |
| C4.5 | ✅ |  |
| C5.0 | ✅ |  |
| CART | ✅ | ✅ |

`DecisionTreeClassifier` en scikit-learn es una implementación de CART.

## [Ensamblaje de Modelos](ensambles.md)


# Preprocesamiento de Datos
Los siguiente modelos requieren que los datos esten normalizados o estandarizados:
- Regresión Lineal
- Regresión Logística
- K-Nearest Neighbors (k-NN)
- Máquinas de Vectores de Soporte (SVM)
- Redes Neuronales

[Leer](https://medium.com/analytics-vidhya/why-is-scaling-required-in-knn-and-k-means-8129e4d88ed7)

# Overfitting y Underfitting
- **Underfitting**: Si el modelo tiene un rendimiento bajo tanto en el conjunto de entrenamiento como en el de validación, podría estar subajustado. Sin embargo, no tenemos información sobre el rendimiento en el conjunto de entrenamiento aquí.
    - Train bajo y Test bajo -> Underfitting
- **Overfitting**: Si el modelo tiene un rendimiento muy alto en el conjunto de entrenamiento pero bajo en el de validación, podría estar sobreajustado. Nuevamente, necesitamos comparar con el rendimiento en el conjunto de entrenamiento.

## Ejemplo:
¡Claro! Aquí tienes un ejemplo de cómo puedes identificar si tu modelo está sufriendo de overfitting o underfitting utilizando las métricas de evaluación:

### Ejemplo de Identificación de Overfitting y Underfitting

Supongamos que tienes un modelo de clasificación binaria y has dividido tus datos en conjuntos de entrenamiento y prueba. Después de entrenar tu modelo, obtienes los siguientes resultados:

#### Conjunto de Entrenamiento:
```python
y_pred_train = pipeline.predict(X_train)
print(classification_report(y_train, y_pred_train))
```
```
              precision    recall  f1-score   support

           0       0.95      0.98      0.96     44510
           1       0.90      0.80      0.85     13386

    accuracy                           0.94     57896
   macro avg       0.92      0.89      0.90     57896
weighted avg       0.94      0.94      0.94     57896
```

#### Conjunto de Prueba:
```python
y_pred_test = pipeline.predict(X_test)
print(classification_report(y_test, y_pred_test))
```
```
              precision    recall  f1-score   support

           0       0.86      0.94      0.90     44510
           1       0.72      0.49      0.58     13386

    accuracy                           0.84     57896
   macro avg       0.79      0.72      0.74     57896
weighted avg       0.83      0.84      0.83     57896
```

### Análisis de Resultados:

1. **Overfitting**:
   - **Indicador**: El modelo tiene un rendimiento significativamente mejor en el conjunto de entrenamiento que en el conjunto de prueba.
   - **Ejemplo**: En el conjunto de entrenamiento, la precisión y el recall para la clase 1 son 0.90 y 0.80, respectivamente, mientras que en el conjunto de prueba son 0.72 y 0.49. Esta gran diferencia sugiere que el modelo está sobreajustado a los datos de entrenamiento y no generaliza bien a nuevos datos.

2. **Underfitting**:
   - **Indicador**: El modelo tiene un rendimiento bajo tanto en el conjunto de entrenamiento como en el de prueba.
   - **Ejemplo**: Si los valores de precisión y recall fueran bajos en ambos conjuntos (por ejemplo, alrededor de 0.50 para ambas clases), esto indicaría que el modelo no está capturando bien las relaciones en los datos y está subajustado.

### Recomendaciones:
- **Para Overfitting**:
  - **Regularización**: Aplica técnicas como L1 (Lasso) o L2 (Ridge) para penalizar la complejidad del modelo.
  - **Aumentar Datos**: Si es posible, añade más datos de entrenamiento para ayudar al modelo a generalizar mejor.
  - **Simplificar el Modelo**: Reduce la complejidad del modelo (por ejemplo, menos capas en una red neuronal).

- **Para Underfitting**:
 - **Modelo Más Complejo**: Prueba con modelos más complejos que puedan capturar mejor las relaciones en los datos.
  - **Más Características**: Añade más características relevantes a los datos de entrada.
  - **Ajuste de Hiperparámetros**: Realiza una búsqueda de hiperparámetros para encontrar los mejores parámetros para tu modelo.

# Sklearn: Fit, Transform, Fit_transform, Predict, Predict_proba
En los modelos de machine learning, los métodos `fit`, `transform` y `fit_transform` tienen roles específicos:

- **fit**: Este método se utiliza para entrenar el modelo utilizando los datos de entrenamiento. En este proceso, el modelo aprende los parámetros necesarios a partir de los datos de entrenamiento.

- **transform**: Una vez que el modelo ha sido entrenado (es decir, después de usar `fit`), el método `transform` se utiliza para aplicar la transformación aprendida a nuevos datos. Esto puede ser útil para varias tareas, como la normalización de datos, la reducción de dimensionalidad, etc.

- **fit_transform**: Este es un método de conveniencia que realiza primero un `fit` (entrenamiento) y luego un `transform` (transformación) en los mismos datos de entrada. Es importante notar que `fit_transform` puede no ser equivalente a `fit().transform()` para algunos estimadores, ya que `fit_transform` puede optimizar ciertos cálculos.

La diferencia principal entre estos métodos radica en su propósito y en el orden en que se deben utilizar. Primero se debe utilizar `fit` para entrenar el modelo, luego `transform` para aplicar la transformación aprendida a los datos. `fit_transform` combina estos dos pasos en uno. Es importante tener en cuenta que no todos los modelos o transformadores en machine learning necesitan un método `fit`, algunos solo pueden necesitar `transform` (por ejemplo, `MinMaxScaler` en scikit-learn). Por otro lado, algunos modelos solo pueden necesitar `fit` (por ejemplo, un clasificador).

# Predict y Predict_proba
- **predict**: Este método se utiliza para predecir las etiquetas de clase o los valores de destino para nuevos datos de entrada. 

- **predict_proba**: Este método se utiliza para predecir las probabilidades de pertenencia a cada clase en un problema de clasificación. Por ejemplo, en un problema de clasificación binaria, `predict_proba` devolverá las probabilidades de pertenencia a la clase 0 y la clase 1 para cada muestra.

## Método `predict_proba`
El [método](https://studyx.ai/homework/101881036-for-notational-ease-we-assume-that-the-target-y-i-takes-values-in-the-set-0-1-for-data) `predict_proba` calcula las probabilidades de pertenencia a cada clase. La forma en que se calculan estas probabilidades depende del modelo:

1. **Regresión Logística**: Utiliza la función sigmoide para calcular las probabilidades.
   $$ P(y=1|x) = \frac{1}{1 + e^{-(\beta_0 + \beta_1 x_1 + \beta_2 x_2)}} $$

2. **Árbol de Decisión**: Calcula las probabilidades basándose en la proporción de muestras de cada clase en las hojas del árbol.
   - Si una hoja tiene 70 muestras de la clase 0 y 30 de la clase 1, las probabilidades serían [0.7, 0.3].

3. **Redes Neuronales**: Utilizan la función softmax para calcular las probabilidades.
   $$ P(y=i|x) = \frac{e^{z_i}}{\sum_{j} e^{z_j}} $$
   Donde \( z_i \) es la salida del modelo para la clase \( i \).


# [Metricas](Metricas.md)

# [Regresión Lineal](Regresion_Lineal.md)

# [knn](knn.md)

# [Decision Tree](Decision_Tree.md)