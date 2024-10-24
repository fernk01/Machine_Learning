# Regresión Lineal
La regresión lineal es un algoritmo de aprendizaje supervisado utilizado para predecir una variable continua (como el precio de una casa) a partir de una o más variables independientes (como el tamaño de la casa, el número de habitaciones, etc.). La regresión lineal encuentra la mejor línea de ajuste a través de los datos que minimiza la suma de los errores cuadrados entre las predicciones y los valores reales.

Cuando el dataset contiene una columna que es categorica, se debe convertir a una variable dummy, esto se hace con la función `pd.get_dummies()`.

Se aplica mínimos cuadrados ordinarios (OLS) para encontrar los coeficientes de la regresión lineal. La fórmula de la regresión lineal es:

$$ y = b_0 + b_1 \cdot x_1 + b_2 \cdot x_2 + ... + b_n \cdot x_n $$

### Regresión Lineal Simple
En una regresión lineal simple, el método `predict` de Scikit-learn toma las características de entrada (por ejemplo, edad y peso) y devuelve una predicción del valor objetivo (por ejemplo, salario) utilizando la fórmula de la línea de regresión:

$$ y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 $$

Donde:
- $ y $ es el valor predicho (salario).
- $ \beta_0 $ es el intercepto.
- $ \beta_1 $ y $ \beta_2 $ son los coeficientes de las características (edad y peso).
- $ x_1 $ y $ x_2 $ son los valores de las características (18 y 87 en tu ejemplo).

Entonces, si tienes un punto (18, 87), el modelo aplicará esta fórmula para calcular y devolver el salario predicho, por ejemplo, 570.