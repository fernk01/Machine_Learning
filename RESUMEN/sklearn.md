# Diferencia entre Parámetros e Hiperparámetros

- **Parámetros**: Son los valores internos del modelo que se aprenden automáticamente durante el proceso de entrenamiento. Por ejemplo, en una regresión lineal, los coeficientes de la línea son parámetros. Estos valores se ajustan para minimizar el error del modelo en los datos de entrenamiento.

- **Hiperparámetros**: Son configuraciones externas al modelo que se establecen antes del proceso de entrenamiento y no se aprenden a partir de los datos. Estos valores deben ser definidos por el usuario y pueden influir en el rendimiento del modelo. Ejemplos de hiperparámetros incluyen la tasa de aprendizaje en un algoritmo de optimización o la profundidad máxima de un árbol de decisión¹².

1. **Parámetros**:
   - Son valores internos que el modelo aprende de los datos durante el proceso de entrenamiento.
   - Representan la estructura interna del modelo, como los pesos en una red neuronal o los coeficientes en una regresión lineal.
   - Ejemplo: Los valores de las ramas y hojas de un árbol de decisión que se determinan en el proceso de ajuste.

2. **Hiperparámetros**:
   - Son valores que se configuran antes del entrenamiento y afectan cómo el modelo aprende los parámetros.
   - No son aprendidos a partir de los datos; son establecidos por el usuario y definen aspectos del modelo, como su estructura o la técnica de optimización.
   - Ejemplo: El número máximo de niveles en un árbol de decisión o la profundidad del árbol.


# Decision Trees
```python
class sklearn.tree.DecisionTreeClassifier(*, criterion='gini', splitter='best', max_depth=None, min_samples_split=2, min_samples_leaf=1, min_weight_fraction_leaf=0.0, max_features=None, random_state=None, max_leaf_nodes=None, min_impurity_decrease=0.0, class_weight=None, ccp_alpha=0.0, monotonic_cst=None)[source]
```
Estos son todos los hiperparámetros:
1. **criterion**: Define la función para medir la calidad de una división. Las opciones son:
   - `'gini'`: Utiliza la impureza de Gini.
   - `'entropy'`: Utiliza la ganancia de información (entropía).
   - `'log_loss'`: Utiliza la pérdida logarítmica.

2. **splitter**: Estrategia utilizada para elegir la división en cada nodo.
   - `'best'`: Elige la mejor división.
   - `'random'`: Elige la mejor división aleatoria.

3. **max_depth**: La profundidad máxima del árbol. Si es `None`, los nodos se expanden hasta que todas las hojas sean puras o contengan menos de `min_samples_split` muestras.

4. **min_samples_split**: El número mínimo de muestras necesarias para dividir un nodo interno.
   - Si es un entero, se considera como el número mínimo.
   - Si es un flotante, se considera como una fracción y `ceil(min_samples_split * n_samples)` es el número mínimo de muestras para cada división.

5. **min_samples_leaf**: El número mínimo de muestras necesarias para estar en un nodo hoja.
   - Si es un entero, se considera como el número mínimo.
   - Si es un flotante, se considera como una fracción y `ceil(min_samples_leaf * n_samples)` es el número mínimo de muestras para cada nodo.

6. **min_weight_fraction_leaf**: La fracción mínima ponderada de la suma total de pesos (de todas las muestras de entrada) requerida para estar en un nodo hoja. Las muestras tienen el mismo peso cuando no se proporciona `sample_weight`.

7. **max_features**: El número de características a considerar al buscar la mejor división.
   - Si es un entero, considera `max_features` características en cada división.
   - Si es un flotante, `max_features` es una fracción y `max(1, int(max_features * n_features_in_))` características se consideran en cada división.
   - `'sqrt'`: `max_features=sqrt(n_features)`.
   - `'log2'`: `max_features=log2(n_features)`.
   - Si es `None`, `max_features=n_features`.

8. **random_state**: Controla la aleatoriedad del estimador. Puede ser un entero, una instancia de `RandomState` o `None`.

9. **max_leaf_nodes**: El número máximo de nodos hoja en el árbol. Si es `None`, el número de nodos hoja es ilimitado.

10. **min_impurity_decrease**: Un nodo se dividirá si esta división induce una disminución de la impureza mayor o igual a este valor.

11. **class_weight**: Pesos asociados con las clases. Si es `None`, todas las clases tienen el mismo peso.

12. **ccp_alpha**: Parámetro de complejidad utilizado para la poda mínima de coste-complejidad. Un nodo se eliminará si la poda reduce el coste total de la complejidad.

13. **monotonic_cst**: Restricciones monotónicas para las características. Si es `None`, no se aplican restricciones.


