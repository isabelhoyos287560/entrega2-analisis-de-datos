# Entrega 2 – Análisis de Datos

**Instituto Tecnológico Metropolitano (ITM)** · Ingeniería de Sistemas
**Curso:** Análisis de Datos · **Docente:** Daniel Alexis Nieto Mora · **Semestre:** 2026-2

## Integrantes

- Isabel Johana Hoyos Echavarria
- Jhon Eduardo Zabala Garzón
- Sebastian Villa Castillo
- Edwin Ramírez Gonzáles

## Objetivo

Explorar tres bases de datos de distinto tipo, justificar la elección de una de ellas, realizar un análisis exploratorio de datos (EDA) completo y aplicar técnicas de preprocesamiento y reducción de dimensionalidad como preparación para un futuro modelado.

## Bases de datos exploradas

| Dataset | Tipo | Tamaño | Fuente |
| --- | --- | --- | --- |
| [Airline Passenger Satisfaction](https://www.kaggle.com/datasets/teejmahal20/airline-passenger-satisfaction) | Tabular | 129,880 registros, 25 columnas (~15 MB) | Secundaria |
| [Chest X-Ray Images (Pneumonia)](https://www.kaggle.com/datasets/paultimothymooney/chest-xray-pneumonia) | Imágenes | 5,856 radiografías (~2.4 GB) | Secundaria |
| [IMDB Dataset of 50K Movie Reviews](https://www.kaggle.com/datasets/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews) | Texto | 50,000 reseñas (~66 MB) | Secundaria |

**Dataset seleccionado: Airline Passenger Satisfaction.** Obtuvo el mayor puntaje en la tabla de criterios (completitud, relevancia, documentación y manejabilidad). Combina variables numéricas, categóricas y 14 escalas ordinales de encuesta, lo que permite aplicar todas las técnicas del curso sin requerir procesamiento especializado de imágenes o texto.

## Estructura del repositorio

| Archivo | Contenido |
| --- | --- |
| `01_exploracion_datasets.ipynb` | Fase 1: exploración de los tres datasets, características, tabla de criterios y justificación de la elección |
| `02_eda.ipynb` | Fase 2: faltantes, outliers (IQR y z-score), distribuciones, análisis univariado y multivariado, pruebas de hipótesis y conclusiones |
| `03_preprocesamiento.ipynb` | Fase 3: limpieza, codificación, escalado, PCA, t-SNE y conclusiones |
| `requirements.txt` | Dependencias del proyecto |

## Ejecución

```bash
pip install -r requirements.txt
jupyter notebook
```

Los notebooks se ejecutan en orden y despues los datos se descargan automáticamente desde Kaggle con `kagglehub` la primera vez.

## Hallazgos principales

1. **La clase y el tipo de viaje son los factores categóricos más asociados con la satisfacción** (V de Cramér de 0.50 y 0.45), con interacción entre ambos: en viajes personales la clase no modifica la satisfacción (~10%), mientras que en viajes de negocios pasa de 30% en Eco a 72% en Business.
2. **`Online boarding` es la calificación que más diferencia a los pasajeros satisfechos** (4.15 vs. 2.71), seguida de entretenimiento a bordo, wifi y comodidad del asiento.
3. **Los ceros de la encuesta representan "sin respuesta" y no son aleatorios** (10,313 filas afectadas): el 99.7% de quienes no calificaron el wifi están satisfechos. Se conservaron como indicadores en el preprocesamiento.
4. **Las demoras reducen la satisfacción con un efecto débil** (Mann-Whitney, r = 0.07–0.11), y la edad tiene una relación no lineal (máxima entre 40 y 60 años).
5. **Las demoras presentan sesgo extremo** (skewness ≈ 6.8); los outliers corresponden a demoras reales, se conservaron y se transformaron con `log1p`.
6. **PCA:** 14 de 26 componentes retienen el 90% de la varianza. El primer componente (comodidad y experiencia a bordo) separa a satisfechos de insatisfechos y por sí solo alcanza 78.4% de exactitud en una regresión logística.
7. **t-SNE** separa mejor los grupos que PCA, lo que indica relaciones no lineales entre las variables y la satisfacción.

## Video

[Video explicativo del proyecto] (https://youtu.be/HErgdeu3mMI)
