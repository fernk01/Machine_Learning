# Pandas

## Memory optimization
### memory_usage
```python
DataFrame.memory_usage(index=True, deep=False)
```
Cuando usas el método memory_usage() en un DataFrame de Pandas, por defecto, este método devuelve el uso de memoria de cada columna en bytes. Sin embargo, para las columnas que contienen objetos de Python, como strings, este método solo cuenta la referencia al objeto, no el tamaño real del objeto. Esto puede dar una estimación baja del uso real de memoria.

Si pasas el argumento **deep=True** a memory_usage(), entonces el método calculará el uso de memoria considerando todos los valores en las columnas. Esto es especialmente útil para las columnas que contienen objetos de Python, ya que deep=True calculará el tamaño real de estos objetos.

Si estás realizando una limpieza de tu DataFrame con `astype()`, es probable que estés cambiando el tipo de datos de una o más columnas. Esto puede afectar el uso de memoria de tu DataFrame.

Por ejemplo, si estás convirtiendo una columna de `float64` a `float32`, deberías ver una disminución en el uso de memoria. Del mismo modo, si estás convirtiendo una columna de objetos (como strings) a un tipo de datos categórico con `astype('category')`, también deberías ver una disminución en el uso de memoria.

Por lo tanto, después de usar `astype()`, puedes usar `memory_usage(deep=True)` para ver el nuevo uso de memoria de tu DataFrame. Esto te dará una idea de cuánto has logrado reducir el uso de memoria con tu limpieza.

Recuerda que `deep=True` te dará una estimación más precisa del uso de memoria para las columnas que contienen objetos de Python, como strings o categorías. Por lo tanto, es útil usar `deep=True` si has realizado cambios que afectan a este tipo de columnas.