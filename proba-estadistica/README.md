#  Bayesian Average Rating
El promedio de las calificaciones no siempre es la mejor métrica para clasificar, especialmente cuando la cantidad de calificaciones es baja. En estos casos, la calificación promedio puede ser engañosa. Por ejemplo, si un artículo tiene una calificación de 5 estrellas, pero solo ha sido calificado por una persona, no es lo mismo que un artículo con una calificación de 4.8 estrellas basada en 100 calificaciones.

Para solucionar este problema, podemos usar el promedio ponderado de Bayes. Este método combina el promedio de calificaciones con la calificación promedio general. La fórmula para calcular el promedio ponderado de Bayes es la siguiente:

$$ WR = \frac{v}{v+m} \cdot R + \frac{m}{v+m} \cdot C $$
$$ WR = \frac{v \cdot R + m \cdot C}{v+m} $$

Donde:
- $WR$ es el promedio ponderado de Bayes.
- $R$ es el promedio de calificaciones por artículo.
- $v$ es el número de calificaciones por artículo.
- $m$ es el número mínimo de calificaciones requeridas para ser considerado en la clasificación.
- $C$ es el promedio general de calificaciones.

## link
- [Bayesian Average Rating](https://en.wikipedia.org/wiki/Bayesian_average)
- [IMDb](https://en.wikipedia.org/wiki/IMDb)
