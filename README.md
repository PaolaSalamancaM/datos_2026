# STEMData

**Asistente conversacional de diagnóstico y planeación STEM+ para cerrar brechas educativas en Colombia**

Concurso Datos al Ecosistema 2026 · Reto 7 — Innovación y Tecnología · Nivel Básico
100% gratuito · 2 datasets oficiales (al menos 1 de datos.gov.co) · IA interpretable

---

## 1. ¿Qué es STEMData?

STEMData es un agente conversacional gratuito que combina tres cosas en una sola experiencia:

1. Muestra al docente el **diagnóstico real de brecha STEM** de su municipio, con datos oficiales del Estado.
2. Le da una **planeación didáctica inicial bajo enfoque STEM+** (Ciencia, Tecnología, Ingeniería y Matemáticas), ajustada a la conectividad y zona de su contexto.
3. Permite **profundizar conversando**: el docente pregunta por los momentos de la clase, los recursos, la evaluación, el ciclo de diseño de ingeniería, o un municipio similar, y el agente responde usando procesamiento de lenguaje natural básico.

No sugiere lo ideal — sugiere lo posible, y lo explica paso a paso.

## 2. El problema

Colombia lleva varios años con más del 70% de sus estudiantes en los niveles más bajos de ciencias naturales y matemáticas en las pruebas Saber 11. Esta brecha es más marcada en zonas rurales y en municipios con menor conectividad — pero ningún asistente existente cruza estos dos factores para dar una recomendación pedagógica contextualizada.

Más detalle y cifras con su fuente en [`docs/planteamiento_problema.md`](docs/planteamiento_problema.md).

## 3. Cómo funciona

```
1. El docente selecciona municipio, zona y grado
2. El agente calcula: brecha STEM (Capa 1) + viabilidad tecnológica (Capa 2)
3. Un botón muestra la planeación inicial: título, reto del mundo real,
   áreas STEM integradas, aprendizaje esperado según el grado
4. El docente conversa con el agente para profundizar: momentos de la
   clase, recursos, evaluación, ciclo de diseño de ingeniería,
   habilidad socioemocional, otro proyecto, o un municipio similar
```

## 4. Datos utilizados

| Dataset | Entidad / Portal | Uso |
|---|---|---|
| Resultados únicos Saber 11 | ICFES / **datos.gov.co** | Diagnóstico de brecha STEM por municipio y zona |
| Accesos de Internet Fijo desde 2024-1T | CRC / postdata.gov.co | Perfil de conectividad del municipio (viabilidad tecnológica) |

Adicionalmente se usa una tabla de referencia geográfica (DIVIPOLA — coordenadas de municipios, datos.gov.co) únicamente para ubicar el municipio en el mapa del agente; no es un dataset de análisis y no cuenta contra el límite de datasets del nivel básico.

Ficha completa de fuentes, enlaces y variables en [`docs/fuentes_datos.md`](docs/fuentes_datos.md) y [`docs/data_dictionary.md`](docs/data_dictionary.md).

## 5. Componentes de Inteligencia Artificial

| Componente | Técnica | Dónde vive |
|---|---|---|
| Brecha STEM | Cálculo de desviación estándar sobre el promedio nacional, clasificación en 4 niveles | Notebook del modelo, Capa 1 |
| Viabilidad tecnológica | Clasificación por desviación estándar (medición objetiva, sin mezclar zona) | Notebook del modelo, Capa 2 |
| Generación automatizada de reportes | A partir de datos estructurados (brecha + conectividad + zona + grado) | `generar_planeacion()` / agente HTML |
| Procesamiento de Lenguaje Natural básico | Reconocimiento de intención por coincidencia de palabras clave | Agente conversacional (`reconocerIntencion()`) |
| Búsqueda de municipio similar | K-Vecino más cercano (KNN), por distancia en brecha y conectividad | Agente conversacional (`municipioSimilar()`) |

Fundamento pedagógico y técnico completo en [`docs/marco_metodologico.md`](docs/marco_metodologico.md).

## 6. Enfoque STEM+ del banco de proyectos

El banco de proyectos didácticos (6 proyectos base, ampliable con aportes de profesores) está diseñado siguiendo literatura académica revisada por pares sobre integración STEM (Martín-Páez et al., 2019; Ramos-Lizcano et al., 2022). Cada proyecto incluye:

- Un **reto del mundo real** (no una instrucción de contenido)
- Un **ciclo de diseño de ingeniería** explícito (Preguntar → Imaginar → Planificar → Crear → Probar y mejorar → Comunicar)
- Los 4 pilares STEM identificados explícitamente (Ciencia, Tecnología —digital o no—, Ingeniería, Matemáticas)
- Aprendizaje esperado diferenciado por banda de grado (primaria / secundaria / media)
- Momentos de clase (apertura / desarrollo / cierre), recursos, evaluación y retroalimentación, siguiendo la *Guía para el diseño de estrategias didácticas* (SEP México, adaptada)

## 7. Estructura del repositorio

```
docs/                   Documentación del proyecto
data/raw/               Datos originales sin tratamiento (parcial — ver resumen final de esta conversación)
data/processed/         Datos limpios y con modelo aplicado, listos para el agente
notebooks/              Limpieza y modelo (Jupyter / Google Colab)
models/                 Clasificador de conectividad entrenado (modelo_entrenado.pkl)
reports/                Reporte final en PDF y gráficas (reports/figures/)
RECURSOS/               Agente conversacional, presentación de sustentación (PDF) y portada
```

## 8. El agente conversacional

El archivo [`RECURSOS/stemdata_agente.html`](RECURSOS/stemdata_agente.html) es autónomo: HTML + CSS + JavaScript en un solo archivo, sin backend ni claves de API, sin costo por uso. Incluye:

- Formulario (municipio, zona, grado) + mapa interactivo (Leaflet.js)
- Insignias de color para brecha y conectividad
- Gráficas comparativas (municipio vs. promedio nacional, posición en conectividad)
- Botón de planeación inicial + chat conversacional para profundizar

Para actualizarlo con datos nuevos, ver la sección "Actualizar los datos del agente" más abajo.

## 9. Equipo

**Concurso Datos al Ecosistema 2026 · Reto 7 — Innovación y Tecnología · Nivel Básico · ID: 364**

| Integrante | Perfil | Responsabilidad |
|---|---|---|
| Carolina Parra Estrada | Lic. en Informática | Lógica pedagógica STEM+, validación con DBA y currículo |
| Paola Salamanca Monroy | Lic. en Matemáticas | Marco metodológico, documentación y coordinación del proyecto |
| Mary Ann Dousdebes | Ing. Electrónica | Modelo (clasificación, regresión) y agente conversacional |
| Yeisson Bernal López | Ing. Industrial | Limpieza y estructuración de datasets, pipeline de datos |

## 10. Documentación completa

- [Planteamiento del problema](docs/planteamiento_problema.md)
- [Fuentes de datos](docs/fuentes_datos.md)
- [Diccionario de datos](docs/data_dictionary.md)
- [Arquitectura del proyecto](docs/arquitectura.md)
- [Marco metodológico (CRISP-ML + fundamento STEM)](docs/marco_metodologico.md)
- [Historias de usuario](docs/historias_usuario.md)
- [Conclusiones](docs/conclusiones.md)
- [Guía de validación para pares evaluadores](docs/validacion_guide.md)
- [Reporte final con resultados y gráficas](reports/reporte_final.pdf)
- [Presentación de sustentación](RECURSOS/presentacion.pdf)

## 11. Actualizar los datos del agente

1. Ejecuta `notebooks/STEMData_Limpieza_Python.ipynb` completo → genera `stemdata_limpio.csv`.
2. Súbelo a `notebooks/STEMData_Modelo_3Capas.ipynb` (Parte 1) → ejecuta todo → genera `stemdata_prototipo.json`.
3. Abre `RECURSOS/stemdata_agente.html` en un editor de código (VS Code recomendado), busca `const DATOS = [`, y reemplaza el contenido por el de `stemdata_prototipo.json`.
4. Guarda y prueba abriendo el archivo en el navegador.

## 12. Licencia

Este proyecto se distribuye bajo licencia MIT — ver [`LICENSE`](LICENSE).

## 13. Nota de transparencia

Este proyecto fue construido con apoyo de herramientas de inteligencia artificial (Claude, de Anthropic) para la limpieza de datos, la construcción del modelo, la documentación y el desarrollo del agente conversacional, bajo la dirección y validación del equipo.
