# Limpieza de datos: Datos faltantes
Tipos de datos faltantes:
- **Missing completely at random (MCAR)**

    En este caso la razón de la falta de datos es ajena a los datos mismos.
    No existen relaciones con la variable misma donde se encuentran los datos
    faltantes, o con las restantes variables en el dataset que expliquen porque
    faltan.

- **Missing Not at Random (MNAR)**

    La razón por la cual faltan los datos depende precisamente de los mismos
    datos que hemos recolectado (está relacionado con la razón por la que
    falta) <br>
    Ej:Cada vez que una variable debería tener un valor entre 10 y 20 el
    mismo no se encuentra registrado (independientemente de los valores que
    tomen las variables restantes)

- **Missing at Random (MAR)**

    Punto intermedio entre los dos anteriores
    La causa de los datos faltantes no depende de estos mismos datos
    faltantes, pero puede estar relacionada con otras variables del dataset
    Por ejemplo encuestas mal diseñadas

# Estratégias para trabajar con datos faltantes
- **Eliminar registros o variables:**
Si la eliminación de un subconjunto disminuye significativamente la utilidad de los datos, la eliminación del caso puede no ser efectiva (No se recomienda en situaciones que no sean **MCAR**)
- **Imputar datos**
    - **Imputación por la media**
    - **Imputación por la mediana**
    - **Imputación por la moda**
    - **Imputación por el valor más frecuente**
    - **Imputación por el valor anterior o posterior**
    - **Imputación por regresión**
    - **Imputación por KNN**
    - **Imputación por MICE**
    - **Imputación por árboles de decisión**
    - **Imputación Cold Deck**: Selecciona valores o usa relaciones obtenidas de fuentes distintas de la base de datos actual. Ejemplo: tener latitud y longitud y usar un mapa para obtener la ciudad.
    - **Imputación Hot Deck**: Se reemplazan los faltantes con valores obtenidos de registros que son los más similares(Hay que definir que es similar, **K vecinos más cercanos** puede servir)

## imputación por la media/mediana/moda

| Imputación por | Ventajas | Desventajas | Cuándo usar |
| --- | --- | --- | --- |
| **Media** | - No afecta drásticamente la distribución cuando no hay valores atípicos | - Sensible a valores atípicos <br> - Puede distorsionar la distribución en presencia de asimetría | - Variables numéricas <br> - Cuando los datos son simétricos y no hay valores atípicos significativos. |
| **Mediana** | - Robusta ante valores atípicos <br> - No distorsiona significativamente la distribución | - No toma en cuenta la media <br> - Puede no ser representativa si la distribución es uniforme | - Variables numéricas <br> - Cuando los datos son asimétricos o hay valores atípicos significativos. |
| **Moda** | - Captura los valores más comunes <br> - Útil para variables categóricas | - Puede no ser única (múltiples modas o ninguna) <br> - No es útil para datos numéricos continuos | - Variables categóricas o nominales <br> - Cuando se trabaja con datos no numéricos o discretos. |



## Sustitución por Media o Mediana o Moda
Se reemplaza utilizando la medida calculada de los valores presentes. <br>
Algunas desventajas:
- La **varianza** estimada de la nueva variable no es válida porque está atenuada por los valores repetidos.
- Se distorsiona la **distribución**
- Las **correlaciones** que se observen estarán deprimidas debido a la repetición de un solo valor constante


## Imputación por KNN
`KNNImputer` es una técnica de imputación utilizada para llenar valores faltantes en un conjunto de datos basándose en el algoritmo de K-Nearest Neighbors (KNN). La idea detrás de `KNNImputer` es que se puede estimar el valor faltante de una muestra utilizando los valores conocidos de sus vecinos más cercanos en función de la distancia en el espacio de características.

### ¿Cómo funciona?
`KNNImputer` funciona de la siguiente manera:
1. **Distancia entre observaciones**: Para cada observación con valores faltantes, se calcula la distancia (normalmente la distancia euclidiana) entre esa observación y todas las demás que no tienen valores faltantes en las características que se están considerando.
2. **K vecinos más cercanos**: Se seleccionan los *K* vecinos más cercanos (ej. K=3 significa que seleccionará los 3 vecinos más cercanos).
3. **Imputación**: El valor faltante de la observación se reemplaza por un valor calculado a partir de los valores de las observaciones vecinas, ya sea tomando un promedio (para variables continuas) o una moda (para variables categóricas).

### Cuándo usarlo
El `KNNImputer` es útil cuando:
- **Los valores faltantes no son aleatorios (MAR)** y se sospecha que las observaciones cercanas pueden tener valores similares.
- **Relaciones entre características**: Si las características están correlacionadas o tienen patrones similares, el `KNNImputer` puede aprovechar esa información para hacer estimaciones más precisas.
- Se tiene un conjunto de datos en el que los valores faltantes no son demasiados, ya que el algoritmo tiene un costo computacional considerable.

### Pre-requisitos y pasos previos:
1. **Escalado de datos**: Es crucial escalar las características (por ejemplo, usando `StandardScaler` o `MinMaxScaler`) antes de aplicar `KNNImputer`, ya que KNN se basa en distancias, y los valores en escalas diferentes pueden afectar el cálculo de la distancia.
2. **Tratamiento de variables categóricas**: Aunque KNN puede aplicarse a variables categóricas, el algoritmo funciona mejor con variables continuas. Para variables categóricas, puede ser más adecuado usar una imputación basada en la moda o una codificación adecuada antes de usar `KNNImputer`.

### Ventajas
1. **Utiliza relaciones entre observaciones**: A diferencia de imputar con la media o la moda, que ignora la relación entre las muestras, KNN tiene en cuenta la similitud entre observaciones.
2. **Puede imputar múltiples características simultáneamente**: Es capaz de manejar varios valores faltantes a la vez, lo que lo hace flexible en casos donde hay múltiples columnas con valores faltantes.
3. **No necesita un modelo predictivo complejo**: Es una técnica relativamente simple en comparación con otros métodos de imputación como modelos de Machine Learning o redes neuronales.

### Desventajas
1. **Costoso computacionalmente**: Debido a que implica calcular distancias para todas las observaciones, puede ser lento en conjuntos de datos grandes.
2. **Escalabilidad**: En datasets con una gran cantidad de observaciones o dimensiones, el cálculo de los vecinos más cercanos puede volverse ineficiente.
3. **Sensibilidad a la elección de *K***: Elegir un valor incorrecto de *K* puede llevar a una imputación inadecuada. Si *K* es demasiado bajo, la imputación puede ser imprecisa; si es demasiado alto, se puede "diluir" la información relevante.
4. **Sensibilidad a valores atípicos**: Los valores atípicos pueden influir en la elección de los vecinos más cercanos y afectar la calidad de la imputación.

### Pasos para usarlo:
1. Escalar las características.
2. Aplicar `KNNImputer`.
3. Evaluar la calidad de la imputación comparando las métricas de rendimiento o haciendo una validación cruzada si se trata de un modelo predictivo.

### Ejemplo de uso con `sklearn`:

```python
from sklearn.impute import KNNImputer
from sklearn.preprocessing import StandardScaler

# Supongamos que tienes un dataset con valores faltantes
X = [[1, 2, np.nan], [3, 4, 3], [np.nan, 6, 5], [7, 8, 9]]

# Escalar los datos
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Imputar con KNN
imputer = KNNImputer(n_neighbors=3)
X_imputed = imputer.fit_transform(X_scaled)

# Desescalar (opcional)
X_final = scaler.inverse_transform(X_imputed)
```

Este método puede ser una opción muy poderosa cuando las relaciones entre las características y las muestras son fuertes, pero es importante siempre validar los resultados con el dominio del problema y analizar el impacto en el modelo o la aplicación.

---
### Funcionamiento con variables categóricas
Para el caso de **variables categóricas**, el uso de `KNNImputer` puede ser más complicado y menos eficiente en comparación con su uso en variables numéricas. A continuación te explico cómo se podría aplicar, cuándo tiene sentido usarlo, sus pros y contras.

Al utilizar `KNNImputer` con variables categóricas, la técnica se comporta de forma similar a como lo hace con variables numéricas, pero en lugar de tomar la media o un promedio ponderado de los valores vecinos, toma la **moda** (el valor más frecuente entre los vecinos) para imputar los valores faltantes.

Es importante destacar que `KNNImputer` no maneja directamente las variables categóricas. Para usarlo, las variables categóricas deben ser codificadas previamente de manera numérica (usando técnicas como **One-Hot Encoding** o **Label Encoding**). Esto introduce algunas limitaciones y consideraciones que detallo a continuación.

### Cuándo usarlo
Usar `KNNImputer` en variables categóricas es útil cuando:
1. **Existe una relación entre las categorías**: Si se sabe que hay una correlación fuerte entre ciertas categorías y otras variables del dataset, `KNNImputer` puede aprovechar estas relaciones para imputar valores faltantes de manera más precisa.
2. **El número de valores faltantes no es muy alto**: Si el porcentaje de valores faltantes es bajo, el algoritmo puede funcionar bien imputando categorías con base en los vecinos más cercanos.

### Pros del uso de `KNNImputer` para variables categóricas
1. **Utiliza relaciones entre muestras**: Aprovecha la similitud entre observaciones para imputar, lo cual puede ser más preciso que métodos simples como la imputación por la moda de la columna completa.
2. **Versatilidad**: Puede imputar tanto variables categóricas como numéricas al mismo tiempo, lo cual es útil si tu dataset tiene ambos tipos de variables con valores faltantes.
3. **Flexibilidad**: Puede manejar situaciones en las que las categorías faltantes podrían depender de otras variables numéricas o categóricas, lo que lo hace útil cuando hay una mezcla de tipos de datos.

### Contras del uso de `KNNImputer` para variables categóricas
1. **Requiere codificación previa**: Antes de aplicar `KNNImputer`, las variables categóricas deben ser codificadas numéricamente. Esto puede introducir sesgos, especialmente si usas **Label Encoding**, ya que asignar valores numéricos a categorías implica un orden que puede no existir en la realidad.
2. **Inconsistencia en las distancias**: KNN funciona mejor con variables numéricas, y calcular distancias entre categorías codificadas puede ser problemático. En particular, si se utiliza **One-Hot Encoding**, la distancia euclidiana no refleja bien la similitud entre categorías, ya que todas las categorías se ven equidistantes.
3. **Sensibilidad al desequilibrio en categorías**: Si una categoría aparece con mayor frecuencia que otras, el algoritmo podría imputar esa categoría dominante más de lo necesario, lo que podría reducir la diversidad de las categorías en los datos imputados.
4. **Complejidad computacional**: Como en el caso de variables numéricas, el cálculo de distancias en un dataset grande con muchas variables categóricas codificadas puede ser costoso en términos de tiempo y memoria.

### Alternativas para imputar variables categóricas
- **Imputación por moda**: Simplemente se imputa el valor más frecuente en la columna. Es rápido y fácil, pero ignora la información contextual de otras observaciones.
- **Imputación por modelos predictivos**: Puedes usar modelos de clasificación (como árboles de decisión, Random Forest o regresión logística) entrenados en las variables no faltantes para predecir las categorías faltantes. Esto puede ser más efectivo que `KNNImputer` en el caso de variables categóricas.

### Ejemplo de uso con variables categóricas

```python
import numpy as np
import pandas as pd
from sklearn.impute import KNNImputer
from sklearn.preprocessing import OneHotEncoder

# Dataset con variables categóricas y numéricas
data = pd.DataFrame({
    'color': ['rojo', 'azul', np.nan, 'verde', 'rojo'],
    'tamaño': ['grande', 'mediano', 'pequeño', np.nan, 'grande'],
    'peso': [70, 60, 50, 80, np.nan]
})

# One-Hot Encoding para convertir variables categóricas
encoder = OneHotEncoder(sparse=False)
data_encoded = encoder.fit_transform(data[['color', 'tamaño']])

# Concatenar las columnas codificadas con las numéricas
data_encoded = np.concatenate([data_encoded, data[['peso']].values], axis=1)

# Aplicar KNNImputer
imputer = KNNImputer(n_neighbors=2)
data_imputed = imputer.fit_transform(data_encoded)

# Decodificar los valores imputados
decoded = encoder.inverse_transform(data_imputed[:, :-1])

# Convertir a DataFrame final
final_data = pd.DataFrame(np.concatenate([decoded, data_imputed[:, -1:]], axis=1), columns=['color', 'tamaño', 'peso'])
```

### Consideraciones finales
Si bien `KNNImputer` puede ser utilizado para imputar variables categóricas, a menudo no es la opción más efectiva debido a los problemas asociados con la codificación y el cálculo de distancias entre categorías. Es importante evaluar si las relaciones entre las observaciones son lo suficientemente significativas como para que la imputación basada en vecinos cercanos sea válida para variables categóricas. En muchos casos, otros métodos como la imputación por la moda o modelos específicos para categorías pueden ser más apropiados.

## Imputación por árboles de decisión