# Frameworks de Redes Neuronales

Como ya hemos aprendido, para poder entrenar redes neuronales de manera eficiente necesitamos hacer dos cosas:

* Operar con tensores, por ejemplo, multiplicar, sumar y calcular funciones como sigmoid o softmax
* Calcular gradientes de todas las expresiones, para poder realizar optimización mediante descenso de gradiente

Aunque la biblioteca `numpy` puede hacer la primera parte, necesitamos algún mecanismo para calcular gradientes. En nuestro framework que desarrollamos en la sección anterior, tuvimos que programar manualmente todas las funciones derivadas dentro del método `backward`, que realiza la retropropagación. Idealmente, un framework debería darnos la posibilidad de calcular gradientes de *cualquier expresión* que definamos.

Otra cosa importante es poder realizar cálculos en GPU, o en cualquier otra unidad de cómputo especializada, como TPU. El entrenamiento de redes neuronales profundas requiere *muchos* cálculos, y poder paralelizar esos cálculos en GPUs es muy importante.

> ✅ El término 'paralelizar' significa distribuir los cálculos entre múltiples dispositivos.

Actualmente, los dos frameworks de redes neuronales más populares son: TensorFlow y PyTorch. Ambos proporcionan una API de bajo nivel para operar con tensores tanto en CPU como en GPU. Sobre esta API de bajo nivel, existen APIs de más alto nivel, llamadas Keras y PyTorch Lightning, respectivamente.

API de Bajo Nivel | TensorFlow | PyTorch
-----------------|------------|---------
API de Alto Nivel | Keras      | PyTorch

Las **APIs de bajo nivel** en ambos frameworks te permiten construir los llamados **grafos computacionales**. Este grafo define cómo calcular la salida (usualmente la función de pérdida) con los parámetros de entrada dados, y puede enviarse para su cálculo en GPU, si está disponible. Existen funciones para diferenciar este grafo computacional y calcular gradientes, que luego pueden usarse para optimizar los parámetros del modelo.

Las **APIs de alto nivel** consideran las redes neuronales como una **secuencia de capas**, y facilitan mucho la construcción de la mayoría de las redes neuronales. Entrenar el modelo usualmente requiere preparar los datos y luego llamar a una función `fit` para realizar el entrenamiento.

La API de alto nivel te permite construir redes neuronales típicas muy rápido sin preocuparte por muchos detalles. Al mismo tiempo, la API de bajo nivel ofrece mucho más control sobre el proceso de entrenamiento, por lo que se usa mucho en investigación, cuando se trabaja con nuevas arquitecturas de redes neuronales.

También es importante entender que puedes usar ambas APIs juntas, por ejemplo, puedes desarrollar tu propia arquitectura de capa de red usando la API de bajo nivel, y luego usarla dentro de una red más grande construida y entrenada con la API de alto nivel. O puedes definir una red usando la API de alto nivel como una secuencia de capas, y luego usar tu propio ciclo de entrenamiento de bajo nivel para realizar la optimización. Ambas APIs usan los mismos conceptos básicos subyacentes y están diseñadas para funcionar bien juntas.

## Aprendizaje

En este curso, ofrecemos la mayoría del contenido tanto para PyTorch como para TensorFlow. Puedes elegir tu framework preferido y solo seguir los notebooks correspondientes. Si no estás seguro de qué framework elegir, lee algunas discusiones en internet sobre **PyTorch vs. TensorFlow**. También puedes echar un vistazo a ambos frameworks para entender mejor.

Cuando sea posible, usaremos APIs de alto nivel por simplicidad. Sin embargo, creemos que es importante entender cómo funcionan las redes neuronales desde cero, por lo que al principio empezamos trabajando con la API de bajo nivel y tensores. Sin embargo, si quieres avanzar rápido y no quieres invertir mucho tiempo en aprender estos detalles, puedes saltarte esa parte y pasar directamente a los notebooks de la API de alto nivel.

## ✍️ Ejercicios: Frameworks

Continúa tu aprendizaje en los siguientes notebooks:

API de Bajo Nivel | Notebook TensorFlow+Keras | PyTorch
-----------------|----------------------------|---------
API de Alto Nivel | Keras                      | *PyTorch Lightning*

Después de dominar los frameworks, repasemos el concepto de sobreajuste.

# Sobreajuste

El sobreajuste es un concepto extremadamente importante en aprendizaje automático, ¡y es fundamental entenderlo bien!

Considera el siguiente problema de aproximar 5 puntos (representados por `x` en los gráficos a continuación):

!linear | overfit
-------------------------|--------------------------
**Modelo lineal, 2 parámetros** | **Modelo no lineal, 7 parámetros**
Error de entrenamiento = 5.3 | Error de entrenamiento = 0
Error de validación = 5.1 | Error de validación = 20

* A la izquierda, vemos una buena aproximación con una línea recta. Debido a que el número de parámetros es adecuado, el modelo capta correctamente la distribución de los puntos.
* A la derecha, el modelo es demasiado potente. Como solo tenemos 5 puntos y el modelo tiene 7 parámetros, puede ajustarse para pasar por todos los puntos, haciendo que el error de entrenamiento sea 0. Sin embargo, esto impide que el modelo entienda el patrón correcto detrás de los datos, por lo que el error de validación es muy alto.

Es muy importante encontrar un equilibrio correcto entre la complejidad del modelo (número de parámetros) y la cantidad de muestras de entrenamiento.

## Por qué ocurre el sobreajuste

  * No hay suficientes datos de entrenamiento
  * Modelo demasiado complejo
  * Demasiado ruido en los datos de entrada

## Cómo detectar el sobreajuste

Como puedes ver en el gráfico anterior, el sobreajuste se detecta por un error de entrenamiento muy bajo y un error de validación alto. Normalmente, durante el entrenamiento veremos que tanto el error de entrenamiento como el de validación comienzan a disminuir, y luego en algún punto el error de validación puede dejar de disminuir y empezar a aumentar. Esto será una señal de sobreajuste, e indicará que probablemente deberíamos detener el entrenamiento en ese punto (o al menos guardar una copia del modelo).

sobreajuste

## Cómo prevenir el sobreajuste

Si ves que ocurre sobreajuste, puedes hacer una de las siguientes cosas:

 * Aumentar la cantidad de datos de entrenamiento
 * Disminuir la complejidad del modelo
 * Usar alguna técnica de regularización, como Dropout, que veremos más adelante.

## Sobreajuste y el compromiso sesgo-varianza

El sobreajuste es en realidad un caso de un problema más general en estadística llamado compromiso sesgo-varianza. Si consideramos las posibles fuentes de error en nuestro modelo, podemos ver dos tipos de errores:

* Los **errores de sesgo** son causados porque nuestro algoritmo no puede capturar correctamente la relación entre los datos de entrenamiento. Esto puede deberse a que nuestro modelo no es lo suficientemente potente (**subajuste**).
* Los **errores de varianza** son causados porque el modelo aproxima el ruido en los datos de entrada en lugar de la relación significativa (**sobreajuste**).

Durante el entrenamiento, el error de sesgo disminuye (a medida que nuestro modelo aprende a aproximar los datos) y el error de varianza aumenta. Es importante detener el entrenamiento - ya sea manualmente (cuando detectamos sobreajuste) o automáticamente (introduciendo regularización) - para evitar el sobreajuste.

## Conclusión

En esta lección, aprendiste sobre las diferencias entre las diversas APIs de los dos frameworks de IA más populares, TensorFlow y PyTorch. Además, aprendiste sobre un tema muy importante: el sobreajuste.

## 🚀 Desafío

En los notebooks acompañantes, encontrarás 'tareas' al final; trabaja con los notebooks y completa las tareas.

## Repaso y Estudio Autónomo

Investiga sobre los siguientes temas:

- TensorFlow
- PyTorch
- Sobreajuste

Hazte las siguientes preguntas:

- ¿Cuál es la diferencia entre TensorFlow y PyTorch?
- ¿Cuál es la diferencia entre sobreajuste y subajuste?

## Tarea

En este laboratorio, se te pide resolver dos problemas de clasificación usando redes totalmente conectadas de una y varias capas, utilizando PyTorch o TensorFlow.

**Aviso legal**:  
Este documento ha sido traducido utilizando el servicio de traducción automática [Co-op Translator](https://github.com/Azure/co-op-translator). Aunque nos esforzamos por la precisión, tenga en cuenta que las traducciones automáticas pueden contener errores o inexactitudes. El documento original en su idioma nativo debe considerarse la fuente autorizada. Para información crítica, se recomienda la traducción profesional realizada por humanos. No nos hacemos responsables de malentendidos o interpretaciones erróneas derivadas del uso de esta traducción.