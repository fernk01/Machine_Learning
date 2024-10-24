# Descenso del Gradiente
El **descenso del gradiente** es un algoritmo de optimización utilizado para encontrar los valores mínimos de una función, que en el contexto del aprendizaje automático generalmente se refiere a la minimización de una función de pérdida. Es una técnica clave en el entrenamiento de modelos de machine learning, especialmente en regresión y redes neuronales.

### Conceptos Clave

1. **Función de Pérdida**: Es una función que mide cuán bien está funcionando un modelo. Por ejemplo, en un problema de regresión, la función de pérdida puede ser el error cuadrático medio entre las predicciones del modelo y los valores reales.

2. **Gradiente**: Es un vector que indica la dirección y la tasa de cambio de la función. En el contexto del descenso del gradiente, el gradiente de la función de pérdida se utiliza para determinar cómo ajustar los parámetros del modelo.

3. **Parámetros del Modelo**: Son los valores que se ajustan durante el entrenamiento para minimizar la función de pérdida (por ejemplo, los coeficientes en una regresión lineal).

### Proceso del Descenso del Gradiente

1. **Inicialización**: Comienza con un conjunto inicial de parámetros (pueden ser elegidos aleatoriamente).

2. **Cálculo del Gradiente**: Calcula el gradiente de la función de pérdida en relación con los parámetros actuales. Esto implica derivar la función de pérdida.

3. **Actualización de Parámetros**: Ajusta los parámetros en la dirección opuesta al gradiente. Esto se hace mediante la siguiente fórmula:
   $$
   \theta_{i+1}  := \theta_{i} - \alpha \cdot \nabla J(\theta)
   $$
   donde:
   - $ \theta $ son los parámetros del modelo.
   - $ \alpha $ es la tasa de aprendizaje (un hiperparámetro que controla el tamaño del paso en cada iteración).
   - $ \nabla J(\theta) $ es el gradiente de la función de pérdida.
    $$ \nabla J(\theta) = \frac{1}{N} \cdot \sum_{i=1}^{N} \nabla L(y_i, f(x_i; \theta)) $$

4. **Iteración**: Repite el cálculo del gradiente y la actualización de parámetros hasta que la función de pérdida converja a un valor mínimo o hasta que se alcance un número máximo de iteraciones.

### Tipos de Descenso del Gradiente

1. **Descenso del Gradiente Batch**: Usa todo el conjunto de datos para calcular el gradiente en cada iteración. Es preciso, pero puede ser lento y consumir mucha memoria.

2. **Descenso del Gradiente Estocástico (SGD)**: Actualiza los parámetros utilizando solo un ejemplo de datos a la vez. Esto hace que el proceso sea más rápido y pueda escapar de mínimos locales, pero la convergencia puede ser más ruidosa.

3. **Descenso del Gradiente Mini-batch**: Combina las ventajas de ambos métodos anteriores, utilizando un pequeño subconjunto (mini-batch) del conjunto de datos para cada actualización.

# Descenso del Gradiente Batch

## Ejemplo 1:Regresión Lineal Simple

| index | X  | y  |
|-- |----|----|
| 0 | 7  | 2  |
| 1 | 1  | 9  |
| 2 | 10 | 2  |
| 3 | 5  | 5  |
| 4 | 4  | 7  |
| 5 | 3  | 11 |
| 6 | 13 | 2  |
| 7 | 10 | 5  |
| 8 | 2  | 14 |

Para realizar el cálculo de una regresión lineal simple usando mínimos cuadrados (RSS), necesitamos ajustar una línea a los datos $X$ y $y$ minimizando la suma de los cuadrados de los errores. La ecuación de la recta es:

$$ y = b_0 + b_1 \cdot x $$

donde:
- $b_0$ es la ordenada al origen (intercepto),
- $b_1$ es la pendiente de la línea.

### Función de Pérdida RSS (Suma de los Cuadrados Residuales)

La función de pérdida que queremos minimizar es:

$$ RSS = \sum_{i=1}^{n} (y_i - \hat{y}_i)^2 = \sum_{i=1}^{n} (y_i - (b_0 + b_1 \cdot x_i))^2 $$

Para encontrar $b_0$ y $b_1$ que minimicen esta función, usamos las siguientes fórmulas:

$$ b_1 = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sum (x_i - \bar{x})^2} $$

$$ b_0 = \bar{y} - b_1 \cdot \bar{x} $$

donde:
- $\bar{x}$ y $\bar{y}$ son los promedios de $X$ e $y$, respectivamente.

### Paso a Paso de los Cálculos

1. **Calcular $\bar{x}$ y $\bar{y}$**:
   
$$ \bar{x} = \frac{\sum x_i}{n}, \quad \bar{y} = \frac{\sum y_i}{n}
 $$

2. **Calcular $b_1$**:
   
$$ b_1 = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sum (x_i - \bar{x})^2}
 $$

3. **Calcular $b_0$**:
   
$$ b_0 = \bar{y} - b_1 \cdot \bar{x}
 $$

Los valores calculados para la regresión lineal son:

- **Intercepto $b_0$**: 11.48
- **Pendiente $b_1$**: -0.84

La ecuación de la recta que ajusta los datos sería:

$$ \hat{y} = 11.48 - 0.84 \cdot x $$

Esto significa que, por cada unidad que aumenta $X$, $y$ disminuye aproximadamente 0.84 unidades.

## Ejemplo 2: Regresión Lineal Simple con Descenso del Gradiente

Para calcular los parámetros de la regresión lineal usando el método de **descenso del gradiente**, necesitamos minimizar la función de pérdida que en este caso es la **Suma de los Cuadrados Residuales (RSS)**. La idea es encontrar los valores de $b_0$ y $b_1$ que minimicen esta función usando gradiente descendente.

### Recordando la función de pérdida (RSS)

La función de pérdida es:

$$ J(b_0, b_1) = \frac{1}{n} \sum_{i=1}^{n} (y_i - (b_0 + b_1 \cdot x_i))^2 $$

Aquí queremos ajustar los parámetros $b_0$ y $b_1$ para minimizar $J(b_0, b_1)$.

#### ¿Por qué $ \frac{1}{n} $ en la Función de Pérdida?

El término $ \frac{1}{n} $ en la función de pérdida se utiliza para calcular el **promedio** de los errores al cuadrado, donde $ n $ es el número de muestras en el conjunto de datos. Esto ayuda a que la función de pérdida no dependa del tamaño del conjunto de datos. Al promediar los errores, se asegura que la magnitud de la pérdida sea comparable, sin importar si se tienen pocos o muchos datos.

Sin el término $ \frac{1}{n} $, la suma de los cuadrados residuales crecería con el tamaño del conjunto de datos, lo que dificultaría comparar los resultados entre diferentes conjuntos de datos. Por lo tanto, se usa para tener una medida más estable y consistente del error.

### Gradiente Descendente para Mínimos Cuadrados

Para ajustar los parámetros, usamos el gradiente descendente:

1. Inicializamos $b_0$ y $b_1$ con valores aleatorios o ceros.
2. Actualizamos los parámetros usando las derivadas parciales de $J$ con respecto a $b_0$ y $b_1$:

    $$ b_0 = b_0 - \alpha \cdot \frac{\partial J}{\partial b_0} $$

    $$ b_1 = b_1 - \alpha \cdot \frac{\partial J}{\partial b_1} $$

donde:
- $\alpha$ es la tasa de aprendizaje (qué tan grandes son los pasos que damos),
- $\frac{\partial J}{\partial b_0}$ y $\frac{\partial J}{\partial b_1}$ son las derivadas parciales de la función de pérdida con respecto a $b_0$ y $b_1$:

$$ \frac{\partial J}{\partial b_0} = -\frac{2}{n} \sum_{i=1}^{n} (y_i - (b_0 + b_1 \cdot x_i)) $$

$$ \frac{\partial J}{\partial b_1} = -\frac{2}{n} \sum_{i=1}^{n} (y_i - (b_0 + b_1 \cdot x_i)) \cdot x_i $$

#### Cálculos
Se comienza con valores iniciales (pueden ser aleatorios) de $b_0 = 0$ y $b_1 = 0$, y se actualizan iterativamente utilizando el gradiente descendente. La tasa de aprendizaje $\alpha$ se fija en 0.01 (es un hiperparametro).

$$ b_0 = 0 - 0.01 \cdot \left(\frac{2}{9} \cdot \sum_{i=0}^{9} y_i \right) = - 0.01 \cdot \frac{2}{9} \cdot 57 = 0.00126 $$

En este caso $b_0 = b_1$.

# Descenso del Gradiente Estocástico (SGD)
[link you tube](https://www.youtube.com/watch?v=Bap0WNIaYHQ)

El **descenso del gradiente estocástico (SGD)** es una variante del descenso del gradiente que actualiza los parámetros del modelo utilizando solo **un** ejemplo de datos a la vez de manera aleatoria. A diferencia del descenso del gradiente batch, que utiliza todo el conjunto de datos para calcular el gradiente en cada iteración, el SGD es más rápido y puede escapar de mínimos locales, pero la convergencia puede ser más ruidosa.

Aunque el SGD puede ser más ruidoso en su convergencia, esa variabilidad puede ayudar a escapar de mínimos locales en funciones de pérdida no convexas. También conviene aclarar que "aleatorio" se refiere a que cada muestra se selecciona de forma aleatoria o siguiendo un orden fijo, pero se considera una por una en cada iteración.

$$ \theta_{i+1}  := \theta_{i} - \alpha \cdot \nabla J(\theta) $$

#### Calculo
1. Inicializar los parámetros del modelo.
2. Para cada iteración:
   - Seleccionar un ejemplo aleatorio del conjunto de datos.
   - Calcular el gradiente de la función de pérdida en relación con los parámetros actuales utilizando ese ejemplo.
   - Actualizar los parámetros en la dirección opuesta al gradiente.
3. Repetir el proceso hasta que la función de pérdida converja o se alcance un número máximo de iteraciones.

La expresión del gradiente

$$ \nabla J(b_0, b_1) = \frac{1}{n} \cdot \sum_{i=1}^{n} (y_i - (b_0 + b_1 \cdot x_i))^2$$

como solo tenemos **un** ejemplo $n=1$.

### Ejemplo SDG

1. **Inicialización**: Comienza con valores aleatorios para $ b_0 $ y $ b_1 $.
2. **Para cada iteración**:
   - Selecciona un ejemplo aleatorio del conjunto de datos (por ejemplo, $ x_3 = 5 $ y $ y_3 = 5 $).
   - Calcula los gradientes parciales:
     $$ \frac{\partial J}{\partial b_0} = - 2 \cdot (y_i - (b_0 + b_1 \cdot x_i)) $$
     $$ \frac{\partial J}{\partial b_1} = - 2 \cdot (y_i - (b_0 + b_1 \cdot x_i)) \cdot x_i $$
   - Actualiza los parámetros:
     $$ b_0 = b_0 - \alpha \cdot \frac{\partial J}{\partial b_0} $$
     $$ b_1 = b_1 - \alpha \cdot \frac{\partial J}{\partial b_1} $$
3. **Repetir** hasta que se alcance la convergencia o el número máximo de iteraciones.


# Links
- [DocCV Descenso del Gradiente](https://www.youtube.com/watch?v=A6FiCDoz8_4)














