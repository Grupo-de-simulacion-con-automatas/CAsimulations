# CAsimulations

```CAsimulations``` proporciona una manera de simular fenómenos asociados con la propagación de enfermedades, basándose en modelos *SIR* y *SIS* implementados en autómatas celulares en Python. ```CAsimulations``` incluye una gran variedad de utilidades para análisis epidemiológicos tales como la capacidad de definir la condición inicial de frontera del sistema, la condición inicial de dispersión de los individuos infectados, variaciones y comparaciones con respecto al cambio de escala y al cambio de frontera del sistema, variaciones promedio para un número arbitrario de simulaciones, entre otros. Prro

## Instalación
Solo debemos usar pip para instalar:
```pip install -i https://test.pypi.org/simple/ casimulation```

## Funciones incluidas
```>>> from CAsimulation import camodels```
### spline3(A)
Realice una interpolación cubica tipo spline, tomando como puntos los elementos de A.
##### Parámetros:
```
A: list   #Lista de coordenadas.
```
##### Devoluciones:
```
np.array    #Arreglo de puntos al aplicar un spline cubico.
```
###  one_function_graph(A, x)
Graficá el spline cubico para los elementos de A.
##### Parámetros:
```
A: list   #Lista de coordenadas de la función x
x: str    #Nombre de la función
```
##### Devoluciones:
```
.plt    #Gráfica de la función x 
```
### one_state_graph(A, x)
Graficá el spline cubico para los elementos de A de manera normalizada
##### Parámetros:
```
A: list   #Lista de coordenadas de la función x
x: str    #Nombre de la función
```
##### Devoluciones:	
```
.plt    #Gráfica de la función normalizada x 
```
### two_states_graph(A, B, X, Y, Z)
Graficá el spline cubico para los elementos de A y B
##### Parámetros:	
```
A: list   #Lista de coordenadas de la función x 
B: list   #Lista de coordenadas de la función y
x: str    #Nombre de la primera función
y: str    #Nombre de la segunda función
z: str    #Título del gráfico
```
##### Devoluciones:	
```
.plt    #Gráfica de las funciones x e y con título z
```
### three_states_graph(A, B, C, x, y, z, w)
Graficá el spline cubico para los elementos de A, B y C
##### Parámetros: 	
```
A: list   #Lista de coordenadas de la función x
B: list   #Lista de coordenadas de la función y
C: list   #Lista de coordenadas de la función z
x: str    #Nombre de la primera función
y: str    #Nombre de la segunda función
z: str    #Nombre de la tercera función
w: str    #Título del gráfico 
```
##### Devoluciones:	
```
.plt    #Gráfica de las funciones x, y, z con título w
```
### distribution_graph(A, B, C, D, E, F, G, H, I, J)
Graficá la variación presente en los cambios de distribución inicial de población infectada
##### Parámetros: 	
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
##### Devoluciones:	
```
.plt    #Gráfica de las variaciones bajo cambios en la distribución de población infectada
```
### scales_graph(A, B, C, D, E)
Graficá los cambios presentes en la variación de escalas
##### Parámetros: 	
```
A: list   #Lista de coordenadas – primera escala
B: list   #Lista de coordenadas – segunda escala
C: list   #Lista de coordenadas – tercera escala
D: list   #Lista de coordenadas – cuarta escala
E: list   #Lista de coordenadas – quinta escala
```
##### Devoluciones:	
```
.plt    #Gráfica de los cambios en el modelo tomando escalas diferentes
```
### systems_graph(A, B, C, D, E, F, G)
Graficá los cambios presentes en la condición de frontera
##### Parámetros: 	
```
A: list   #Lista de coordenadas – primera región
B: list   #Lista de coordenadas – segunda región
C: list   #Lista de coordenadas – tercera región
D: list   #Lista de coordenadas – cuarta región
E: list   #Lista de coordenadas – quinta región
F: list   #Lista de coordenadas – sexta región
G: list   #Lista de coordenadas – séptima región
```
##### Devoluciones:	
```
.plt    #Gráfica de los cambios en el modelo tomando condiciones de frontera diferentes
```
### scales_differences_graph(A, B, C, D)
Graficá los cambios presentes en la variación de escalas
##### Parámetros: 	
```
A: list   #Lista de coordenadas – primera escala vs última escala
B: list   #Lista de coordenadas – segunda escala vs última escala
C: list   #Lista de coordenadas – tercera escala vs última escala
D: list   #Lista de coordenadas – cuarta escala vs última escala
```
##### Devoluciones:	
```
.plt    #Gráfica de los cambios en el modelo tomando escalas diferentes
```
### array_generator(A, i, j)
Genera la vecindad de Moore para la célula en la fila i columna j
##### Parámetros: 	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
I: int        #Fila i de A
J: int        #Fila j de A
```
##### Devoluciones:	
```
np.array    #Vecindad de Moore de la célula en la fila i columna j
```
### vector_S(A)
Genera la lista de posiciones de individuos susceptibles
##### Parámetros:
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:
```
list    #Lista de posiciones de individuos susceptibles
```
### vector_I(A)
Genera la lista de posiciones de individuos infectados   	
##### Parámetros:	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:	
```
list    #Vector de posiciones de individuos infectados
```
### sumaS(V)
cantidad de individuos susceptibles en la vecindad
##### Parámetros:
```
V: np.array   #Vecindad
```
##### Devoluciones:
```
int   #Cantidad de individuos susceptibles en la vecindad V
```
### sumaI(V)
cantidad de individuos infectados en la vecindad
##### Parámetros: 	
```
V: np.array   #Vecindad
```
##### Devoluciones:	
```
int   #Cantidad de individuos infectados en la vecindad V
```
### sumaR(V)
cantidad de individuos recuperados en la vecindad
##### Parámetros: 	
```
V: np.array   #Vecindad
```
##### Devoluciones:	
```
int   #Cantidad de individuos recuperados en la vecindad V
```
### sumaV(V)
cantidad de espacios vacíos en la vecindad
##### Parámetros: 	
```
V: np.array   #Vecindad
```
##### Devoluciones:	
```
int   #Cantidad de espacios vacíos en la vecindad V
```
### count_S(A)
Cantidad de individuos susceptibles
##### Parámetros:	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones: 	
```
int   #Cantidad de individuos susceptibles en el sistema A
```
### count_I(A)
Cantidad de individuos infectados
##### Parámetros:	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:	
```
int   #Cantidad de individuos infectados en el sistema A
```
### count_R(A)
Cantidad de individuos recuperados
##### Parámetros:	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:	
```
int   #Cantidad de individuos recuperados en el sistema A
```
### count_D(A)
Cantidad de individuos muertos
##### Parámetros:	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:	
```
int   #Cantidad de individuos recuperados en el sistema A
```
### num_individuals(A)
Cantidad de espacios no vacíos
##### Parámetros:	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:
```
int   #Cantidad de espacios no vacíos en el sistema A
```
### count_s(A)
Promedio de individuos susceptibles
##### Parámetros: 	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:	
```
float   #Promedio de individuos susceptibles en el sistema A con respecto a la cantidad de espacios no                                                   vacíos
```
### count_i(A)
Promedio de individuos infectados
##### Parámetros:	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:	
```
float   #Promedio de individuos infectados en el sistema A con respecto a la cantidad de espacios no vacíos
```
### count_r(A)
Promedio de individuos recuperados
##### Parámetros: 	
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:
```
float   #Promedio de individuos recuperados en el sistema A con respecto a la cantidad de espacios no vacíos
```
### count_d(A)
Promedio de individuos muertos
##### Parámetros:
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:
```
float   #Promedio de individuos muertos en el sistema A con respecto a la cantidad de espacios no vacíos
```
### base_rule(alpha, beta, V)
Aplica la regla base de interacción local 
##### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
V:     np.array   #Vecindad 
```
##### Devoluciones:	
```
float   #Si es 1, el individuo en la célula central de se infectó o se mantuvo enfermo. Si es 0, el individuo en la célula central paso a un estado de susceptibilidad o se mantuvo susceptible
```
### evolution_sis(alpha, beta, U)
Aplica la regla base de interacción global
##### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
U:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones: 	
```
np.array    #Evolución del sistema al aplicar la regla base de interacción global
```
### evolution_SIS(alpha, beta, tf, A)
Aplica la regla base de interacción global al sistema tf veces
##### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:	
```
list    #Lista cuyos elementos son la evolución del sistema A desde el tiempo 0 hasta el tiempo tf
```
### SIS_model(alpha, beta, tf, A)
Modelo SIS
##### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:	
```
list    #Contiene las coordenadas (x,n^x(S)) donde x es una iteración y n^x(S) es la cantidad de individuos susceptibles normalizada. las coordenadas (x,n^x(I)) donde x es una iteración y n^x(I) es la cantidad de individuos infectados normalizada
```
### num_I(a,b)
Porcentaje de infectados
##### Parámetros:
```
a: int    #Cantidad de infectados por cada b habitantes
b: int    #Cantidad de habitantes
```
##### Devoluciones:	
```list   #Retorna la lista con una cantidad a de infectados con respecto a una población de tamaño b```
### initial_condition(I0, A)
Define la condición inicial del sistema
##### Parámetros: 	
```
I0: float       #Porcentaje de individuos infectados en el sistema 
A:  np.array    #Arreglo sobre el modelo epidemiológico
```
##### Devoluciones:
```
np.array    #Condición inicial del sistema
```
### graph_sis_S(alpha, beta, tf, A) 
Graficá la cantidad de individuos susceptibles normalizada hasta un tiempo tf
##### Parámetros: 
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones: 
```
.plt    #Gráfica que describe la evolución del estado S en el sistema A hasta un tiempo tf
```
### graph_sis_I(alpha, beta, tf, A) 
Graficá la cantidad de individuos infectados normalizada hasta un tiempo tf
##### Parámetros: 
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones: 
```
.plt    #Gráfica que describe la evolución del estado I en el sistema A hasta un tiempo tf
```
### graph_sis(alpha, beta, tf, A)
Graficá la cantidad de individuos susceptibles e infectados normalizadas hasta un tiempo tf
##### Parámetros:
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:
```
.plt    #Gráfica que describe la evolución de los estados S e I en el sistema A hasta un tiempo tf
```
### interaction_SI(alpha, beta, A)
Aplica la regla de interacción del estado S 
##### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
A:     np.array   #Sistema 
```
##### Devoluciones:	
```
np.array    #Arreglo que cuenta con los individuos que se infectaron, individuos que se mantuvieron susceptibles e individuos que ya se encontraban recuperados
```
### num_R(a, b)
Porcentaje de recuperados
##### Parámetros: 	
```
a: int    #Cantidad de recuperados por cada b infectados
b: int    #Cantidad de infectados
```
##### Devoluciones:	
```list   #Retorna la lista con una cantidad a de recuperados con respecto a una población infectada de tamaño b```
### interaction_IR(alpha, beta, A)
Aplica la regla de interacción del estado I 
##### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
A:     np.array   #Sistema 
```
##### Devoluciones:	
```np.array   #Arreglo que cuenta con los individuos que se recuperaron de la enfermedad, individuos que se mantuvieron enfermos e individuos susceptibles```
### evolution_sir(alpha, beta, U)
Aplica la regla que define el comportamiento del modelo sir
##### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
U:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:
```np.array   #Evolución del sistema al aplicar la regla de comportamiento sir```
### evolution_SIR(alpha, beta, tf, A)
Aplica la regla base de comportamiento sir de manera global al sistema tf veces
##### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:	
```list   #Lista cuyos elementos son la evolución del sistema A desde el tiempo 0 hasta el tiempo tf```
### SIR_model(alpha, beta, tf, A)
Modelo SIR
##### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:	
```list   #Contiene las coordenadas (x,n^x(S)) donde x es una iteración y n^x(S) es la cantidad de individuos susceptibles normalizada. las coordenadas (x,n^x(I)) donde x es una iteración y n^x(I) es la cantidad de individuos infectados normalizada y las coordenadas (x,n^x(R)) donde x es una iteración y n^x(R) es la cantidad de individuos recuperados normalizada```
### graph_sir_S(alpha, beta, tf, A) 
Graficá la cantidad de individuos susceptibles normalizada hasta un tiempo tf
##### Parámetros:
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones: 
```.plt   #Gráfica que describe la evolución del estado S en el sistema A hasta un tiempo tf```
### graph_sir_I(alpha, beta, tf, A) 
Graficá la cantidad de individuos infectados normalizada hasta un tiempo tf
##### Parámetros:
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:
```.plt   #Gráfica que describe la evolución del estado I en el sistema A hasta un tiempo tf```
### graph_sir_R(alpha, beta, tf, A) 
Grafica la cantidad de individuos recuperados normalizada hasta un tiempo tf
##### Parámetros:
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:
```.plt   #Gráfica que describe la evolución del estado R en el sistema A hasta un tiempo tf```
### graph_sir(alpha, beta, tf, A)
Graficá la cantidad de individuos susceptibles, infectados y recuperados normalizadas hasta un tiempo tf
##### Parámetros:
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:
```.plt   #Gráfica que describe la evolución de los estados S, I y R en el sistema A hasta un tiempo tf```
### color(A)
Graficá el entorno espacial en una escala de colores rgb usando la paleta nipy_spectral de Python
##### Parámetros:
```
A: np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:	
```np.array   #Arreglo con entradas en escala rgb```
### heatmap_sis(alpha, beta, tf, A)
Graficá el comportamiento espacial de la enfermedad hasta un tiempo tf
##### Parámetros: 	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:
```.plt   #Gráfica del mapa de calor que describe como evoluciono la enfermedad en el sistema A hasta un tiempo tf```
### heatmap_sir_I(alpha, beta, tf, A)
Graficá el comportamiento espacial de la población infectada hasta un tiempo tf para el modelo SIR
##### Parámetros:
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:
```.plt   #Gráfica del mapa de calor que describe como evoluciono la población infectada en el sistema A hasta un tiempo tf para el modelo SIR```
### heatmap_sir_R(alpha, beta, tf, A)
Graficá el comportamiento espacial de la población recuperada hasta un tiempo tf para el modelo SIR
##### Parámetros:
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de iteraciones
A:     np.array   #Arreglo donde se aplicará el modelo epidemiológico
```
##### Devoluciones:
```.plt   #Gráfica del mapa de calor que describe como evoluciono la población recuperada en el sistema A hasta un tiempo tf para el modelo SIR```
### northwest(n, m, I0)
Localiza la población infectada en la zona noroeste del rectángulo
##### Parámetros:
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
##### Devoluciones:
```np.array   #Condición inicial con toda la población infectada en la zona noroeste del sistema rectangular de dimensión n*m ```
### north(n, m, I0)
Localiza la población infectada en la zona norte del rectángulo 
##### Parámetros:	
```
n:  int          #Cantidad de filas 
m:  int	         #Cantidad de columnas
I0: float	       #Porcentaje inicial de individuos infectados
```
##### Devoluciones:
```np.array   #Condición inicial con toda la población infectada en la zona norte del sistema rectangular de dimensión n*m```
### northeast(n, m, I0)
Localiza la población infectada en la zona noreste del rectángulo
##### Parámetros:	
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
##### Devoluciones:
```np.array   #Condición inicial con toda la población infectada en la zona noreste del sistema rectangular de dimensión n*m```
### west(n, m, I0)
Localiza la población infectada en la zona oeste del rectángulo
##### Parámetros:
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
##### Devoluciones:
```np.array   #Condición inicial con toda la población infectada en la zona oeste del sistema rectangular de dimensión n*m```
### center(n, m, I0)
Localiza la población infectada en la zona central del rectángulo
##### Parámetros:
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
##### Devoluciones:
```np.array   #Condición inicial con toda la población infectada en la zona central del sistema rectangular de dimensión n*m```
### east(n, m, I0)
Localiza la población infectada en la zona este del rectángulo
##### Parámetros:
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
##### Devoluciones:
```np.array   #Condición inicial con toda la población infectada en la zona este del sistema rectangular de dimensión n*m```
### southwest(n, m, I0)
Localiza la población infectada en la zona suroeste del rectángulo
##### Parámetros:	
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
##### Devoluciones:
```np.array   #Condición inicial con toda la población infectada en la zona suroeste del sistema rectangular de dimensión n*m```
### south(n, m, I0)
Localiza la población infectada en la zona sur del rectángulo
##### Parámetros:
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
##### Devoluciones:
```np.array   #Condición inicial con toda la población infectada en la zona sur del sistema rectangular de dimensión n*m```
### southeast(n, m, I0)
Localiza la población infectada en la zona sureste del rectángulo
##### Parámetros:	
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
##### Devoluciones: 
```np.array   #Condición inicial con toda la población infectada en la zona sureste del sistema rectangular de dimensión n*m```
### aleatorio(n, m, I0)
Localiza la población infectada de manera uniforme en el rectángulo
##### Parámetros:
```
n:  int     #Cantidad de filas 
m:  int     #Cantidad de columnas
I0: float   #Porcentaje inicial de individuos infectados
```
##### Devoluciones:
```np.array   #Condición inicial con toda la población infectada ubicada de manera uniforme en el sistema rectangular de dimensión n*m```
### medium_curves_sis(alpha, beta, tf, csim, I0, A)
Genera las listas de coordenadas promedio al aplicar el modelo sis en una cantidad csim de simulaciones para una condición inicial del I0% de infectados en el espacio
##### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de tics
Csim:  int        #Cantidad de simulaciones
I0:    float      #Porcentaje inicial de infectados
A:     np.array   #Sistema sobre el cual se aplica el modelo
```
##### Devoluciones:
```list   #Lista de coordenadas promedio para el estado S, para el estado I y valores en el tiempo de los estados S e I ubicados en listas respectivamente```
### graph_medium_curves_sis(alpha, beta, tf, csim, I0, A)
Grafica los valores promedio al aplicar csim veces el modelo sis para un valor inicial fijo de individuos infectados
##### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de tics
Csim:  int        #Cantidad de simulaciones
I0:    float      #Porcentaje inicial de infectados
A:     np.array   #Sistema sobre el cual se aplica el modelo
```
##### Devoluciones:
```.plt   #Gráfica con los valores promedio para cada estado del modelo SIS```
### medium_curves_sir(alpha, beta, tf, csim, I0, A)
Genera las listas de coordenadas promedio al aplicar el modelo SIR en una cantidad csim de simulaciones para una condición inicial del I0% de infectados en el espacio
##### Parámetros:	
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de tics
Csim:  int        #Cantidad de simulaciones
I0:    float      #Porcentaje inicial de infectados
A:     np.array   #Sistema sobre el cual se aplica el modelo
```
##### Devoluciones:
```list   #Lista de coordenadas promedio para los estados S, I y R y valores en el tiempo de los estados S, I y R ubicados en listas respectivamente```
### graph_medium_curves_sir(alpha, beta, tf, csim, I0, A)
Gráfica los valores promedio al aplicar csim veces el modelo SIR para un valor inicial fijo de individuos infectados
##### Parámetros:
```
alpha: float      #Tasa de recuperación
beta:  float      #Tasa de infección
tf:    int        #Cantidad de tics
Csim:  int        #Cantidad de simulaciones
I0:    float      #Porcentaje inicial de infectados
A:     np.array   #Sistema sobre el cual se aplica el modelo
```
##### Devoluciones:
```.plt   #Gráfica con los valores promedio para cada estado del modelo SIR```
### boundary(L,M)
Genera sub-matrices nulas en la matriz M
##### Parámetros:
```
L: list       #Lista de coordenadas que se anularan para definir donde se aplican los modelos epidemiológicos
M: np.array   #Arreglo sobre el cual se definen las condiciones iniciales de entorno de ejecución de los modelos epidemiológicos
```
##### Devoluciones: 
```np.array   #Sistema	en el cual se aplican los modelos bajo condiciones no regulares de frontera```
### domain_definition(n, m, a, b, M)
Define y genera las sub-matrices nulas donde se aplicarán los análisis epidemiológicos
##### Parámetros:	
```
n: int        #Cantidad de filas de la sub-matriz
m: int        #Cantidad de columnas de la sub-matriz
a: int        #Fila en la cual se va a ubicar la sub-matriz
b: int        #Columna en la cual se va a ubicar a sub-matriz
M: np.array   #Arreglo sobre el cual se va a generar la sub-matriz nula
```
##### Devoluciones: 
```np.array   #Sistema	en el cual se aplican los modelos bajo condiciones no regulares de frontera```
