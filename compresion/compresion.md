# Archivo
Todos los archivos en una computadora están representados en binario, es decir, en una secuencia de bits (0s y 1s). Esto se debe a que los sistemas informáticos operan a nivel fundamental utilizando transistores, que pueden estar en un estado de encendido (1) o apagado (0). 

1. **Nivel Físico**: En el nivel más bajo, los datos en una computadora están representados por estados físicos de los componentes electrónicos, como transistores, que se interpretan como bits.

2. **Nivel Binario**: Estos bits se agrupan para formar bytes (1 byte = 8 bits). Todos los archivos, sin importar su tipo (texto, imagen, video, etc.), están compuestos por bytes.

3. **Codificación de Datos**: Diferentes tipos de archivos tienen diferentes formas de codificar la información:
   - **Archivos de texto**: Usan sistemas de codificación como ASCII o Unicode para representar caracteres como combinaciones de bytes.
   - **Imágenes**: Los archivos de imagen como JPEG, PNG, o BMP codifican información de píxeles y colores en una estructura binaria específica.
   - **Audio y Video**: Los archivos de audio (como MP3 o WAV) y video (como MP4 o AVI) tienen sus propios formatos de codificación para representar ondas sonoras y secuencias de imágenes.

4. **Estructura de Archivos**: Cada tipo de archivo tiene una estructura específica, definida por su formato. Por ejemplo, un archivo PDF tiene una estructura que permite incluir texto, imágenes y otros elementos en un formato portátil.

5. **Sistemas de Archivos**: A nivel del sistema operativo, los archivos se gestionan mediante sistemas de archivos (como NTFS, FAT32, ext4), que organizan y almacenan los datos binarios en el disco duro u otros medios de almacenamiento.

En resumen, aunque vemos y manipulamos archivos en formas comprensibles (texto legible, imágenes visibles, etc.), en el fondo, todos estos datos están representados y almacenados en forma binaria dentro de la computadora.

# Codificación y Compresión

1. **Codificación**: 
   - Cada tipo de archivo tiene una manera específica de organizar y representar la información en formato binario.
   - Un archivo de texto utiliza codificaciones como ASCII o Unicode para convertir caracteres en secuencias de bytes.
   - Una imagen JPEG utiliza una codificación que incluye compresión para reducir el tamaño del archivo, almacenando la información de los píxeles en una forma eficiente.

2. **Compresión**:
   - Formatos como JPEG, MP3, y ZIP usan algoritmos de compresión para reducir el tamaño del archivo. La compresión puede ser con pérdida (donde se pierde algo de la información original, como en JPEG y MP3) o sin pérdida (donde no se pierde ninguna información, como en ZIP).
   - Al descomprimir un archivo, se recupera la información original en una forma más legible, aunque el tamaño del archivo puede aumentar.

## Peso en Bytes

- Un archivo de imagen comprimido en formato JPEG puede ser mucho más pequeño que la versión descomprimida debido a la reducción de redundancias y otras técnicas de compresión.
- Por ejemplo, una imagen comprimida de 20 bytes en formato JPEG, cuando se descomprime, podría ocupar muchos más bytes si se almacena en un formato sin compresión como BMP.

## Interpretación de los Datos Binarios

- **Interpretación Dependiente del Formato**:
  - Los mismos bytes pueden representar diferentes tipos de datos según el formato del archivo. Por ejemplo, los bytes `0xFF, 0xD8, 0xFF` al inicio de un archivo se interpretan como el comienzo de un archivo JPEG.
  - Un archivo de texto de 20 bytes podría contener caracteres legibles, como "Hello, world!" si está en ASCII o Unicode.

- **Comparación de Binarios**:
  - Un archivo de texto de 20 bytes y una imagen comprimida de 20 bytes pueden tener la misma cantidad de bits, pero se interpretan de manera completamente diferente debido a su formato.
  - Al visualizar los bytes en binario, ambos tendrán secuencias de 0s y 1s, pero el contexto y la forma en que se decodifican diferirán según el tipo de archivo.

Claro, continuemos con el ejemplo práctico y la explicación:

## Ejemplo Práctico

1. **Archivo de Texto (20 bytes)**:
   - **Contenido**: "Hello, world!12345"
   - **Codificación**: Usando ASCII, cada carácter se convierte en un byte. Por ejemplo, 'H' es 72 (en decimal), que es `01001000` en binario.
   - **Bytes**: Los primeros 20 caracteres del texto convertidos en ASCII se representan como una secuencia de 20 bytes.
   - **Binario**:
     ```
     01001000 01100101 01101100 01101100 01101111 00101100 00100000 01110111 01101111 01110010 01101100 01100100 00100001 00110001 00110010 00110011 00110100 00110101
     ```
   - **Peso en bytes**: 20 bytes.

2. **Archivo de Imagen JPEG (20 bytes)**:
   - **Contenido**: 20 bytes de un archivo JPEG pueden representar la cabecera y parte de los datos comprimidos de la imagen.
   - **Codificación**: El formato JPEG usa compresión con pérdida y una estructura específica que incluye segmentos como la cabecera, bloques de datos de imagen comprimidos, etc.
   - **Bytes**: Los primeros 20 bytes pueden incluir información como la cabecera JPEG y parte de los datos de la imagen.
   - **Binario**:
     ```
     11111111 11011000 11111111 11100000 00000010 00010000 01001101 01011010 10010010 11010101 01101111 01100110 11011010 10001000 01110101 01101001 11100100 01001101 01111010 10101001
     ```
   - **Peso en bytes**: 20 bytes (comprimidos).

## Comparación de Interpretación

- **Mismo Peso, Diferente Interpretación**:
  - Aunque ambos archivos tienen el mismo tamaño en bytes, se interpretan de manera muy diferente debido a sus respectivos formatos.
  - El archivo de texto se lee directamente como caracteres según la codificación ASCII.
  - El archivo de imagen JPEG se interpreta mediante el algoritmo de decodificación JPEG que extrae la información de imagen comprimida.

## Descompresión y Cambio de Tamaño

- **Texto**:
  - El tamaño en bytes de un archivo de texto suele permanecer constante porque no se comprime de la misma manera que una imagen.
  
- **Imagen JPEG**:
  - Al descomprimir una imagen JPEG, los datos se expanden a un formato sin compresión (por ejemplo, BMP), lo cual puede incrementar significativamente el tamaño del archivo.
  - Ejemplo:
    - Imagen comprimida JPEG: 20 bytes.
    - Imagen descomprimida BMP: podría ser varios kilobytes o megabytes dependiendo de la resolución y profundidad de color.

## Conclusión
En resumen, todos los archivos en una computadora están compuestos de bits, pero la interpretación de esos bits depende del formato del archivo. Un archivo de texto y una imagen JPEG pueden tener el mismo tamaño en bytes, pero la manera en que se decodifican e interpretan esos bytes es completamente diferente. La compresión y descompresión también afectan el tamaño del archivo y cómo se almacena la información.

# Compresión de Datos

**¿Qué es la compresión de datos?**

La compresión de datos es el proceso de reducir el tamaño de un archivo o una cadena de datos. Esto se logra eliminando redundancias y representando los datos de manera más eficiente. Existen dos tipos principales de compresión:

- **Compresión sin pérdida**: Se reduce el tamaño del archivo sin perder ninguna información. Al descomprimir, se recupera el archivo original exactamente. Ejemplos: ZIP, PNG, FLAC.
- **Compresión con pérdida**: Se elimina parte de la información, generalmente imperceptible para el usuario, para reducir aún más el tamaño del archivo. Al descomprimir, no se recupera el archivo original exactamente. Ejemplos: JPEG, MP3.

En el contexto de Kolmogorov, la compresión sin pérdida se usa para aproximar la complejidad de una cadena. La idea es que una cadena con patrones repetitivos (baja complejidad) puede ser comprimida a un tamaño más pequeño, mientras que una cadena más aleatoria (alta complejidad) no se comprime tan bien.

# Complejidad
## Complejidad de Kolmogorov
Definition: Sea x un string, K(x) es igual a la cantidad de bits minimos
que debe tener un programa que genera x. 


La clave aquí es entender que la **complejidad de Kolmogorov** no está directamente relacionada con la longitud de la cadena, sino con la longitud del programa más corto que puede generar esa cadena. 

K(x) es intractable o incomputable, es decir,
no existe forma de calcular K(x).

Ejemplo:

1. Para la cadena "ABAB...AB" de 100 millones de caracteres, puedes tener un programa muy corto que lo genere, algo como `for i=1 to 50x10^6 print "AB"`. Aunque la cadena es muy larga, el programa necesario para generarla es relativamente corto. Por lo tanto, decimos que esta cadena tiene una **baja complejidad de Kolmogorov**.

2. Para una cadena de 100 millones de caracteres aleatorios, necesitarías un programa que simplemente imprima la cadena completa, algo como `print "ABCDEFGHI...JKLMNOPQRST"`. Aunque la cadena es igual de larga que la anterior, el programa necesario para generarla es mucho más largo. Por lo tanto, decimos que esta cadena tiene una **alta complejidad de Kolmogorov**.

3. Ahora, si consideras una cadena de solo 5 caracteres, digamos "ABCDE", el programa más corto para generarla sería algo como `print "ABCDE"`. En este caso, la longitud de la cadena y la longitud del programa son similares, por lo que su complejidad de Kolmogorov sería moderada.

## C(x)
La complejidad de Kolmogorov \( K(x) \) no es computable. Sin embargo, podemos aproximar \( K(x) \) utilizando técnicas de compresión de datos. Una forma común de aproximar \( K(x) \) es mediante la complejidad de compresión \( C(x) \). La idea es que la longitud del archivo comprimido puede servir como una estimación de la complejidad de Kolmogorov.

## Cómo calcular \( C(x) \)

Para calcular \( C(x) \), podemos usar un algoritmo de compresión sin pérdida como `zlib`, `gzip`, o `bzip2`. La longitud del archivo comprimido se toma como una aproximación de \( C(x) \).



| Simbolo | Cod 1 | Cod 2 | Cod 3 |
|---------|-------|-------|-------|
| A       | 0     | 10    | 0   |
| B       | 010   | 00    | 10  |
| C       | 01    | 11    | 110 |
| D       | 10    | 110   | 111 |

**Desigualdad de Kraft y McMillan**
(Desigualdad de Kraft) Sea li la longitud de cada codigo,
se conoce a la desigualdad de Kraft como:
$$ \sum_{i=1}^{n} \frac{1}{r} ^{l_i} \leq 1 $$

Dada una fuente de $n$ simbolos, con longitudes $l_1, l_2, ..., l_n$ y un alfabeto de tamaño $r$, si existe un codigo que cumple con la desigualdad de Kraft, entonces existe un codigo que cumple con la desigualdad de McMillan.

- SSi la desigualdad de Kraft se cumple con desigualdad estricta ($< 1$), el código tiene cierta redundancia.
- Si la desigualdad de Kraft se cumple con igualdad ($= 1$), el código es un código de prefijo óptimo y sin redundancia, el código en cuestión es un código completo.
- Si la desigualdad de Kraft no se cumple, el código no es decodificable de forma única.
- Para cada código decodificable de forma única, existe un código de prefijo con la misma distribución de longitud.

**Ejemplo tabla:**<br>
Sea una fuente de 4 simbolos con longitudes de codigo $l_1 = 1, l_2 = 3, l_3 = 2, l_4 = 2$ (Cod 1) y un alfabeto de tamaño $r = 2$ (binario). La desigualdad de Kraft se cumple si:

$$ \left( \frac{1}{2} \right)^1 + \left( \frac{1}{2} \right)^3 + \left( \frac{1}{2} \right)^2 + \left( \frac{1}{2} \right)^2 \leq 1 $$
$$ \frac{1}{2} + \frac{1}{8} + \frac{1}{4} + \frac{1}{4} \leq 1 $$
$$ 1.125 \leq 1 $$

La desigualdad de Kraft no se cumple, por lo tanto no es decodicable.

