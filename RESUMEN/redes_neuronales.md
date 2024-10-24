# Redes Neuronales
Ver [Descenso del Gradiente](descenso_del_gradiente.md) para más detalles sobre cómo se optimizan los pesos de una red neuronal.




# Perceptrón: Compuerta AND
**Perceptrón simple** utilizando la **función sigmoide** como función de activación  y realizar los pasos de forward propagation y backward propagation para ajustar los pesos.

| $x_1$ | $x_2$ | $y$ |
| --- | --- | --- |
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

### Supuestos:

- Tenemos un perceptrón con **dos entradas** ($x_1$ y $x_2$).
- Los **pesos** asociados a las entradas son $w_1$ y $w_2$.
- Hay un **sesgo** (bias) $b$.
- La **función de activación** será la función sigmoide.

### Inicialización
- Pesos iniciales (aleatorios): $ w_1 = 0.3 $, $ w_2 = 0.3 $.
- Sesgo inicial: $ b = -0.4 $.
- Tasa de aprendizaje: $ \alpha = 0.1 $.
- Función de activación: **Función Sigmoide**.

### Función Sigmoide

La función sigmoide es una función no lineal que mapea cualquier valor real en un rango entre 0 y 1. Matemáticamente, se define como:

$$ \sigma(z) = \frac{1}{1 + e^{-z}} $$

Donde:
- $ z $ es la suma ponderada de las entradas más el sesgo.

## Forward propagation 
Supongamos que estamos procesando la entrada (1, 1), donde queremos que la salida sea 1 (según la tabla de verdad de la compuerta AND).

1. **Cálculo de la suma ponderada $z$**:

    $$ z = w_1 \cdot x_1 + w_2 \cdot x_2 + b $$
    
    Sustituyendo los valores:

    $$ z = (0.3 \cdot 1) + (0.3 \cdot 1) + (- 0.4) = 0.2 $$

2. **Aplicar la función de activación (sigmoide) para obtener la salida $\hat{y}$**:

    $$ \hat{y} = \sigma(z) = \frac{1}{1 + e^{-z}} $$
    
    Como $ z = 0.2 $, tenemos:

    $$ \hat{y} = \frac{1}{1 + e^{-0.2}} \approx 0.55 $$

La salida predicha es $ \hat{y} \approx 0.55 $.

## Backward propagation (Backpropagation)
El **Backward Propagation** para el perceptrón simple con la función sigmoide, explicando cómo se ajustan los pesos y el sesgo durante el entrenamiento. En backward propagation, calculamos el error y luego usamos el **descenso de gradiente** para actualizar los pesos y el sesgo, minimizando el error en las predicciones futuras.

Ahora vamos a ajustar los pesos y el sesgo para reducir el error. Consideremos que la salida esperada es $ y = 1 $ y la salida predicha es $ \hat{y} = 0.55 $.

1. **Cálculo del Error (Función de Pérdida)**

    El error se mide utilizando una **función de pérdida**. Aquí usamos el **error cuadrático medio** (MSE):

    $$ L = \frac{1}{2} (y - \hat{y})^2 $$

    Donde:
    - $ L $ es la pérdida.
    - $ y $ es la salida esperada.
    - $ \hat{y} $ es la salida predicha.

    $$ L = \frac{1}{2} \cdot (1 - 0.55)^2 = \frac{1}{2} \cdot (0.45)^2 = 0.10125 $$

2. Calcular el Gradiente (Derivadas Parciales)

    Para ajustar los pesos y el sesgo, necesitamos calcular cómo cambia el error con respecto a cada uno de ellos. Usamos **derivadas parciales** para encontrar estos gradientes.

    **Derivada respecto a $ w_1 $ (peso asociado a $ x_1 $):**

    $$ \frac{\partial L}{\partial w_1} = \frac{\partial L}{\partial \hat{y}} \cdot \frac{\partial \hat{y}}{\partial z} \cdot \frac{\partial z}{\partial w_1} $$

    1. **$\frac{\partial L}{\partial \hat{y}}$:**

        $$ \frac{\partial L}{\partial \hat{y}} = \frac{\partial}{\partial \hat{y}} \left( \frac{1}{2} (y - \hat{y})^2 \right) = - (y - \hat{y}) $$

        $$ \frac{\partial L}{\partial \hat{y}} = - (1 - 0.55) = -0.45 $$

    2. **$\frac{\partial \hat{y}}{\partial z}$:**

        $$ \hat{y} = \sigma(z) = \frac{1}{1 + e^{-z}}, \text{ así que } \frac{\partial \hat{y}}{\partial z} = \hat{y} (1 - \hat{y}) $$

        $$ \frac{\partial \hat{y}}{\partial z} = 0.55 \cdot (1 - 0.55) = 0.2475 $$

    3. **$\frac{\partial z}{\partial w_1}$:**

        $$ z = w_1 \cdot x_1 + w_2 \cdot x_2 + b \Rightarrow \frac{\partial z}{\partial w_1} = x_1 $$

        $$ \frac{\partial z}{\partial w_1} = 1 $$

    4. Combinando todo:

        $$ \frac{\partial L}{\partial w_1} = -0.45 \cdot 0.2475 \cdot 1 = -0.111375 $$

Resumen de las derivadas parciales:
- $$\frac{\partial L}{\partial w_1} = -0.111375$$
- $$\frac{\partial L}{\partial w_2} = -0.111375$$
- $$\frac{\partial L}{\partial b} = -0.111375$$

### Actualización de los Pesos y Sesgo

Ahora, usamos el gradiente y la **tasa de aprendizaje** ($\alpha = 0.1$) para actualizar $ w_1 $, $ w_2 $ y $ b $:

$$ w_i = w_i - \alpha \cdot \frac{\partial L}{\partial w_i}  \quad\quad \text{para } i = 1, 2 $$

Resumen de las actualizaciones:
- $$ w_1 = 0.3 - 0.1 \cdot (-0.111375) = 0.3111375 $$
- $$ w_2 = 0.3 - 0.1 \cdot (-0.111375) = 0.3111375 $$
- $$ b = -0.4 - 0.1 \cdot (-0.111375) = -0.3888625 $$
