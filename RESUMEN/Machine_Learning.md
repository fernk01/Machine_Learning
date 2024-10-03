# Introduction to Machine Learning
En los modelos de machine learning, los métodos `fit`, `transform` y `fit_transform` tienen roles específicos:

- **fit**: Este método se utiliza para entrenar el modelo utilizando los datos de entrenamiento. En este proceso, el modelo aprende los parámetros necesarios a partir de los datos de entrenamiento.

- **transform**: Una vez que el modelo ha sido entrenado (es decir, después de usar `fit`), el método `transform` se utiliza para aplicar la transformación aprendida a nuevos datos. Esto puede ser útil para varias tareas, como la normalización de datos, la reducción de dimensionalidad, etc.

- **fit_transform**: Este es un método de conveniencia que realiza primero un `fit` (entrenamiento) y luego un `transform` (transformación) en los mismos datos de entrada. Es importante notar que `fit_transform` puede no ser equivalente a `fit().transform()` para algunos estimadores, ya que `fit_transform` puede optimizar ciertos cálculos.

La diferencia principal entre estos métodos radica en su propósito y en el orden en que se deben utilizar. Primero se debe utilizar `fit` para entrenar el modelo, luego `transform` para aplicar la transformación aprendida a los datos. `fit_transform` combina estos dos pasos en uno. Es importante tener en cuenta que no todos los modelos o transformadores en machine learning necesitan un método `fit`, algunos solo pueden necesitar `transform` (por ejemplo, `MinMaxScaler` en scikit-learn). Por otro lado, algunos modelos solo pueden necesitar `fit` (por ejemplo, un clasificador).


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



# [Metricas](Metricas.md)

# Regresión Lineal
La regresión lineal es un algoritmo de aprendizaje supervisado utilizado para predecir una variable continua (como el precio de una casa) a partir de una o más variables independientes (como el tamaño de la casa, el número de habitaciones, etc.). La regresión lineal encuentra la mejor línea de ajuste a través de los datos que minimiza la suma de los errores cuadrados entre las predicciones y los valores reales.

Cuando el dataset contiene una columna que es categorica, se debe convertir a una variable dummy, esto se hace con la función `pd.get_dummies()`.

Se aplica mínimos cuadrados ordinarios (OLS) para encontrar los coeficientes de la regresión lineal. La fórmula de la regresión lineal es:

$$ y = b_0 + b_1 \cdot x_1 + b_2 \cdot x_2 + ... + b_n \cdot x_n $$

# [knn](knn.md)

# [Decision Tree](Decision_Tree.md)
