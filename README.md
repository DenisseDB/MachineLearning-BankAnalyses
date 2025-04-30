# Clasificador de Perfiles para la Adquisición de Tarjeta Bancaria

## Descripción del Proyecto

Este proyecto tiene como objetivo desarrollar un modelo de **machine learning** capaz de clasificar perfiles de potenciales compradores de una tarjeta de crédito. La meta es identificar, de forma rápida y precisa, a aquellas personas que cumplen con las características ideales para adquirir una tarjeta bancaria.

De esta manera, se busca optimizar el proceso comercial, evitando invertir tiempo en perfiles que probablemente rechazarán la oferta, y enfocándose directamente en aquellos con alta probabilidad de aceptación.

## Descripción del Dataset

Para este proyecto se utiliza un dataset titulado **Bank Marketing**, el cual fue descargado del repositorio de **UC Irvine Machine Learning Repository**. Este conjunto de datos contiene **45,211 instancias** y **17 características (features)** en total.

Las variables incluyen información socioeconómica y de comportamiento de los clientes, como edad, ocupación, estado civil, nivel de educación, saldo en cuenta bancaria, entre otros. El objetivo del modelo es predecir si un cliente aceptará o no la oferta de una **tarjeta de crédito**, representado por la **variable objetivo (target)**, que es de tipo binaria (sí/no).

## Proceso

### Selección de Columnas de Interés

De todo el dataset original, se seleccionaron únicamente aquellas columnas que resultan más relevantes para el objetivo del proyecto.

### Limpieza de los Datos

Una vez seleccionadas las columnas de interés, se procedió a la limpieza de los datos. Este paso es fundamental para eliminar registros inconsistentes, valores nulos o duplicados que puedan afectar negativamente el rendimiento y la precisión del modelo durante el entrenamiento.

### Separación del Set de Entrenamiento y Prueba

Con los datos ya limpios, se realizó la división del dataset en dos subconjuntos:  
- **`train_data`**: utilizado para entrenar el modelo  
- **`test_data`**: utilizado para evaluar
  
### Preprocesado del Target: Label Encoder

Como los modelos de machine learning trabajan únicamente con valores numéricos, es necesario transformar la variable objetivo (`y`) a formato binario. Para ello se utiliza **Label Encoder**, ya que:

- Solo existen dos categorías posibles: `yes` y `no`
- No hay riesgo de confusión por orden jerárquico entre clases
- Utiliza menos memoria y es eficiente computacionalmente

### Preprocesado de las Features: One-Hot Encoding

Para las variables categóricas con más de dos clases, se aplicó **One-Hot Encoding**, una técnica común que permite transformar estas categorías en variables binarias independientes. Esta técnica es especialmente útil cuando las categorías no tienen un orden específico.

Nos guiamos por la estrategia de "Titanic Solution: One-Hot-Encode All The Things", asegurando que todas las variables categóricas relevantes estén representadas correctamente sin introducir sesgos en el modelo.

## Construcción del Modelo

Una vez los datos están preprocesados, se procede a construir y entrenar el modelo.

### Hiperparámetros utilizados

- **Learning Rate**: Ajustado a `0.0005` para lograr una convergencia más estable.
- **Batch Size**: Establecido en `64`, balanceando entre ruido y eficiencia.
- **Class Weight**: Dar mayor peso a la clase minoritaria.
- **Threshold**: Reducido de `0.5` a `0.4` para favorecer la detección de la clase "Yes".
- **Capas Densas**: Se usaron 4 capas con distintas profundidades y `dropout` para evitar sobreajuste.

### Balanceo de Datos

El principal problema de este conjunto de datos es el desbalanceo entre clases. Para conocer las estrategias y métodos implementados para abordar esta situación, consulte el siguiente documento.
[Reporte Balanceo de Datos](Resultados_Obtenidos.pdf)

### Matriz de Confusión

Para evaluar el desempeño del modelo, se utilizó una **matriz de confusión**, la cual permite visualizar:

- Verdaderos positivos (TP)
- Verdaderos negativos (TN)
- Falsos positivos (FP)
- Falsos negativos (FN)

Esto permite no solo medir la precisión general del modelo, sino también entender su comportamiento frente a cada clase, especialmente en contextos con desbalance de datos.

### Métricas
Dado que nuestro dataset presentaba un desbalance de clases que fue corregido mediante técnicas de balanceo, utilizamos las siguientes métricas para evaluar el desempeño del modelo de predicción:
- Precision: Cuantos eran realmente positivos
- Racall: De los TP, cuantos detecto el modelo
- F1 Score: Media entre Precision y Recall (para datos desbalanceados)
- Support: Cuantos yes y no había

### Resultados
Te invito a consultar el siguiente documento, donde podrás encontrar los distintos enfoques que exploramos, junto con sus respectivos resultados. Al final, también se presenta la estrategia seleccionada y su desempeño final.
[Resultados](Resultados_Obtenidos.pdf)


