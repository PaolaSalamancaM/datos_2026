# Planteamiento del problema

## ¿Cuál es el problema?

Colombia lleva varios años consecutivos con un alto porcentaje de sus estudiantes en los niveles más bajos de ciencias naturales y matemáticas en las pruebas Saber 11, repercutiendo en el rendimiento académico que tendrán posteriormente al ingresar a una carrera universitaria, esto se evidencia en la UNIMINUTO, en la escuela de educación es frecuente identificar dificultades de los estudiantes en primeros semtres. Los datos que evidencian esta crisis ya existen y están publicados en fuentes oficiales del Estado, pero nadie los traduce en acción concreta para el docente que está en el aula. Esta brecha además se relaciona con la conectividad disponible: los datos del propio modelo (ver `conclusiones.md`) muestran que la gran mayoría de municipios tiene conectividad básica, lo que limita qué tipo de actividades STEM son realmente aplicables en cada contexto.

## ¿A quién afecta?

Principalmente a docentes de educación básica y media, en zonas urbanas y rurales, que no tienen acceso claro a datos oficiales sobre la realidad STEM de su propio municipio. También afecta indirectamente a los estudiantes de esos municipios, cuya brecha educativa se mantiene sin intervención dirigida.

La paradoja central: muchos docentes ya usan o querrían usar IA para planear clases, pero ninguna herramienta existente conoce la realidad tecnológica de su colegio, les sugieren videos a colegios sin internet, o proyectos que asumen recursos que no tienen.

## ¿Por qué es importante resolverlo?

Porque los datos que resolverían esto están publicados en fuentes oficiales del Estado desde hace años, y nadie los ha conectado con la planeación docente diaria. Existe una oportunidad clara de usar datos abiertos del Estado para generar valor pedagógico concreto, alineado con el objetivo del Reto 7 del concurso: diseñar asistentes virtuales que faciliten el acceso ciudadano a datos abiertos.

## Cifras que demuestran el problema (con su fuente, verificables en el repositorio)

| Cifra | Descripción | Fuente |
|---|---|---|
| 701 + 583 + 317 de 1.888 | Combinaciones municipio+zona en nivel medio, alto o crítico de brecha STEM (más del 84% del total) | Cálculo propio sobre Resultados Saber 11 (ICFES), ver `conclusiones.md` |
| 1.645 de 1.888 | Combinaciones municipio+zona con conectividad "básica" (el nivel más bajo con datos, ~87% del total) | Cálculo propio sobre Accesos de Internet Fijo (CRC/postdata.gov.co), ver `conclusiones.md` |


## Objetivo del proyecto

Diseñar y construir un asistente que, a partir de datos abiertos oficiales, permita a cualquier docente:
1. Conocer el diagnóstico real de brecha STEM de su municipio y zona.
2. Conocer el nivel de conectividad real de su contexto.
3. Recibir una planeación didáctica STEM+ inicial, ajustada a la brecha, la conectividad, la zona y el grado, así como profundizar conversando con el agente.
