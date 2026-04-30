# Proyecto integrador III — Entrega 1

Análisis exploratorio de datos (**EDA**) sobre abandono de clientes (**churn**) en una empresa de telecomunicaciones, desarrollado en el notebook `Telco.ipynb`.

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
