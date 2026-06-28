# Uso de Inteligencia Artificial

## Herramienta utilizada
- **Claude (Anthropic)** - Asistente de codificacion con capacidades agénticas

## Generado con asistencia de IA

### Pipeline de datos
- Implementacion de `vector_documento(tokens)` como promedio de vectores de tokens, manejando el caso de lista vacia con un vector de ceros
- Construccion de `EMB_DOCS = {id: vector_documento(tokens)}` para todo el corpus usando `zip(ids, documentos)`
- Implementacion de `buscar_semantico(consulta, k)`: preprocesamiento de la consulta con el pipeline del Lab 1, conversion a vector documento y ranking por coseno contra `EMB_DOCS`

### Documentacion
- `AI_USAGE.md` - registro del uso de IA en este laboratorio

---

## Realizado por el estudiante
- Definición de funciones utilizadas en laboratorios anteriores
- Elección de consultas de prueba
- Implementacion de `ranking_semantico(consulta, k)` como wrapper compatible con `ndcg_at_k` para calcular nDCG medio de los tres motores sobre las consultas etiquetadas

### Decisiones de diseno
- Decision de reutilizar `preprocesar()` del Lab 1 dentro de `buscar_semantico`, garantizando que la consulta pase exactamente el mismo pipeline de normalizacion y lematizacion que los documentos del corpus
- Construccion y etiquetado manual de `qrels` con relevancia graduada (3/2/1) para 5 consultas, incluyendo la justificacion de cada nivel de relevancia segun el contenido real de cada documento del corpus
- Eleccion del modelo `cc.es.300.bin` de fastText en espanol de 300 dimensiones como representacion base

### Analisis
- Interpretacion de los resultados de `ft.get_nearest_neighbors()` para 'sequia', 'cafe' y 'chiapas', comentando vecinos sorprendentes y sus causas
- Explicacion de por que `coseno(agua, hidrico) ≈ 0.44` se considera alto en espacios de 300 dimensiones, a pesar de parecer bajo intuitivamente
- Analisis de los casos de analogias que funcionan (`rey - hombre + mujer`, `chiapas - Mexico + Argentina`) y los que fallan, con justificacion basada en la estructura del espacio vectorial
- Interpretacion de la tabla comparativa de nDCG entre TF-IDF, BM25 y semantico, identificando las consultas donde el semantico aporta mayor ganancia por capturar sinonimia y relaciones lexicas no presentes en los tokens

### Documentacion academica
- Redaccion final de las respuestas justificadas solicitadas en el notebook, incluyendo la identificacion de los casos donde la busqueda semantica supera a los metodos de recuperacion exacta