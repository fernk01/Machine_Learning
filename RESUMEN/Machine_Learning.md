# Introduction to Machine Learning
En los modelos de machine learning, los métodos `fit`, `transform` y `fit_transform` tienen roles específicos:

- **fit**: Este método se utiliza para entrenar el modelo utilizando los datos de entrenamiento. En este proceso, el modelo aprende los parámetros necesarios a partir de los datos de entrenamiento.

- **transform**: Una vez que el modelo ha sido entrenado (es decir, después de usar `fit`), el método `transform` se utiliza para aplicar la transformación aprendida a nuevos datos. Esto puede ser útil para varias tareas, como la normalización de datos, la reducción de dimensionalidad, etc.

- **fit_transform**: Este es un método de conveniencia que realiza primero un `fit` (entrenamiento) y luego un `transform` (transformación) en los mismos datos de entrada. Es importante notar que `fit_transform` puede no ser equivalente a `fit().transform()` para algunos estimadores, ya que `fit_transform` puede optimizar ciertos cálculos.

La diferencia principal entre estos métodos radica en su propósito y en el orden en que se deben utilizar. Primero se debe utilizar `fit` para entrenar el modelo, luego `transform` para aplicar la transformación aprendida a los datos. `fit_transform` combina estos dos pasos en uno. Es importante tener en cuenta que no todos los modelos o transformadores en machine learning necesitan un método `fit`, algunos solo pueden necesitar `transform` (por ejemplo, `MinMaxScaler` en scikit-learn). Por otro lado, algunos modelos solo pueden necesitar `fit` (por ejemplo, un clasificador).



# Predict y Predict_proba
- **predict**: Este método se utiliza para predecir las etiquetas de clase o los valores de destino para nuevos datos de entrada. 

- **predict_proba**: Este método se utiliza para predecir las probabilidades de pertenencia a cada clase en un problema de clasificación. Por ejemplo, en un problema de clasificación binaria, `predict_proba` devolverá las probabilidades de pertenencia a la clase 0 y la clase 1 para cada muestra.


## Ejemplos
### Regresión Lineal Simple
En una regresión lineal simple, el método `predict` de Scikit-learn toma las características de entrada (por ejemplo, edad y peso) y devuelve una predicción del valor objetivo (por ejemplo, salario) utilizando la fórmula de la línea de regresión:

$$ y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 $$

Donde:
- $ y $ es el valor predicho (salario).
- $ \beta_0 $ es el intercepto.
- $ \beta_1 $ y $ \beta_2 $ son los coeficientes de las características (edad y peso).
- $ x_1 $ y $ x_2 $ son los valores de las características (18 y 87 en tu ejemplo).

Entonces, si tienes un punto (18, 87), el modelo aplicará esta fórmula para calcular y devolver el salario predicho, por ejemplo, 570.

### Clasificación Binaria con Árbol de Decisión
En una clasificación binaria con un árbol de decisión, el método `predict` sigue las reglas del árbol para asignar una clase a cada muestra. Estas reglas se pueden visualizar en el diagrama del árbol, donde cada nodo representa una decisión basada en una característica.

## Método `predict_proba`
El [método](https://studyx.ai/homework/101881036-for-notational-ease-we-assume-that-the-target-y-i-takes-values-in-the-set-0-1-for-data) `predict_proba` calcula las probabilidades de pertenencia a cada clase. La forma en que se calculan estas probabilidades depende del modelo:

1. **Regresión Logística**: Utiliza la función sigmoide para calcular las probabilidades.
   $$ P(y=1|x) = \frac{1}{1 + e^{-(\beta_0 + \beta_1 x_1 + \beta_2 x_2)}} $$

2. **Árbol de Decisión**: Calcula las probabilidades basándose en la proporción de muestras de cada clase en las hojas del árbol.
   - Si una hoja tiene 70 muestras de la clase 0 y 30 de la clase 1, las probabilidades serían [0.7, 0.3].

3. **Redes Neuronales**: Utilizan la función softmax para calcular las probabilidades.
   $$ P(y=i|x) = \frac{e^{z_i}}{\sum_{j} e^{z_j}} $$
   Donde \( z_i \) es la salida del modelo para la clase \( i \).












# Machine Learning

---
Las redes neuronales pueden ser utilizadas tanto en aprendizaje supervisado como no supervisado. En el aprendizaje supervisado, las redes neuronales se utilizan para aprender a partir de ejemplos etiquetados. En el aprendizaje no supervisado, las redes neuronales se utilizan para aprender patrones y estructuras a partir de datos no etiquetados.

Aquí tienes dos tablas con algunos modelos de aprendizaje supervisado y no supervisado:

**Aprendizaje Supervisado**

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

**Aprendizaje No Supervisado**

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

**Bagging**: Los modelos se construyen de forma paralela y se combinan para obtener una predicción. Algunos algoritmos de bagging populares son:

| algoritmo | clasificacion | regresion |
| --- | --- | --- |
| Random Forest | ✅ | ✅ |
| Extra Trees | ✅ | ✅ |

**Boosting**: Los modelos se construyen secuencialmente y cada modelo intenta corregir los errores del modelo anterior. Algunos algoritmos de boosting populares son:

| algoritmo | clasificacion | regresion |
| --- | --- | --- |
| AdaBoost | ✅ | ✅ |
| Gradient Boosting Machine (GBM) | ✅ | ✅ |
| XGBoost | ✅ | ✅ |
| LightGBM | ✅ | ✅ |
| CatBoost | ✅ | ✅ |

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




# [Metricas](Metricas.md)

# Regresión Lineal
La regresión lineal es un algoritmo de aprendizaje supervisado utilizado para predecir una variable continua (como el precio de una casa) a partir de una o más variables independientes (como el tamaño de la casa, el número de habitaciones, etc.). La regresión lineal encuentra la mejor línea de ajuste a través de los datos que minimiza la suma de los errores cuadrados entre las predicciones y los valores reales.

Cuando el dataset contiene una columna que es categorica, se debe convertir a una variable dummy, esto se hace con la función `pd.get_dummies()`.

Se aplica mínimos cuadrados ordinarios (OLS) para encontrar los coeficientes de la regresión lineal. La fórmula de la regresión lineal es:

$$ y = b_0 + b_1 \cdot x_1 + b_2 \cdot x_2 + ... + b_n \cdot x_n $$

# [knn](knn.md)

# [Decision Tree](Decision_Tree.md)
