# Regresión Lineal
La clase `sklearn.linear_model.LinearRegression` en scikit-learn es utilizada para ajustar un modelo de regresión lineal utilizando el método de mínimos cuadrados ordinarios. 

## Parámetros de `LinearRegression`:
- `fit_intercept` (booleano, valor predeterminado: `True`): Determina si se debe calcular el término de intercepción para el modelo. Si se establece en `False`, no se utilizará un intercepto en los cálculos (es decir, se espera que los datos ya estén centrados).
- `copy_X` (booleano, valor predeterminado: `True`): Si es `True`, se copiará la matriz de características `X`; de lo contrario, se puede sobrescribir.
- `n_jobs` (entero, valor predeterminado: `None`): El número de trabajos (hilos) a utilizar para el cálculo. Esto solo proporcionará una aceleración en caso de problemas lo suficientemente grandes, es decir, si primero `n_targets > 1` y segundo `X` es disperso o si `positive` se establece en `True`. `None` significa 1 a menos que estemos en un contexto de `joblib.parallel_backend`. `-1` significa usar todos los procesadores disponibles.
- `positive` (booleano, valor predeterminado: `False`): Cuando se establece en `True`, fuerza a los coeficientes a ser positivos. Esta opción solo es compatible con matrices densas y se agregó en la versión 0.24.

## Atributos
1. **`coef_`**:
   - Tipo: Array de forma `(n_features,)` o `(n_targets, n_features)`
   - Descripción: Coeficientes estimados para el problema de regresión lineal. Si se pasan múltiples objetivos durante el ajuste (es decir, `y` es 2D), esto es un array 2D de forma `(n_targets, n_features)`. Si solo se pasa un objetivo, es un array 1D de longitud `n_features`.
   - Ejemplo: Si ajustamos un modelo a datos de entrada `X` y etiquetas `y`, los coeficientes estimados serían `[1., 2.]`.

2. **`rank_`**:
   - Tipo: Entero
   - Descripción: Rango de la matriz `X`. Solo está disponible cuando `X` es denso.

3. **`singular_`**:
   - Tipo: Array de forma `(min(X, y),)`
   - Descripción: Valores singulares de `X`. Solo está disponible cuando `X` es denso.

4. **`intercept_`**:
   - Tipo: Flotante o array de forma `(n_targets,)`
   - Descripción: Término independiente en el modelo lineal. Se establece en `0.0` si `fit_intercept = False`.

5. **`n_features_in_`**:
   - Tipo: Entero
   - Descripción: Número de características observadas durante el ajuste. Agregado en la versión 0.24.

6. **`feature_names_in_`**:
   - Tipo: Matriz ndarray de forma `(n_features_in_,)`
   - Descripción: Nombres de las características observadas durante el ajuste. Definido solo cuando `X` tiene nombres de características que son todas cadenas. Agregado en la versión 1.0.

En resumen, estos atributos proporcionan información importante sobre los coeficientes, el término de intercepción y otras características del modelo de regresión lineal. Si tienes más preguntas o necesitas más ejemplos, no dudes en preguntar.