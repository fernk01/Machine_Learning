# Limpieza de datos: Datos faltantes
1. Missing Completely At Random (MCAR)

    **Descripción**: Los datos faltantes no tienen relación con los valores de la variable ni con otras variables del conjunto de datos. En otras palabras, la falta de datos es completamente aleatoria.

    **Ejemplo**: Un encuestador accidentalmente se salta algunas preguntas en una encuesta sin un patrón específico.

    **Implicaciones**: Si los datos son MCAR, los resultados de análisis son válidos incluso si se eliminan las observaciones con datos faltantes. Imputaciones simples (como la media) pueden funcionar bien.

2. Missing At Random (MAR)

    **Descripción**: Los datos faltantes son aleatorios, pero su probabilidad de estar ausentes está relacionada con otras variables observadas en el conjunto de datos, no con los valores que faltan.

    **Ejemplo**: En un estudio sobre ingresos, las personas con ingresos más altos podrían ser menos propensas a reportar sus ingresos, pero esta falta no está relacionada con el nivel de ingresos que no reportaron, sino con otras variables (como su nivel educativo).

    **Implicaciones**: En este caso, la imputación puede ser más efectiva utilizando información de otras variables. Métodos como MICE y el Iterative Imputer son apropiados.

3. Missing Not At Random (MNAR)

    **Descripción**: Los datos faltantes están relacionados con el propio valor que falta. Es decir, la falta de datos no es aleatoria y depende del valor que se espera obtener.

    **Ejemplo**: En un estudio de salud, los pacientes más enfermos podrían ser menos propensos a responder a preguntas sobre su estado de salud, lo que hace que los datos faltantes estén relacionados con la gravedad de su enfermedad.

    **Implicaciones**: La imputación es más complicada y puede ser sesgada, ya que la falta de datos está relacionada con la variable que se está estudiando. En este caso, podría ser necesario usar técnicas más avanzadas o hacer suposiciones sobre los datos faltantes.

Resumen

- **MCAR**: Falta de datos aleatoria; las imputaciones simples funcionan bien.
- **MAR**: Falta de datos relacionada con otras variables observadas; métodos de imputación más sofisticados son útiles.
- **MNAR**: Falta de datos relacionada con los propios valores que faltan; requiere atención especial y puede ser difícil de manejar.

Conocer la naturaleza de los datos faltantes te ayudará a elegir el método de imputación adecuado.


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

# KNNImputer en Python
Claro, te explico cómo funciona el **KNN Imputer** paso a paso con un ejemplo sencillo de dos columnas.

### ¿Qué es el KNN Imputer?
El **KNN Imputer** (K-Nearest Neighbors Imputer) es un método que utiliza los valores de los vecinos más cercanos para rellenar los valores faltantes en el dataset. Funciona buscando las observaciones más parecidas (vecinos) a la que tiene un valor faltante y usa los valores de esos vecinos para imputar (rellenar) el valor perdido.

### Ejemplo paso a paso:
Imagina que tienes un dataset con dos columnas: `MinTemp` y `MaxTemp`, donde algunos valores están faltando.

| MinTemp | MaxTemp |
|---------|---------|
| 20      | 35      |
| Nan     | 40      |
| 22      | 37      |
| NaN     | Nan     |
| 21      | NaN     |
| 23      | 39      |

Vamos a imputar los valores faltantes en este dataset usando el **KNN Imputer** con `k=2` (es decir, usaremos los 2 vecinos más cercanos para imputar los valores faltantes).

### Cálculo de distancias
El KNN Imputer calcula la **distancia** entre las filas completas (sin valores faltantes) y las filas con valores faltantes. Usualmente, la distancia que se utiliza es la **distancia euclidiana**.

### Caso 1: Fila con un valor faltante
Cuando tienes una fila como `MinTemp = NaN` y `MaxTemp = 40`, al calcular la distancia con otra fila completa, ignoras la parte que tiene **NaN**.

Ejemplo:

- Fila con valores faltantes: `MinTemp = NaN`, `MaxTemp = 40`
- Otra fila completa: `MinTemp = 20`, `MaxTemp = 35`

La distancia euclidiana se calcula como:

$$
\text{Distancia} = \sqrt{(MinTemp_{fila1} - MinTemp_{fila2})^2 + (MaxTemp_{fila1} - MaxTemp_{fila2})^2}
$$


Pero dado que `MinTemp` es **NaN**, se omite esa parte, quedando:

$$
\text{Distancia} = \sqrt{(Nan - 20)^2 + (40 - 35)^2} = \sqrt{5^2} = 5
$$

Se decarta la parte con NaN y se calcula la distancia solo con los valores completos.

---

Vamos fila por fila:

Notar que solo se consideran las filas completas para calcular la distancia y no se toman en cuenta las filas imputadas en pasos anteriores (no es iterativo).

1) **Fila 1** (NaN, 40):
   * Necesitamos imputar MinTemp
   * Buscamos las 2 filas más cercanas basándonos en MaxTemp=40
   * Las más cercanas son:
        - Fila 0: MinTemp=20 → MaxTemp=35
        $$\text{Distancia} = \sqrt{(40 - 35)^2} = \sqrt{5^2} = 5$$
        - Fila 2: MinTemp=22 → MaxTemp=37
        $$\text{Distancia} = \sqrt{(40 - 37)^2} = \sqrt{3^2} = 3  \quad \checkmark$$
        - Fila 5: MinTemp=23 → MaxTemp=39
        $$\text{Distancia} = \sqrt{(40 - 39)^2} = \sqrt{1^2} = 1 \quad \checkmark$$

    Los dos vecinos más cercanos son las filas 2 y 5.
    * MinTemp imputado = (22 + 23)/2 = 22.5

2) **Fila 3** (NaN, NaN):
   * Al ser todos NaN: Cuando una fila tiene todos los valores faltantes, el imputador KNN en scikit-learn imputa los valores faltantes con la media de la columna. Este comportamiento se implementa en el método de transformación de la clase KNNImputer. 

    - MinTemp imputado = (20 + 22 + 21 + 23)/4 = 21.5 (fila 3 MinTemp)
    - MaxTemp imputado = (35 + 40 + 37 + 39)/4 = 38.5 (fila 3 MaxTemp)

3) **Fila 4** (21, NaN):
    - Buscamos las 2 filas más cercanas basándonos en MinTemp=21
    - Las más cercanas son:
        - Fila 0: MinTemp=20 → MaxTemp=35
            $$\text{Distancia} = \sqrt{(21 - 20)^2 + (NaN - 35)^2} = \sqrt{1^2} = 1 \quad \checkmark$$
        - Fila 2: MinTemp=22 → MaxTemp=37
            $$\text{Distancia} = \sqrt{(22 - 21)^2} = \sqrt{1^2} = 1 \quad \checkmark$$
        - Fila 5: MinTemp=23 → MaxTemp=39
            $$\text{Distancia} = \sqrt{(23 - 21)^2} = \sqrt{2^2} = 2$$ 

    Los dos vecinos más cercanos son las filas 0 y 2.
    - MaxTemp imputado = (35 + 37)/2 = 36

El resultado final sería:

| MinTemp | MaxTemp |
|---------|---------|
| 20      | 35      |
| **22.5**    | 40      |
| 22      | 37      |
| **21.5**   | **38.5**    |
| 21      | **36**      |
| 23      | 39      |


# MissForest
from missingpy import MissForest

# Iterative imputer
Claro, te explico los parámetros principales del `IterativeImputer` y luego te detallo los pasos para imputar valores faltantes usando el ejemplo anterior.

### Parámetros del `IterativeImputer`

1. **estimator**: El modelo que se utilizará para predecir los valores faltantes. Por defecto, es `BayesianRidge`, pero puedes usar otros modelos como `LinearRegression`.

2. **missing_values**: El marcador de posición para los valores faltantes. Por defecto, es `np.nan`.

3. **sample_posterior**: Si se debe tomar una muestra del posterior predictivo (gaussiano) del estimador ajustado para cada imputación. Útil para imputaciones múltiples. Por defecto, es `False`.

4. **max_iter**: Número máximo de rondas de imputación a realizar. Cada ronda implica una imputación de cada característica con valores faltantes. Por defecto, es `10`.

5. **tol**: Tolerancia de la condición de parada. El proceso se detiene si el cambio relativo entre iteraciones es menor que este valor. Por defecto, es `1e-3`.

6. **n_nearest_features**: Número de otras características a usar para estimar los valores faltantes de cada columna. Si es `None`, se usan todas las características. Por defecto, es `None`.

7. **initial_strategy**: Estrategia inicial para imputar valores faltantes antes de comenzar las iteraciones. Puede ser `'mean'`, `'median'`, `'most_frequent'` o `'constant'`. Por defecto, es `'mean'`.

8. **imputation_order**: Orden en el que se imputan las características. Puede ser `'ascending'`, `'descending'`, `'roman'`, `'arabic'` o `'random'`. Por defecto, es `'ascending'`.

9. **random_state**: Semilla para el generador de números aleatorios. Útil para reproducibilidad. Por defecto, es `None`.

### Pasos para Imputar Valores Faltantes

1. **Inicialización**:
   - Se inicia con un DataFrame que contiene valores faltantes. En tu caso, las columnas `A`, `B` y `C` tienen algunos valores `NaN`.
   
2. **Imputación Inicial**:
   - Se usa un `initial_strategy='mean'`, que significa que primero se llenan los valores faltantes con la media de las columnas. Esto crea un primer conjunto de datos completo (aunque aproximado).

   Para tus datos:
   - Media de `A`: $$\frac{25 + 27 + 29 + 31 + 33}{5} = 29 $$ (el NaN se reemplaza por 29).
   - Media de `B`: $$ \frac{3 + 5 + 7 + 9 + 11}{5} = 7 $$ (se reemplaza el NaN por 7).
   - Media de `C`: $$ \frac{50 + 80 + 90 + 100 + 130}{5} = 90 $$ (se reemplaza el NaN por 90).

   El DataFrame después de la imputación inicial se vería así:

   |Fila |    A   |   B   |    C   |
   |--- |:------:|:-----:|:------:|
   | 0 |  25.0  |  ${\color{green}7.0}$  |  50.0  |
   |1 |  27.0  |  3.0  |  ${\color{green}90.0}$  |
   |2 |  29.0  |  5.0  |  80.0  |
   |3 |  31.0  |  7.0  |  90.0  |
   |4 |  33.0  |  9.0  | 100.0  |
   |5 |  ${\color{green}29.0}$  | 11.0  | 130.0  |


3. **Primer Iteración**:
    - step 1: Se imputa `A[5]` usando las columnas `B` y `C`.

        |Fila |    A   |   B   ||    C   |
        |--- |:------:|:-----:|:------:|:------:|
        | 0 |  25.0  |  ${\color{green}7.0}$  ||  50.0  |
        |1 |  27.0  |  3.0  ||  ${\color{green}90.0}$  |
        |2 |  29.0  |  5.0  ||  80.0  |
        |3 |  31.0  |  7.0  ||  90.0  |
        |4 |  33.0  |  9.0  || 100.0  |

        Se entrenan dos modelos de regresión lineal con las columnas `A` y `B` para predecir `A[5]`.
        ```python
        model = LinearRegression()
        model.fit(df[['B','C']], df['A'])
        model.predict([[11, 130]])  # Predicción para A[5]= 38.75
        ``` 
   
        |Fila |    A   |   B   |    C   |
        |--- |:------:|:-----:|:------:|
        | 0 |  25.0  |  ${\color{green}7.0}$  |  50.0  |
        |1 |  27.0  |  3.0  |  ${\color{green}90.0}$  |
        |2 |  29.0  |  5.0  |  80.0  |
        |3 |  31.0  |  7.0  |  90.0  |
        |4 |  33.0  |  9.0  | 100.0  |
        |5 |  ${\color{yellow}38.75}$  | 11.0  | 130.0  |

    - step 2: Se imputa `B[0]` usando las columnas `A` y `C`.

        |Fila |    A   |   C  ||    B   |
        |--- |:------:|:-----:|:------:|:------:|
        |1 |  27.0  |   ${\color{green}90.0}$  ||  3.0  |
        |2 |  29.0  |  80.0  ||  5.0  |
        |3 |  31.0  |  90.0  ||  7.0  |
        |4 |  33.0  | 100.0  ||  9.0  |
        |5 |  ${\color{green}38.75}$  | 130.0  || 11.0  |


        Se entrenan dos modelos de regresión lineal con las columnas `A` y `C` para predecir `B[0]`.
        ```python
            model = LinearRegression()
            model.fit(df[['A','C']], df['B'])
            model.predict([[25, 50]]) # Predicción para B[0]= 4.05
        ```
        |Fila |    A   |   B   |    C   |
        |--- |:------:|:-----:|:------:|
        | 0 |  25.0  |  ${\color{yellow}4.05}$  |  50.0  |
        |1 |  27.0  |  3.0  |  ${\color{green}90.0}$  |
        |2 |  29.0  |  5.0  |  80.0  |
        |3 |  31.0  |  7.0  |  90.0  |
        |4 |  33.0  |  9.0  | 100.0  |
        |5 |  ${\color{green}38.75}$  | 11.0  | 130.0  |

    - step 2: Se imputa `C[1]` usando las columnas `A` y `B`.

        |Fila |    A   |   B  ||    C   |
        |--- |:------:|:-----:|:------:|:------:|
        |0 |  25.0  |   ${\color{green}4.05}$  ||  50.0  |
        |2 |  29.0  |  80.0  ||  80.0  |
        |3 |  31.0  |  90.0  ||  90.0  |
        |4 |  33.0  | 100.0  || 100.0  |
        |5 |  ${\color{green}38.75}$  | 130.0  || 130.0  |

        Se entrenan dos modelos de regresión lineal con las columnas `A` y `B` para predecir `C[1]`.
        ```python
            model = LinearRegression()
            model.fit(df[['A','B']], df['C'])
            model.predict([[27, 3]]) # Predicción para C[1]= 68.53
        ```
        |Fila |    A   |   B   |    C   |
        |--- |:------:|:-----:|:------:|
        | 0 |  25.0  |  ${\color{green}4.05}$  |  50.0  |
        |1 |  27.0  |  3.0  |  ${\color{yellow}68.53}$  |
        |2 |  29.0  |  5.0  |  80.0  |
        |3 |  31.0  |  7.0  |  90.0  |
        |4 |  33.0  |  9.0  | 100.0  |
        |5 |  ${\color{green}38.75}$  | 11.0  | 130.0 |

        