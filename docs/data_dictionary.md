# Diccionario de datos

## Variables finales del modelo (dentro del límite de 3 a 10 del nivel básico)

| # | Variable | Dataset de origen | Tipo | Descripción |
|---|---|---|---|---|
| 1 | municipio | Saber 11 / Conectividad | Texto | Nombre del municipio; llave de cruce |
| 2 | zona | Saber 11 | Texto (URBANO/RURAL) | Ubicación del establecimiento educativo |
| 3 | promedio_ciencias | Saber 11 | Número | Puntaje promedio en ciencias naturales |
| 4 | promedio_matematicas | Saber 11 | Número | Puntaje promedio en matemáticas |
| 5 | total_accesos_internet | Conectividad (CRC) | Número | Suma de accesos a internet fijo en el municipio |

**5 variables base** — muy por debajo del límite de 10, dejando margen amplio para las variables derivadas.

## Variables derivadas (calculadas por el equipo)

| Variable derivada | Cómo se calcula | Uso |
|---|---|---|
| puntaje_stem | Promedio de `promedio_ciencias` y `promedio_matematicas` | Indicador combinado de desempeño STEM |
| brecha_stem | `puntaje_stem` municipio − promedio nacional | Base para clasificar el nivel de brecha |
| nivel_brecha | Clasificación por desviación estándar de `brecha_stem`: crítico / alto / medio / bajo | Capa 1 del modelo |
| nivel_conectividad_base | Clasificación por desviación estándar de `total_accesos_internet`: desconectado / básico / medio / alto | Cálculo intermedio |
| nivel_conectividad | Igual a `nivel_conectividad_base` (medición objetiva, sin mezclar zona — ver nota abajo) | Capa 2 del modelo |
| municipio_normalizado | `municipio` sin tildes ni puntuación (vía `quitar_tildes`) | Cruces robustos entre fuentes |
| latitud, longitud | Tabla de referencia DIVIPOLA, cruzada por `municipio_normalizado` | Ubicación en el mapa del agente |

## Por qué se usa desviación estándar y no cuartiles

Se descartó `pd.qcut` (cuartiles) porque fuerza 4 grupos de tamaño igual (25% cada uno) sin importar la gravedad real de los datos. Se usa la desviación estándar para que el número de municipios en cada categoría refleje la gravedad real del problema (ej. si la mayoría de municipios tiene brecha alta, la mayoría debe clasificar como "alto", no forzar solo un 25%).

## Por qué la zona no se usa en la Capa 2 (conectividad)

La Capa 2 debe ser una **medición objetiva** de los datos de conectividad. La zona (rural/urbana) sí importa, pero para decidir **qué tan práctico es aplicar cierta actividad** — eso es un juicio pedagógico, no una medición, y por eso vive en la Capa 3 (ajusta la logística de materiales sugerida), no en la Capa 2. Un árbol de decisión entrenado confirmó que la zona no aporta información adicional para predecir el nivel de conectividad medido.

## Deserción escolar (variable descartada)

Se evaluó incluir la tasa de deserción escolar (dataset del MEN) como tercera variable de análisis, pero se descartó al reemplazar la fuente de conectividad (el MEN dejó de reportarla desde 2017) por una de la CRC — mantener ambas fuentes hubiera significado usar 3 datasets, superando el límite del nivel básico.

## Columnas exportadas en `stemdata_prototipo.json` (para el agente)

`municipio`, `zona`, `lat`, `lon`, `promedio_ciencias`, `promedio_matematicas`, `puntaje_stem`, `nivel_brecha`, `total_accesos_internet`, `nivel_conectividad`.
