# Conclusiones

## Hallazgos principales (distribución real, 1.888 combinaciones municipio+zona)

**Brecha STEM:**
| Nivel | Municipios (filas municipio+zona) |
|---|---|
| Medio | 701 |
| Alto | 583 |
| Crítico | 317 |
| Bajo | 287 |

Más del 84% de las combinaciones municipio+zona están en nivel medio, alto o crítico — confirma cuantitativamente que la brecha STEM es un problema generalizado en el país, no aislado a unos pocos municipios. Usar desviación estándar (en vez de cuartiles) permitió que esta distribución desigual saliera a la luz, en vez de forzarse a un 25%/25%/25%/25% artificial.

**Conectividad:**
| Nivel | Municipios |
|---|---|
| Básico | 1.645 |
| Medio | 156 |
| Alto | 87 |

La inmensa mayoría de combinaciones municipio+zona (87%) tiene conectividad básica — es decir, el problema de conectividad también está generalizado, y refuerza la necesidad de que la planeación didáctica del agente esté diseñada, por defecto, pensando en actividades de baja o nula dependencia de internet (como ya lo hace la mayoría del banco de proyectos).

## Resultados del modelo

- **Capa 1 (brecha STEM):** clasificación por desviación estándar sobre `puntaje_stem`, validada manualmente con municipios conocidos (ej. Medellín urbano en "bajo", Quibdó urbano en "crítico", consistente con lo esperado).
- **Capa 2 (conectividad):** un árbol de decisión (`DecisionTreeClassifier`, profundidad 3) entrenado sobre `total_accesos_internet` confirmó que la zona no aporta información adicional a la clasificación — validando la decisión de mantener la Capa 2 como una medición objetiva, sin mezclar juicios pedagógicos.
- **Validación cualitativa:** se probó el agente con al menos 3 municipios de perfiles distintos (alto/bajo/crítico en brecha; alto/básico en conectividad), confirmando que el flujo de diagnóstico → planeación inicial → chat conversacional responde de forma coherente en cada caso.

## Límites de la solución

- El modelo depende de que los datasets de origen (Saber 11, conectividad CRC) sigan actualizándose; ya se documentó un caso (MEN, MinTIC) donde una fuente de conectividad dejó de estar disponible, obligando a cambiar de fuente.
- El banco de proyectos actual (6 proyectos base) es un punto de partida; su cobertura de la diversidad de contextos colombianos es limitada hasta que se amplíe con aportes reales de docentes (ver Fase 6 del marco metodológico).
- El reconocimiento de intención en el chat (PLN básico) funciona por coincidencia de palabras clave — no comprende lenguaje completamente libre ni sinónimos no anticipados.
- La variable de deserción escolar, inicialmente considerada, se descartó para mantener el proyecto dentro del límite de 2 datasets del concurso.

## Próximos pasos (trabajo futuro)

- Diseñar y aplicar formulario a docentes (aporte de actividades reales) para ampliar el banco de proyectos, con revisión pedagógica antes de publicar cada aporte.
- Evaluar la inclusión de más años históricos de Saber 11 para observar tendencia, no solo el panorama de los últimos 2 años.
- Considerar una versión con mayor granularidad de PLN (ej. coincidencia difusa) si el volumen de uso real lo justifica.
- Evaluar la incorporación de un tercer dataset (ej. pobreza multidimensional o infraestructura educativa) para enriquecer el diagnóstico.
