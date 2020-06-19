# CAsimulations

```CAsimulations``` proporciona una manera de simular fenómenos asociados con la propagación de enfermedades, basándose en modelos *SIR* y *SIS* implementados en autómatas celulares en Python. ```CAsimulations``` incluye una gran variedad de utilidades para análisis epidemiológicos tales como la capacidad de definir la condición inicial de frontera del sistema, la condición inicial de dispersión de los individuos infectados, variaciones y comparaciones con respecto al cambio de escala y al cambio de frontera del sistema, variaciones promedio para un número arbitrario de simulaciones, entre otros. 

## Instalación
Solo debemos usar pip para instalar:

```pip install -i https://test.pypi.org/simple/ casimulation```
## Preliminares
Se decidió implementar una interpolación tipo spline cubica para la correcta visualización de los datos obtenidos a partir de listas de coordenadas. ```spline3``` genera los coeficientes de los polinomios cúbicos que mejor se aproximan a la lista ```A``` .
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
#### Ejemplo:
```
>>> from CAsimulation import camodels as cm
>>> Point_list=[[1,0.2],[2,2.7],[3,3],[4,1],[5,2]]
>>> cm.spline3(Point_list)
array([[ 0.2       ,  2.87142857,  0.        , -0.37142857],
       [ 2.7       ,  1.75714286, -1.11428571, -0.34285714],
       [ 3.        , -1.5       , -2.14285714,  1.64285714],
       [ 1.        , -0.85714286,  2.78571429, -0.92857143]])
```
