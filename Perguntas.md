1. Cuál de los siguientes métodos en Pandas es menos performante pararealizar una agregación?
    - apply $\checkmark$
    - agg
    - transform
    - sum



El método `apply()` en pandas tiende a ser menos eficiente en términos de rendimiento en comparación con los métodos `agg()`, `transform()` y `sum()`. Esto se debe a que `apply()` es un método más general que puede tomar cualquier función arbitraria. Esto significa que pandas no puede hacer las mismas optimizaciones que puede hacer con `agg()`, `transform()` y `sum()`, que están diseñados para operaciones específicas³.

Por ejemplo, si quisieras calcular la suma de una columna en un DataFrame agrupado, usar `sum()` sería más rápido que usar `apply()` con una función personalizada para calcular la suma⁴. Aquí tienes un ejemplo:

```python
import pandas as pd
import numpy as np

# Crear un DataFrame de ejemplo
df = pd.DataFrame({
    'A': np.random.choice(['foo', 'bar', 'baz'], size=5000),
    'B': np.random.rand(5000),
})

# Usar apply() con una función personalizada para calcular la suma
%timeit df.groupby('A').apply(lambda x: np.sum(x['B']))

# Usar sum() para calcular la suma
%timeit df.groupby('A')['B'].sum()
```

En este ejemplo, encontrarás que usar `sum()` es significativamente más rápido que usar `apply()` con una función personalizada para calcular la suma⁴. Sin embargo, `apply()` sigue siendo útil por su flexibilidad, ya que puede manejar operaciones más complejas que no se pueden realizar con los métodos de agregación incorporados³.
