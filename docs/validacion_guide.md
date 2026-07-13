# Guía de validación para pares evaluadores

Este documento permite comprobar de forma independiente que los datos, el modelo y el agente de este repositorio funcionan como se describe, sin depender de la palabra del equipo.

## 1. Verificar las fuentes de datos

1. Abrir https://www.datos.gov.co/Educaci-n/Resultados-nicos-Saber-11/kgxf-xxbe y confirmar que el dataset existe, es público y corresponde a resultados de Saber 11 del ICFES.
2. Abrir https://www.postdata.gov.co/resource/797/download/file y confirmar que descarga un archivo CSV con columnas de municipio y accesos a internet fijo.
3. Los identificadores y enlaces completos están en `docs/fuentes_datos.md`.

## 2. Reproducir la limpieza de datos

1. Abrir `notebooks/STEMData_Limpieza_Python.ipynb` en Google Colab.
2. Ejecutar todas las celdas (menú Entorno de ejecución → Ejecutar todas).
3. Verificar que el archivo resultante `stemdata_limpio.csv` tenga aproximadamente 1.888 filas (municipio + zona) y las columnas: `municipio`, `zona`, `promedio_ciencias`, `promedio_matematicas`, `total_accesos_internet`.
4. Verificar el caso de Bogotá específicamente: `df[df['municipio'] == 'BOGOTA']` debe mostrar dos filas (rural y urbano) sin valores vacíos.

## 3. Reproducir el modelo

1. Abrir `notebooks/STEMData_Modelo_3Capas.ipynb`, subir el `stemdata_limpio.csv` generado en el paso anterior.
2. Ejecutar todas las celdas.
3. Verificar que `df['nivel_brecha'].value_counts()` y `df['nivel_conectividad'].value_counts()` coincidan con las cifras reportadas en `docs/conclusiones.md`.
4. Probar la función `generar_planeacion("MEDELLIN", "URBANA")` y confirmar que devuelve un diagnóstico coherente con los datos de ese municipio.

## 4. Verificar el clasificador de conectividad

El archivo `models/modelo_entrenado.pkl` contiene un árbol de decisión (`sklearn.tree.DecisionTreeClassifier`) entrenado sobre `total_accesos_internet` para predecir `nivel_conectividad`. Para cargarlo y probarlo:

```python
import pickle
with open('models/modelo_entrenado.pkl', 'rb') as f:
    modelo = pickle.load(f)

modelo.predict([[50000]])
```

La exactitud reportada en `reports/reporte_final.pdf` se calculó sobre un conjunto de prueba separado (20% de los datos, no usado en el entrenamiento).

## 5. Probar el agente sin depender del equipo

1. Descargar `RECURSOS/stemdata_agente.html`.
2. Abrirlo con doble clic en cualquier navegador (no requiere instalación ni conexión a un servidor propio; sí requiere internet para cargar el mapa).
3. Seleccionar un municipio, zona y grado, y presionar "Consultar".
4. Verificar que aparecen las insignias de color, el mapa centrado en el municipio elegido y las dos gráficas comparativas.
5. Presionar "Ver planeación inicial" y luego escribir preguntas de prueba en el chat: `momentos`, `recursos`, `evaluación`, `componentes STEM`, `el reto`, `similar`.

## 6. Puntos de atención conocidos

- El agente reconoce intención por coincidencia de palabras clave, no por comprensión de lenguaje libre; preguntas formuladas de forma muy distinta a las palabras clave documentadas en `docs/historias_usuario.md` pueden no ser reconocidas.
- El banco de proyectos incluido tiene 6 actividades base; no cubre todas las combinaciones posibles de contexto.
- La variable de conectividad depende de que el dataset de la CRC en postdata.gov.co siga activo; en `docs/fuentes_datos.md` se documentan dos fuentes anteriores que dejaron de estar disponibles durante el desarrollo del proyecto.
