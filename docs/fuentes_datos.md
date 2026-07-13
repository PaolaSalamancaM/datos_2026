# Fuentes de datos utilizadas

## Dataset 1 (primario, análisis): Resultados únicos Saber 11

| Campo | Valor |
|---|---|
| Entidad responsable | ICFES |
| Portal | datos.gov.co |
| Identificador del dataset | `kgxf-xxbe` |
| Enlace directo | https://www.datos.gov.co/Educaci-n/Resultados-nicos-Saber-11/kgxf-xxbe |
| Método de acceso | API SODA (`$select`, `$where`, `$group` sobre `/resource/kgxf-xxbe.csv`) |
| Periodos usados | Últimos 2 años disponibles al momento de la consulta (ver notebook, Parte 2-3) |
| Filtro aplicado | Se agrupó por `municipio` + `zona`, promediando `punt_c_naturales` y `punt_matematicas` |

**Variables utilizadas:** `cole_mcpio_ubicacion` (→ `municipio`), `cole_area_ubicacion` (→ `zona`), `punt_matematicas`, `punt_c_naturales`.

**Uso en el proyecto:** diagnóstico de brecha STEM (Capa 1), clasificación por municipio y zona.

---

## Dataset 2 (secundario, análisis): Accesos de Internet Fijo desde 2024-1T

| Campo | Valor |
|---|---|
| Entidad responsable | Comisión de Regulación de Comunicaciones (CRC) |
| Portal | postdata.gov.co |
| Enlace de descarga directa | https://www.postdata.gov.co/resource/797/download/file |
| Método de acceso | Descarga directa de archivo CSV (separador `;`, no requiere parámetros de consulta) |
| Cobertura | Nacional, por municipio, desde 2024-1T |

**Variables utilizadas:** `MUNICIPIO`, `ACCESOS` (sumados por municipio → `total_accesos_internet`).

**Uso en el proyecto:** perfil de conectividad del municipio (Capa 2, viabilidad tecnológica).

**Nota sobre el cumplimiento de la regla de datasets:** la regla del concurso exige *al menos 1* dataset de datos.gov.co, no que ambos lo sean. Como Saber 11 ya es de datos.gov.co, usar este segundo dataset de postdata.gov.co (otro portal oficial del Estado colombiano) es válido y cumple el límite de 2 datasets totales.

**Historial de intentos previos (documentado por transparencia):**
- MEN, dataset de estadísticas por municipio (`nudc-7mev`): descontinuó el reporte de conectividad desde 2017.
- MinTIC, "Internet Fijo Penetración Municipio" (`fut2-keu8`, datos.gov.co): el dataset quedó archivado, su endpoint de consulta ya no responde (error 404).
- Se resolvió con el dataset de la CRC en postdata.gov.co, que sí se mantiene actualizado.

---

## Tabla de referencia (no analítica): Coordenadas de municipios (DIVIPOLA)

| Campo | Valor |
|---|---|
| Entidad responsable | DANE |
| Portal | datos.gov.co |
| Identificador del dataset | `gdxc-w37w` ("DIVIPOLA - Códigos municipios") |
| Enlace de descarga directa | https://www.datos.gov.co/api/views/gdxc-w37w/rows.csv?accessType=DOWNLOAD |
| Uso | Únicamente para ubicar el municipio en el mapa del agente (Leaflet.js) — no es un dataset de análisis |

**Variables utilizadas:** `Nombre Municipio`, `Latitud`, `longitud` (vienen con coma decimal, se convierten a punto en la limpieza).

---

## Variable de cruce entre los datasets de análisis

`municipio` está presente en Saber 11 y en el dataset de conectividad, y permite unir el diagnóstico de brecha STEM con el perfil de conectividad. Antes de cruzar, se estandarizan mayúsculas, tildes, puntuación y casos especiales (ver nota sobre Bogotá abajo).

## Caso especial: Bogotá D.C.

Bogotá aparece con distintas variantes de escritura entre fuentes (`BOGOTÁ`, `BOGOTÁ, D.C.`, `BOGOTÁ D.C.`). Se corrigió explícitamente en el notebook de limpieza (antes de agrupar/sumar la conectividad, y después de estandarizar mayúsculas en Saber 11), unificando todas las variantes a `BOGOTA`. Ver `notebooks/STEMData_Limpieza_Python.ipynb`, celdas de agrupación de conectividad y de estandarización de Saber 11.

## Transformaciones realizadas (resumen)

- [x] Agrupación de Saber 11 por municipio + zona (promedio de puntajes)
- [x] Suma de accesos a internet por municipio (conectividad)
- [x] Corrección de codificación de caracteres (tildes, tildes con tratamiento especial vía `quitar_tildes`)
- [x] Corrección de casos especiales de nombre (Bogotá D.C.)
- [x] Eliminación de filas vacías y duplicadas
- [x] Cruce (merge) de ambos datasets por `municipio`
- [x] Adición de coordenadas (tabla de referencia) para el mapa del agente
