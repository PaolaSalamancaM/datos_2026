# Marco metodológico

## Parte 1: CRISP-ML(Q)

Este proyecto sigue la metodología CRISP-ML(Q), tal como lo exigen las reglas de participación del concurso.

### Fase 1: Comprensión del negocio y de los datos
Se definió el problema (brecha STEM en Colombia), se fijaron los criterios de éxito y se validaron los dos datasets oficiales. Ver [`planteamiento_problema.md`](planteamiento_problema.md) y [`fuentes_datos.md`](fuentes_datos.md).

### Fase 2: Ingeniería de datos
Limpieza, estandarización de nombres de municipio (incluyendo casos especiales como Bogotá D.C.), eliminación de duplicados/vacíos, y cruce de los dos datasets. Ver `notebooks/STEMData_Limpieza_Python.ipynb`.

### Fase 3: Ingeniería de modelos de IA
Ver sección "Componentes de IA" más abajo.

### Fase 4: Evaluación del modelo
Validación manual con municipios de prueba, revisión de la distribución de categorías por desviación estándar. Ver [`conclusiones.md`](conclusiones.md).

### Fase 5: Despliegue
El modelo se integró en un agente conversacional autónomo (`RECURSOS/stemdata_agente.html`), sin backend ni dependencias de pago.

### Fase 6: Monitoreo y mantenimiento
Trabajo futuro: actualización periódica de los datasets, ampliación del banco de proyectos con aportes de docentes (ver sección 5 de este documento).

---

## Parte 2: Justificación del componente de IA (nivel básico)

El concurso exige, para este nivel, técnicas como *"regresión lineal o logística, árboles de decisión simples o modelos de clasificación básicos"*, además de *"generación automatizada de reportes a partir de datos estructurados"* y opcionalmente *"aproximaciones iniciales de procesamiento de lenguaje natural"*. STEMData incorpora los cuatro, de forma literal:

| Técnica exigida por el concurso | Implementación en STEMData |
|---|---|
| Clasificación / árboles de decisión | Capa 1 (brecha STEM) y Capa 2 (conectividad), clasificadas por desviación estándar; árbol de decisión entrenado (`DecisionTreeClassifier`) usado para validar que la clasificación de conectividad es objetiva y no depende de la zona |
| Regresión | Cálculo de brecha como diferencia frente al promedio nacional (regresión respecto a la media) |
| Generación automatizada de reportes | `generar_planeacion()` / lógica del agente conversacional: convierte datos estructurados (brecha, conectividad, zona, grado) en texto legible, sin intervención humana por consulta |
| Procesamiento de Lenguaje Natural básico | Reconocimiento de intención por coincidencia de palabras clave, en el chat del agente (`reconocerIntencion()`) |

No se conecta el agente a un modelo de lenguaje externo (tipo Claude o ChatGPT) por tres razones: (1) requeriría exponer una clave de API en una página pública, un riesgo de seguridad; (2) tendría costo por consulta, rompiendo el carácter gratuito del proyecto; (3) el nivel básico del concurso pide explícitamente técnicas de análisis de patrones sobre datos propios, no un modelo de lenguaje de propósito general.

Como componente adicional (no exigido, mejora el análisis), se incluyó **K-Vecino más cercano (KNN)** para sugerir un municipio con condiciones similares (`municipioSimilar()`), calculando distancia euclidiana normalizada entre brecha STEM y conectividad.

---

## Parte 3: Fundamento académico del enfoque STEM+

- **Sanders, M. (2009).** *STEM, STEM Education, STEMmania.* Propone STEM como enfoque interdisciplinario entre Ciencia, Tecnología, Ingeniería y Matemáticas.
- **Martín-Páez, T., Aguilera, D., Perales-Palacios, F. J., y Vílchez-González, J. M. (2019).** *What Are We Talking about When We Talk about STEM Education? A Review of Literature.* Science Education. Define la instrucción STEM como la integración de conceptos de 2 o más disciplinas STEM para que los estudiantes apliquen prácticas de ciencia e ingeniería a **problemas del mundo real** — no la enseñanza aislada de contenidos.
- **Ramos-Lizcano, C., Ángel-Uribe, I. C., López-Molina, G., y Cano-Ruiz, Y. M. (2022).** *Elementos centrales de experiencias educativas con enfoque STEM.* Revista Científica, 45(3), 345-357. Universidad Distrital Francisco José de Caldas (Colombia). Identifica los elementos centrales de una experiencia STEM bien diseñada: propósitos de aprendizaje centrados en competencias, colaboración, aprendizaje activo, la tecnología como articuladora (no como fin en sí misma), y un rol docente que prioriza el proceso sobre la respuesta correcta.

**Cómo se aplicó esto en el banco de proyectos** (`RECURSOS/stemdata_agente.html`, objeto `BANCO_PROYECTOS`):

1. Cada proyecto parte de un **reto del mundo real** explícito (`retoMundoReal`), no de una instrucción de contenido.
2. Cada proyecto tiene un **ciclo de diseño de ingeniería** de 6 pasos (`cicloDiseno`): Preguntar → Imaginar → Planificar → Crear → Probar y mejorar → Comunicar — el marco de *Engineering is Elementary* (Museum of Science, Boston), ampliamente adoptado en currículos STEM de básica.
3. Cada proyecto documenta explícitamente cómo aparecen los **4 pilares STEM** (`componentesSTEM`), aclarando que "Tecnología" no se limita a lo digital — incluye el diseño de instrumentos y técnicas no digitales (ej. un pluviómetro casero, un filtro de agua con arena y grava).
4. Se reconocen dos variantes válidas de integración (`tipoIntegracion`): "Diseño de ingeniería" (los estudiantes construyen una solución) e "Indagación científica con diseño de protocolo" (los estudiantes investigan un fenómeno con un método propio) — reflejando la diversidad de enfoques STEM documentada por Ramos-Lizcano et al. (2022).
5. La estructura de momentos de clase (apertura / desarrollo / cierre), recursos (equipo / material / fuentes) y evaluación (tipo / agente / instrumento) sigue la *Guía para el diseño de estrategias didácticas* de la Subsecretaría de Educación Media Superior (SEP, México), adaptada al contexto colombiano de educación básica y media.

---

