# Distancias

| Distancia | Sistema de Coordenadas |
| --- | --- |
| Euclidiana | Euclidiano |
| Coseno | Euclidiano |
| Hamming | Discreto |
| Manhattan | Euclidiano |
| Minkowski | Euclidiano |
| Chebyshev | Euclidiano |
| Jaccard | Discreto |
| Haversine | Geográfico |
| Sorensen-Dice | Discreto |

## Distancia Euclidiana: 
La distancia euclidiana entre dos puntos en un espacio euclidiano es la longitud del segmento de línea que los une, se deduce del teorema de Pitágoras.

Definición: En queneral, la distancia euclidiana entre dos puntos $p$ y $q$ en un espacio euclidiano n-dimensional, con coordenadas $p = (p_1, p_2, ..., p_n)$ y $q = (q_1, q_2, ..., q_n)$, se define como:

$$ d(p, q) = \sqrt{(p_1 - q_1)^2 + (p_2 - q_2)^2 + ... + (p_n - q_n)^2} $$
$$ d(p, q) = \sqrt{\sum_{i=1}^{n} (p_i - q_i)^2} $$

## Distancia de Coseno:
La distancia de coseno es una medida de similitud entre dos vectores en un espacio euclidiano. Se define como el coseno del ángulo entre los dos vectores.

Definición: La distancia de coseno entre dos vectores $p$ y $q$ en un espacio euclidiano n-dimensional, con coordenadas $p = (p_1, p_2, ..., p_n)$ y $q = (q_1, q_2, ..., q_n)$, se define como:

$$ d(p, q) = \frac{p \cdot q}{||p|| \cdot ||q||} $$

## Distancia de Hamming:
La distancia de Hamming es una métrica de distancia entre dos cadenas de igual longitud que se define como el número de posiciones en las que los símbolos correspondientes son diferentes.

Definición: La distancia de Hamming entre dos cadenas de igual longitud es el número de posiciones en las que los símbolos correspondientes son diferentes.

$$ d(p, q) = \sum_{i=1}^{n} \delta(p_i, q_i) $$
Donde:
- $\delta(p_i, q_i) = 0$ si $p_i = q_i$.
- $\delta(p_i, q_i) = 1$ si $p_i \neq q_i$.

## Distancia de Manhattan:
La distancia de Manhattan es la suma de las diferencias absolutas de sus coordenadas. Se llama así porque se puede pensar en una cuadrícula de calles de Manhattan, que tiene calles que corren horizontalmente y verticalmente, en lugar de en diagonal.

Definición: En general, la distancia de Manhattan entre dos puntos $p$ y $q$ en un espacio euclidiano n-dimensional, con coordenadas $p = (p_1, p_2, ..., p_n)$ y $q = (q_1, q_2, ..., q_n)$, se define como:

$$ d(p, q) = |p_1 - q_1| + |p_2 - q_2| + ... + |p_n - q_n| $$
$$ d(p, q) = \sum_{i=1}^{n} |p_i - q_i| $$

## Distancia de Minkowski:
La distancia de Minkowski es una generalización de las distancias de Manhattan y Euclidiana. La distancia de Minkowski entre dos puntos $p$ y $q$ en un espacio euclidiano n-dimensional, con coordenadas $p = (p_1, p_2, ..., p_n)$ y $q = (q_1, q_2, ..., q_n)$, se define como:

$$ d(p, q) = \left( \sum_{i=1}^{n} |p_i - q_i|^r \right)^{\frac{1}{r}} $$
Donde:
- $r$ es un número real positivo.
- Si $r = 1$, la distancia de Minkowski es la distancia de Manhattan.
- Si $r = 2$, la distancia de Minkowski es la distancia Euclidiana.

## Distancia de Chebyshev:
La distancia de Chebyshev es una métrica de distancia que se define como la distancia máxima entre sus coordenadas.

Definición: La distancia de Chebyshev entre dos puntos $p$ y $q$ en un espacio euclidiano n-dimensional, con coordenadas $p = (p_1, p_2, ..., p_n)$ y $q = (q_1, q_2, ..., q_n)$, se define como:

$$ d(p, q) = \max_{i=1}^{n} |p_i - q_i| $$
$$ d(p, q) = \max(|p_1 - q_1|, |p_2 - q_2|, ..., |p_n - q_n|) $$

## Distancia de Jaccard:
La distancia de Jaccard es una métrica de distancia que se utiliza para medir la similitud entre dos conjuntos. Se define como el tamaño de la intersección dividido por el tamaño de la unión de los conjuntos.

Definición: La distancia de Jaccard entre dos conjuntos $A$ y $B$ se define como:

$$ d(A, B) = 1 - \frac{|A \cap B|}{|A \cup B|} $$
$$ d(A, B) = 1 - \frac{|A \cap B|}{|A| + |B| - |A \cap B|} $$

## Distancia de Haversine:
La distancia de Haversine es una fórmula que se utiliza para calcular la distancia entre dos puntos en la superficie de una esfera, como la Tierra. Se basa en la ley de los cosenos para triángulos esféricos.

Definición: La distancia de Haversine entre dos puntos $p$ y $q$ en la superficie de una esfera de radio $r$ se define como:

$$ d(p, q) = 2r \arcsin \left( \sqrt{\sin^2 \left( \frac{\phi_2 - \phi_1}{2} \right) + \cos(\phi_1) \cos(\phi_2) \sin^2 \left( \frac{\lambda_2 - \lambda_1}{2} \right)} \right) $$
Donde:
- $\phi_1$ y $\phi_2$ son las latitudes de los puntos $p$ y $q$ en radianes.
- $\lambda_1$ y $\lambda_2$ son las longitudes de los puntos $p$ y $q$ en radianes.
- $r$ es el radio de la esfera.

## Distancia de Sorensen-Dice:
La distancia de Sorensen-Dice es una métrica de distancia que se utiliza para medir la similitud entre dos conjuntos. Se define como el doble del tamaño de la intersección dividido por la suma de los tamaños de los conjuntos.

Definición: La distancia de Sorensen-Dice entre dos conjuntos $A$ y $B$ se define como:

$$ d(A, B) = 1 - \frac{2|A \cap B|}{|A| + |B|} $$

## Distancia de Mahalanobis
La distancia de Mahalanobis es una medida de la distancia entre un punto y un conjunto de puntos. Se utiliza para medir la distancia entre un punto y un conjunto de puntos en un espacio multidimensional.

Definición: Formalmente, la distancia de Mahalanobis entre dos variables aleatorias con la misma distribución de probabilidad $\vec{x}$ y $\vec{y}$  con matriz de covarianza $ 
\Sigma $ se define como:

$$ d(\vec{x}, \vec{y}) = \sqrt{(\vec{x} - \vec{y})^T \Sigma^{-1} (\vec{x} - \vec{y})} $$