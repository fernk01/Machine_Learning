# Regresión Logística
La regresión logística es un algoritmo de aprendizaje supervisado utilizado para la clasificación de datos. A pesar de su nombre, la regresión logística se utiliza para problemas de clasificación, no de regresión. Es un método simple pero efectivo que se utiliza ampliamente en la industria y la investigación.

1. **Regresión Logística**: Utiliza la función sigmoide para calcular las probabilidades.
   $$ P(y=1|x) = \frac{1}{1 + e^{-(\beta_0 + \beta_1 x_1 + \beta_2 x_2)}} $$



## Umbral
En la regresión logística, el umbral de clasificación por defecto es **0.5**. Esto significa que si la probabilidad predicha de pertenencia a la clase positiva (por ejemplo, clase 1) es mayor o igual a 0.5, el modelo clasifica la muestra como perteneciente a esa clase. Si es menor, la clasifica como perteneciente a la clase negativa (por ejemplo, clase 0).

Sin embargo, este umbral se puede ajustar según las necesidades del problema. Por ejemplo, si quieres ser más conservador y solo clasificar como positivo cuando la probabilidad es muy alta, podrías aumentar el umbral. Aquí tienes un ejemplo de cómo hacerlo en código:

```python
import numpy as np
from sklearn.linear_model import LogisticRegression
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split

# Cargar datos
iris = load_iris()
X = iris.data
y = (iris.target == 2).astype(int)  # Clasificación binaria: clase 2 vs. no clase 2

# Dividir datos en entrenamiento y prueba
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Entrenar el modelo
model = LogisticRegression(max_iter=200)
model.fit(X_train, y_train)

# Predecir probabilidades
probabilidades = model.predict_proba(X_test)[:, 1]

# Ajustar el umbral
umbral = 0.7
predicciones_ajustadas = (probabilidades >= umbral).astype(int)

print("Predicciones ajustadas:", predicciones_ajustadas)
```

