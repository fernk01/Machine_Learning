
# Decision Trees (Árboles de Decisión) [Decision Trees](https://python-course.eu/machine-learning/decision-trees-in-python.php)
Un Árbol de Decisión es un algoritmo de aprendizaje supervisado no paramétrico, que se utiliza tanto para tareas de **clasificación** como de **regresión**. Tiene una estructura de árbol jerárquica, que consta de un nodo raíz, ramas, nodos internos y nodos hoja. Los nodos de decisión realizan evaluaciones para formar subconjuntos homogéneos, que se indican mediante nodos hoja o nodos terminales. Los nodos hoja representan todos los resultados posibles dentro del conjunto de datos.

## Metricas
- **Entropía**: Mide la impureza de un conjunto de datos. Cuanto mayor sea la entropía, mayor será la incertidumbre en los datos. La entropía se calcula como:
    $$ H(S) = - \sum_{i=1}^{n} p_i \log_2(p_i) $$

    - $S$: Conjunto de datos
    - $n$: Número de clases
    - $p_i$: Proporción de la clase i en el conjunto de datos

    Cuanto mayor sea la entropía, mayor será la incertidumbre en los datos y, por lo tanto, mayor será la impureza. En el contexto de un árbol de decisión, se busca dividir el conjunto de datos en subconjuntos más puros, es decir, con menor entropía.

- **Impureza de Gini**: Mide la probabilidad de clasificar incorrectamente un elemento en un conjunto de datos. La impureza de Gini se calcula como:
    $$ Gini(S) = 1 - \sum_{i=1}^{n} p_i^2 $$

    - $S$: Conjunto de datos
    - $n$: Número de clases
    - $p_i$: Proporción de la clase i en el conjunto de datos

    Cuanto menor sea la impureza de Gini, más puro será el conjunto de datos. En un árbol de decisión, se busca dividir el conjunto de datos de manera que se minimice la impureza de Gini en los subconjuntos resultantes.

- **Log Loss (Pérdida Logarítmica)**: Es una métrica utilizada para evaluar la precisión de un clasificador de probabilidades. La pérdida logarítmica se calcula como:
    $$ L_{log}(y, p) = - \frac{1}{N} \cdot \sum_{i=1}^{N} \left( y_i \cdot \log(p_i) + (1 - y_i) \cdot \log(1 - p_i) \right) $$

    - $N$: Número total de observaciones
    - $y_i$: Valor real de la clase (0 o 1)
    - $p_i$: Probabilidad predicha de la clase 1

    La pérdida logarítmica penaliza las predicciones incorrectas más que las correctas. Un valor de pérdida logarítmica más bajo indica un mejor rendimiento del modelo.

- **impurity ponderada (weighted impurity)**: La impureza ponderada se calcula como:
    $$ impurity(S, A) = \sum_{v \in V} \frac{|S_v|}{|S|} \cdot H(S_v) $$

    **Propósito de la impureza Ponderada**

    El propósito de la impureza ponderada es medir la cantidad de desorden o impureza después de dividir el conjunto de datos en función de un atributo específico. La impureza ponderada toma en cuenta tanto la impureza de cada subconjunto como el tamaño de los subconjuntos relativos al conjunto original. 

    Este término nos dice cuánta "impureza" queda en los datos después de realizar una división particular. En otras palabras, evalúa la efectividad de una división para separar los datos en grupos más homogéneos con respecto a la variable objetivo (en este caso, el problema cardíaco).

- **Ganancia de Información**: Mide la reducción en la impureza después de dividir un conjunto de datos en función de un atributo específico. La ganancia de información se calcula como:

    $$IG(S, A) =  impurity(S) - \sum_{v \in \text{valores}(A)} \frac{|S_v|}{|S|} \times impurity(S_v)$$

    donde:
    - $impurity(S)$ es la impureza del conjunto de datos original $S$. (entropy, gini, LogLoss).
    - $A$ es el atributo (o feature) para el cual estamos calculando la ganancia de información.
    - $ \text{valores}(A)$ son los posibles valores del atributo $A$.
    - $S_v$ es el subconjunto de $ S $ para el valor $ v $ del atributo $A$.
    - $\frac{|S_v|}{|S|}$ es la proporción de datos en el subconjunto $S_v$.
    - $impurity(S_v)$ es la impureza del subconjunto $S_v$.


## Ejemplo Hallar el Nodo Raíz en un Árbol de Decisión
| index | edad | colesterol | problema_cardiaco |
|-------|------|------------|------------------|
| 0     | 63   | 233        | 1                |
| 1     | 37   | 250        | 0                |
| 2     | 41   | 204        | 1                |
| 3     | 56   | 236        | 0                |
| 4     | 57   | 354        | 1                |
| 5     | 57   | 192        | 1                |
| 6     | 56   | 294        | 0                |
| 7     | 44   | 263        | 1                |
| 8     | 52   | 199        | 1                |
| 9     | 57   | 168        | 0                |
| 10    | 54   | 239        | 0                |
| 11    | 48   | 275        | 0                |
| 12    | 49   | 266        | 1                |
| 13    | 64   | 211        | 1                |
| 14    | 58   | 283        | 0                |
| 15    | 50   | 219        | 0                |
| 16    | 58   | 340        | 1                |
| 17    | 66   | 226        | 1                |
| 18    | 43   | 247        | 0                |
| 19    | 69   | 239        | 1                |

Para hallar el nodo raíz de un árbol de decisión, seguimos los siguientes pasos:

1. **Calcular la entropía del conjunto de datos original.**
2. **Evaluar las posibles divisiones en cada atributo y calcular la ganancia de información.**
3. **Seleccionar la división con la mayor ganancia de información como nodo raíz.**


### 1. Calcular la Entropía del Conjunto de Datos Original

La entropía es una medida de desorden o impureza en un conjunto de datos. La fórmula para la entropía $H(S)$ de un conjunto de datos $S$ es:
    $$ H(S) = - \left( p_1 \log_2(p_1) + p_0 \log_2(p_0) \right)$$

donde $p_1$ es la proporción de casos positivos y $p_0$ es la proporción de casos negativos.

Tenemos 20 casos en total con 11 casos positivos (problema_cardiaco = 1) y 9 casos negativos (problema_cardiaco = 0):

$p_1 = \frac{11}{20}, \quad p_0 = \frac{9}{20}$

La entropía del conjunto de datos es:

$$H(S) = - \left( \frac{11}{20} \log_2 \left( \frac{11}{20} \right) + \frac{9}{20} \log_2 \left( \frac{9}{20} \right) \right) \approx 0.992$$

### 2. Calcular la Ganancia de Información para Cada Atributo

Para cada atributo, evaluamos todas las posibles divisiones y calculamos la ganancia de información. Vamos a realizar estos cálculos para ambos atributos: Edad y Colesterol.

#### Atributo: Edad

Primero, ordenamos las edades de menor a mayor:

$$37, 41, 43, 44, 48, 49, 50, 52, 54, 56, 56, 57, 57, 57, 58, 58, 63, 64, 66, 69$$

Evaluamos todas las posibles subdivisiones. Comenzamos con la primera fila:

**División: edades <= 37 y edades > 37**

- Izquierda: edades <= 37
  - 0 positivos, 1 negativo
- Derecha: edades > 37
  - 11 positivos, 8 negativos

Calculamos la entropía de cada subconjunto:

$$H(S_{\text{izquierda}}) = 0 \quad \text{(sólo un valor, no hay desorden)}$$

$$H(S_{\text{derecha}}) = - \left( \frac{11}{19} \log_2 \left( \frac{11}{19} \right) + \frac{8}{19} \log_2 \left( \frac{8}{19} \right) \right) \approx 0.994$$

La ganancia de información es:

$$IG(S, \text{edad}) = 0.992 - \left( \frac{1}{20} \times 0 + \frac{19}{20} \times 0.994 \right) \approx 0.992 - 0.944 \approx 0.048$$

Continuamos con las siguientes subdivisiones:

**División: edades <= 41 y edades > 41**

- Izquierda: edades <= 41
  - 1 positivo, 1 negativo
- Derecha: edades > 41
  - 10 positivos, 8 negativos

Entropías:

$$ H(S_{\text{izquierda}}) = - \left( \frac{1}{2} \log_2 \left( \frac{1}{2} \right) + \frac{1}{2} \log_2 \left( \frac{1}{2} \right) \right) = 1 $$

$$ H(S_{\text{derecha}}) = - \left( \frac{10}{18} \log_2 \left( \frac{10}{18} \right) + \frac{8}{18} \log_2 \left( \frac{8}{18} \right) \right) \approx 0.991 $$

Ganancia de información:

$$ IG(S, \text{edad}) = 0.992 - \left( \frac{2}{20} \times 1 + \frac{18}{20} \times 0.991 \right) \approx 0.992 - 0.953 \approx 0.039 $$

**(Continuar este proceso para todas las subdivisiones posibles.)**

#### Atributo: Colesterol

Ordenamos los valores de colesterol de menor a mayor:

$$ 168, 192, 199, 204, 211, 219, 226, 233, 236, 239, 239, 247, 250, 263, 266, 275, 283, 294, 340, 354 $$

Evaluamos todas las posibles subdivisiones.

**División: colesterol <= 168 y colesterol > 168**

- Izquierda: colesterol <= 168
  - 0 positivos, 1 negativo
- Derecha: colesterol > 168
  - 11 positivos, 8 negativos

Entropías:

$$ H(S_{\text{izquierda}}) = 0 $$

$$ H(S_{\text{derecha}}) = - \left( \frac{11}{19} \log_2 \left( \frac{11}{19} \right) + \frac{8}{19} \log_2 \left( \frac{8}{19} \right) \right) \approx 0.994 $$

Ganancia de información:

$$ IG(S, \text{colesterol}) = 0.992 - \left( \frac{1}{20} \times 0 + \frac{19}{20} \times 0.994 \right) \approx 0.048 $$

**División: colesterol <= 192 y colesterol > 192**

- Izquierda: colesterol <= 192
  - 1 positivo, 1 negativo
- Derecha: colesterol > 192
  - 10 positivos, 8 negativos

Entropías:

$$ H(S_{\text{izquierda}}) = 1 $$

$$ H(S_{\text{derecha}}) = - \left( \frac{10}{18} \log_2 \left( \frac{10}{18} \right) + \frac{8}{18} \log_2 \left( \frac{8}{18} \right) \right) \approx 0.991 $$

Ganancia de información:

$$ IG(S, \text{colesterol}) = 0.992 - \left( \frac{2}{20} \times 1 + \frac{18}{20} \times 0.991 \right) \approx 0.039 $$

**(Continuar este proceso para todas las subdivisiones posibles.)**

### 3. Selección del Nodo Raíz

Comparar las ganancias de información para todas las posibles divisiones de ambos atributos. La división con la mayor ganancia de información será el nodo raíz.

## Ejemplo 2
- **Conjunto original \( S \)**:
  - 11 positivos $ p_1 = \frac{11}{20} $
  - 9 negativos  $ p_0 = \frac{9}{20} $

### Cálculo de la Entropía del Conjunto Original:

$$ H(S) = - \left( \frac{11}{20} \log_2 \left( \frac{11}{20} \right) + \frac{9}{20} \log_2 \left( \frac{9}{20} \right) \right) \approx 0.992 $$

### Cálculo de la Impureza de Gini del Conjunto Original:

$$Gini(S) = 1 - \left( \left( \frac{11}{20} \right)^2 + \left( \frac{9}{20} \right)^2 \right) = 0.495$$

### Cálculo del Log Loss del Conjunto Original:

$$ \text{LogLoss}(S) = - \left( \frac{11}{20} \log \left( \frac{11}{20} \right) + \frac{9}{20} \log \left( \frac{9}{20} \right) \right) \approx 0.636$$

Luego, se aplica la fórmula de la ganancia de información utilizando la métrica de impureza correspondiente (entropía, Gini o Log Loss).

## Ejemplo 3
Otro ejemplo [data set categorical](https://python-course.eu/machine-learning/decision-trees-in-python.php) es mas facil, son las mismas cuentas pero lo hace todo junto y se hace medio comufuso.

## Pros VS. Cons
Pros
- Los árboles de decisión son fáciles de interpretar y visualizar.
- Puede capturar fácilmente patrones no lineales.
- Requiere menos procesamiento previo de datos por parte del usuario; por ejemplo, no es necesario **normalizar** las columnas.
- Se puede utilizar para ingeniería de características, como predecir valores faltantes, y es adecuado para la selección de variables.
- El árbol de decisión no tiene suposiciones sobre la distribución debido a la naturaleza no paramétrica del algoritmo.

Contras
- Sensible a datos ruidosos. Puede sobreajustar datos ruidosos.
- La pequeña variación (o varianza) en los datos puede dar como resultado un árbol de decisión diferente. Esto se puede reducir mediante algoritmos de embolsado (Bagging) e impulso (Boosting).
- Los árboles de decisión están sesgados con conjuntos de datos de desequilibrio, por lo que se recomienda equilibrar el conjunto de datos antes de crear el árbol de decisión.

## Consideraciones Adicionales

**Repetición de características en el mismo nivel de rama**: En teoría, es posible que una característica se repita en el mismo nivel de rama de un árbol de decisión, especialmente si estás utilizando un algoritmo de árbol de decisión que permite divisiones multivariadas (es decir, divisiones basadas en más de una característica). Sin embargo, en la práctica, muchos algoritmos de árboles de decisión, incluyendo el algoritmo `DecisionTreeClassifier` de `scikit-learn`, realizan divisiones univariadas (es decir, divisiones basadas en una sola característica), por lo que una característica no se repetiría en el mismo nivel de rama. En cambio, una vez que una característica ha sido utilizada para dividir el conjunto de datos, esa característica no se consideraría para divisiones adicionales en el mismo nivel de rama.
