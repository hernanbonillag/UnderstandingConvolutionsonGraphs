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



## Resolución de problemas y notación.

![part1Graph](https://user-images.githubusercontent.com/65386838/173960290-a19e17bb-050b-47f1-a0e2-701a30f46012.PNG)
![part2Graph](https://user-images.githubusercontent.com/65386838/173960295-4bd026b0-5c86-449c-907f-3eaccd853376.PNG)


## Extendiendo circunvoluciones a grafos.

![ConvinCNS](https://user-images.githubusercontent.com/65386838/173960385-8972ebc1-f7ba-450e-9a1f-88ce7bc771a0.PNG)


## Filtros polinómicos en grafos.
### El grafo laplaciano.
![Eq1](https://user-images.githubusercontent.com/65386838/173960579-72dc0528-c6b8-46c6-b6d0-6576b459df49.PNG)
![LaplacianLoG](https://user-images.githubusercontent.com/65386838/173960589-937d782e-7f43-42a9-bf05-2fdc40ade6a2.PNG)

### Polinomios del Laplaciano.

![eq2](https://user-images.githubusercontent.com/65386838/173960742-a75e7b61-6c47-46b0-8848-e3bf2741ab84.PNG)
![Fixing](https://user-images.githubusercontent.com/65386838/173962635-9f33ddc4-0608-432a-9847-94f6be524a77.PNG)


### ChebNet

![eqcheb](https://user-images.githubusercontent.com/65386838/173961575-d0611f9f-5371-4ddb-8c10-cea60eeb5851.PNG)
![eqcheb2](https://user-images.githubusercontent.com/65386838/173961582-5eb0f1e4-2f5a-4778-a7b3-1fffec4c4e0c.PNG)


### Los filtros polinómicos son equivalentes al orden de los nodos.

video

### Computación embebida.
La computación embebida o incrustrada es una asignación de una variable categórica discreta a un vector de números continuos. En el contexto de las redes neuronales, las incrustaciones son representaciones vectoriales continúas aprendidas de baja dimensión de variables discretas. Las incrustaciones de redes neuronales son útiles porque pueden reducir la dimensionalidad de las variables categóricas y representar categorías de manera significativa en el espacio transformado.
Ahora describimos cómo podemos construir una red neuronal gráfica apilando capas de ChebNet (o cualquier filtro polinomial) una tras otra con no linealidades, como una CNN estándar. En particular, si tenemos K capas de filtros polinómicos diferentes, la k^{th} de las cuales tiene sus propios pesos aprendibles w^{k}, realizaríamos el siguiente cálculo:
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

## De circunvoluciones locales a globales.



### Convoluciones espectrales.
video
### Representaciones espectrales de imágenes naturales.
<p align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/IVrypFvNxFA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>
### Computación embebida.
Ahora tenemos los antecedentes para comprender las convoluciones espectrales y cómo se pueden usar para calcular incrustaciones/representaciones de características de nodos.

Como antes, el modelo que describimos a continuación tiene K capas: cada capa k tiene parámetros aprendibles w^(k), llamados "pesos de filtro". Estos pesos se convolucionarán con las representaciones espectrales de las características del nodo. Como resultado, el número de pesos necesarios en cada capa es igual a m, el número de vectores propios utilizados para calcular las representaciones espectrales. Habíamos demostrado en la sección anterior que podemos tomar m<<n y aun así no perder cantidades significativas de información.

Por lo tanto, la convolución en el dominio espectral permite el uso de significativamente menos parámetros que solo la convolución directa en el dominio natural. Además, en virtud de la suavidad de los vectores propios laplacianos en el gráfico, el uso de representaciones espectrales impone automáticamente un sesgo inductivo para que los nodos vecinos obtengan representaciones similares.

Asumiendo características de nodos unidimensionales por ahora, la salida de cada capa es un vector de representaciones de nodos h^{(k)}, donde la representación de cada nodo corresponde a una fila del vector.

Fijamos un ordenamiento de los nodos en G. Esto nos da la matriz de adyacencia A y el gráfico laplaciano L, lo que nos permite calcular U_m. Finalmente, podemos describir el cálculo que realizan las capas, una tras otra:

El método anterior se generaliza fácilmente para el caso en que cada h^{(k)} \in {R}^{d_k} también:
![embebida3](https://user-images.githubusercontent.com/65386838/173962058-be9683f5-5ee7-4af8-8b24-6b2212593238.PNG)

Con las ideas de la sección anterior, vemos que la convolución en el dominio espectral de los gráficos se puede considerar como la generalización de la convolución en el dominio de la frecuencia de las imágenes.

![embebida3-2](https://user-images.githubusercontent.com/65386838/173962069-e3c2c779-b43c-4535-a2b7-e53ce32625f2.PNG)


### Las circunvoluciones espectrales son equivalentes al orden de los nodos.
video

### Propagación global a través de grafos embebidos.

## Aprendizaje de parámetros GNN.
![Leq1](https://user-images.githubusercontent.com/65386838/173962358-d5b85127-d910-4173-9b4c-3c2356249e90.PNG)
![Leq2](https://user-images.githubusercontent.com/65386838/173962364-688b11e0-b42e-464e-8c60-dc29a761709d.PNG)
![Leq3](https://user-images.githubusercontent.com/65386838/173962371-3de4e2f9-2136-498e-a8f7-0b76a776c83b.PNG)
![Leq4](https://user-images.githubusercontent.com/65386838/173962380-3f3b68a7-3313-42f4-a673-e4d879960eee.PNG)
## Conclusión y lecturas adicionales.
### GNNs en Práctica.
### Diferentes tipos de Grafos.
### puesta en común
![Pooling](https://user-images.githubusercontent.com/65386838/173962541-5b0aac1a-f602-4449-a818-a3a6940fb752.PNG)

## Referencias.



```markdown
Ejemplo de código en markdown

```


