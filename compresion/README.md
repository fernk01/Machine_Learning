# Entropia
Es la longitud promedio en bits de los codigos usados para representar un mensaje. Por otro lado, es una medida de la cantidad de informacion representada en la fuente.

Se en lo emplea en los arboles de decision.

- **Entropía**: Mide la impureza de un conjunto de datos. Cuanto mayor sea la entropía, mayor será la incertidumbre en los datos. La entropía se calcula como:
    $$ H(S) = - \sum_{i=1}^{n} p_i \log_2(p_i) $$

    - S: Conjunto de datos
    - n: Número de clases
    - $p_i$: Proporción de la clase i en el conjunto de datos

    Cuanto mayor sea la entropía, mayor será la incertidumbre en los datos y, por lo tanto, mayor será la impureza. En el contexto de un árbol de decisión, se busca dividir el conjunto de datos en subconjuntos más puros, es decir, con menor entropía.