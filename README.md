# CAsimulations

```CAsimulations``` proporciona una manera de simular fenómenos asociados con la propagación de enfermedades, basándose en modelos *SIR* y *SIS* implementados en autómatas celulares en Python. ```CAsimulations``` incluye una gran variedad de utilidades para análisis epidemiológicos tales como la capacidad de definir la condición inicial de frontera del sistema, la condición inicial de dispersión de los individuos infectados, variaciones y comparaciones con respecto al cambio de escala y al cambio de frontera del sistema, variaciones promedio para un número arbitrario de simulaciones, entre otros. 

### Instalación
Solo debemos usar pip para instalar:

```pip install -i https://test.pypi.org/simple/ casimulation==0.0.0.2```
### Preliminares
Se decidió implementar una interpolación tipo spline cubica para la correcta visualización de los datos obtenidos a partir de listas de coordenadas. ```spline3``` genera los coeficientes de los polinomios cúbicos que mejor se aproximan a la lista ```A``` .
#### spline3(A)
Realice una interpolación cubica tipo spline, tomando como puntos los elementos de A.
###### Parámetros:
```
A: list   #Lista de coordenadas.
```
###### Devoluciones:
```
np.array    #Arreglo de puntos al aplicar un spline cubico.
```
##### Ejemplo:
```
>>> from CAsimulation import camodels as cm
>>> Point_list=[[1,0.2],[2,2.7],[3,3],[4,1],[5,2]]
>>> cm.spline3(Point_list)
array([[ 0.2       ,  2.87142857,  0.        , -0.37142857],
       [ 2.7       ,  1.75714286, -1.11428571, -0.34285714],
       [ 3.        , -1.5       , -2.14285714,  1.64285714],
       [ 1.        , -0.85714286,  2.78571429, -0.92857143]])
```
## Autómatas celulares 2-dimensionales
Para el caso de AC en dos dimensiones, encontramos una gran variedad de vecindarios, sin embargo, para los intereses de investigación analizamos la vecindad de Moore, que consideran los vecinos diagonales y ortogonales.

![texto alternativo](Vecindad_de_Moore.png)

#### array_generator(A, i, j)
Genera la vecindad de Moore para la célula en la fila i columna j
###### Parámetros: 	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
I: int        #Fila i de A
J: int        #Fila j de A
```
###### Devoluciones:	
```
np.array    #Vecindad de Moore de la célula en la fila i columna j
```
Inicialmente debemos identificar dos estados básicos en la simulación basada en modelos de propagación. El primero de ellos será el estado de susceptibilidad, los agentes (píxeles o componentes de la matriz) que tengan este estado, podrán adquirir la enfermedad y por otro lado tendremos los individuos que cuenten con el estado de infección, los cuales podrían infectar a los individuos susceptibles.

Identificaremos los estados *susceptible* e *infectado* con los valores numéricos 0 (cero) y 1 (uno) respectivamente.

#### vector_S(A)
Genera la lista de posiciones de individuos susceptibles, los cuales identificamos con 0 (cero)
###### Parámetros:
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:
```
list    #Lista de posiciones de individuos susceptibles
```
#### vector_I(A)
Genera la lista de posiciones de individuos infectados, identificados con 1 (uno)	
###### Parámetros:	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:	
```
list    #Vector de posiciones de individuos infectados
```
##### Ejemplo:
```
>>> import random
>>> random_matrix = [[random.randint(-1,3) for e in range(6)] for e in range(8)]
>>> random_matrix
[[3, 1, 0, 1, 1, 2],
 [0, 1, -1, -1, 2, 1],
 [-1, 1, 1, 0, 2, 0],
 [0, -1, 2, -1, 1, -1],
 [0, 2, 1, -1, -1, 2],
 [-1, -1, 3, 1, 0, 2],
 [3, 3, 2, 2, -1, 3],
 [1, 2, -1, -1, 3, 3]]
>>> cm.array_generator(random_matrix, 3,4)
array([[ 0.,  2.,  0.],
       [-1.,  1., -1.],
       [-1., -1.,  2.]])
>>> import numpy as np
>>> random_matrix=np.array(random_matrix)
>>> cm.vector_S(random_matrix)
[[0, 2], [1, 0], [2, 3], [2, 5], [3, 0], [4, 0], [5, 4]]
>>> cm.vector_I(random_matrix)
[[0, 1], [0, 3], [0, 4], [1, 1], [1, 5], [2, 1], [2, 2], [3, 4], [4, 2], [5, 3], [7, 0]]
```
