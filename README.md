# Proyecto integrador III — Entrega 1

Análisis exploratorio de datos (**EDA**) sobre abandono de clientes (**churn**) en una empresa de telecomunicaciones, desarrollado en el notebook `EA1_Telco.ipynb`.

## Participantes

- Aleicer Vesga  
- Guillermo Leon Loaiza  
- Jaider Morales  
- Robinson Marin Morales  

## Contexto

Las empresas con servicios digitales pierden usuarios “en silencio” cuando cancelan sin aviso previo (*churn*), lo que reduce ingresos recurrentes y encarece la adquisición de nuevos clientes.

## Objetivo

Identificar y comprender los factores demográficos, de cuenta y de servicios con mayor impacto en la cancelación del servicio, para orientar estrategias de retención.

## Pregunta analítica

¿Qué usuarios tienen mayor probabilidad de abandonar el servicio en los próximos 30 días y cuáles deben priorizarse en campañas de re-engagement?

## Hipótesis (resumen)

- Los clientes con contrato **mes a mes** tienden a cancelar más que quienes tienen contrato a **largo plazo** (1 o 2 años).
- Quienes **no** tienen servicios de valor agregado (p. ej. soporte técnico o seguridad en línea) son más propensos a irse.
- Hay **correlación positiva** entre **cargos mensuales** más altos y la probabilidad de **churn**.

## Datos

- **Origen:** [Telco Customer Churn — Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn) (descarga con `opendatasets`; requiere credenciales de Kaggle).
- **Tamaño:** 7 043 filas y 21 columnas (~1,1 MB).
- **Variable objetivo:** `Churn` (renombrada a `churn` en el notebook).

En el notebook las columnas se traducen al español; se ajustan tipos (p. ej. `cargo_total`), se revisan duplicados y valores faltantes, se analizan variables numéricas y categóricas, se construye un mapa de correlación y un informe con **ydata-profiling** (`ProfileReport`).

## Herramientas principales

Python, **pandas**, **matplotlib**, **seaborn**, **ydata-profiling**, **opendatasets**.

---

Para ejecutar el notebook localmente, adapta la ruta del CSV tras descargar el dataset y configura tus credenciales de Kaggle si usas `opendatasets.download`.

---

# Proyecto integrador III — Entrega 2

Limpieza y transformación del dataset **Telco Customer Churn** para garantizar su calidad y adecuación al análisis, desarrollado en el notebook `EA2_Telco_Limpieza.ipynb`.

## Objetivo

Llevar a cabo un proceso estructurado de limpieza y transformación que deje el dataset listo para el modelado predictivo, documentando cada decisión tomada y validando que el resultado final sigue permitiendo responder la pregunta de investigación.

## Contenido del notebook

El notebook está dividido en tres secciones principales:

**I. Descripción de Necesidades de Limpieza** — análisis previo de los seis aspectos de calidad del dataset antes de hacer cualquier cambio: duplicados, valores nulos, inconsistencias en valores, tipos de datos, valores atípicos y nivel de granularidad.

**II. Limpieza y Transformación de Datos** — implementación paso a paso de las correcciones identificadas:

- Verificación y eliminación preventiva de duplicados con `drop_duplicates()`
- Conversión de `cargo_total` de `object` a `float64` e imputación de 11 valores nulos con `0` (clientes nuevos sin cargos acumulados)
- Conversión de variables categóricas a tipo `category` de pandas y `churn` a `int8` (0/1)
- Visualización de outliers con boxplots y análisis IQR para las tres variables numéricas continuas
- Normalización de los valores `"No internet service"` y `"No phone service"` a `"No"` con `replace()` en 7 columnas de servicios
- Traducción de columnas descriptivas al español con `map()` (contrato, método de pago, género, tipo de internet)
- Traducción de columnas binarias `Yes/No` → `Sí/No` con `map()`
- Creación de columna `segmento` combinando tipo de contrato e internet con `zip()`
- Eliminación de `id_cliente` por ser un identificador sin valor analítico
- Agregaciones complementarias con `groupby()` para validar hipótesis por tipo de contrato y tipo de internet

**III. Validación** — verificación de completitud (0 nulos), relevancia de variables y granularidad individual, con contraste directo contra los tres objetivos de análisis e hipótesis definidas en la Entrega 1.

## Hallazgos principales tras la limpieza

- **Hipótesis 1 confirmada:** los clientes con contrato mes a mes presentan una tasa de churn del ~43 %, frente al ~11 % en contratos anuales y ~3 % en bianuales.
- **Hipótesis 2 confirmada:** los clientes sin soporte técnico tienen mayor tasa de churn que los que sí lo contratan.
- **Hipótesis 3 confirmada:** `cargo_mensual` correlaciona positivamente con churn (r ≈ 0.19), mientras que `meses_permanencia` correlaciona negativamente (r ≈ -0.35).

## Dataset limpio

El archivo `telco_customer_churn_limpio.csv` es el resultado final del proceso: 7 043 registros, 21 variables analíticas, sin valores nulos, con todos los tipos correctos y los valores estandarizados en español.

## Herramientas utilizadas

Python, **pandas**, **matplotlib**, **seaborn**.

---

Para ejecutar `EA2_Telco_Limpieza.ipynb` localmente, coloca el archivo `WA_Fn-UseC_-Telco-Customer-Churn.csv` en la misma carpeta del notebook antes de correrlo.


---
# Proyecto integrador III — Entrega 3

## Anexo — Dashboard Power BI (`analisisTelcoW.pbix`)

Informe interactivo de **Power BI** que complementa el EDA del notebook `EA1_Telco.ipynb`. Consolida visualizaciones y segmentaciones sobre el dataset **Telco Customer Churn** para explorar patrones de abandono y apoyar la priorización de acciones de retención.

### Contenido del informe

- Visualizaciones de tasas y distribuciones de **churn** por variables demográficas, de contrato, servicios y facturación.
- Cruces y filtros alineados con las **tres hipótesis** y la **pregunta analítica** del proyecto.
- Segmentación orientada a identificar perfiles de mayor riesgo de cancelación.

### Cómo abrirlo

1. Instalar [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (Windows).
2. Abrir `analisisTelcoW.pbix` desde la raíz del repositorio.
3. Si el informe referencia un archivo local (CSV o Excel), apuntar la fuente de datos al dataset del proyecto (`WA_Fn-UseC_-Telco-Customer-Churn.csv` o `telco_customer_churn_limpio.csv`, según la versión usada al publicar el `.pbix`).

### Conclusiones del análisis exploratorio

El análisis exploratorio permitió identificar con claridad los factores que más influyen en la cancelación del servicio. De las tres hipótesis planteadas, **dos quedaron completamente confirmadas** y **una fue confirmada de forma parcial**:

| Hipótesis | Resultado en el dashboard |
|-----------|---------------------------|
| Contrato mes a mes vs. largo plazo | **Confirmada.** El tipo de contrato es el predictor más fuerte: clientes mes a mes cancelan a una tasa **~15 veces mayor** que los de contrato a dos años. |
| Ausencia de servicios de valor agregado | **Confirmada.** Servicios como el **soporte técnico** reducen el churn aproximadamente a la **mitad**. |
| Cargos mensuales altos y churn | **Parcialmente confirmada.** Los cargos mensuales más altos **sí** correlacionan con mayor abandono, pero la **antigüedad del cliente** (`meses_permanencia`) tiene un **efecto protector más pronunciado**. |

**Respuesta a la pregunta de investigación:** los usuarios con mayor probabilidad de abandonar el servicio en los **próximos 60 días** son quienes combinan:

- Contrato **mes a mes**
- Menos de **12 meses** de antigüedad
- **Sin** servicios adicionales contratados
- Acceso a **fibra óptica**
- Pago mediante **cheque electrónico**

Este perfil debe ser la **primera prioridad** en campañas de re-engagement.

### Líneas de trabajo futuro

El informe dejó visibles dos segmentos que requieren **análisis adicional**: clientes con **fibra óptica** y quienes pagan con **cheque electrónico**, ambos con patrones de churn inusualmente altos no explicados del todo por las hipótesis originales. En entregas siguientes conviene profundizar con un **modelo predictivo** que cuantifique el riesgo individual de cada cliente.
