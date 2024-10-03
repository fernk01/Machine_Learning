# Feature Engineering
Esta etapa incluye cualquier proceso de modificación de la forma de los datos (es común que los datos sufran algún tipo de **transformación**)

El objetivo principal de esta etapa es mejorar el rendimiento de los modelos creados mediante la transformación de los datos que utilizan

**Algunas técnicas son:**
- Creación de nuevas variables
- Transformación de variables
    - Normalización
        - Min-Max Scaling: $sklearn.preprocessing.MinMaxScaler$
        - Z-Score Normalization (Standardization): $sklearn.preprocessing.StandardScaler$
        - Decimal Scaling: $sklearn.preprocessing.StandardScaler$
    - Estandarización: $sklearn.preprocessing.StandardScaler$
    - Discretización: $sklearn.preprocessing.KBinsDiscretizer$

## Normalización
Se aplica sobre valores numéricos.

Consiste en escalar los features de manera que puedan ser mapeados a un rango más pequeño. Por ejemplo: 0 a 1 o 1 a 1.


Es principalmente utilizada cuando:
- Las unidades de medidas dificultan la comparación de features.
- Se quiere evitar que atributos con mayores magnitudes tengan pesos muy diferentes al resto

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

## Discretización