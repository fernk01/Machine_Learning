# Feature Engineering
Esta etapa incluye cualquier proceso de modificación de la forma de los datos (es común que los datos sufran algún tipo de **transformación**)

El objetivo principal de esta etapa es mejorar el rendimiento de los modelos creados mediante la transformación de los datos que utilizan

**Algunas técnicas son:**
- Creación de nuevas variables
- Transformación de variables
    | Técnica                          | Descripción                                                                 | Librería                             |
    |----------------------------------|-----------------------------------------------------------------------------|--------------------------------------|
    | Min-Max Scaling                  | Escala los datos entre 0 y 1; útil para datos sin outliers.                 | `sklearn.preprocessing.MinMaxScaler` |
    | Z-Score Normalization (Standardization) | Ajusta los datos para que tengan media 0 y desviación estándar 1; buena para datos con outliers. | `sklearn.preprocessing.StandardScaler` |
    | Decimal Scaling                  | Asegura que cada valor normalizado se encuentra entre -1 y 1.               | `sklearn.preprocessing.StandardScaler` |
    | Estandarización                  | Transforma los datos para que tengan una media de 0 y una desviación estándar de 1. | `sklearn.preprocessing.StandardScaler` |
    | Discretización                   | Convierte variables continuas en discretas.                                 | `sklearn.preprocessing.KBinsDiscretizer` |

## Normalización
Se aplica sobre valores numéricos. [leer](https://medium.com/analytics-vidhya/why-is-scaling-required-in-knn-and-k-means-8129e4d88ed7)

Consiste en escalar los features de manera que puedan ser mapeados a un rango más pequeño. Por ejemplo: 0 a 1 o 1 a 1.


Es principalmente utilizada cuando:
- Las unidades de medidas dificultan la comparación de features.
- Se quiere evitar que atributos con mayores magnitudes tengan pesos muy diferentes al resto

Tipos de normalización:
- Min-Max Scaling: Escala los datos entre 0 y 1; útil para datos sin **outliers**.
- Estandarización (Z-score): Ajusta los datos para que tengan media 0 y desviación estándar 1; buena para datos con outliers.
- Escalado robusto: Utiliza la mediana y el rango intercuartílico; ideal para datos muy sesgados.

La normalización es especialmente importante para modelos sensibles a la escala de los datos, como:

1. **Regresión lineal**: Puede afectar la convergencia del algoritmo.
2. **K-vecinos más cercanos (KNN)**: La distancia entre puntos se ve alterada.
3. **Máquinas de soporte vectorial (SVM)**: La separación de clases puede ser ineficaz sin normalización.
4. **Redes neuronales**: La convergencia puede ser más lenta y menos efectiva sin una escala uniforme.
5. **Clustering (como K-means)**: La asignación de clusters se ve afectada por la escala de las variables.

Normalizar ayuda a mejorar el rendimiento y la estabilidad de estos modelos.

### Min-Max Scaling
```python	
from sklearn.preprocessing import MinMaxScaler
```	

Funciona al ver cuánto más grande es el valor actual del valor mínimo del feature y escala esta diferencia por el rango.

$$ X_{norm} = \frac{X - X_{min}}{X_{max} - X_{min}} $$

Donde:
- $X_{norm}$ es el valor normalizado
- $X$ es el valor original
- $X_{min}$ es el valor mínimo del feature
- $X_{max}$ es el valor máximo del feature

Los valores normalizados estarán en el rango de 0 a 1.

Ejemplo:
$$vector = [1, 2, 3, 4, 5, 6]$$
Si aplicamos Min-Max Scaling, el vector normalizado sería:
$$vector = [0, 0.2, 0.4, 0.6, 0.8, 1]$$

### Normalizar en función de la norma
```python
from sklearn.preprocessing import Normalizer
```
Utiliza la norma L1 o L2 para normalizar los datos.

$$ X_{norm} = \frac{X}{||X||} $$


### Decimal Scaling
Asegura que cada valor normalizado se encuentra entre -1 y 1.
    $$ X_{norm} = \frac{X}{10^d} $$
Donde:
- $X_{norm}$ es el valor normalizado
- $X$ es el valor original
- $d$ representa el número de dígitos en los valores de la variable con el valor absoluto más grande

## Estandarización
Se aplica sobre valores numéricos.

Consiste en transformar los datos para que tengan una media de 0 y una desviación estándar de 1.

Se utiliza cuando los datos tienen una distribución normal o cuando se requiere que los datos tengan una distribución normal.

```python
from sklearn.preprocessing import StandardScaler
```
### Z-Score Normalization
Los valores para un atributo se normalizan en base a su media y desvío estándar

$$ X_{norm} = \frac{X - \mu}{\sigma} $$
Donde:
- $X_{norm}$ es el valor normalizado
- $X$ es el valor original
- $\mu$ es la media del feature $X$
- $\sigma$ es la desviación estándar del feature $X$

Los valores normalizados tendrán una media de 0 y una desviación estándar de 1.
Los valores para un atributo se normalizan en base a su media y desvío estándar.


### Comparación entre RobustScaler y StandardScaler

La diferencia clave entre `RobustScaler` y `StandardScaler` radica en cómo manejan los outliers y la sensibilidad a la distribución de los datos:

1. **RobustScaler**:
   - **Uso de Mediana y IQR**: Utiliza la mediana y el rango intercuartílico (IQR) para escalar los datos. Esto significa que es menos afectado por valores atípicos.
   - **Ideal para Datos con Outliers**: Si tus datos tienen outliers significativos, `RobustScaler` es más adecuado porque proporciona una representación más robusta de la mayoría de los datos.

2. **StandardScaler**:
   - **Uso de Media y Desviación Estándar**: Escala los datos utilizando la media y la desviación estándar. Esto significa que es sensible a los outliers.
   - **Suponiendo Normalidad**: Funciona mejor cuando los datos están distribuidos normalmente y no tienen muchos valores atípicos.

#### Cuándo Usar Cada Uno:
- **Usa `RobustScaler`** si tus datos tienen outliers y no se distribuyen de manera normal.
- **Usa `StandardScaler`** si tus datos están más cerca de una distribución normal y no tienen valores atípicos significativos.

En resumen, `RobustScaler` es mejor en situaciones donde la robustez frente a outliers es una prioridad.

## Discretización

## Eliminación de Ruido
La reducción de dimensionalidad y la binarización son conceptos diferentes, aunque pueden estar relacionados en ciertos contextos.

### Binarización
Binarizar un conjunto de datos implica convertir las características a un formato binario (0 o 1). Esto puede ser útil para simplificar los datos y facilitar su procesamiento en ciertos algoritmos, como en modelos de clasificación o clustering. Sin embargo, no se considera reducción de dimensionalidad en sí misma; más bien, es una transformación de los datos.

### Reducción de Dimensionalidad
La reducción de dimensionalidad se refiere a técnicas que disminuyen el número de características en un conjunto de datos mientras se intenta conservar la información relevante. Métodos comunes incluyen PCA (Análisis de Componentes Principales), t-SNE y UMAP. Estas técnicas buscan representar los datos en un espacio de menor dimensión.

### Eliminación de Ruido
La eliminación de ruido se refiere al proceso de reducir o eliminar datos irrelevantes o perturbaciones en un conjunto de datos. Esto puede incluir:

- **Filtrado de datos**: Eliminar características que no aportan información significativa.
- **Eliminación de outliers**: Identificar y quitar datos atípicos que pueden distorsionar el análisis.
- **Suavizado**: Usar técnicas que reducen la variabilidad en los datos sin perder tendencias significativas.

La eliminación de ruido es importante porque puede mejorar la calidad del modelo y su capacidad de generalización.

Existen varias técnicas de suavizado que se utilizan para reducir la variabilidad en los datos sin sacrificar las tendencias significativas. Algunas de las más comunes son:

1. **Media Móvil**: Se calcula la media de un conjunto de puntos de datos en una ventana deslizante. Esto ayuda a suavizar las fluctuaciones a corto plazo.

2. **Suavizado Exponencial**: Asigna pesos decrecientes a los datos pasados, lo que permite que las observaciones más recientes tengan más influencia en el valor suavizado.

3. **Filtros de Kalman**: Un método estadístico que estima el estado de un sistema dinámico y reduce el ruido en los datos mediante un proceso de predicción y corrección.

4. **Spline de Curva**: Utiliza funciones polinómicas para ajustar una curva a un conjunto de datos, proporcionando una forma suave que puede capturar tendencias en los datos.

5. **Regresión Local (LOESS o LOWESS)**: Ajusta modelos polinómicos locales a diferentes partes del conjunto de datos, permitiendo una mayor flexibilidad y suavizado adaptativo.

6. **Transformaciones Logarítmicas o Raíces**: Estas transformaciones pueden reducir la variabilidad de los datos y ayudar a estabilizar la varianza.

7. **Métodos de Suavizado de Series Temporales**: Como el suavizado de Holt-Winters, que es útil para datos con tendencias y estacionalidades.

Estas técnicas son útiles para mejorar la visualización de los datos y la interpretación de las tendencias, así como para mejorar el rendimiento de los modelos de aprendizaje automático al reducir el ruido en los datos de entrenamiento.