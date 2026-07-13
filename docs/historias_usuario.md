# Historias de usuario

Formato usado en todas las historias:

> **Como** [tipo de usuario]
> **Quiero** [acción que realiza]
> **Para** [beneficio que obtiene]
>
> **Criterio de aceptación:**
> **Dado que** [situación de partida]
> **Cuando** [acción concreta]
> **Entonces** [resultado esperado]

---

### HU-01
**Como** docente, **quiero** ingresar el municipio, la zona y el grado que enseño, **para** empezar a usar el agente.

**Criterio de aceptación:** Dado que abro el agente, cuando selecciono municipio, zona y grado y presiono "Consultar", entonces veo las insignias de diagnóstico, el mapa y las gráficas de mi municipio.

### HU-02
**Como** docente, **quiero** ver de un vistazo el nivel de brecha STEM y de conectividad de mi municipio, **para** entender mi contexto sin tener que leer números.

**Criterio de aceptación:** Dado que consulté mi municipio, cuando se muestra el resultado, entonces veo insignias de color (🔴🟠🟡🟢) y dos gráficas comparándome con el promedio y la distribución nacional.

### HU-03
**Como** docente, **quiero** recibir una planeación inicial con un solo clic, **para** tener un punto de partida inmediato.

**Criterio de aceptación:** Dado que ya vi mi diagnóstico, cuando presiono "Ver planeación inicial", entonces veo una tarjeta con el reto del mundo real, las áreas STEM integradas, el aprendizaje esperado para mi grado y la duración.

### HU-04
**Como** docente, **quiero** conversar con el agente para profundizar en la planeación, **para** obtener el detalle que necesito sin tener que consultar un documento aparte.

**Criterio de aceptación:** Dado que ya vi la planeación inicial, cuando escribo preguntas como "momentos", "recursos", "evaluación", "componentes STEM", "el reto" o "ciclo de diseño", entonces el agente responde con el contenido correspondiente del proyecto activo.

### HU-05
**Como** docente, **quiero** que la planeación se ajuste a mi grado y a la zona de mi colegio, **para** que sea aplicable en mi contexto real.

**Criterio de aceptación:** Dado que seleccioné un grado y una zona, cuando pido el "detalle" o los "recursos", entonces el aprendizaje esperado corresponde a mi banda de grado (primaria/secundaria/media) y la logística sugerida corresponde a mi zona (rural/urbana).

### HU-06
**Como** docente, **quiero** ver un municipio con condiciones similares al mío, **para** tener una referencia comparativa.

**Criterio de aceptación:** Dado que ya consulté mi municipio, cuando escribo "similar", entonces el agente muestra el municipio más cercano en brecha y conectividad, calculado por distancia (KNN).

### HU-07
**Como** jurado/evaluador del concurso, **quiero** ver de dónde salió cada dato usado, **para** confiar en que la información es real y verificable.

**Criterio de aceptación:** Dado que reviso el repositorio, cuando abro `docs/fuentes_datos.md`, entonces encuentro el enlace, entidad y variables exactas de cada dataset usado, incluyendo los intentos previos documentados con transparencia.
