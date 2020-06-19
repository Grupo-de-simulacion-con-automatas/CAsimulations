# CAsimulations

```CAsimulations``` proporciona una manera de simular fenomenos asociados con la propagación de enfermedades, basandose en modelos *SIR* y *SIS* implementados en autómatas celulares en Python. ```CAsimulations``` incluye una gran variedad de utilidades para análisis epidemiologicos tales como la capacidad de definir la condición inicial de frontera del sistema, la condición inicial de dispersión de los individuos infectados, variaciones y comparaciones con respecto al cambio de escala y al cambio de frontera del sistema, variaciones promedio para un número arbitrario de simulaciones, entre otros.
## Instalación
Solo debemos usar pip para instalar:
```pip install -i https://test.pypi.org/simple/ casimulation```
## Funciones incluidas
```>>> from CAsimulation import camodels```
### Spline3(A)
Realice una interpolación cubica tipo spline, tomando como puntos los elementos de A.
##### Parámetros:
```A: List	 	#Lista de coordenadas.```
##### Devoluciones:
```np.array 	#Arreglo de puntos al aplicar un spline cubico.```
###  One_function_graph(A, x)
Grafique el spline cubico para los elementos de A.
##### Parámetros:
```
A: list   #Lista de coordenadas de la función x
x: str    #Nombre de la función
```
##### Devoluciones:
```.plt 	#Grafica de la función x ```
### One_state_graph(A, x)
Grafique el spline cubico para los elementos de A de manera normalizada
##### Parámetros:
```
A: list   #Lista de coordenadas de la función x
x: str    #Nombre de la función
```
##### Devoluciones:	
```.plt   #Grafica de la función normalizada x ```
### Two_states_graph(A, B, X, Y, Z)
Grafique el spline cubico para los elementos de A y B
##### Parámetros:	
```
A: list   #Lista de coordenadas de la función x 
B: list   #Lista de coordenadas de la función y
x: str    #Nombre de la primera función
y: str    #Nombre de la segunda función
z: str    #Título del gráfico
```
##### Devoluciones:	
```.plt	  #Grafica de las funciones x e y con título z```
### Three_states_graph(A, B, C, x, y, z, w)
Grafique el spline cubico para los elementos de A, B y C
##### Parámetros: 	
```
A: list	  #Lista de coordenadas de la función x
B: list	  #Lista de coordenadas de la función y
C: list	  #Lista de coordenadas de la función z
x: str	  #Nombre de la primera función
y: str	  #Nombre de la segunda función
z: str	  #Nombre de la tercera función
w: str	  #Título del grafico 
```
##### Devoluciones:	
```.plt	  #Grafica de las funciones x, y, z con título w```
### Distribution_graph(A, B, C, D, E, F, G, H, I, J)
Grafica la variación presente en los cambios de distribución inicial de población infectada
##### Parámetros: 	
```
A: list	  #Lista de coordenadas - bloque noroeste
B: list	  #Lista de coordenadas - bloque norte 
C: list	  #Lista de coordenadas - bloque noreste
D: list	  #Lista de coordenadas – bloque oeste
E: list   #Lista de coordenadas – bloque central
F: list	  #Lista de coordenadas – bloque este
G: list	  #Lista de coordenadas – bloque suroeste
H: list	  #Lista de coordenadas – bloque sur
I: list	  #Lista de coordenadas – bloque sureste
J: list	  #Lista de coordenadas – distribución aleatoria	 
```
##### Devoluciones:	
```.plt	  #Grafica de las variaciones bajo cambios en la distribución de población infectada```
### Scales_graph(A, B, C, D, E)
Grafica los cambios presentes en la variación de escalas
##### Parámetros: 	
```
A: list	  #Lista de coordenadas – primera escala
B: list	  #Lista de coordenadas – segunda escala
C: list	  #Lista de coordenadas – tercera escala
D: list	  #Lista de coordenadas – cuarta escala
E: list   #Lista de coordenadas – quinta escala
```
##### Devoluciones:	
```.plt	  #Grafica de los cambios en el modelo tomando escalas diferentes```
### Systems_graph(A, B, C, D, E, F, G)
Grafica los cambios presentes en la condición de frontera
##### Parámetros: 	
```
A: list	  #Lista de coordenadas – primera región
B: list	  #Lista de coordenadas – segunda región
C: list	  #Lista de coordenadas – tercera región
D: list   #Lista de coordenadas – cuarta región
E: list   #Lista de coordenadas – quinta región
F: list	  #Lista de coordenadas – sexta región
G: list	  #Lista de coordenadas – séptima región
```
##### Devoluciones:	
```.plt	  #Grafica de los cambios en el modelo tomando condiciones de frontera diferentes```
### Scales_differences_graph(A, B, C, D)
Grafica los cambios presentes en la variación de escalas
##### Parámetros: 	
```
A: list   #Lista de coordenadas – primera escala vs última escala
B: list	  #Lista de coordenadas – segunda escala vs última escala
C: list	  #Lista de coordenadas – tercera escala vs última escala
D: list	  #Lista de coordenadas – cuarta escala vs última escala
```
##### Devoluciones:	
```.plt	  #Grafica de los cambios en el modelo tomando escalas diferentes```
### Array_generator(A, i, j)
Genera la vecindad de Moore para la célula en la fila i columna j
##### Parámetros: 	
```
A: np.array #Arreglo donde se aplicará el modelo epidemiológico
I: int      #Fila i de A
J: int      #Fila j de A
```
##### Devoluciones:	
```np.array	#Vecindad de Moore de la célula en la fila i columna j```
### Vector_S(A)
Genera la lista de posiciones de individuos susceptibles
##### Parámetros:
```
A: np.array #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:
```list	    #Lista de posiciones de individuos susceptibles```
### Vector_I(A)
Genera la lista de posiciones de individuos infectados   	
##### Parámetros:	
```A: np.array #Arreglo donde se aplicará el modelo epidemiológico```
##### Devoluciones:	
```list     #Vector de posiciones de individuos infectados```
### sumaS(V)
cantidad de individuos susceptibles en la vecindad
##### Parámetros:
```V: np.array #Vecindad```
##### Devoluciones:
```int      #Cantidad de individuos susceptibles en la vecindad V```
### sumaI(V)
cantidad de individuos infectados en la vecindad
##### Parámetros: 	
```V: np.array #Vecindad```
##### Devoluciones:	
```int      #Cantidad de individuos infectados en la vecindad V```
### sumaR(V)
cantidad de individuos recuperados en la vecindad
##### Parámetros: 	
```V: np.array #Vecindad```
##### Devoluciones:	
```int      #Cantidad de individuos recuperados en la vecindad V```
### sumaV(V)
cantidad de espacios vacíos en la vecindad
##### Parámetros: 	
```V: np.array #Vecindad```
##### Devoluciones:	
```int      #Cantidad de espacios vacíos en la vecindad V```
### Count_S(A)
Cantidad de individuos susceptibles
##### Parámetros:	
```A: np.array #Arreglo donde se aplicará el modelo epidemiológico```
##### Devoluciones: 	
```int      #Cantidad de individuos susceptibles en el sistema A```
### Count_I(A)
Cantidad de individuos infectados
##### Parámetros:	
```A: np.array #Arreglo donde se aplicará el modelo epidemiológico```
##### Devoluciones:	
```int     #Cantidad de individuos infectados en el sistema A```
### Count_R(A)
Cantidad de individuos recuperados
##### Parámetros:	
```A: np.array #Arreglo donde se aplicará el modelo epidemiológico```
##### Devoluciones:	
```int     #Cantidad de individuos recuperados en el sistema A```
### Count_D(A)
Cantidad de individuos muertos
##### Parámetros:	
```A: np.array #Arreglo donde se aplicará el modelo epidemiológico```
##### Devoluciones:	
```int     #Cantidad de individuos recuperados en el sistema A```
### Num_individuals(A)
Cantidad de espacios no vacíos
##### Parámetros:	
```A: np.array #Arreglo donde se aplicará el modelo epidemiológico```
##### Devoluciones:
```int     #Cantidad de espacios no vacíos en el sistema A```
### count_s(A)
Promedio de individuos susceptibles
##### Parámetros: 	
```A: np.array #Arreglo donde se aplicará el modelo epidemiológico```
##### Devoluciones:	
```float    #Promedio de individuos susceptibles en el sistema A con respecto a la cantidad de espacios no                                                   vacíos```
