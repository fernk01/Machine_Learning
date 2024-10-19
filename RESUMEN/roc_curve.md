
# Curva ROC
[VER goggle matrix de confusion](https://developers.google.com/machine-learning/crash-course/classification/thresholding?hl=es-419)

La **curva ROC** (Receiver Operating Characteristic) es una herramienta gráfica que te permite evaluar el rendimiento de un modelo de clasificación binaria en función de diferentes **umbrales** de decisión. La curva ROC representa la relación entre la **tasa de verdaderos positivos (TPR)** y la **tasa de falsos positivos (FPR)** a lo largo de diferentes umbrales de decisión.

- **Matriz de confusión:** Te da una instantánea del desempeño de tu modelo para un umbral de decisión dado.
- **Curva ROC:** Te muestra cómo varía el desempeño de tu modelo al cambiar el umbral de decisión, lo que te permite elegir el umbral óptimo para tu problema específico.
    - Un solo punto en la curva ROC: Cada punto en la curva ROC corresponde a una matriz de confusión específica, calculada con un umbral de decisión diferente.
    - Variando el umbral: Al variar el umbral de decisión, se generan diferentes matrices de confusión, y cada una de ellas contribuirá a un punto en la curva ROC.
- Umbral de decisión: Es el punto de corte en la probabilidad predicha que determina cómo se clasifican las muestras (por ejemplo, si la probabilidad predicha es mayor o igual a 0.5, clasificar como positivo, regresion logistica).

## Construyendo la curva ROC
¡Absolutamente! Entendamos primero por qué necesitamos las probabilidades para construir la curva ROC y cómo obtenerlas.

### ¿Por qué necesitamos las probabilidades?

* **Curva ROC:** Para construir una curva ROC, necesitamos evaluar el desempeño del modelo en un rango de umbrales de decisión. Estos umbrales se aplican directamente a las probabilidades que el modelo asigna a cada instancia.
* **Flexibilidad:** Las probabilidades nos permiten ajustar el punto de corte entre las clases, lo que es fundamental para encontrar el mejor equilibrio entre la sensibilidad y la especificidad del modelo.

### ¿Cómo obtener el vector de probabilidades?

La mayoría de los algoritmos de clasificación en Python (como los de scikit-learn) proporcionan un método para obtener las probabilidades de pertenencia a cada clase. Este método suele llamarse `predict_proba()`.

**Ejemplo con scikit-learn:**

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

# Supongamos que X es tu matriz de características y y es tu vector objetivo
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Entrenamos un modelo de regresión logística
model = LogisticRegression()
model.fit(X_train, y_train)

# Obtenemos las probabilidades para el conjunto de test
y_proba = model.predict_proba(X_test)
```

En este ejemplo:

* `y_proba` será una matriz donde cada fila representa una instancia y cada columna la probabilidad de pertenecer a una clase.
* Si tienes una clasificación binaria, la primera columna suele corresponder a la probabilidad de la clase negativa y la segunda a la probabilidad de la clase positiva.

### Construyendo la curva ROC

Una vez que tienes el vector de probabilidades, puedes utilizar una biblioteca como scikit-learn para calcular los valores de TPR y FPR para diferentes umbrales y construir la curva ROC:

```python
from sklearn.metrics import roc_curve, roc_auc_score

# Calculamos la curva ROC
fpr, tpr, thresholds = roc_curve(y_test, y_proba[:, 1])

# Calculamos el área bajo la curva (AUC)
roc_auc = roc_auc_score(y_test, y_proba[:, 1])
```

* `fpr`: Tasa de falsos positivos
* `tpr`: Tasa de verdaderos positivos
* `thresholds`: Los diferentes umbrales utilizados
* `roc_auc`: Área bajo la curva ROC (AUC)

**En resumen:**

1. **Obtén las probabilidades:** Utiliza el método `predict_proba()` de tu modelo para obtener las probabilidades de pertenencia a cada clase.
2. **Varia el umbral:** Explora diferentes umbrales de decisión.
3. **Calcula métricas:** Para cada umbral, calcula TPR y FPR.
4. **Grafica la curva:** Traza los puntos (FPR, TPR) en un gráfico.


## Ejemplo
Para calcular la curva ROC paso a paso a partir de probabilidades de predicción, podemos partir de los valores reales y las predicciones proporcionadas. Sin embargo, para construir la curva ROC, necesitamos asignar **probabilidades** a las predicciones (en lugar de solo predicciones binarias como "🫑" y "🐺").

### Paso 1: Asignación de Probabilidades

Asumamos que el modelo ha predicho las siguientes probabilidades para que la clase sea 🫑 (tomando 🫑 como la clase positiva):

| Valores Reales | Probabilidades de 🫑 |
|----------------|----------------------|
| 🫑              | 0.9                  |
| 🐺              | 0.2                  |
| 🫑              | 0.7                  |
| 🐺              | 0.3                  |
| 🫑              | 0.8                  |
| 🐺              | 0.4                  |
| 🫑              | 0.6                  |
| 🐺              | 0.2                  |
| 🫑              | 0.5                  |
| 🐺              | 0.3                  |

Ahora tenemos las probabilidades predichas, y podemos comenzar a construir la curva ROC.

### Paso 2: Ordenar por Probabilidades

Primero, ordenamos los datos por las probabilidades de que sea 🫑 en orden descendente, y asignamos etiquetas de clase (🫑=1 y 🐺=0).

| Probabilidad de 🫑 | Valor Real |
|-------------------|------------|
| 0.9               | 🫑 (1)      |
| 0.8               | 🫑 (1)      |
| 0.7               | 🫑 (1)      |
| 0.6               | 🫑 (1)      |
| 0.5               | 🫑 (1)      |
| 0.4               | 🐺 (0)      |
| 0.3               | 🐺 (0)      |
| 0.3               | 🐺 (0)      |
| 0.2               | 🐺 (0)      |
| 0.2               | 🐺 (0)      |

### Paso 3: Calcular TPR y FPR para Cada Umbral

La curva ROC se construye evaluando diferentes umbrales y calculando la tasa de verdaderos positivos (TPR) y la tasa de falsos positivos (FPR) en cada uno. Vamos a hacer este cálculo paso a paso:

1. **Umbral = 0.9**: 
   - **Predicciones**: 🫑 (solo el primer caso).
   - TPR: $ \frac{1}{5} = 0.2 $ (solo un verdadero positivo de 5 posibles 🫑).
   - FPR: $ \frac{0}{5} = 0 $ (ningún falso positivo).

2. **Umbral = 0.8**: 
   - **Predicciones**: 🫑 (primeros dos casos).
   - TPR: $ \frac{2}{5} = 0.4 $.
   - FPR: $ \frac{0}{5} = 0 $.

3. **Umbral = 0.7**: 
   - **Predicciones**: 🫑 (primeros tres casos).
   - TPR: $ \frac{3}{5} = 0.6 $.
   - FPR: $ \frac{0}{5} = 0 $.

4. **Umbral = 0.6**: 
   - **Predicciones**: 🫑 (primeros cuatro casos).
   - TPR: $ \frac{4}{5} = 0.8 $.
   - FPR: $ \frac{0}{5} = 0 $.

5. **Umbral = 0.5**: 
   - **Predicciones**: 🫑 (primeros cinco casos).
   - TPR: $ \frac{5}{5} = 1.0 $.
   - FPR: $ \frac{0}{5} = 0 $.

6. **Umbral = 0.4**: 
   - **Predicciones**: 🫑 (primeros seis casos).
   - TPR: $ \frac{5}{5} = 1.0 $.
   - FPR: $ \frac{1}{5} = 0.2 $ (un falso positivo).

7. **Umbral = 0.3**: 
   - **Predicciones**: 🫑 (primeros siete casos).
   - TPR: $ \frac{5}{5} = 1.0 $.
   - FPR: $ \frac{3}{5} = 0.6 $.

8. **Umbral = 0.2**: 
   - **Predicciones**: 🫑 (primeros ocho casos).
   - TPR: $ \frac{5}{5} = 1.0 $.
   - FPR: $ \frac{5}{5} = 1.0 $.

### Paso 4: Crear la Curva ROC

Para los valores de TPR (True Positive Rate) y FPR (False Positive Rate) que obtuvimos:

| Umbral  | TPR (Sensibilidad) | FPR (Falsos Positivos) |
|---------|--------------------|-----------------------|
| 0.9     | 0.2                | 0.0                   |
| 0.8     | 0.4                | 0.0                   |
| 0.7     | 0.6                | 0.0                   |
| 0.6     | 0.8                | 0.0                   |
| 0.5     | 1.0                | 0.0                   |
| 0.4     | 1.0                | 0.2                   |
| 0.3     | 1.0                | 0.6                   |
| 0.2     | 1.0                | 1.0                   |

Ahora podemos graficar la curva ROC a partir de estos puntos.

### Paso 5: Graficar la Curva ROC

En la curva ROC, graficamos FPR en el eje X y TPR en el eje Y. A continuación, te muestro cómo hacerlo:

```python
import matplotlib.pyplot as plt

# FPR y TPR calculados
fpr = [0.0, 0.0, 0.0, 0.0, 0.0, 0.2, 0.6, 1.0]
tpr = [0.2, 0.4, 0.6, 0.8, 1.0, 1.0, 1.0, 1.0]

# Graficar la curva ROC
plt.figure()
plt.plot(fpr, tpr, color='darkorange', lw=2, label='Curva ROC')
plt.plot([0, 1], [0, 1], color='navy', lw=2, linestyle='--')  # Línea de no discriminación
plt.xlim([0.0, 1.0])
plt.ylim([0.0, 1.05])
plt.xlabel('Tasa de Falsos Positivos (FPR)')
plt.ylabel('Tasa de Verdaderos Positivos (TPR)')
plt.title('Curva ROC')
plt.legend(loc="lower right")
plt.show()
```

Con estos pasos, construimos la curva ROC, y cada punto corresponde a un umbral diferente. Al cambiar el umbral, cambian los valores de TPR y FPR, que forman la curva.

## interpretación de la Curva ROC
La interpretación de la **curva ROC** y su relación con el umbral de decisión te proporciona información importante sobre el rendimiento del modelo y cómo ajusta sus predicciones en función de las probabilidades. Vamos a desglosar la interpretación de los resultados y lo que el gráfico te dice sobre el modelo.

### 1. **Relación entre el umbral y la curva ROC**

- **Punto de origen (0,0)**: Este punto en la curva ROC corresponde a un **umbral muy alto** (por ejemplo, cercano a 1). Significa que el modelo es muy conservador y clasifica casi todos los casos como negativos (es decir, la clase 🐺), ya que solo considera predicciones positivas (🫑) cuando la probabilidad predicha es extremadamente alta.
  
- **Punto (1,1)**: Este punto, en el extremo opuesto, corresponde a un **umbral muy bajo** (por ejemplo, cercano a 0). En este caso, el modelo clasifica casi todos los ejemplos como positivos (🫑), ya que cualquier predicción con una probabilidad mayor que 0 se clasifica como 🫑.
  
  - En resumen:
    - **Umbrales altos** → Menos predicciones positivas (solo las predicciones con probabilidades muy altas se clasifican como positivas).
    - **Umbrales bajos** → Más predicciones positivas (casi cualquier predicción se clasifica como positiva).

### 2. **Interpretación de la Curva ROC**

- **Curva ROC ideal**: Una curva que se acerca mucho al **eje Y** y pasa cerca del **punto (0,1)** es ideal. Esto significa que el modelo tiene **una alta tasa de verdaderos positivos (TPR)** y **una baja tasa de falsos positivos (FPR)**. Un modelo perfecto tendría una curva que sube directamente desde (0,0) hasta (0,1) y luego se mantiene plana hasta (1,1).

- **Curva ROC aleatoria**: La **diagonal** que va de (0,0) a (1,1) representa un modelo que hace predicciones **aleatorias**. Cuanto más cerca esté la curva ROC de esta línea, peor será el modelo. Esto indica que el modelo no tiene capacidad de discriminar entre las clases 🫑 y 🐺 mejor que el azar.

- **El área bajo la curva (AUC)**: La métrica **AUC-ROC** mide el área bajo la curva ROC. Valores cercanos a 1 indican un excelente rendimiento, mientras que un valor de 0.5 significa que el modelo es tan bueno como una clasificación aleatoria. Valores por debajo de 0.5 indican un modelo muy pobre que está prediciendo incorrectamente la mayoría de las veces.

### 3. **Qué dice el gráfico sobre tu modelo**

- **Si la curva está más cerca del eje Y**: Esto indica que, para muchos umbrales, el modelo logra una **alta tasa de verdaderos positivos** (es decir, identifica correctamente 🫑) mientras mantiene una **baja tasa de falsos positivos**. Esto es **deseable**, ya que significa que el modelo está haciendo buenas predicciones con un umbral adecuado.
  
- **Si la curva se acerca a la diagonal (0,0)-(1,1)**: Esto indica que el modelo tiene un desempeño **pobre**. Sus predicciones son similares a hacer conjeturas al azar.

- **Si la curva tiene una sección plana**: Cuando la curva ROC tiene una **sección horizontal**, esto indica que hay un aumento en los falsos positivos sin un aumento en los verdaderos positivos, lo cual no es bueno para el modelo.

### 4. **Impacto del umbral en las predicciones**

- **Aumentar el umbral**: Si subes el umbral (cerca de 1), tendrás **menos predicciones positivas**, pero también reducirás los falsos positivos (FPR), a costa de posiblemente aumentar los falsos negativos (FN), lo que afectaría al **recall**.

- **Reducir el umbral**: Si bajas el umbral (cerca de 0), el modelo será más generoso en clasificar positivos (🫑), lo que aumenta el TPR (recall), pero también puede aumentar los falsos positivos (FP), lo que afecta la **precisión**.

### 5. **Conclusiones sobre el modelo**

- Si la curva ROC está **lejos de la diagonal** y tiene un **área bajo la curva (AUC) cercana a 1**, el modelo tiene **una buena capacidad de discriminación** entre las clases 🫑 y 🐺. 
- Un **AUC alto** indica que el modelo tiene un buen equilibrio entre la capacidad de predecir positivos y negativos a lo largo de varios umbrales.
- **Optimización del umbral**: Puedes ajustar el umbral de decisión dependiendo de si prefieres tener más **recall** o más **precisión** dependiendo del caso de uso.

Por ejemplo:
- En un problema donde es más importante capturar todos los 🫑 posibles (mayor **recall**), podrías optar por un umbral más bajo.
- En un problema donde es más importante evitar falsos positivos 🫑 (mayor **precisión**), puedes optar por un umbral más alto.


# Curva roc en clasificación multiclase

```python
y_scores = pipeline.predict_proba(X_test)[:, 1]
```

estás seleccionando las probabilidades de la **clase 1** en una clasificación binaria. Esto significa que estás obteniendo las probabilidades de que el modelo prediga la clase positiva (en tu caso, la clase "1" o "lloverá").

### Explicación de los puntajes:

Dado un vector de probabilidades de clase 1:

```python
y_scores = [0.1, 0.7, 0.5, 0.88, 0.55, 0.2]
```

Significa que:
- La probabilidad de que la primera muestra sea de la clase 1 es 0.1, por lo que la probabilidad de que sea de la clase 0 es 0.9.
- La probabilidad de que la segunda muestra sea de la clase 1 es 0.7, entonces la probabilidad de que sea de la clase 0 es 0.3.
- Y así sucesivamente.

Como mencionas, las probabilidades para la clase 0 son simplemente el complemento de las probabilidades de la clase 1, es decir:

$$
P(\text{clase 0}) = 1 - P(\text{clase 1})
$$

Así que efectivamente, el vector de probabilidades para la clase 0 sería:

```python
[0.9, 0.3, 0.5, 0.12, 0.45, 0.8]
```

### Sobre la Curva ROC:

Para una **clasificación binaria**, solo necesitas una **curva ROC** que se basa en las probabilidades de la **clase positiva** (clase 1 en tu caso). Esto es porque la curva ROC representa la relación entre:
- **TPR (True Positive Rate)** o **recall** de la clase positiva (eje y).
- **FPR (False Positive Rate)** o la tasa de falsos positivos para la clase negativa (eje x).

Ya que las probabilidades de las dos clases son complementarias (la suma siempre es 1), **no es necesario graficar dos curvas ROC** para cada clase. El cálculo de TPR y FPR para la clase 1 te da suficiente información para analizar el desempeño del modelo.

### Clasificación multiclase:

En el caso de una **clasificación multiclase** (más de dos clases), se requiere un enfoque diferente para evaluar el rendimiento con curvas ROC. Aquí tienes algunas opciones:

1. **Curva ROC para cada clase vs. las demás** (también llamado **"one-vs-all"** o "uno contra todos"):
   - Para cada clase \(i\), consideras esa clase como la "positiva" (clase 1) y todas las demás como "negativas" (clase 0).
   - Entonces, graficas una curva ROC para cada clase individualmente.

2. **Promedio de las curvas ROC**:
   - Puedes calcular un promedio ponderado de las curvas ROC para todas las clases, lo que da una única curva ROC general para el modelo.

### Resumen:

- **Clasificación binaria**: Solo necesitas una curva ROC basada en las probabilidades de la clase 1.
- **Clasificación multiclase**: Necesitarás múltiples curvas ROC (una para cada clase) o un enfoque de promedio de curvas.
