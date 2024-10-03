# NLP
Similaridad coseno
$$ \cos(\theta) = \frac{A \cdot B}{\|A\| \|B\|} $$
Donde $A$ y $B$ son vectores y $\|A\|$ es la norma de $A$.

- Si $\cos(\theta) = 1$ entonces $A$ y $B$ son iguales
- Si $\cos(\theta) = 0$ entonces $A$ y $B$ son ortogonales

## Bag Of Words
1. **Representación de texto:**
   - El objetivo del modelo de bolsa de palabras es convertir un documento de texto en una representación numérica que pueda ser utilizada por algoritmos de aprendizaje automático.
   - En lugar de considerar la estructura gramatical o el orden de las palabras, este modelo simplemente cuenta la frecuencia de cada palabra en el texto.

2. **Pasos para crear una bolsa de palabras:**
   - **Tokenización:** Primero, se divide el texto en palabras individuales (tokens). Esto puede incluir eliminar signos de puntuación y convertir todas las palabras a minúsculas.
   - **Creación del vocabulario:** A continuación, se crea un vocabulario único a partir de **TODAS** las palabras en el conjunto de documentos. Cada palabra se asigna a un índice único. Cada palabra se asigna a un índice único en el vocabulario. Por lo tanto, si hay 1000 palabras distintas en los documentos, habrá 1000 índices en el vocabulario.
   - **Vectorización:** Para cada documento, se crea un vector de características. Cada posición en el vector corresponde a una palabra del vocabulario, y el valor en esa posición representa la **frecuencia** de esa palabra en el documento.

3. **Ejemplo:**
   - Supongamos que tenemos dos documentos:
     - Documento 1: "El gato come pescado."
     - Documento 2: "El perro ladra."
   - El vocabulario sería: ["el", "gato", "come", "pescado", "perro", "ladra"].
   - La representación vectorial sería:
     - Documento 1: [1, 1, 1, 1, 0, 0]
     - Documento 2: [1, 0, 0, 0, 1, 1]

4. **Saltos de línea y espacios:**
   - El modelo de bolsa de palabras no considera saltos de línea ni espacios. Trata todo el texto como una secuencia continua de palabras.
   - Si un texto tiene varios saltos de línea, estos no afectarán la representación de la bolsa de palabras. Las palabras se contarán independientemente de su posición en el documento.

5. **Consideraciones**:
    - El modelo de bolsa de palabras no distingue entre palabras comunes o raras. Todas las palabras contribuyen a la representación vectorial.
    - Esto significa que incluso las palabras menos relevantes (como artículos, preposiciones, etc.) se incluyen en el vocabulario y afectan la representación.

## Term Frequency (Count Vectorizer)
- Coloca cantidad de veces que aparece una palabra en un documento

## Inverse Document Frequency
- Coloca un peso a las palabras que aparecen en pocos documentos

## Term Frequency-Inverse Document Frequency (TF-IDF)

$$ \text{TF-IDF} = log( \frac{N+1}{frecuencia} ) $$
Donde:
- $N$: es el número de documentos
- $frecuencia$: es la cantidad de documentos en los que aparece la palabra


Si coincide con una palabra que muy rara este va pesar mas con el producto escalar

Ayuda a destacar palabras importantes y reducir el impacto de palabras comunes

# Normalizacion
## Stemming
Es un proceso en donde se elimina la última parte de las palabras por algún proceso (hay stemmers de varios tipos). EI objetivo es llegar a la raíz (stem) de la palabra por medio de su prefijo. 

Ejemplos:
- caballo, caballería -> caball
- biblioteca, bibliotecario -> bibliotec
- canto, canta, cantamos, cantan -> cant
- cantidad, cantidades -> cant

## Lemmatization
Devuelve la base de la palabra (lemma),  muchas veces por medio de un diccionario de lemmas para cada palabra.

Ejemplos :
- caballo, caballería -> caballo
- biblioteca, bibliotecario -> biblioteca
- canto, canta, cantamos, cantan -> canto
- cantidad, cantidades -> cantidad

## Stop Words
Palabras que no aportan significado al texto, como preposiciones, artículos, pronombres, etc.
