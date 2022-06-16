## Explicación de Grafos.

Primeramente empezaremos por explicar lo que es un grafo para tener un mejor entendimiento de lo que se tratará a contunuación.
<p align ="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/-DTWroWMB3Q" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>

Ahora que tenemos la noción acerca de lo que es un grafo podemos empezar a explicar acerca de estos en las redes neuronales, como sabemos una red neuronal tiene entradas fijas las cuales pueden ser, archivos como imágenes, audios, etc.
¿Pero qué pasa cuando intentamos implementar un dato estructurado cómo entrada?

![entradasRN](https://user-images.githubusercontent.com/65386838/173957546-4e9c7b22-1de4-4d4c-98c0-69248de14e89.PNG)

## Redes Neuronales Gráficas o en Grafos(GNN)
En este punto es dónde entran las redes neuronales gráficas las cuales se destacan porque pueden manejarse bien o operar de cierta forma con este tipo de datos estructurados al extraer y utilizar características del grafo subyacente.
Ahora bien.
Empezareos por definir que son las Redes Neuronales Gráficas o de Grafo, estás manejan entradas en una estructura de datos como son vectores, matrices o tensores, entonces aprovechan que  los dominios complejos al tener una rica estructura relacional que se puede representar como un grafo relacional se puede entonces obtener al modelar explícitamente las relaciones un mejor desempeño.

Lo que hace la gran diferencia entre este tipo de redes neuronales y las "típicas" por llamarlas de alguna forma es que al trabajar con este tipo de estructura no solo se analiza información o números aíslados, si no que tambien se trabaja con las relaciones entre estos.

Este tipo de redes neuronales cobran cada vez más fuerza al punto en que en su momento llegaron a desplazar a los metodos anteriores que se usaban para este tipo de información en grafos como lo son los núcleos de grafos y los métodos de caminata aleatoria.

Para dar un poco de contexto, la caminata aleatoria o Random Walks por su nombre en ingles es un proceso el cual fué fructifero en diversas areas como son la física el cual se aplicó para saber la trayectoría seguida por una molécula que viaja a través de un líquido o un gas, las finanzas para determinar el precio de una acción fluctuante, en ecología  se emplea para modelar los movimientos de un animal de pastoreo y muchas otras más areas y aplicaciones, en teoría estos se basan en cadenas de Márkov o proceso de Márkov, pero su campo tambien abarca grafos finitos o bien rectas o planos.

El objetivo que se presenta en este articulo es el poder explicar como surjen así como dar a conocer cuales son las variantes más populares actualmente.

## Los desafíos de la computación en grafos.
<p align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/X75vNB7lSGY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>
### Falta de estructura consistente
A lo primero que nos vamos a encontrar como un desafío en este campo es que se tiene una estructura incosistente, esto se refiere a que los grafos tienen tantas variedades en su estructura ya que puede haber unos con un pequeño número de nodos, pero por otra parte se puede tener uno con mucho más número de nodos por lo que esto dificulta su tratamiento, a continuación se explica con un ejemplo en moleculas.
Para esto se va a considerar la tarea de predecir si una molécula química es tóxica o no.

![moleculas](https://user-images.githubusercontent.com/65386838/173958401-3b87fccd-e293-4ae3-90c6-40adcbbceb38.PNG)

Las principales complicaciones que se pueden observar en la imagen anterior son las siguientes.
* Las moléculas pueden tener diferente número de átomos.
* Los átomos en una molécula pueden ser de diferentes tipos.
* Cada uno de estos átomos puede tener diferente número de conexiones.
* Estas conexiones pueden tener diferentes puntos fuertes.
* La representación de gráficos en un formato que se pueda calcular no es trivial, y la representación final elegida a menudo depende significativamente del problema real.

### Equivarianza de orden del nodo

Para esto tomaremos prestado de las redes neuronales convolucionales los terminos invarianza y equivarianza los cuales son más ocupados en ese tipo de arquitecturas, definiendo estas dos palabras como:  
* La invarianza nos dice que la salida del modelo no es afectado por las transformaciones. 
* La equivarianza permite que la salida sea afectada, pero de una manera controlada y útil.

Por lo tanto si ampliamos el punto anterior se puede decir que los grafos a menudo no tienen un orden inherente presente entre los nodos.  si de compara esto con las imágenes, donde cada píxel está determinado únicamente por su posición absoluta dentro de la imagen, nos podemos dar una idea del problema.

![graphsDistill](https://user-images.githubusercontent.com/65386838/173960157-a0ecdbc3-b987-494c-804e-08e3671ac07f.PNG)

Como resultado, nos gustaría que nuestros algoritmos fueran equivalentes al orden de los nodos: no deberían depender del orden de los nodos del grafo. Si permutamos los nodos de alguna manera, las representaciones resultantes de los nodos calculadas por nuestros algoritmos también deberían permutarse de la misma manera.

### Escalabilidad

¡Los gráficos pueden ser realmente grandes! Piense en las redes sociales como Facebook y Twitter, que tienen más de mil millones de usuarios. Operar con datos tan grandes no es fácil.

Afortunadamente, la mayoría de los gráficos que ocurren naturalmente son "escasos": tienden a tener un número de aristas lineal en su número de vértices. Veremos que esto permite el uso de métodos inteligentes para calcular de manera eficiente las representaciones de los nodos dentro del gráfico. Además, los métodos que analizamos aquí tendrán significativamente menos parámetros en comparación con el tamaño de los gráficos en los que operan.

## Resolución de problemas y notación.
Hay muchos problemas útiles que se pueden formular sobre gráficos:

* __Clasificación de nodos__: clasificación de nodos individuales.
* __Clasificación de grafos__ : clasificación de gráficos completos.
* __Agrupación de nodos__ : agrupación de nodos similares en función de la conectividad.
* __Predicción de enlaces__ : predicción de enlaces perdidos.
* __Maximización de influencia__ : identificación de nodos influyentes.
![part1Graph](https://user-images.githubusercontent.com/65386838/173960290-a19e17bb-050b-47f1-a0e2-701a30f46012.PNG)
![part2Graph](https://user-images.githubusercontent.com/65386838/173960295-4bd026b0-5c86-449c-907f-3eaccd853376.PNG)

Un precursor común para resolver muchos de estos problemas es el aprendizaje de representación de nodos: aprender a asignar nodos individuales a vectores de valores reales de tamaño fijo (llamados "representaciones" o "incrustaciones").

En Aprendizaje de parámetros GNN (Se explican más adelante), veremos cómo se pueden utilizar las incrustaciones aprendidas para estas tareas.
Las diferentes variantes de GNN se distinguen por la forma en que se calculan estas representaciones. Sin embargo, en general, las GNN calculan las representaciones de los nodos en un proceso iterativo. Usaremos la notación ![hsubvk](https://user-images.githubusercontent.com/65386838/174001928-f834050e-c3c4-4e3e-bb7b-c5fbe2bfd88d.PNG) para indicar la representación del nodo v después de la k iteración. Cada iteración se puede considerar como el equivalente de una "capa" en las redes neuronales estándar.

Definiremos un grafo G como un conjunto de nodos, V, con un conjunto de aristas E que los conectan. Los nodos pueden tener características individuales como parte de la entrada: lo denotaremos por x_v la característica individual para el nodo v∈V. Por ejemplo, las "características del nodo" para un píxel en una imagen en color serían los valores de los canales rojo, verde y azul (RGB) en ese píxel.

Para facilitar la exposición, supondremos que G no está dirigido y que todos los nodos son del mismo tipo. Este tipo de gráficos se denominan "homogéneos". Muchas de las mismas ideas que veremos aquí se aplican a otros tipos de gráficos: discutiremos esto más adelante en Diferentes tipos de gráficos.

A veces necesitaremos denotar una propiedad de grafo mediante una matriz M, donde cada fila M_v

representa una propiedad correspondiente a un vértice particular v.


## Extendiendo convoluciones a grafos.

Ahora retomaremos el concepto de red neuronal Las redes neuronales convolucionales surgen del estudio de la corteza visual en gatos realizado por David H. Hubel y Torsten Wiesel. Estos autores demostraron que existen grupos de neuronas en la corteza visual que tienen un campo receptivo local. Un campo receptivo se define como una región limitada del espacio en la que un grupo de neuronas reaccionan en función a un estímulo. [2]
Se puede ver el siguiente video como apoyo.
<p align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/mgaUjJ-430Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>

Se ha visto que las redes neuronales convolucionales son bastante poderosas para extraer características de las imágenes. Sin embargo, las imágenes en sí pueden verse como grafos con una estructura similar a una cuadrícula muy regular, donde los píxeles individuales son nodos y los valores del canal RGB en cada píxel son las características del nodo.

Una idea natural, entonces, es considerar la generalización de convoluciones a grafos arbitrarios. Sin embargo, recuerde los desafíos enumerados en la sección anterior: en particular, las circunvoluciones ordinarias no son invariantes en el orden de los nodos, ya que dependen de las posiciones absolutas de los píxeles. Inicialmente, no está claro cómo generalizar convoluciones sobre cuadrículas a convoluciones sobre gráficos generales, donde la estructura de vecindad difiere de un nodo a otro. El lector curioso puede preguntarse si se podría realizar algún tipo de relleno y ordenamiento para garantizar la consistencia de la estructura de vecindad entre los nodos. Esto se ha intentado con cierto éxito, pero las técnicas que veremos aquí son más generales y poderosas.

![ConvinCNS](https://user-images.githubusercontent.com/65386838/173960385-8972ebc1-f7ba-450e-9a1f-88ce7bc771a0.PNG)

Las circunvoluciones en las CNN están inherentemente localizadas. Los vecinos que participan en la convolución en el píxel central se resaltan en gris.

## Filtros polinómicos en grafos.
Comenzamos presentando la idea de construir filtros polinómicos sobre vecindarios de nodos, de forma muy similar a cómo las CNN calculan filtros localizados sobre píxeles vecinos. Luego, veremos cómo enfoques más recientes amplían esta idea con mecanismos más potentes. Finalmente, discutiremos métodos alternativos que pueden usar información de nivel de gráfico "global" para calcular representaciones de nodos.
### El grafo laplaciano.
Dado un gráfico G, fijemos un orden arbitrario de los n nodos de G. Denotamos la matriz de adyacencia 0−1 de G por A, podemos construir la matriz de grado diagonal D de G como:
![Eq1](https://user-images.githubusercontent.com/65386838/173960579-72dc0528-c6b8-46c6-b6d0-6576b459df49.PNG)
donde A_vu denota la entrada en la fila correspondiente a v y la columna correspondiente a uu en la matriz A. Usaremos esta notación a lo largo de esta sección.

Entonces, el grafo laplaciano L es la matriz cuadrada n×n definida como: L = D - A.

![LaplacianLoG](https://user-images.githubusercontent.com/65386838/173960589-937d782e-7f43-42a9-bf05-2fdc40ade6a2.PNG)

El laplaciano L para un grafo no dirigido G, con la fila correspondiente al nodo C resaltada. Los ceros en L no se muestran arriba. El laplaciano L depende solo de la estructura del gráfico G, no de las características de los nodos.

### Polinomios del Laplaciano.

![eq2](https://user-images.githubusercontent.com/65386838/173960742-a75e7b61-6c47-46b0-8848-e3bf2741ab84.PNG)
![Fixing](https://user-images.githubusercontent.com/65386838/173962635-9f33ddc4-0608-432a-9847-94f6be524a77.PNG)


### ChebNet

ChebNet refina esta idea de filtros polinómicos observando filtros polinómicos de la forma:

![eqcheb](https://user-images.githubusercontent.com/65386838/173961575-d0611f9f-5371-4ddb-8c10-cea60eeb5851.PNG)

donde T_i es el polinomio de Chebyshev de grado ii del primer tipo y L^~ es el laplaciano normalizado definido usando el valor propio más grande de L: Discutimos los valores propios del laplaciano L con más detalle en una sección posterior.

![eqcheb2](https://user-images.githubusercontent.com/65386838/173961582-5eb0f1e4-2f5a-4778-a7b3-1fffec4c4e0c.PNG)

¿Cuál es la motivación detrás de estas elecciones?

L es en realidad semidefinida positiva: todos los valores propios de L no son menores que 0. Si λmax(L)>1, las entradas en las potencias de L aumentan rápidamente de tamaño. L^~ es efectivamente una versión reducida de L, con valores propios garantizados en el rango [-1, 1]. Esto evita que las entradas de potencias de L^~ exploten. De hecho, en la visualización anterior: restringimos los coeficientes de orden superior cuando se selecciona el Laplaciano LL no normalizado, pero permitimos valores más grandes cuando se selecciona el Laplaciano L^~ normalizado, para mostrar el resultado x’ en la misma escala de color.
Los polinomios de Chebyshev tienen ciertas propiedades interesantes que hacen que la interpolación sea numéricamente más estable. No hablaremos de esto con más profundidad aquí, pero recomendaremos a los lectores interesados que le echen un vistazo como un recurso definitivo.


### Los filtros polinómicos son equivalentes al orden de los nodos.

Los filtros polinómicos que consideramos aquí son en realidad independientes del orden de los nodos. Esto es particularmente fácil de ver cuando el grado del polinomio p_w es 11: donde la característica de cada nodo se agrega con la suma de las características de su vecino. Claramente, esta suma no depende del orden de los vecinos. Se sigue una prueba similar para polinomios de mayor grado: las entradas en las potencias de L son equivalentes al orden de los nodos.

__Details for the Interested Reader__

Como arriba, supongamos un orden de nodo arbitrario sobre los n nodos de nuestro gráfico. Cualquier otro orden de nodos se puede considerar como una permutación de este orden de nodos original. Podemos representar cualquier permutación mediante una matriz de permutación __P__. __P__ siempre será una matriz ortogonal 0−1:

![PT1](https://user-images.githubusercontent.com/65386838/174026199-090a28a8-d0bf-4014-bac6-2a7b896c8d53.PNG)

Entonces, llamamos a un algoritmo _f_ equivalente de orden de nodo si para todas las permutaciones __P__:

![PT2](https://user-images.githubusercontent.com/65386838/174026365-b1421ac1-905c-4b7f-be99-a5be429f5dca.PNG)

Al cambiar al nuevo orden de nodos usando la permutación __P__, las cantidades a continuación se transforman de la siguiente manera:

![PT3](https://user-images.githubusercontent.com/65386838/174026469-32eacf0f-08e0-4bff-9ec1-780a9bdd2f0e.PNG)


y así, para el caso de los filtros polinómicos, podemos ver que:

![PT4](https://user-images.githubusercontent.com/65386838/174026560-e8f4a4e9-f098-4e4d-b06b-cd1ee417ef42.PNG)

según sea necesario.


### Computación embebida.
La computación embebida o incrustrada es una asignación de una variable categórica discreta a un vector de números continuos. En el contexto de las redes neuronales, las incrustaciones son representaciones vectoriales continúas aprendidas de baja dimensión de variables discretas. Las incrustaciones de redes neuronales son útiles porque pueden reducir la dimensionalidad de las variables categóricas y representar categorías de manera significativa en el espacio transformado.
Ahora describimos cómo podemos construir una red neuronal gráfica apilando capas de ChebNet (o cualquier filtro polinomial) una tras otra con no linealidades, como una CNN estándar. En particular, si tenemos K capas de filtros polinómicos diferentes, la k^th de las cuales tiene sus propios pesos aprendibles w^k, realizaríamos el siguiente cálculo:


![embebida1](https://user-images.githubusercontent.com/65386838/173961623-ef20b755-533f-48a4-a009-409b0ef54ba3.PNG)


Tenga en cuenta que estas redes reutilizan los mismos pesos de filtro en diferentes nodos, imitando exactamente el peso compartido en las redes neuronales convolucionales (CNN) que reutilizan pesos para filtros convolucionales en una cuadrícula.


## Redes neuronales gráficas modernas

![moderngraph](https://user-images.githubusercontent.com/65386838/173961653-84495082-e506-4b0d-bab5-399efbe58969.PNG)


### Computación embebida.
El paso de mensajes forma la columna vertebral de muchas arquitecturas GNN en la actualidad. Describimos los más populares en profundidad a continuación:

- Redes convolucionales gráficas (GCN)
- Redes de Atención Grafica (GAT)
- Gráfico de muestra y agregado (GraphSAGE)
- Red de isomorfismo gráfico (GIN)

VIDEO

## Redes neuronales gráficas interactivas.

video

## De convoluciones locales a globales.



### Convoluciones espectrales.
video
### Representaciones espectrales de imágenes naturales.
<p align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/IVrypFvNxFA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>
### Computación embebida.
Ahora tenemos los antecedentes para comprender las convoluciones espectrales y cómo se pueden usar para calcular incrustaciones/representaciones de características de nodos.

Como antes, el modelo que describimos a continuación tiene K capas: cada capa k tiene parámetros aprendibles w^(k), llamados "pesos de filtro". Estos pesos se convolucionarán con las representaciones espectrales de las características del nodo. Como resultado, el número de pesos necesarios en cada capa es igual a m, el número de vectores propios utilizados para calcular las representaciones espectrales. Habíamos demostrado en la sección anterior que podemos tomar m<<n y aun así no perder cantidades significativas de información.

Por lo tanto, la convolución en el dominio espectral permite el uso de significativamente menos parámetros que solo la convolución directa en el dominio natural. Además, en virtud de la suavidad de los vectores propios laplacianos en el gráfico, el uso de representaciones espectrales impone automáticamente un sesgo inductivo para que los nodos vecinos obtengan representaciones similares.

Asumiendo características de nodos unidimensionales por ahora, la salida de cada capa es un vector de representaciones de nodos h^(k), donde la representación de cada nodo corresponde a una fila del vector.

Fijamos un ordenamiento de los nodos en G. Esto nos da la matriz de adyacencia A y el gráfico laplaciano L, lo que nos permite calcular U_m. Finalmente, podemos describir el cálculo que realizan las capas, una tras otra:

El método anterior se generaliza fácilmente para el caso en que cada h^(k) en  R^d_ktambién:


![embebida3](https://user-images.githubusercontent.com/65386838/173962058-be9683f5-5ee7-4af8-8b24-6b2212593238.PNG)

Con las ideas de la sección anterior, vemos que la convolución en el dominio espectral de los gráficos se puede considerar como la generalización de la convolución en el dominio de la frecuencia de las imágenes.

![embebida3-2](https://user-images.githubusercontent.com/65386838/173962069-e3c2c779-b43c-4535-a2b7-e53ce32625f2.PNG)


### Las convoluciones espectrales son equivalentes al orden de los nodos.
video

### Propagación global a través de grafos embebidos.
Una forma más sencilla de incorporar información a nivel de gráfico es calcular incrustaciones de todo el gráfico agrupando incrustaciones de nodos (y posiblemente bordes) y luego usar la incrustación de gráficos para actualizar las incrustaciones de nodos, siguiendo un esquema iterativo similar al que hemos visto aquí. . Este es un enfoque utilizado por Graph Networks. Discutiremos brevemente cómo se pueden construir incrustaciones a nivel de gráfico en Pooling. Sin embargo, tales enfoques tienden a ignorar la topología subyacente del gráfico que pueden capturar las convoluciones espectrales.

## Aprendizaje de parámetros GNN.

Todos los cálculos de incrustación que hemos descrito aquí, ya sean espectrales o espaciales, son completamente diferenciables. Esto permite que las GNN se entrenen de un extremo a otro, al igual que una red neuronal estándar, una vez que se define una función de pérdida L adecuada:
* __Clasificación del Nodo__: Al minimizar cualquiera de las pérdidas estándar para las tareas de clasificación, como la entropía cruzada categórica cuando hay varias clases presentes:


![Leq1](https://user-images.githubusercontent.com/65386838/173962358-d5b85127-d910-4173-9b4c-3c2356249e90.PNG)


donde y_vc es la probabilidad prevista de que el nodo v esté en la clase c. Los GNN se adaptan bien a la configuración semisupervisada, que es cuando solo se etiquetan algunos nodos en el gráfico. En este escenario, una forma de definir una pérdida LG
sobre un gráfico de entrada G es:


![Leq2](https://user-images.githubusercontent.com/65386838/173962364-688b11e0-b42e-464e-8c60-dc29a761709d.PNG)


donde, solo calculamos las pérdidas sobre los nodos etiquetados Lab(G).
* __Clasificación de grafos__: al agregar representaciones de nodos, se puede construir una representación vectorial de todo el gráfico. Esta representación gráfica se puede utilizar para cualquier tarea a nivel de gráfico, incluso más allá de la clasificación. Consulte Agrupación para ver cómo se pueden construir las representaciones de gráficos.
* __Predicción de enlaces__: al muestrear pares de nodos adyacentes y no adyacentes, y usar estos pares de vectores como entradas para predecir la presencia/ausencia de un borde. Para un ejemplo concreto, al minimizar la siguiente pérdida similar a la 'regresión logística':


![Leq3](https://user-images.githubusercontent.com/65386838/173962371-3de4e2f9-2136-498e-a8f7-0b76a776c83b.PNG)


donde σ es la función sigmoidea y e_vu = 1
si f existe una arista entre los nodos vv y uu, siendo 00 en caso contrario.

* __Agrupación de nodos__: simplemente agrupando las representaciones de nodos aprendidas.
El amplio éxito del entrenamiento previo para modelos de procesamiento de lenguaje natural como ELMo y BERT ha despertado el interés en técnicas similares para GNN. La idea clave en cada uno de estos artículos es entrenar GNN para predecir propiedades gráficas locales (p. ej., grados de nodo, coeficiente de agrupamiento, atributos de nodo enmascarado) y/o globales (p. ej., distancias por pares, atributos globales enmascarados).

Otra técnica autosupervisada es hacer cumplir que los nodos vecinos obtengan incrustaciones similares, imitando enfoques de caminata aleatoria como node2vec y DeepWalk:

![Leq4](https://user-images.githubusercontent.com/65386838/173962380-3f3b68a7-3313-42f4-a673-e4d879960eee.PNG)


donde N_R(v) es un conjunto múltiple de nodos visitados cuando se inician caminatas aleatorias desde vv. Para gráficos grandes, donde calcular la suma de todos los nodos puede ser costoso desde el punto de vista computacional, las técnicas como la Estimación de contraste de ruido son especialmente útiles.

## Conclusión y lecturas adicionales.

Si bien hemos analizado muchas técnicas e ideas en este artículo, el campo de Graph Neural Networks es extremadamente amplio. Nos hemos visto obligados a restringir nuestra discusión a un pequeño subconjunto de toda la literatura, sin dejar de comunicar las ideas clave y los principios de diseño detrás de las GNN. Recomendamos al lector interesado que eche un vistazo a una encuesta más completa.

Terminamos con sugerencias y referencias para conceptos adicionales que podrían interesar a los lectores:

### GNNs en Práctica.
Resulta que acomodar las diferentes estructuras de los gráficos a menudo es difícil de hacer de manera eficiente, pero aún podemos representar muchas ecuaciones de actualización de GNN utilizando productos de vectores de matriz dispersos (ya que, en general, la matriz de adyacencia es escasa para la mayoría de los conjuntos de datos de gráficos del mundo real). ) Por ejemplo, la variante GCN discutida aquí se puede representar como:


![GNNpractice](https://user-images.githubusercontent.com/65386838/174019364-e6a3465c-0897-4190-83db-7495c169981a.PNG)


La reestructuración de las ecuaciones de actualización de esta manera permite implementaciones vectorizadas eficientes de GNN en aceleradores como GPU.

Las técnicas de regularización para redes neuronales estándar, como Dropout , se pueden aplicar de manera directa a los parámetros (por ejemplo, poner a cero filas enteras de W^(k) arriba). Sin embargo, existen técnicas específicas de gráficos, como DropEdge, que elimina los bordes completos al azar del gráfico, que también mejoran el rendimiento de muchos modelos GNN.

### Diferentes tipos de Grafos.

Aquí, nos hemos centrado en gráficos no dirigidos, para evitar entrar en demasiados detalles innecesarios. Sin embargo, hay algunas variantes simples de convoluciones espaciales para:

* Grafos dirigidos: agregados a través de entidades del vecindario y/o del vecindario.
* Grafos temporales: agregados a través de características de nodos anteriores y/o futuras.
* Grafos heterogéneos: aprenda diferentes funciones de agregación para cada tipo de nodo/borde.

Existen técnicas más sofisticadas que pueden aprovechar las diferentes estructuras de estos gráficos: consulte para obtener más información.

### puesta común

Este artículo analiza cómo las GNN calculan representaciones útiles de nodos. Pero, ¿qué pasaría si quisiéramos calcular representaciones de gráficos para tareas a nivel de gráfico (por ejemplo, predecir la toxicidad de una molécula)?

Una solución simple es simplemente agregar las incrustaciones de nodos finales y pasarlas a través de otra red neuronal PREDICT G:


![Pooling](https://user-images.githubusercontent.com/65386838/173962541-5b0aac1a-f602-4449-a818-a3a6940fb752.PNG)


Sin embargo, existen técnicas más poderosas para 'agrupar' representaciones de nodos:

SortPool: ordene los vértices del gráfico para obtener una representación invariable del orden de nodos de tamaño fijo del gráfico y luego aplique cualquier arquitectura de red neuronal estándar.
DiffPool: aprenda a agrupar vértices, cree un gráfico más grueso sobre grupos en lugar de nodos, luego aplique un GNN sobre el gráfico más grueso. Repita hasta que solo quede un grupo.
SAGPool: aplique un GNN para conocer las puntuaciones de los nodos, luego conserve solo los nodos con las puntuaciones más altas y deseche el resto. Repita hasta que solo quede un nodo.

## Referencias.
* Texto de referencia tomado: (https://distill.pub/2021/understanding-gnns/)
* [1] Zhou, J., Cui, G., Hu, S., Zhang, Z., Yang, C., Liu, Z., ... & Sun, M. (2020). Graph neural networks: A review of methods and applications. AI Open, 1, 57-81.
* [2] Cicero, I. E. (2018). Utilización de redes neuronales convoluciones para la detección de tipos de imágenes.



