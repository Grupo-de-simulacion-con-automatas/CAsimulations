# CAsimulations

```CAsimulations``` proporciona una manera de simular fenómenos asociados con la propagación de enfermedades, basándose en modelos *SIR* y *SIS* implementados en autómatas celulares en Python. ```CAsimulations``` incluye una gran variedad de utilidades para análisis epidemiológicos tales como la capacidad de definir la condición inicial de frontera del sistema, la condición inicial de dispersión de los individuos infectados, variaciones y comparaciones con respecto al cambio de escala y al cambio de frontera del sistema, variaciones promedio para un número arbitrario de simulaciones, entre otros. 

### Instalación
Solo debemos usar pip para instalar:

```pip install -i https://test.pypi.org/simple/ casimulation```
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
####  one_function_graph(A, x)
Grafica el spline cubico para los elementos de A.
###### Parámetros:
```
A: list   #Lista de coordenadas de la función x
x: str    #Nombre de la función
```
###### Devoluciones:
```
.plt    #Gráfica de la función x 
```
#### one_state_graph(A, x)
Graficá el spline cubico para los elementos de A de manera normalizada
###### Parámetros:
```
A: list   #Lista de coordenadas de la función x
x: str    #Nombre de la función
```
###### Devoluciones:	
```
.plt    #Gráfica de la función normalizada x 
```
#### two_states_graph(A, B, X, Y, Z)
Graficá el spline cubico para los elementos de A y B
###### Parámetros:	
```
A: list   #Lista de coordenadas de la función x 
B: list   #Lista de coordenadas de la función y
x: str    #Nombre de la primera función
y: str    #Nombre de la segunda función
z: str    #Título del gráfico
```
###### Devoluciones:	
```
.plt    #Gráfica de las funciones x e y con título z
```
#### three_states_graph(A, B, C, x, y, z, w)
Graficá el spline cubico para los elementos de A, B y C
###### Parámetros: 	
```
A: list   #Lista de coordenadas de la función x
B: list   #Lista de coordenadas de la función y
C: list   #Lista de coordenadas de la función z
x: str    #Nombre de la primera función
y: str    #Nombre de la segunda función
z: str    #Nombre de la tercera función
w: str    #Título del gráfico 
```
###### Devoluciones:	
```
.plt    #Gráfica de las funciones x, y, z con título w
```
### Autómatas celulares 2-dimensionales
Para el caso de AC en dos dimensiones, encontramos una gran variedad de vecindarios, sin embargo, para los intereses de investigación analizamos la vecindad de Moore, que consideran los vecinos diagonales y ortogonales.

![texto alternativo](Imagenes/Vecindad_de_Moore.png)

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
## Modelos epidemiológicos en AC
Para comenzar con nuestro estudio en los modelos epidemiológicos usando AC, es importante definir los estados modelo. Trabajaremos con estados susceptibles *S*, infectados *I*, recuperados *R* y muertos *D*, adicionalmente incluiremos el estado vació *V* en nuestro modelo, esto permitirá realizar un análisis en el cambio de la topología de la vecindad de Moore, está noción se explicara de manera mas precisa en secciones posteriores. De esta manera, el conjunto de estados estará dado por $\sum=\{S,I,R,D,V\}$. 

Representaremos con los colores amarillo, rojo, verde y blanco los estados *S*, *I*, *R* y *D* respectivamente. En la siguiente ilustración se muestran únicamente uno de los casos posibles de permutación por cada estado de interacción la vecindad. 

![texto alternativo](Imagenes/estados.png)

Para plantear adecuadamente la regla de evolución local, debemos implementar una manera de contar los individuos que tengan un estado especifico en algún tiempo $t$ y en una vecindad determinada. Las funciones ```sumaS, sumaI``` y ```sumaR``` nos permiten contar la cantidad de vecinos que sean susceptibles, infectados o recuperados respectivamente, además de incluir la función ```sumaV``` que nos permite contar la cantidad de espacios vacíos en la vecindad a estudiar.

#### sumaS(V)
cantidad de individuos susceptibles en la vecindad
###### Parámetros:
```
V: np.array   #Vecindad
```
###### Devoluciones:
```
int   #Cantidad de individuos susceptibles en la vecindad V
```
#### sumaI(V)
cantidad de individuos infectados en la vecindad
###### Parámetros: 	
```
V: np.array   #Vecindad
```
###### Devoluciones:	
```
int   #Cantidad de individuos infectados en la vecindad V
```
#### sumaR(V)
cantidad de individuos recuperados en la vecindad
###### Parámetros: 	
```
V: np.array   #Vecindad
```
###### Devoluciones:	
```
int   #Cantidad de individuos recuperados en la vecindad V
```
#### sumaV(V)
cantidad de espacios vacíos en la vecindad
###### Parámetros: 	
```
V: np.array   #Vecindad
```
###### Devoluciones:	
```
int   #Cantidad de espacios vacíos en la vecindad V
```
##### Ejemplo:
```
>>> V = cm.array_generator(random_matrix, 6, 3)
>>> print(cm.sumaS(V), cm.sumaI(V), cm.sumaR(V), cm.sumaV(V))
1 1 1 3
```
#### color(A)
La función ```color``` nos permite graficar el entorno espacial de una manera intuitiva en una escala de colores rgb, usando la paleta nipy_spectral de Python.
###### Parámetros:
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:	
```np.array   #Arreglo con entradas en escala rgb```
##### Ejemplo:
```
>>> import matplotlib.pyplot as plt
>>> plt.imshow(cm.color(random_matrix),cmap="nipy_spectral", interpolation='nearest')
```

![texto alternativo](Imagenes/color.png)

Las funciones ```count_S, count_I, count_R``` y ```count_D``` nos permiten conocer el número exacto de individuos pertenecientes a alguno de los estados *S, I, R* o *D*, mientras que con las funciones ```count_s, count_i, count_r``` y ```count_d``` podemos conocer el promedio de individuos con un estado especifico con respecto a la cantidad de píxeles no vacíos.

#### count_S(A)
Cantidad de individuos susceptibles
###### Parámetros:	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones: 	
```
int   #Cantidad de individuos susceptibles en el sistema A
```
#### count_I(A)
Cantidad de individuos infectados
###### Parámetros:	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:	
```
int   #Cantidad de individuos infectados en el sistema A
```
#### count_R(A)
Cantidad de individuos recuperados
###### Parámetros:	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:	
```
int   #Cantidad de individuos recuperados en el sistema A
```
#### count_D(A)
Cantidad de individuos muertos
###### Parámetros:	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:	
```
int   #Cantidad de individuos recuperados en el sistema A
```
#### num_individuals(A)
Cantidad de espacios no vacíos
###### Parámetros:	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:
```
int   #Cantidad de espacios no vacíos en el sistema A
```
#### count_s(A)
Promedio de individuos susceptibles
###### Parámetros: 	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:	
```
float   #Promedio de individuos susceptibles en el sistema A con respecto a la cantidad de espacios no                                                   vacíos
```
#### count_i(A)
Promedio de individuos infectados
###### Parámetros:	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:	
```
float   #Promedio de individuos infectados en el sistema A con respecto a la cantidad de espacios no vacíos
```
#### count_r(A)
Promedio de individuos recuperados
###### Parámetros: 	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:
```
float   #Promedio de individuos recuperados en el sistema A con respecto a la cantidad de espacios no vacíos
```
#### count_d(A)
Promedio de individuos muertos
###### Parámetros:
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:
```
float   #Promedio de individuos muertos en el sistema A con respecto a la cantidad de espacios no vacíos
```
##### Ejemplo:
```
>>> print(cm.count_S(random_matrix), cm.count_I(random_matrix), cm.count_R(random_matrix), cm.count_D(random_matrix))
7 11 10 7
>>> print(cm.num_individuals(random_matrix))
35
>>> print(cm.count_s(random_matrix), cm.count_i(random_matrix), cm.count_r(random_matrix), cm.count_d(random_matrix))
0.2 0.3142857142857143 0.2857142857142857 0.2
```
### La regla base de evolución y el modelo *SIS*
Una vez dicho esto considere los siguientes eventos:

1.   Si $\beta>\alpha$, es decir, si el individuo tiene un estado de susceptibilidad la probabilidad de adquirir la infección es mas alta que la probabilidad de mantenerse sano, mientras que si el individuo se encuentra infectado la probabilidad de mantenerse en ese estado sera mayor que la probabilidad de pasar al estado susceptible; debemos tener también en cuenta que el indicador $N_{ij}^t(I)$ sera de vital importancia debido a que a mayor valor de $N_{ij}^t(I)$ mayor sera la probabilidad de infectarse independientemente de el parámetro  $\beta$, teniendo esto en cuenta la regla para este evento sera:

    $$\textit{"Si }x_{i,j}^{t}=0\textit{, }N_{ij}^t(I)>N_{ij}^t(S)\textit{ y }\rho>\frac{\beta}{\alpha}\cdot \frac{N_{ij}^t(I)}{8}\cdot100\textit{ entonces }x_{ij}^{t+1}=1\textit{"}$$
    
    donde $\rho$ es un valor aleatorio entre 0 y 100, de igual manera se define la siguiente regla:
    $$\textit{"Si }x_{i,j}^{t}=1\textit{ y }\rho<\frac{\beta}{\alpha}\cdot \frac{N_{ij}^t(I)}{8}\cdot100\textit{, entonces }x_{ij}^{t+1}=1\textit{"}$$
2.   Si $\beta<\alpha$, es decir, si el individuo tiene un estado de infección la probabilidad de adquirir pasar al estado sano es mas alta que la probabilidad de mantenerse infectado, mientras que si el individuo se encuentra sano la probabilidad de mantenerse en ese estado sera mayor que la probabilidad de pasar al estado infectado, teniendo esto en cuenta la regla para este evento sera:
    $$\textit{"Si }x_{ij}^{t}=1\textit{, }N_{ij}^t(I)<N_{ij}^t(S)\textit{ y }\rho\leq\frac{\beta}{\alpha}\cdot \frac{N_{ij}^t(I)}{8}\cdot100\textit{ entonces }x_{ij}^{t+1}=0\textit{"}$$
    de igual manera se define la siguiente regla:
    $$\textit{"Si }x_{ij}^{t}=0\textit{ y }\rho\geq\frac{\beta}{\alpha}\cdot \frac{N_{ij}^t(I)}{8}\cdot100\textit{, entonces }x_{ij}^{t+1}=0\textit{"}$$


Observe que los estados 1. y 2. se pueden representar mediante la siguiente asignación

$$\Phi_{ij}^t(\alpha,\beta)=\left\{\begin{array}{cc}
0 & \textrm{si }\rho\leq\frac{\beta}{\alpha}\cdot \frac{N_{ij}^t(I)}{8}\cdot100\\
1 & \textrm{en otro caso}
\end{array}\right.$$

Claramente la asignación $\Phi_{ij}^t$ corresponde a una regla totalística, se decidió hacer uso de estas reglas sobre autómatas celulares debido a la complejidad encontrada en la variedad de vecindades que puede tener un agente perteneciente a cualquiera de los dos estados.

De manera forma definimos la *regla base de interacción local* como

\begin{equation}
\Phi_{ij}^t(\alpha,\beta)=\left\{\begin{array}{cc}
0 & \textrm{si }r\leq\frac{\beta}{\alpha}\cdot \frac{N_{ij}^t(I)}{8}\cdot100\\
1 & \textrm{en otro caso}
\end{array}\right.
\end{equation}

donde $\alpha$ y $\beta$ representan la tasa de recuperación y la tasa de infección, respectivamente.

*Observación:* Como veremos más adelante, la cantidad de individuos que interactúan en la vecindad no necesariamente es 8, esto se deberá a que los individuos que posean el estado vació se mantendrán en ese estado para todo tiempo $t$, de esta forma el comportamiento del individuo central no se verá afectado por los espacios vacíos, por lo tanto una consideración importante en nuestra regla base de interacción local, será la cantidad de vecinos que interactúan con la célula central, de esta forma:

\begin{equation}
\Phi_{ij}^t(\alpha,\beta)=\left\{\begin{array}{cc}
0 & \textrm{si }r\leq\frac{\beta}{\alpha}\cdot \frac{N_{ij}^t(I)}{8-N_{ij}^t(V)}\cdot100\textrm{, si }N_{ij}^t(V)\neq8\\
1 & \textrm{en otro caso}
\end{array}\right.
\end{equation}
#### base_rule(alpha, beta, V)
Aplica la regla base de interacción local 
###### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
V:     np.array   #Vecindad 
```
###### Devoluciones:	
```
float   #Si es 1, el individuo en la célula central de se infectó o se mantuvo enfermo. Si es 0, el individuo en la célula central paso a un estado de susceptibilidad o se mantuvo susceptible
```
##### Ejemplo:
```
>>> cm.base_rule(0.2,0.5,V)
1.0
```
Una vez dicho esto, podemos definir un comportamiento tipo *SIS*, el cual puede entenderse como una regla de interacción entre dos estados (susceptible e infectado). Para poder generar este tipo de dinámica basta con aplicar la regla base de evolución a cada uno de los agentes del sistema.
#### evolution_sis(alpha, beta, U)
Aplica la regla base de interacción global
###### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
U:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones: 	
```
np.array    #Evolución del sistema al aplicar la regla base de interacción global
```
##### Ejemplo:
```
>>> random_matrix_2 =  np.array([[random.randint(0,1) for e in range(6)] for e in range(8)])
>>> cm.evolution_sis(0.2,0.5,random_matrix_2)
array([[1, 0, 1, 1, 1, 1],
       [1, 1, 1, 1, 1, 1],
       [1, 1, 1, 1, 1, 1],
       [1, 1, 1, 1, 1, 1],
       [1, 1, 1, 1, 1, 1],
       [0, 1, 1, 1, 1, 1],
       [0, 1, 1, 1, 0, 0],
       [1, 1, 1, 1, 1, 1]])
```
Si usamos la función color obtenemos:

![texto alternativo](Imagenes/color2.png)

Teniendo en cuenta la manera en la que se definió la regla de evolución, podemos analizar el comportamiento de alguna enfermedad en el sistema ```random_matrix_2``` para un número *tf* de iteraciones, este tipo de análisis los podemos realizar usando la función ```evolution_SIS```.

#### evolution_SIS(alpha, beta, tf, A)
Aplica la regla base de interacción global al sistema tf veces
###### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:	
```
list    #Lista cuyos elementos son la evolución del sistema A desde el tiempo 0 hasta el tiempo tf
```
Finalmente, para el caso del modelo *SIS* se implemento una función ```SIS_model``` que fuera capaz de reunir las cantidades de individuos por estado junto con sus valores normalizados y la visualización del cambio generado por la regla de evolución en el sistema. 
#### SIS_model(alpha, beta, tf, A)
Modelo SIS
###### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:	
```
list    #Contiene las coordenadas (x,n^x(S)) donde x es una iteración y n^x(S) es la cantidad de individuos susceptibles normalizada. las coordenadas (x,n^x(I)) donde x es una iteración y n^x(I) es la cantidad de individuos infectados normalizada
```
Intentemos ahora definir una condición inicial para el sistema, basada en el porcentaje de individuos infectados que queremos incluir, es decir, si quisiéramos generar una condición inicial de *10%* de infectados, esto es equivalente a decir que 1 de cada 10 individuos tiene la enfermedad. La función ```num_I``` nos permite definir la razón a:b de infectados y la función ```initial_condition``` nos permite aplicarla en la condición inicial del sistema.
#### num_I(a,b)
Porcentaje de infectados 
###### Parámetros:
```
a: int    #Cantidad de infectados por cada b habitantes
b: int    #Cantidad de habitantes
```
###### Devoluciones:	
```list   #Retorna la lista con una cantidad a de infectados con respecto a una población de tamaño b```
#### initial_condition(I0, A)
Define la condición inicial del sistema
###### Parámetros: 	
```
I0: float       #Porcentaje de individuos infectados en el sistema 
A:  np.array    #Arreglo sobre el modelo epidemiológico
```
###### Devoluciones:
```
np.array    #Condición inicial del sistema
```
##### Ejemplo:
```
>>> system_0 = np.zeros((5,8))
>>> system_0 = cm.initial_condition(0.1, system_0)
>>> system_0
array([[0., 0., 1., 0., 0., 0., 0., 0.],
       [0., 0., 0., 0., 0., 0., 0., 0.],
       [0., 0., 0., 0., 1., 0., 0., 0.],
       [0., 0., 0., 0., 1., 0., 0., 0.],
       [0., 0., 0., 0., 0., 1., 0., 0.]])
>>> plt.imshow(cm.color(system_0),cmap="nipy_spectral", interpolation='nearest')
```
![texto alternativo](Imagenes/system_0.png)


#### graph_sis_S(alpha, beta, tf, A) 
Grafica la cantidad de individuos susceptibles normalizada hasta un tiempo tf
###### Parámetros: 
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones: 
```
.plt    #Gráfica que describe la evolución del estado S en el sistema A hasta un tiempo tf
```
##### Ejemplo:
```
>>> cm.graph_sis_S(0.2,0.5,30,system_0)
```
![texto alternativo](Imagenes/sus_sis.png)

#### graph_sis_I(alpha, beta, tf, A) 
Grafica la cantidad de individuos infectados normalizada hasta un tiempo tf
###### Parámetros: 
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones: 
```
.plt    #Gráfica que describe la evolución del estado I en el sistema A hasta un tiempo tf
```
##### Ejemplo:
```
>>> cm.graph_sis_I(0.2,0.5,30,system_0)
```
![texto alternativo](Imagenes/inf_sis.png)

#### graph_sis(alpha, beta, tf, A)
Grafica la cantidad de individuos susceptibles e infectados normalizadas hasta un tiempo tf
###### Parámetros:
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:
```
.plt    #Gráfica que describe la evolución de los estados S e I en el sistema A hasta un tiempo tf
```
##### Ejemplo:
```
>>> cm.graph_sis(0.2,0.5,30,system_0)
```
![texto alternativo](Imagenes/sis_sis.png)

Podemos observar también el comportamiento del sistema mediante el siguiente código:
```
>>> ex_1 = cm.SIS_model(0.2,0.5,10,system_0)[4]
>>> for i in range(10):
......plt.imshow(cm.color(ex_1[i]),cmap="nipy_spectral", interpolation='nearest')
......plt.savefig('ex_1'+str(i)+'.jpg')

>>> import cv2
>>> img_ex_1 = []
>>> for i in range(10):
......img = cv2.imread('ex_1'+str(i)+'.jpg')
......height, width, layers = img.shape
......size = (width,height)
......img_ex_1.append(img)

>>> out = cv2.VideoWriter('ex_1.mp4',cv2.VideoWriter_fourcc(*'DIVX'), 15, size)
 
>>> for i in range(len(img_ex_1)):
......out.write(img_ex_1[i])
>>> out.release()
```

![texto alternativo](Imagenes/ex_1.gif)

### Las reglas de interacción *SI* , *IR* y el modelo *SIR*
#### Regla de interacción para el estado S
Basándonos en el principio de que los individuos susceptibles a la enfermedad no puedan recuperarse, es decir, un individuo que no haya tenido la enfermedad no podrá curarse de ella. Además, si suponemos también que los individuos que están infectados o recuperados en un tiempo �� no pueden adquirir la cualidad de susceptibilidad para un periodo de tiempo posterior, bien sea porque generaron inmunidad frente a la enfermedad (en el caso de los recuperados) o porque si tiene la enfermedad, no es un paciente con riesgo de adquirir la enfermedad debido a que ya la posee (caso infectado).

La manera en la que se implemento esta regla de interacción fue mediante la función ```interaction_SI``` la cual aplica la ***regla base de evolución*** únicamente a los individuos susceptibles.
#### interaction_SI(alpha, beta, A)
Aplica la regla de interacción del estado S 
###### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
A:     np.array   #Sistema 
```
###### Devoluciones:	
```
np.array    #Arreglo que cuenta con los individuos que se infectaron, individuos que se mantuvieron susceptibles e individuos que ya se encontraban recuperados
```
#### Regla de interacción para el estado I
Usualmente la tasa de recuperación �� se interpreta como la probabilidad de recuperación individual, para implementar este concepto en ```Casimulations``` se interpreto la tasa de recuperación individual como una tasa de recuperación global, es decir, ��% de las personas infectadas se recuperarán de la enfermedad.

Al igual que en el modelo *SIS*, se impĺementó una función ```num_R ``` la cual se encarga de describir la razón de individuos recuperados frente a individuos infectados.
#### num_R(a, b)
Porcentaje de recuperados
###### Parámetros: 	
```
a: int    #Cantidad de recuperados por cada b infectados
b: int    #Cantidad de infectados
```
###### Devoluciones:	
```list   #Retorna la lista con una cantidad a de recuperados con respecto a una población infectada de tamaño b```
#### interaction_IR(alpha, beta, A)
Aplica la regla de interacción del estado I 
###### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
A:     np.array   #Sistema 
```
###### Devoluciones:	
```np.array   #Arreglo que cuenta con los individuos que se recuperaron de la enfermedad, individuos que se mantuvieron enfermos e individuos susceptibles```

La regla de interacción para el modelo *SIR* se implemento por medio de la función ```evolution_sir```, con la cual se puede expresar la regla de evolución para el modelo *SIR*  ```evolution_SIR``` para un número tf de iteraciones.
#### evolution_sir(alpha, beta, U)
Aplica la regla que define el comportamiento del modelo sir
###### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
U:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:
```np.array   #Evolución del sistema al aplicar la regla de comportamiento sir```
#### evolution_SIR(alpha, beta, tf, A)
Aplica la regla base de comportamiento sir de manera global al sistema tf veces
###### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:	
```list   #Lista cuyos elementos son la evolución del sistema A desde el tiempo 0 hasta el tiempo tf```
#### SIR_model(alpha, beta, tf, A)
Modelo SIR
###### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:	
```list   #Contiene las coordenadas (x,n^x(S)), (x,n^x(I)) y (x,n^x(R)) donde las primeras componentes de cada coordenada es una iteración y la segunda componente es la cantidad de individuos perteneciente a los estados S, I o R, respectivamente.```

![texto alternativo](Imagenes/system_0_1.png)

#### graph_sir_S(alpha, beta, tf, A) 
Grafica la cantidad de individuos susceptibles normalizada hasta un tiempo tf
###### Parámetros:
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones: 
```.plt   #Gráfica que describe la evolución del estado S en el sistema A hasta un tiempo tf```
##### Ejemplo:
```
>>> cm.graph_sir_S(0.2,0.5,30,system_0)
```
![texto alternativo](Imagenes/sus_sir.png)

#### graph_sir_I(alpha, beta, tf, A) 
Grafica la cantidad de individuos infectados normalizada hasta un tiempo tf
###### Parámetros:
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:
```.plt   #Gráfica que describe la evolución del estado I en el sistema A hasta un tiempo tf```
##### Ejemplo:
```
>>> cm.graph_sir_I(0.2,0.5,30,system_0)
```
![texto alternativo](Imagenes/inf_sir.png)

#### graph_sir_R(alpha, beta, tf, A) 
Grafica la cantidad de individuos recuperados normalizada hasta un tiempo tf
###### Parámetros:
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:
```.plt   #Gráfica que describe la evolución del estado R en el sistema A hasta un tiempo tf```
##### Ejemplo:
```
>>> cm.graph_sir_R(0.2,0.5,30,system_0)
```
![texto alternativo](Imagenes/rec_sir.png)

#### graph_sir(alpha, beta, tf, A)
Graficá la cantidad de individuos susceptibles, infectados y recuperados normalizadas hasta un tiempo tf
###### Parámetros:
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:
```.plt   #Gráfica que describe la evolución de los estados S, I y R en el sistema A hasta un tiempo tf```
##### Ejemplo:
```
>>> cm.graph_sir(0.2,0.5,30,system_0)
```
![texto alternativo](Imagenes/sir_sir.png)

Podemos observar también el comportamiento del sistema mediante el siguiente código:
```
>>> ex_2 = cm.SIR_model(0.2,0.5,20,system_0)[6]
>>> for i in range(20):
......plt.imshow(cm.color(ex_2[i]),cmap="nipy_spectral", interpolation='nearest')
......plt.savefig('ex_2'+str(i)+'.jpg')

>>> import cv2
>>> img_ex_2 = []
>>> for i in range(10):
......img = cv2.imread('ex_2'+str(i)+'.jpg')
......height, width, layers = img.shape
......size = (width,height)
......img_ex_2.append(img)

>>> out = cv2.VideoWriter('ex_2.mp4',cv2.VideoWriter_fourcc(*'DIVX'), 15, size)
 
>>> for i in range(len(img_ex_2)):
......out.write(img_ex_2[i])
>>> out.release()
```
![texto alternativo](Imagenes/ex_2.gif)
```
A: list       #Lista de coordenadas -- bloque noroeste
B: listlista de coordenadas – bloque norte 
C: list	lista de coordenadas – bloque noreste
D: list	lista de coordenadas – bloque oeste
E: list 	lista de coordenadas – bloque central
F: list	lista de coordenadas – bloque este
G: list	lista de coordenadas – bloque suroeste
H: list	lista de coordenadas – bloque sur
I: list	lista de coordenadas – bloque sureste
J: list	lista de coordenadas – distribución aleatoria	
```
### La dispersión como un factor clave en la velocidad de propagación

Vale la pena preguntarnos si es posible que la ubicación inicial de los individuos infectados afecta el comportamiento de la enfermedad en un periodo de tiempo determinado. Las funciones ```northwest, north, northeast, west, center, east, southwest, south``` y ```southeast``` nos permiten ubicar a casi la totalidad de la población infectada en una de nueve divisiones realizadas sobre el sistema basandonos en los puntos cardinales, también contamos con la función ```aleatorio``` la cual distribuye aleatoriamente a los individuos infectados, cabe resaltar que estas funciones son únicamente para definir la condición inicial del sistema de una manera mas especifica que la función ```initial_condition```.
#### northwest(n, m, I0)
Localiza la población infectada en la zona noroeste del rectángulo
###### Parámetros:
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
###### Devoluciones:
```np.array   #Condición inicial con toda la población infectada en la zona noroeste del sistema rectangular de dimensión n*m ```
#### north(n, m, I0)
Localiza la población infectada en la zona norte del rectángulo 
###### Parámetros:	
```
n:  int          #Cantidad de filas 
m:  int	         #Cantidad de columnas
I0: float	       #Porcentaje inicial de individuos infectados
```
###### Devoluciones:
```np.array   #Condición inicial con toda la población infectada en la zona norte del sistema rectangular de dimensión n*m```
#### northeast(n, m, I0)
Localiza la población infectada en la zona noreste del rectángulo
###### Parámetros:	
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
###### Devoluciones:
```np.array   #Condición inicial con toda la población infectada en la zona noreste del sistema rectangular de dimensión n*m```
#### west(n, m, I0)
Localiza la población infectada en la zona oeste del rectángulo
###### Parámetros:
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
###### Devoluciones:
```np.array   #Condición inicial con toda la población infectada en la zona oeste del sistema rectangular de dimensión n*m```
#### center(n, m, I0)
Localiza la población infectada en la zona central del rectángulo
###### Parámetros:
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
###### Devoluciones:
```np.array   #Condición inicial con toda la población infectada en la zona central del sistema rectangular de dimensión n*m```
#### east(n, m, I0)
Localiza la población infectada en la zona este del rectángulo
###### Parámetros:
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
###### Devoluciones:
```np.array   #Condición inicial con toda la población infectada en la zona este del sistema rectangular de dimensión n*m```
#### southwest(n, m, I0)
Localiza la población infectada en la zona suroeste del rectángulo
###### Parámetros:	
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
###### Devoluciones:
```np.array   #Condición inicial con toda la población infectada en la zona suroeste del sistema rectangular de dimensión n*m```
#### south(n, m, I0)
Localiza la población infectada en la zona sur del rectángulo
###### Parámetros:
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
###### Devoluciones:
```np.array   #Condición inicial con toda la población infectada en la zona sur del sistema rectangular de dimensión n*m```
#### southeast(n, m, I0)
Localiza la población infectada en la zona sureste del rectángulo
###### Parámetros:	
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
###### Devoluciones: 
```np.array   #Condición inicial con toda la población infectada en la zona sureste del sistema rectangular de dimensión n*m```
#### aleatorio(n, m, I0)
Localiza la población infectada de manera uniforme en el rectángulo
###### Parámetros:
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
###### Devoluciones:
```np.array   #Condición inicial con toda la población infectada ubicada de manera uniforme en el sistema rectangular de dimensión n*m```
```CAsimulation``` incluye también maneras de visualizar las zonas de riesgo en un sistema, es posible generar mapas de calor específicos por medio de las funciones ```heatmap_sis, heatmap_sir_I``` y ```heatmap_sir_R```, mientras que los mapas generados por ```heatmap_sis``` y ```heatmap_sir_I``` muestran el comportamiento de la población infectada para los modelos *SIS* y *SIR* respectivamente, la función ```heatmap_sir_R``` nos muestra como evolucionó la población recuperada, es decir, que individuos se recuperaron primero de la enfermedad.
#### heatmap_sis(alpha, beta, tf, A)
Grafica el comportamiento espacial de la enfermedad hasta un tiempo tf
###### Parámetros: 	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:
```.plt   #Gráfica del mapa de calor que describe como evoluciono la enfermedad en el sistema A hasta un tiempo tf```
#### heatmap_sir_I(alpha, beta, tf, A)
Grafica el comportamiento espacial de la población infectada hasta un tiempo tf para el modelo SIR
###### Parámetros:
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:
```.plt   #Gráfica del mapa de calor que describe como evoluciono la población infectada en el sistema A hasta un tiempo tf para el modelo SIR```
#### heatmap_sir_R(alpha, beta, tf, A)
Grafica el comportamiento espacial de la población recuperada hasta un tiempo tf para el modelo SIR
###### Parámetros:
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
###### Devoluciones:
```.plt   #Gráfica del mapa de calor que describe como evoluciono la población recuperada en el sistema A hasta un tiempo tf para el modelo SIR```
##### Ejemplo:
```
>>> system_1 = cm.northwest(30, 30, 0.1)
>>> plt.imshow(cm.color(system_1), cmap="nipy_spectral", interpolation='nearest')
```
![texto alternativo](Imagenes/system_1.png)
```
>>> cm.heatmap_sis(0.2, 0.5, 30, system_1)
```
![texto alternativo](Imagenes/hm_sis.png)
```
>>> cm.heatmap_sir_I(0.2, 0.5, 30, system_1)
```
![texto alternativo](Imagenes/hm_sir_I.png)
```
>>> cm.heatmap_sir_R(0.2, 0.5, 30, system_1)
```
![texto alternativo](Imagenes/hm_sir_R.png)
```
>>> ex_3 = cm.SIS_model(0.2, 0.5, 30, system_1)[4]
>>> for i in range(30):
......plt.imshow(cm.color(ex_3[i]),cmap="nipy_spectral", interpolation='nearest')
......plt.savefig('ex_3'+str(i)+'.jpg')

>>> img_ex_3 = []
>>> for i in range(30):
......img = cv2.imread('ex_3'+str(i)+'.jpg')
......height, width, layers = img.shape
......size = (width,height)
......img_ex_3.append(img)

>>> out = cv2.VideoWriter('ex_3.mp4',cv2.VideoWriter_fourcc(*'DIVX'), 15, size)
 
>>> for i in range(len(img_ex_3)):
......out.write(img_ex_3[i])
>>> out.release()
```
![texto alternativo](Imagenes/ex_3.gif)
```
>>> ex_4 = cm.SIR_model(0.2, 0.5, 45, system_1)[6]
>>> for i in range(45):
......plt.imshow(cm.color(ex_4[i]),cmap="nipy_spectral", interpolation='nearest')
......plt.savefig('ex_4'+str(i)+'.jpg')

>>> img_ex_4 = []
>>> for i in range(45):
......img = cv2.imread('ex_4'+str(i)+'.jpg')
......height, width, layers = img.shape
......size = (width,height)
......img_ex_4.append(img)

>>> out = cv2.VideoWriter('ex_4.mp4',cv2.VideoWriter_fourcc(*'DIVX'), 15, size)
 
>>> for i in range(len(img_ex_4)):
......out.write(img_ex_4[i])
>>> out.release()
```
![texto alternativo](Imagenes/ex_4.gif)

Si lo que queremos es analizar el comportamiento para las diferentes condiciones iniciales basadas en los puntos cardinales, podemos utilizar la función ```distribution_graph``` la cual nos permitirá graficar 10 posibles condiciones iniciales.
#### distribution_graph(A, B, C, D, E, F, G, H, I, J)
Grafica la variación presente en los cambios de distribución inicial de población infectada
###### Parámetros: 	
```
A: list   #Lista de coordenadas - bloque noroeste
B: list   #Lista de coordenadas - bloque norte 
C: list   #Lista de coordenadas - bloque noreste
D: list   #Lista de coordenadas – bloque oeste
E: list   #Lista de coordenadas – bloque central
F: list   #Lista de coordenadas – bloque este
G: list   #Lista de coordenadas – bloque suroeste
H: list   #Lista de coordenadas – bloque sur
I: list   #Lista de coordenadas – bloque sureste
J: list   #Lista de coordenadas – distribución aleatoria	 
```
###### Devoluciones:	
```
.plt    #Gráfica de las variaciones bajo cambios en la distribución de población infectada
```
#####  Ejemplo:
```
>>> con_1=cm.SIS_model(0.2, 0.5, 30, cm.northwest(30, 30, 0.1))
>>> con_2=cm.SIS_model(0.2, 0.5, 30, cm.north(30, 30, 0.1))
>>> con_3=cm.SIS_model(0.2, 0.5, 30, cm.northeast(30, 30, 0.1))
>>> con_4=cm.SIS_model(0.2, 0.5, 30, cm.west(30, 30, 0.1))
>>> con_5=cm.SIS_model(0.2, 0.5, 30, cm.center(30, 30, 0.1))
>>> con_6=cm.SIS_model(0.2, 0.5, 30, cm.east(30, 30, 0.1))
>>> con_7=cm.SIS_model(0.2, 0.5, 30, cm.southwest(30, 30, 0.1))
>>> con_8=cm.SIS_model(0.2, 0.5, 30, cm.south(30, 30, 0.1))
>>> con_9=cm.SIS_model(0.2, 0.5, 30, cm.southeast(30, 30, 0.1))
>>> con_10=cm.SIS_model(0.2, 0.5, 30, cm.aleatorio(30, 30, 0.1))
>>> cm.distribution_graph(con_1[0], con_2[0], con_3[0], con_4[0], con_5[0], con_6[0], con_7[0], con_8[0], con_9[0], con_10[0])
```
![texto alternativo](Imagenes/dist.png)
También es posible realizar un gran número de simulaciones, esto con el fin de analizar diferentes condiciones iniciales. Las funciones ```medium_surves_sis``` y ```medium_surves_sir``` son capaces de generar las coordenadas promedio para un número *csim* de simulaciones mientras que las funciones ```graph_medium_curves_sis``` y ```graph_medium_curves_sir``` nos permiten visualizar estos comportamientos "promedio".
#### medium_curves_sis(alpha, beta, tf, csim, I0, A)
Genera las listas de coordenadas promedio al aplicar el modelo sis en una cantidad csim de simulaciones para una condición inicial del I0% de infectados en el espacio
###### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de tics
Csim:  int        #Cantidad de simulaciones
I0:    float      #Porcentaje inicial de infectados
A:     np.array   #Sistema sobre el cual se aplica el modelo
```
###### Devoluciones:
```list   #Lista de coordenadas promedio para el estado S, para el estado I y valores en el tiempo de los estados S e I ubicados en listas respectivamente```
#### medium_curves_sir(alpha, beta, tf, csim, I0, A)
Genera las listas de coordenadas promedio al aplicar el modelo SIR en una cantidad csim de simulaciones para una condición inicial del I0% de infectados en el espacio
###### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de tics
Csim:  int        #Cantidad de simulaciones
I0:    float      #Porcentaje inicial de infectados
A:     np.array   #Sistema sobre el cual se aplica el modelo
```
###### Devoluciones:
```list   #Lista de coordenadas promedio para los estados S, I y R y valores en el tiempo de los estados S, I y R ubicados en listas respectivamente```
#### graph_medium_curves_sis(alpha, beta, tf, csim, I0, A)
Graficá los valores promedio al aplicar csim veces el modelo sis para un valor inicial fijo de individuos infectados
###### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de tics
Csim:  int        #Cantidad de simulaciones
I0:    float      #Porcentaje inicial de infectados
A:     np.array   #Sistema sobre el cual se aplica el modelo
```
###### Devoluciones:
```.plt   #Gráfica con los valores promedio para cada estado del modelo SIS```
#### graph_medium_curves_sir(alpha, beta, tf, csim, I0, A)
Gráfica los valores promedio al aplicar csim veces el modelo SIR para un valor inicial fijo de individuos infectados
###### Parámetros:
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de tics
Csim:  int        #Cantidad de simulaciones
I0:    float      #Porcentaje inicial de infectados
A:     np.array   #Sistema sobre el cual se aplica el modelo
```
###### Devoluciones:
```.plt   #Gráfica con los valores promedio para cada estado del modelo SIR```
##### ejemplos:
```
>>> system_2 = np.zeros((20, 20))
>>> cm.graph_medium_curves_sir(0.2, 0.5, 30, 50, 0.1, system_2)
```
![texto alternativo](Imagenes/gmc_sir.png)
```
>>> cm.graph_medium_curves_sis(0.2,0.5,30,100,0,cm.southeast(15,15,0.1))
```
![texto alternativo](Imagenes/gmc_sis.png)
### Análisis cambiando la condición de frontera del sistema
Implementaremos ahora una manera de definir cualquier tipo de sistema, lo primero que debemos hacer es definir el espacio sobre el cual queremos definir nuestro sistema, es decir, si por ejemplo quisiéramos definir una región triangular, lo primero que debemos hacer es definir una región rectangular que lo contenga, posteriormente se debe generar una lista con las coordenadas del sistema. La función ```boundary``` se encarga de convertir cada píxel con coordenadas en la lista que define el sistema en un agente que inicialmente tiene un estado *S*, si buscamos una manera de facilitar el trabajo de definir dicha lista, la función ```domain_definition``` nos permitirá definir bloques o submatrices para abarcar mas espacio en el espacio inicial.
#### boundary(L,M)
Genera sub-matrices nulas en la matriz M
###### Parámetros:
```
L: list       #Lista de coordenadas que se anularan para definir donde se aplican los modelos epidemiológicos
M: np.array   #Arreglo sobre el cual se definen las condiciones iniciales de entorno de ejecución de los modelos epidemiológicos
```
###### Devoluciones: 
```np.array   #Sistema en el cual se aplican los modelos bajo condiciones no regulares de frontera```
#### domain_definition(n, m, a, b, M)
Define y genera las sub-matrices nulas donde se aplicarán los análisis epidemiológicos
###### Parámetros:	
```
n: int        #Cantidad de filas de la sub-matriz
m: int        #Cantidad de columnas de la sub-matriz
a: int        #Fila en la cual se va a ubicar la sub-matriz
b: int        #Columna en la cual se va a ubicar a sub-matriz
M: np.array   #Arreglo sobre el cual se va a generar la sub-matriz nula
```
###### Devoluciones: 
```np.array   #Sistema en el cual se aplican los modelos bajo condiciones no regulares de frontera```
##### Ejemplo:
```
>>> empty_space = -np.ones((15, 20))
>>> system_2 = cm.boundary([[2, 5], [3, 7], [8, 2], [14, 15]], empty_space)
>>> system_2 = cm.domain_definition(3, 3, 6, 12, system_2)
>>> system_2 = cm.domain_definition(4, 2, 8, 7, system_2)
>>> plt.imshow(cm.color(system_2),cmap="nipy_spectral", interpolation='nearest')
```
![texto alternativo](Imagenes/system_2.png)
A partir de esto es posible implementar funciones mas complejas para la definición de algún sistema particular, este es el caso de las funciones ```rombo``` y la función ```triangulo```
#### rombo(a, b, c, d, M)
Define un sistema tipo rombo, con vértice izquierdo ubicado en (a, b) y con dimensión de la primera submatriz cxd en el espacio M
###### Parámetros:
```
a: int        #Columna donde se ubica el vértice izquierdo del rombo
b: int        #Ancho del rombo -1 
c: int        #Fila donde se ubica el vértice izquierdo del rombo 
d: int        #Columna donde se ubica la primera submatriz 
M: np.array   #Espacio donde se definirá el sistema
```
###### Devoluciones:  
```np.array#Arreglo de coordenadas con un sistema tipo rombo```
##### Ejemplo:
```
>>> empty = -np.ones((9,14))
>>> Rombo = cm.rombo(1,14,4,0,empty)
>>> plt.imshow(cm.color(Rombo),cmap="nipy_spectral", interpolation='nearest')
```

![texto alternativo](Imagenes/rombo.png)
#### triangulo(n, m, a, b, M)
Define un sistema triangular, con vértice izquierdo ubicado en (n, m) y con dimensión de la primera submatriz axb en el espacio M
###### Parámetros: 
```
n: int        #Columna donde se ubica el vértice izquierdo del triangulo
m: int        #Ancho del triangulo
a: int        #Fila donde se ubica el vértice izquierdo del triángulo
b: int        #Columna donde se ubica la primera submatriz
M: np.array   #Espacio donde se definirá el sistema
```
###### Devoluciones:   
```np.array	arreglo de coordenadas con un sistema triangular```
##### Ejemplo:
```
>>> empty = -np.ones((10,19))
>>> Triangle = cm.triangulo(1,19,9,0,empty)
>>> plt.imshow(cm.color(Triangle),cmap="nipy_spectral", interpolation='nearest')
```

![texto alternativo](Imagenes/triangulo.png)
Entre las funciones de visualización de ```CAsimulation``` también encontramos a ```systems_graph```, la cual nos permite comparar 7 sistemas distintos, esto con el fin de analizar la evolución de la enfermedad para diferentes tipos de sistemas.
#### systems_graph(A, B, C, D, E, F, G)
Grafica los cambios presentes en la condición de frontera
###### Parámetros: 	
```
A: list   #Lista de coordenadas – primera región
B: list   #Lista de coordenadas – segunda región
C: list   #Lista de coordenadas – tercera región
D: list   #Lista de coordenadas – cuarta región
E: list   #Lista de coordenadas – quinta región
F: list   #Lista de coordenadas – sexta región
G: list   #Lista de coordenadas – séptima región
```
###### Devoluciones:	
```
.plt    #Gráfica de los cambios en el modelo tomando condiciones de frontera diferentes
```
##### Ejemplo:
```
>>> lineal = cm.SIS_model(0.2,0.5,30,cm.initial_condition(0.1,np.zeros((1,20))))
>>> square = cm.SIS_model(0.2,0.5,30,cm.initial_condition(0.1,np.zeros((10,10))))
>>> rectangle = cm.SIS_model(0.2,0.5,30,cm.initial_condition(0.1,np.zeros((10,20))))
>>> rombo = cm.SIS_model(0.2,0.5,30,cm.initial_condition(0.1,Rombo))
>>> triangle = cm.SIS_model(0.2,0.5,30,cm.initial_condition(0.1,Triangle))
>>> square_2 = cm.SIS_model(0.2,0.5,30,cm.initial_condition(0.1,np.zeros((5,5))))
>>> square_3 = cm.SIS_model(0.2,0.5,30,cm.initial_condition(0.1,np.zeros((3,3))))
>>> cm.systems_graph(lineal[1],square[1],rectangle[1],rombo[1],triangle[1],square_2[1],square_3[1])
```

![texto alternativo](Imagenes/sys_gr.png)
Ya sabemos como generar sistemas de cualquier tipo y de cualquier tamaño, es tiempo de ver las posibilidades de los modelos epidemiológicos frente a cambios de escala, si definimos por medio de ```domain_definition``` diferentes escalas para un mismo tipo de sistema, la función ```scale_differences``` nos permitirá ver calcular la variación entre dos escalas, por medio de ```scales_graph``` podremos visualizar los cambios presentes en 5 escalas diferentes, mientras que ```scales_differences_graph``` nos permitirá visualizar las diferencias entre cuatro escalas distintas.
#### scale_differences(L1, L2)
Calcula las diferencias por cada iteración entre dos escalas diferentes
###### Parámetros: 
```
L1: list      #Lista con los valores numéricos obtenidos en una primera escala
L2: list      #Lista con los valores numéricos obtenidos en la segunda escala
```
###### Devoluciones: 
```list	#Lista con las diferencias entre ambas escalas por cada iteración.```
#### scales_graph(A, B, C, D, E)
Grafica los cambios presentes en la variación de escalas
###### Parámetros: 	
```
A: list   #Lista de coordenadas – primera escala
B: list   #Lista de coordenadas – segunda escala
C: list   #Lista de coordenadas – tercera escala
D: list   #Lista de coordenadas – cuarta escala
E: list   #Lista de coordenadas – quinta escala
```
###### Devoluciones:	
```
.plt    #Gráfica de los cambios en el modelo tomando escalas diferentes
```
##### Ejemplo:
```
>>> lineal_1 = np.zeros((1,100))
>>> lineal_2 = np.zeros((1,200))
>>> lineal_3 = np.zeros((1,300))
>>> lineal_4 = np.zeros((1,400))
>>> lineal_5 = np.zeros((1,500))
>>> sis_l1 = cm.SIS_model(0.2,0.5,30,cm.initial_condition(0.1,lineal_1))
>>> sis_l2 = cm.SIS_model(0.2,0.5,30,cm.initial_condition(0.1,lineal_2))
>>> sis_l3 = cm.SIS_model(0.2,0.5,30,cm.initial_condition(0.1,lineal_3))
>>> sis_l4 = cm.SIS_model(0.2,0.5,30,cm.initial_condition(0.1,lineal_4))
>>> sis_l5 = cm.SIS_model(0.2,0.5,30,cm.initial_condition(0.1,lineal_5))
>>> cm.scales_graph(sis_l1[1],sis_l2[1],sis_l3[1],sis_l4[1],sis_l5[1])
```

![texto alternativo](Imagenes/esc_gr.png)
#### scales_differences_graph(A, B, C, D)
Grafica los cambios presentes en la variación de escalas
###### Parámetros: 	
```
A: list   #Lista de coordenadas – primera escala vs última escala
B: list   #Lista de coordenadas – segunda escala vs última escala
C: list   #Lista de coordenadas – tercera escala vs última escala
D: list   #Lista de coordenadas – cuarta escala vs última escala
```
###### Devoluciones:	
```
.plt    #Gráfica de los cambios en el modelo tomando escalas diferentes
```
##### Ejemplo:
```
>>> l1_vs_l5 = cm.scale_differences(sis_l1[2],sis_l5[2])
>>> l2_vs_l5 = cm.scale_differences(sis_l2[2],sis_l5[2])
>>> l3_vs_l5 = cm.scale_differences(sis_l3[2],sis_l5[2])
>>> l4_vs_l5 = cm.scale_differences(sis_l4[2],sis_l5[2])
>>> cm.scales_difference_graph(l1_vs_l5,l2_vs_l5,l3_vs_l5,l4_vs_l5)
```

![texto alternativo](Imagenes/dif_gr.png)
### Modelos SIS y SIR con natalidad y mortalidad
Para el caso del análisis de propagación con natalidad y mortalidad ```CAsimulation``` nos ofrece la posibilidad de distribuir edades sobre los agentes de acuerdo con el porcentaje que necesitamos, usando la función ```ages```  podemos asignarle edades a todos los agentes del sistema de acuerdo con un porcentaje que se necesite, por ejemplo: si quisiéramos que el 15% de la población tuviera entre 14 y 25 años lo único que debemos hacer es incluir en la lista rangos ```[14,25,0.15]``` y posteriormente usar ```ages```sobre el sistema.
#### ages(rangos, A)
Genera la matriz de edades para A basada en los datos de rangos
###### Parámetros:
```
rangos: list         #Lista de rangos de edad: Las primeras dos componentes de cada elemento deben ser los valores extremos del rango y la tercera componente, lo proporción de individuos con esa edad en el espacio
A:      np.array     #Sistema sobre el cual se definirán las edades
```
###### Devoluciones:
```np.array   #Matriz de edades```
También podemos seleccionar un grupo de edad sobre el sistema, la función ```age_group``` nos permite conocer las coordenadas de los individuos que tengan una edad en un rango deseado, contamos además con la función ```evolution_ages``` la cual representará el paso del tiempo, los parámetros *time_unit* y *year* nos servirán para saber si el los agentes en el sistema "cumplieron años", esto ocurrirá si *time_unit* es un múltiplo de *year*.
#### age_group(a, b, A)
Genera las posiciones de los individuos que tienen entre a y b años en A
###### Parámetros:
```
a: int               #Valor inicial del grupo de edad
b: int               #Valor final del grupo de edad
A: np.array          #Matriz de edades
```
###### Devoluciones:
```list   #Lista con las coordenadas de los individuos en el grupo de edad```
#### evolution_ages(br,mr,E,time_unit,year):
Evolución por año de los agentes
###### Parámetros:
```
br: float            #Tasa de natalidad
mr: list             #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
E:  np.array         #Matriz de edades
time_unit: int       #Unidad de tiempo a analizar (minutos, días, meses, años)
year: int            #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```np.array   #Matriz con la evolución de edades```
Una vez controlado el factor de edad de los agentes, podemos implementar las reglas de interacción para los modelos SIS y SIR con natalidad y mortalidad, usando las funciones ```evolution_sis_bm``` y ```evolution_sir_bm``` podemos conocer el comportamiento de alguna enfermedad para un día o mes según se tome *time_unit* con respecto a la unidad de *year*. Por otro lado, las funciones ```evolution_SIS_bm``` y ```evolution_SIR_bm``` nos permitirán aplicar el modelo una cantidad *tf* de veces. Finalmente, las funciones ```SIS_bm_model``` y ```SIR_bm_model``` generarán los datos de la enfermedad, luego de aplicarla sobre un sistema especifico para *tf* iteraciones, mientras que ```graph_sis_bm``` y ```graph_sir_bm``` nos permitirán visualizar el comportamiento de la enfermedad.
#### evolution_sis_bm(alpha,beta,br,mr,A,E,time_unit,year)
Regla de evolución del modelo SIS con natalidad y mortalidad
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta: float          #Tasa de infección
br: float            #Tasa de natalidad
mr: list             #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema a evaluar
E: np.array          #Matriz de edades del sistema A
time_unit: int       #Unidad de tiempo a analizar (minutos, días, meses, años)
year: int            #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #En la primera componente encontraremos la evolución del sistema con natalidad y mortalidad mientras que en la segunda las edades con las que cuentan los agentes al realizar la evolución SIS```
#### evolution_sir_bm(alpha,beta,br,mr,A,E,time_unit,year)
Regla de evolución del modelo SIR con natalidad y mortalidad
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta: float          #Tasa de infección
br:   float          #Tasa de natalidad
mr:   list           #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema a evaluar
E: np.array          #Matriz de edades del sistema A
time_unit: int       #Unidad de tiempo a analizar (minutos, días, meses, años)
year: int            #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #En la primera componente encontraremos la evolución del sistema con natalidad y mortalidad mientras que en la segunda las edades con las que cuentan los agentes al realizar la evolución SIR```
#### evolution_SIS_bm(alpha,beta,tf,br,mr,A,E,year)
Aplica el modelo SIS con natalidad y mortalidad tf veces sobre el sistema A
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta: float          #Tasa de infección
tf: int              #Cantidad de iteraciones basado en la unidad de tiempo
br: float            #Tasa de natalidad
mr: list             #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema a evaluar
E: np.array          #Matriz de edades del sistema A
year: int            #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista con las evoluciones del sistema bajo un modelo SIS con natalidad y mortalidad, cada elemento de la lista contiene el sistema junto con su matriz de edades```
#### evolution_SIR_bm(alpha,beta,tf,br,mr,A,E,year)
Aplica el modelo SIR con natalidad y mortalidad tf veces sobre el sistema A
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta: float          #Tasa de infección
tf: int              #Cantidad de iteraciones basado en la unidad de tiempo
br: float            #Tasa de natalidad
mr: list             #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema a evaluar
E: np.array          #Matriz de edades del sistema A
year: int            #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista con las evoluciones del sistema bajo un modelo SIR con natalidad y mortalidad, cada elemento de la lista contiene el sistema junto con su matriz de edades```
#### SIS_bm_model(alpha,beta,tf,br,mr,A,E,year)
Modelo SIS con natalidad y mortalidad
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta: float          #Tasa de infección
tf: int              #Cantidad de iteraciones basado en la unidad de tiempo
br: float            #Tasa de natalidad
mr: list             #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema a evaluar
E: np.array          #Matriz de edades del sistema A
year: int            #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista que contiene las cantidad de individuos pertenecientes a los estados S, I  y D junto con su iteración, cantidad de individuos para cada estado, lista con las evoluciones del sistema y de sus edades```
#### SIR_bm_model(alpha,beta,tf,br,mr,A,E,year)
Modelo SIR con natalidad y mortalidad
###### Parámetros:
```
alpha: float	       #Tasa de recuperación	
beta: float          #Tasa de infección
tf: int              #Cantidad de iteraciones basado en la unidad de tiempo
br: float            #Tasa de natalidad
mr: list             #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema a evaluar
E: np.array          #Matriz de edades del sistema A
year: int            #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista que contiene las cantidad de individuos pertenecientes a los estados S, R,  I  y D junto con su iteración, cantidad de individuos para cada estado, lista con las evoluciones del sistema y de sus edades```
##### Ejemplo:
```
>>> ranges = [[1, 15, 0.2], [16, 40, 0.6], [41, 100, 0.2]]
>>> mr = [[1, 25, 0.25], [26, 51, 0.44], [52, 100, 0.8]]
>>> sys = np.zeros((10,10))
>>> ages_sys = cm.ages(ranges, sys)
>>> ex_5 = cm.SIS_bm_model(0.2, 0.5, 30, 2, mr, sys, ages_sys, 365)[9]
>>> for i in range(30):
......plt.imshow(cm.color(ex_5[i]),cmap="nipy_spectral", interpolation='nearest')
......plt.savefig('ex_5'+str(i)+'.jpg')
>>> img_ex_5 = []
>>> for i in range(30):
......img = cv2.imread('ex_5'+str(i)+'.jpg')
......height, width, layers = img.shape
......size = (width,height)
......img_ex_5.append(img)

>>> out = cv2.VideoWriter('ex_5.mp4',cv2.VideoWriter_fourcc(*'DIVX'), 15, size)
 
>>> for i in range(len(img_ex_5)):
......out.write(img_ex_5[i])
>>> out.release()
```

![texto alternativo](Imagenes/ex_5.gif)
#### graph_sis_bm(alpha,beta,tf,br,mr,A,E,year)
Gráfica del modelo SIS con natalidad y mortalidad
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta: float          #Tasa de infección
tf: int              #Cantidad de iteraciones basado en la unidad de tiempo
br: float            #Tasa de natalidad
mr: list             #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema a evaluar
E: np.array          #Matriz de edades del sistema A
year: int            #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones: 
```.plt   #Gráfica del modelo SIS con natalidad y mortalidad```
#### graph_sir_bm(alpha,beta,tf,br,mr,A,E,year)
Gráfica del modelo SIR con natalidad y mortalidad
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta: float          #Tasa de infección
tf: int              #Cantidad de iteraciones basado en la unidad de tiempo
br: float            #Tasa de natalidad
mr: list             #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema a evaluar
E: np.array          #Matriz de edades del sistema A
year: int            #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones: 
```.plt   #Gráfica del modelo SIR con natalidad y mortalidad```
##### Ejemplo:
```
>>> cm.graph_sis_bm(0.2, 0.5, 30, 2, mr, sys, ages_sys, 365)
```
![texto alternativo](Imagenes/gr_sir_bm.png)
### Modelos SIS y SIR con muerte por enfermedad
```CAsimulation``` nos permite también analizar enfermedades que puedan causar la muerte en los individuos que la posean de una manera muy especifica, si se tratase de una enfermedad que afecte mas a un grupo especifico de edad, podremos definir los rangos sobre los cuales la enfermedad afecta gravemente, usando ```dead_by_disease``` podremos aplicar las tasas de mortalidad por enfermedad a estos grupos especificos y mediante las funciones ```evolutioin_sis_dd``` y ```evolution_sir_dd``` podremos aplicar esta característica a cada iteración de la misma manera que se aplicó en los modelos con natalidad y mortalidad. Adicionalmente, las funciones ```evolution_SIS_dd``` y ```evolution_SIR_dd``` nos permiten analizar el comportamiento hasta un tiempo o iteración especifica, con lo cual llegamos finalmente a los modelos con muerte por enfermedad: ```SIS_dd_model``` y ```SIR_dd_model```, la manera en que podremos visualizar de manera concreta el estos comportamientos será usando las funciones ```graph_sis_dd``` y ```graph_sir_dd```.
#### dead_by_disease(ranges_dead,A,E)
Aplica probabilidades de muerte por enfermedad a grupos de edad sobre el sistema A 
###### Parámetros:
```
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema sobre el cual se esta trabajando
E: np.array          #Matriz de edades del sistema A
```
###### Devoluciones:
```list   #Lista que contiene la evolución del sistema al aplicar la muerte por enfermedad y la matriz de edades luego de aplicar la regla de muerte por enfermedad```

#### evolution_sis_dd(alpha,beta,br,mr,ranges_dead,A,E,time_unit,year)
Regla de evolución para el modelo SIS con muerte por enfermedad
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta:  float         #Tasa de infección
br:    float         #Tasa de natalidad
mr:    list          #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A:     np.array      #Sistema a evaluar
E:     np.array      #Matriz de edades del sistema A
time_unit:   int     #Unidad de tiempo a analizar (minutos, días, meses, años)
year:  int           #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista con el sistema al aplicar el modelo SIS con muerte por enfermedad y con la matriz de edades del sistema```

#### evolution_sir_dd(alpha,beta,br,mr,ranges_dead,A,E,time_unit,year)
Regla de evolución para el modelo SIR con muerte por enfermedad
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta:  float         #Tasa de infección
br:    float         #Tasa de natalidad
mr:    list          #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A:     np.array      #Sistema a evaluar
E:     np.array      #Matriz de edades del sistema A
time_unit:   int     #Unidad de tiempo a analizar (minutos, días, meses, años)
year:  int           #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista con el sistema al aplicar el modelo SIR con muerte por enfermedad y con la matriz de edades del sistema```

#### evolution_SIS_dd(alpha,beta,tf,br,mr,ranges_dead,A,E,year):   
Aplica el modelo SIS con muerte por enfermedad tf veces sobre el sistema A
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta:  float         #Tasa de infección
tf:    int           #Cantidad de iteraciones basado en la unidad de tiempo
br:    float         #Tasa de natalidad
mr:    list          #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A:     np.array      #Sistema a evaluar
E:     np.array      #Matriz de edades del sistema A
year:  int           #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista con las evoluciones del sistema luego de aplicar el modelo SIS con muerte por enfermedad y las matrices de edad por cada iteración.```

#### evolution_SIR_dd(alpha,beta,tf,br,mr,ranges_dead,A,E,year)
Aplica el modelo SIR con muerte por enfermedad tf veces sobre el sistema A
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta:  float         #Tasa de infección
tf:    int           #Cantidad de iteraciones basado en la unidad de tiempo
br:    float         #Tasa de natalidad
mr:    list          #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A:     np.array      #Sistema a evaluar
E:     np.array      #Matriz de edades del sistema A
year:  int           #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista con las evoluciones del sistema luego de aplicar el modelo SIR con muerte por enfermedad y las matrices de edad por cada iteración.```

#### SIS_dd_model(alpha,beta,tf,br,mr,ranges_dead,A,E,year)
Modelo SIS con muerte por enfermedad
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta:  float         #Tasa de infección
tf:    int           #Cantidad de iteraciones basado en la unidad de tiempo
br:    float         #Tasa de natalidad
mr:    list          #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A:     np.array      #Sistema a evaluar
E:     np.array      #Matriz de edades del sistema A
year:  int           #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista que cuenta con las cantidades normalizadas por estados S, I y D de la población con respecto a la iteración, incluye además las cantidades normalizadas de las poblaciones con tales estados y las respectivas evoluciones del sistema junto con cada matriz de edad por iteración.```

#### SIR_dd_model(alpha,beta,tf,br,mr,ranges_dead,A,E,year)
Modelo SIR con muerte por enfermedad
###### Parámetros:
```
alpha: float		#Tasa de recuperación	
beta:  float		#Tasa de infección
tf:    int		#Cantidad de iteraciones basado en la unidad de tiempo
br:    float		#Tasa de natalidad
mr:    list	    	#Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list	#Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A:     np.array	#Sistema a evaluar
E:     np.array	#Matriz de edades del sistema A
year:  int  		#Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista que cuenta con las cantidades normalizadas por estados S, I, R y D de la población con respecto a la iteración, incluye además las cantidades normalizadas de las poblaciones con tales estados y las respectivas evoluciones del sistema junto con cada matriz de edad por iteración.```
##### Ejemplo:
```
>>> ranges_dead = [[0,25,0.002],[26,40,0.05],[41,100,0.0028]]
>>> ranges = [[1, 15, 0.2], [16, 40, 0.6], [41, 100, 0.2]]
>>> sys_6 = np.zeros((10,10))
>>> sys_6 = cm.initial_condition(0.7,sys_6)
>>> ages_sys_6 = cm.ages(ranges,sys_6)
>>> mr = [[1, 25, 0.25], [26, 51, 0.14], [52, 100, 0.08]]
>>> ex_6 = cm.SIS_dd_model(0.2,0.37,20,7,mr,ranges_dead,sys_6,ages_sys_6,365)[6]
>>>for i in range(20):
......plt.imshow(cm.color(ex_6[i]),cmap="nipy_spectral", interpolation='nearest')
......plt.savefig('ex_6'+str(i)+'.jpg')
>>> img_ex_6 = []
>>> for i in range(20):
......img = cv2.imread('ex_6'+str(i)+'.jpg')
......height, width, layers = img.shape
......size = (width,height)
......img_ex_6.append(img)
>>> out = cv2.VideoWriter('ex_6.mp4',cv2.VideoWriter_fourcc(*'DIVX'), 15, size) 
>>> for i in range(len(img_ex_6)):
......out.write(img_ex_6[i])
>>> out.release()
```
![texto alternativo](Imagenes/ex_6.gif)
#### graph_sis_dd(alpha,beta,tf,br,mr,ranges_dead,A,E,year)
Gráfica del modelo SIS con muerte por enfermedad
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta:  float         #Tasa de infección
tf:    int           #Cantidad de iteraciones basado en la unidad de tiempo
br:    float         #Tasa de natalidad
mr:    list          #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A:     np.array      #Sistema a evaluar
E:     np.array      #Matriz de edades del sistema A
year:  int           #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```.plt   #Gráfica del modelo SIS con muerte por enfermedad```

#### graph_sir_dd(alpha,beta,tf,br,mr,ranges_dead,A,E,year)
Gráfica del modelo SIR con muerte por enfermedad
###### Parámetros:
```
alpha: float		#Tasa de recuperación	
beta:  float		#Tasa de infección
tf:    int		#Cantidad de iteraciones basado en la unidad de tiempo
br:    float		#Tasa de natalidad
mr:    list 		#Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list	#Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A:     np.array	#Sistema a evaluar
E:     np.array	#Matriz de edades del sistema A
year:  int  		#Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```.plt   #Gráfica del modelo SIR con muerte por enfermedad```
###### Ejemplo:
```
>>> cm.graph_sis_dd(0.2,0.37,20,7,mr,ranges_dead,sys_6,ages_sys_6,365)
```
![texto alternativo](Imagenes/sis_dd.png)
Si lo que queremos es evaluar diferentes condiciones iniciales y analizar el comportamiento promedio de alguna enfermedad particular, las funciones ```graph_medium_curves_sis_dd``` y ```graph_medium_curves_sir_dd``` nos permitirán graficar los comportamientos promedio para un mismo sistema, bajo diferentes condiciones iniciales, representando los comportamientos obtenidos al usar ```medium_curves_sis_dd``` o ```medium_curves_sir_dd```.
#### medium_curves_sis_dd(alpha,beta,tf,csim,I0,br,mr,ranges_dead,A,E,year)
Promedio de csim simulaciones para el modelo SIS con muerte por enfermedad
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta:  float         #Tasa de infección
tf:    int           #Cantidad de iteraciones basado en la unidad de tiempo
csim:  int           #Cantidad de simulaciones
I0:    float         #Porcentaje inicial de infectados en el sistema
br:    float         #Tasa de natalidad
mr:    list          #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A:     np.array      #Sistema a evaluar
E:     np.array      #Matriz de edades del sistema A
year:  int           #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista que cuenta con los promedios de las cantidades normalizadas por estados S, I y D de la población con respecto a la iteración, incluye además los promedios de las cantidades normalizadas de las poblaciones con tales estados y las respectivas evoluciones del sistema junto con cada matriz de edad por iteración.```

#### graph_medium_curves_sis_dd(alpha,beta,tf,csim,I0,br,mr,ranges_dead,A,E,year)
Grafica del promedio de simulaciones para el modelo SIS con muerte por enfermedad
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta:  float         #Tasa de infección
tf:    int           #Cantidad de iteraciones basado en la unidad de tiempo
csim:  int           #Cantidad de simulaciones
I0:    float         #Porcentaje inicial de infectados en el sistema
br:    float         #Tasa de natalidad
mr:    list          #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A:     np.array      #Sistema a evaluar
E:     np.array      #Matriz de edades del sistema A
year:  int           #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```.plt   #Gráfica del modelo SIS con muerte por enfermedad promedio para un número csim de simulaciones``` 

#### medium_curves_sir_dd(alpha,beta,tf,csim,I0,br,mr,ranges_dead,A,E,year)
Promedio de csim simulaciones para el modelo SIR con muerte por enfermedad
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta:  float         #Tasa de infección
tf:    int           #Cantidad de iteraciones basado en la unidad de tiempo
csim:  int           #Cantidad de simulaciones
I0:    float         #Porcentaje inicial de infectados en el sistema
br:    float         #Tasa de natalidad
mr:    list          #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A:     np.array      #Sistema a evaluar
E:     np.array      #Matriz de edades del sistema A
year:  int           #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista que cuenta con los promedios de las cantidades normalizadas por estados S, I, R y D de la población con respecto a la iteración, incluye además los promedios de las cantidades normalizadas de las poblaciones con tales estados y las respectivas evoluciones del sistema junto con cada matriz de edad por iteración.```

#### graph_medium_curves_sir_dd(alpha,beta,tf,csim,I0,br,mr,ranges_dead,A,E,year)
Grafica del promedio de simulaciones para el modelo SIR con muerte por enfermedad
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta:  float         #Tasa de infección
tf:    int           #Cantidad de iteraciones basado en la unidad de tiempo
csim:  int           #Cantidad de simulaciones
I0:    float         #Porcentaje inicial de infectados en el sistema
br:    float         #Tasa de natalidad
mr:    list          #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A:     np.array      #Sistema a evaluar
E:     np.array      #Matriz de edades del sistema A
year:  int           #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```.plt   #Gráfica del modelo SIR con muerte por enfermedad promedio para un número csim de simulaciones```
### Modelos SIS y SIR con movimiento de agentes
Para implementar el movimiento en nuestros análisis, debemos añadir un nuevo tipo de espacio vacío en nuestro sistema, este espacio será identificado con el valor numérico 75. La idea de incluir un nuevo tipo de estado para un píxel, nos sirve para conservar la estructura del sistema.

```CAsimulation``` toma las reglas de movimiento como unas reglas del tipo probabilístico, el usuario puede definir una probabilidad de movimiento para cada estado, esto nos permite visualizar diferentes escenarios de comportamiento de los agentes, la función ```transport``` nos permite modelar estas reglas de movimiento para cada posible estado usando ```state_coor```, la cual actúa como una generalización de funciones similares a  ```vector_S```, finalmente si lo que queremos es visualizar como se desarrollan las reglas de movimiento entre dos sistemas, la función ```superposición``` resulta ser una herramienta indispensable pues nos permite superponer los sistemas con los que estemos trabajando.

#### state_coor(A, state_value)
Enlista los agentes que tengan un estado identificado con state_value
###### Parámetros:
```
A: np.array          #Sistema sobre el cual se está trabajando
state_value: int	#Valor con el cual se identifica el estado de interés
```
###### Devoluciones:
```list   #Lista con las coordenadas de los individuos que tengan el estado identificado con state_value```

#### transport(output,arrival,ages,list_prob)
Todos los agentes tendrán una probabilidad de moverse, de acuerdo con el estado que posea
###### Parámetros:
```
output: np.array     #Sistema de salida: los individuos en output son los que podrán moverse
arrival: np.array    #Sistema de llegada: Los individuos que se muevan de output caerán en arrival
ages: np.array       #Edades de los individuos en el sistema
list_prob: list      #Lista con la probabilidad de movimiento de cada estado
```
###### Devoluciones:
```list  #Lista con los cambios realizados sobre output y arrival luego de aplicar el movimiento de agentes, además incluye la matriz de edades de los agentes luego de realizar el movimiento```
#### superposicion(A,B)
Permite visualizar dos sistemas sobre un mismo dominio 
###### Parámetros:
```
A: np.array          #Sistema 1
B: np.array          #Sistema 2
```
###### Devoluciones:
```np.array   #Arreglo en el cual están descritos los sistemas A y B```
Es tiempo de hablar de los modelos SIS y SIR, con movimiento. De manera similar a como se definieron las funciones previas para cada uno de los modelos anteriores, se definen ```evolution_sis_wm```, ```evolution_sir_wm```, ```evolution_SIS_wm``` y ```evolution_SIR_wm```, obteniendo al final las funciones que describen los comportamientos SIS y SIR con una población "movil", las cuales se identificarán como ```SIS_wm_model``` y ```SIR_wm_model```. Finalmente se definieron también las funciones que nos permitirán visualizar estos comportamientos de manera analítica, las funciones ```graph_sis_wm``` y ```graph_sir_wm``` actuarán como funciones de análisis gráfico para un número arbitrario de iteraciones.
#### evolution_sis_wm(alpha,beta,list_prob,br,mr,ranges_dead,A,B,E,time_unit,year)
Regla de evolución para el modelo SIS con movimiento de agentes
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta: float          #Tasa de infección
list_prob: list      #Lista con la probabilidad de movimiento de cada estado
br: float            #Tasa de natalidad
mr: list             #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema 1 a evaluar
B: np.array          #Sistema 2 a evaluar
E: np.array          #Matriz de edades del sistema A
time_unit: int       #Unidad de tiempo a analizar (minutos, días, meses, años)
year: int            #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista con el sistema al aplicar el modelo SIS con movimiento a cada sistema y con la matriz de edades del sistema```

#### evolution_sir_wm(alpha,beta,list_prob,br,mr,ranges_dead,A,B,E,time_unit,year)
Regla de evolución para el modelo SIR con movimiento de agentes
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta: float          #Tasa de infección
list_prob: list      #Lista con la probabilidad de movimiento de cada estado
br: float            #Tasa de natalidad
mr: list             #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema 1 a evaluar
B: np.array          #Sistema 2 a evaluar
E: np.array          #Matriz de edades del sistema A
time_unit: int       #Unidad de tiempo a analizar (minutos, días, meses, años)
year: int            #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista con el sistema al aplicar el modelo SIR con movimiento a cada sistema y con la matriz de edades del sistema``` 
#### evolution_SIS_wm(alpha,beta,tf,list_prob,br,mr,ranges_dead,A,B,E,year)
Aplica el modelo SIS con movimiento tf veces sobre los sistemas A y B
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta: float          #Tasa de infección
tf: int              #Cantidad de iteraciones
list_prob: list      #Lista con la probabilidad de movimiento de cada estado
br: float            #Tasa de natalidad
mr: list             #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema 1 a evaluar
B: np.array          #Sistema 2 a evaluar
E: np.array          #Matriz de edades del sistema A
year: int            #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista con los sistemas A y B luego de aplicar el modelo SIS con transporte, incluye también la matriz de edades luego de esta transformación```

#### evolution_SIR_wm(alpha,beta,tf,list_prob,br,mr,ranges_dead,A,B,E,year)
Aplica el modelo SIR con movimiento tf veces sobre los sistemas A y B
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta: float          #Tasa de infección
tf: int              #Cantidad de iteraciones
list_prob: list      #Lista con la probabilidad de movimiento de cada estado
br: float            #Tasa de natalidad
mr: list             #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema 1 a evaluar
B: np.array          #Sistema 2 a evaluar
E: np.array          #Matriz de edades del sistema A
year: int            #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista con los sistemas A y B luego de aplicar el modelo SIR con transporte, incluye también la matriz de edades luego de esta transformación```
#### SIS_wm_model(alpha,beta,tf,list_prob,br,mr,ranges_dead,A,B,E,year)
Modelo SIS con movimiento
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta: float          #Tasa de infección
tf: int              #Cantidad de iteraciones
list_prob: list      #Lista con la probabilidad de movimiento de cada estado
br: float            #Tasa de natalidad
mr: list             #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema 1 a evaluar
B: np.array          #Sistema 2 a evaluar
E: np.array          #Matriz de edades del sistema A
year: int            #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista que contiene el comportamiento de los estados S, I y D con respecto a cada iteración (Se forman en tuplas donde la primera componente es la iteración y la segunda el comportamiento de alguno de los estados), se incluyen también los valores numéricos de crecimiento y por último la evolución del sistema junto con la evolución de u matriz de edades```

#### SIR_wm_model(alpha,beta,tf,list_prob,br,mr,ranges_dead,A,B,E,year)
Modelo SIR con movimiento
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta: float          #Tasa de infección
tf: int              #Cantidad de iteraciones
list_prob: list      #Lista con la probabilidad de movimiento de cada estado
br: float            #Tasa de natalidad
mr: list             #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema 1 a evaluar
B: np.array          #Sistema 2 a evaluar
E: np.array          #Matriz de edades del sistema A
year: int            #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```list   #Lista que contiene el comportamiento de los estados S, I, R y D con respecto a cada iteración (Se forman en tuplas donde la primera componente es la iteración y la segunda el comportamiento de alguno de los estados), se incluyen también los valores numéricos de crecimiento y por último la evolución del sistema junto con la evolución de u matriz de edades```
#### graph_sis_wm(alpha,beta,tf,list_prob,br,mr,ranges_dead,A,B,E,year)
Gráfica del modelo SIS con movimiento
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta: float          #Tasa de infección
tf: int              #Cantidad de iteraciones
list_prob: list      #Lista con la probabilidad de movimiento de cada estado
br: float            #Tasa de natalidad
mr: list             #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema 1 a evaluar
B: np.array          #Sistema 2 a evaluar
E: np.array          #Matriz de edades del sistema A
year: int            #Unidad de tiempo de referencia (por lo general un año)
```
###### Devoluciones:
```.plt   #Gráfica del modelo SIS con movimiento```

#### graph_sir_wm(alpha,beta,tf,list_prob,br,mr,ranges_dead,A,B,E,year)
Gráfica del modelo SIR con movimiento
###### Parámetros:
```
alpha: float         #Tasa de recuperación	
beta: float          #Tasa de infección
tf: int              #Cantidad de iteraciones
list_prob: list      #Lista con la probabilidad de movimiento de cada estado
br: float            #Tasa de natalidad
mr: list             #Lista con las tasas de mortalidad por rango de edad: en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
ranges_dead: list    #Lista con los rangos de edad y la probabilidad de muerte, en las dos primeras componentes de cada elemento debe ir el rango de edad y en la tercera, la probabilidad de morir en ese grupo
A: np.array          #Sistema 1 a evaluar
B: np.array          #Sistema 2 a evaluar
E: np.array          #Matriz de edades del sistema A
year: int            #Unidad de tiempo de referencia (por lo general un año)
``` 
###### Devoluciones:
```.plt   #Gráfica del modelo SIR con movimiento```
