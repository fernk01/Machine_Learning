# K-Nearest Neighbors (K-NN)
El algoritmo de K-Nearest Neighbors (K-NN) es un algoritmo de aprendizaje supervisado utilizado para clasificación y regresión.

- Es sensible a conjuntos de datos no balanceados.
- Es muy sensible aoutliers.
- La normalización de los datos de entrenamiento puede mejorar drásticamente su precisión
- Si se aplica en un comjunto de datos desbalanceado, puede ser que el algoritmo siempre prediga la clase mayoritaria. 

## Explicación del Algoritmo K-NN

1. **Definir K**: Elegir el número de vecinos más cercanos \( K \).
2. **Calcular distancias**: Para cada punto de prueba, calcular la distancia entre este punto y todos los puntos del conjunto de entrenamiento.
3. **Identificar vecinos**: Seleccionar los \( K \) puntos más cercanos del conjunto de entrenamiento.
4. **Clasificación**: 
    - Para clasificación, asignar la clase más común entre los \( K \) vecinos. 
    - Para regresión, calcular la media de los valores de los \( K \) vecinos.

## Cálculo de la Distancia

Una de las distancias más comunes utilizadas en K-NN es la distancia euclidiana. La fórmula para calcular la distancia euclidiana entre dos puntos $( \mathbf{x} = (x_1, x_2, ..., x_n) ) $ y $( \mathbf{y} = (y_1, y_2, ..., y_n) ) $ en un espacio n-dimensional es:

$$ \ d(\mathbf{x}, \mathbf{y}) = \sqrt{\sum_{i=1}^{n} (x_i - y_i)^2} ] $$

## Ejemplo de Cálculo
[YouTube](https://www.youtube.com/watch?v=0p0o5cmgLdE)

Supongamos que tenemos un conjunto de datos con dos características $( x_1 )$ y $( x_2 )$ y queremos clasificar un nuevo punto $ ( \mathbf{p} = (2, 3) )$. Consideremos que K = 3. Aquí hay un ejemplo paso a paso:

### Conjunto de Datos de Entrenamiento
| Punto | $( x_1 )$ | $( x_2 $) | Clase | Valor |
|-------|----------|----------|-------| ------|
| \( A \) | 1        | 2        | 0     | 2.5   |
| \( B \) | 2        | 4        | 0     | 3.0   |
| \( C \) | 4        | 4        | 1     | 4.5   |
| \( D \) | 5        | 2        | 1     | 5.0   |

### Calcular Distancias Euclidianas

1. **Distancia entre ($\mathbf{p}$) y (A)**:
  $$ d(\mathbf{p}, A) = \sqrt{(2-1)^2 + (3-2)^2} = \sqrt{1 + 1} = \sqrt{2} \approx 1.41 $$

2. **Distancia entre ($\mathbf{p}$) y (B)**:
  $$ d(\mathbf{p}, B) = \sqrt{(2-2)^2 + (3-4)^2} = \sqrt{0 + 1} = 1$$

3. **Distancia entre ($\mathbf{p}$) y (C)**:
  $$ d(\mathbf{p}, C) = \sqrt{(2-4)^2 + (3-4)^2} = \sqrt{4 + 1} = \sqrt{5} \approx 2.24$$

4. **Distancia entre ($\mathbf{p}$) y (D)**:
  $$d(\mathbf{p}, D) = \sqrt{(2-5)^2 + (3-2)^2} = \sqrt{9 + 1} = \sqrt{10} \approx 3.16$$

### Identificar los 3 Vecinos Más Cercanos
Las distancias ordenadas son:
- ( B ): 1
- ( A ): 1.41
- ( C ): 2.24

### Clasificación
Los 3 vecinos más cercanos son 
- (B) (Clase 0)
- (A) (Clase 0)
- (C) (Clase 1)

La clase más común entre los 3 vecinos más cercanos es la clase 0. Por lo tanto, el nuevo punto $( \mathbf{p} = (2, 3))$ se clasifica como clase 0.

### Regresión
Para predecir el valor del nuevo punto $(\mathbf{p})$, se toma la media de los valores de los 3 vecinos más cercanos:
- ( B ): 3.0
- ( A ): 2.5
- ( C ): 4.5

$$ \text{Valor predicho} = \frac{3.0 + 2.5 + 4.5}{3} = 3.33 $$

## Implementación en Python

Aquí hay un ejemplo sencillo de implementación de K-NN en Python usando el cálculo de la distancia euclidiana:

```python
import numpy as np
from collections import Counter

def euclidean_distance(point1, point2):
    return np.sqrt(np.sum((point1 - point2)**2))

def knn_classify(training_data, training_labels, new_point, k):
    distances = []
    for i in range(len(training_data)):
        distance = euclidean_distance(training_data[i], new_point)
        distances.append((distance, training_labels[i]))
    
    distances.sort(key=lambda x: x[0])
    nearest_neighbors = distances[:k]
    
    classes = [label for _, label in nearest_neighbors]
    majority_class = Counter(classes).most_common(1)[0][0]
    
    return majority_class

# Datos de entrenamiento
training_data = np.array([[1, 2], [2, 4], [4, 4], [5, 2]])
training_labels = np.array([0, 0, 1, 1])

# Punto nuevo
new_point = np.array([2, 3])

# Clasificación
k = 3
predicted_class = knn_classify(training_data, training_labels, new_point, k)
print(f"La clase predicha para el punto {new_point} es: {predicted_class}")
```

Este código clasifica el nuevo punto \( [2, 3] \) como clase 0 utilizando el algoritmo K-NN con \( K = 3 \).

## KNN sklearn
- Entrenamiento (fit): En la etapa de "entrenamiento" de K-NN, en realidad no hay un proceso de aprendizaje como en otros algoritmos de aprendizaje supervisado. En lugar de eso, K-NN simplemente almacena el conjunto de datos de entrenamiento completo. Esto incluye tanto las características (features) como las etiquetas de clase asociadas.
- Predicción (predict): Cuando se solicita una predicción para un nuevo punto de datos, el algoritmo realiza los siguientes pasos:
    - Calcula la distancia entre el nuevo punto y todos los puntos en el conjunto de datos de entrenamiento.
    - Ordena estos puntos según la distancia calculada.
    - Selecciona los 𝐾 puntos más cercanos.
    - Determina la clase del nuevo punto en función de la mayoría de las clases de los 𝐾 vecinos más cercanos (para un problema de clasificación) o la media de los valores de los K vecinos (para un problema de regresión).