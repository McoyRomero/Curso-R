Ejercicio de programación VI: Estructuras de Control
====================================================

### [IMSER 2013]

De otros años:

* Ejercicio de programación:
  - for: hacer un script que cuente por fila de una matriz la cantidad de elementos que cumplan una condición (mayores que 0, por ejemplo)
  - complementar con un ej. extra que haga lo mismo pero usando apply

* Cambiar parte d del útimo parcial: si el bus tiene el máximo de pasajeros no sube a más nadie y si tiene el mínimo (0) no baja nadie.

* Crecimiento exponencial ...?

* Caminata del borracho?

* Símil función preg?

* Loops con errores: un while que es infinito, un for que tiene mal puesto el rango, ...

- - -

1. Conteos por fila
-------------------

### 1.a Loop for

Suponga que usted debe regularmente analizar matrices con datos, con cantidades de filas variables y con varios datos faltantes (`NA`s) en ubicaciones imposibles de determinar de antemano. Una de las tareas que se le pide realizar cotidianamente es hacer un conteo de la cantidad de `NA`s *por filas* de la matriz. Para no tener que hacerlo manualmente, usted decide que lo mejor es crear un script de R con el cual hacer este conteo automáticamente.

Para hacer el script lo mejor es usar una matriz de prueba con la cual hacer pruebas. Para esto sirven las siguientes líneas (que también se encuentran en el script del ejercicio):


```r
# Generación de la matriz datos:
datos <- matrix(rpois(rpois(1, 125) * 15, 43), ncol = 15)
datos[sample(length(datos), rpois(1, 250))] <- NA
```


Para lograr su objetivo, usted deberá usar un loop `for`, con el cual completará el vector `out`, el cual contendrá las sumas de `NA`s por filas. Como un mini ejemplo, si su matriz `datos` es la siguiente:


```r
datos <- matrix(sample(100, 16), 4, 4)
datos[c(1, 3, 8, 11, 13, 14)] <- NA
datos
```

```
##      [,1] [,2] [,3] [,4]
## [1,]   NA   79   93   NA
## [2,]   63   76   32   NA
## [3,]   NA   45   NA   58
## [4,]   19   NA   88   22
```




Entonces el vector `out` será así:

```r
out
```

```
## [1] 2 1 2 1
```



### 1.b Extra: apply





Ejercicio 1: secuencia de Fibonacci
-----------------------------------

Ideada por el matemático italiano [Fibonacci](https://es.wikipedia.org/wiki/Fibonacci), la serie homónima se trata de una secuencia de números creada con una regla muy simple. Se trata simplemente de sumar los dos números anteriores para generar el siguiente, comenzando por el 0 y el 1. Así el tercer número es 1 = 1 + 0, el cuarto número es 2 = 1 + 1, el quinto número es 3 = 2 + 1, etc. Matemáticamente se puede describir como una secuencia $S$ que sigue la siguiente ecuación:

$$
  S_i = S_{i - 1} + S_{i - 2}
$$

y agregando la condición de que los valores iniciales $S_0$ y $S_1$ equivalen a 1. Así los primeros 10 números de la secuencia de Fibonacci son: 0, 1, 1, 2, 3, 5, 8, 13, 21 y 34.

### 1a. Calcular los valores del $S_0$ al $S_{20}$.

En este ejercicio usted deberá trabajar modificando el archivo `fibonacci.R`. En el mismo usted encontrará que el vector `fibo` es el designado para guardar los primeros 20 elementos de la secuencia. Para lograr hacer esta secuencia usted tendrá que crear un loop del tipo `for` con el número correcto de iteraciones. No olvide considerar que los primeros dos elementos de la secuencia ya están agregados al vector `fibo` a la hora de determinar el número de iteraciones así como los valores de `i` inicial e `i` final.

Puede comprobar que su resultado es correcto comparando la siguiente imagen, generada con los comandos:




```r
i <- 0:19
plot(fibo ~ i, main = "Secuencia de Fibonacci", ylab = expression(S[i]), xlab = "i")
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6.png) 


### 1b. Crear una función genérica

En esta parte del ejercicio usted trabajará modificando el archivo `funcionFibonacci.R`. El objetivo de este archivo es crear una función que calcule la secuencia de Fibonacci para una cantidad de números arbitraria. Tome en cuenta que el código es casi idéntico al contenido en el archivo `fibonacci.R`, pero debe ser modificado estratégicamente para que el argumento `n` modifique el resultado final.

Si usted ha modificado correctamente el archivo `funcionFibonacci.R` entonces el siguiente comando debería devolver el resultado que se muestra aquí:



```r
funcionFibonacci(13)
```

```
##  [1]   0   1   1   2   3   5   8  13  21  34  55  89 144
```


- - -

Parcial II
==========

#### Curso IMSER 2012

Instrucciones:
--------------

En el archivo “[parcial-II.R](http://eva.universidad.edu.uy/file.php/1454/ejercicios_de_programacion/parcial-II.R)” ud. tiene un script en el cual deberá guardar todos los comandos del ejercicio, siguiendo la demarcación que se muestra en el mismo.

Nota: los ejercicios del parcial son dependientes de los anteriores en el sentido de que utilizan objetos creados, pero no implica que no se puedan tratar de resolver independientemente.

Los ejercicios con (``*``) presentan un puntaje de 1.5, mientras que los que no tienen (``*``) equivalen a 1 punto.

Una vez terminado el parcial usted deberá subir a la [página del EVA](http://eva.universidad.edu.uy/mod/assignment/view.php?id=102998) el archivo “parcial-II.R” con su código.

- - -

Letra
-----

Para simular la cantidad de pasajeros de un ómnibus urbano se ha creado el código que aparece sobre el final del ejercicio (y que también se encuentra en el script parcial-II.R). El criterio es el siguiente: el bus recorre 25 paradas, empezando el trayecto sin pasajeros. En cada parada se subirá una cantidad aleatoria de entre 0 a 6 personas (siendo todas las cantidades equiprobables), pero debido a que existe un máximo estipulado de 44 pasajeros, a partir del momento en que se alcanza ese valor el vehículo deja de subir gente.

- - -

### (``*``) a. Código incompleto

Completar el código: las líneas en blanco que se encuentran dentro de los límites del código indican en dónde debe cambiarse. **El resto de las líneas están correctas**.

Código fuente:


```r
# Preparación:
paradas <- 25
pasajeros <- 0

registro[1] <- pasajeros
for (i in 1:paradas) {
    
    # A ver si no se llenó:
    if (pasajeros >= 44) 
        {
            # Ajuste por si llega a 44 antes de terminar:
            registro[i:paradas] <- 44
            cat("Bus lleno!\n")  # Mensaje de aviso...
            break
        }  # <- este no estaba
    
    # Si no se corta el loop, se agrega un nuevo registro:
    registro[i] <- pasajeros
    # Para ir viendo cuánto hay:
    cat("Parada", i, "hay", pasajeros, "pasajeros\n")
}
plot(registro, xlab = "Parada", ylab = "No. de pasajeros")
```


Sugerencias: (1) la función ``sample`` puede ser útil para simular la subida de pasajeros. (2) Tanto en este como en los siguientes ejercicios, en caso de no estar seguro/a de cómo proceder, puede facilitar mucho la tarea hacer un diagrama de flujo sencillo antes de empezar a escribir código.




La siguiente imagen se obtuvo haciendo la simulación, ejecutando previamente ``set.seed(11)`` y luego el comando gráfico:


```r
plot(registro, xlab = "Parada", ylab = "No. de pasajeros")
```

![plot of chunk unnamed-chunk-11](figure/unnamed-chunk-11.png) 


- - -

### b. Cambio de loop

Modifique el código de la parte anterior de forma tal que haga lo mismo, pero utilizando un loop ``while``.

Sugerencias: (1) agrege manualmente una variable (p.ej.: ``i``) que sirva para indexar los distintos objetos y recuerde actualizarla en la linea correcta del código y (2) usar un ``if`` posterior al loop puede ser útil para sustituir los ceros del final por 44 en el vector registro (aunque no es de ninguna manera el único método).

Nota: el gráfico que se dió en la parte anterior tamibén aplica para este ejercicio. 

### (``*``) c. Función ``bus``

Modifique el código reparado en la parte **a** para crear una función llamada ``bus`` que ejecute la misma simulación, en la que el número de paradas y capacidad máxima del bus sean los argumentos de la misma. El nombre de estos argumentos son a su elección.

Como salida la función debe devolver simplemente el vector ``registro``.

Nota: recuerde que esta función debe trabajar correctamente para cualquier elección del número de paradas y máximo de pasajeros. En el siguiente ejemplo se muestra un caso que puede servir de referencia:





```r
set.seed(11)
# Nro. de paradas = 40 Máximo de pasajeros = 80
x <- bus(40, 80)
```

```
## Parada 1 hay 1 pasajeros
## Parada 2 hay 1 pasajeros
## Parada 3 hay 4 pasajeros
## Parada 4 hay 4 pasajeros
## Parada 5 hay 4 pasajeros
## Parada 6 hay 10 pasajeros
## Parada 7 hay 10 pasajeros
## Parada 8 hay 12 pasajeros
## Parada 9 hay 18 pasajeros
## Parada 10 hay 18 pasajeros
## Parada 11 hay 19 pasajeros
## Parada 12 hay 22 pasajeros
## Parada 13 hay 28 pasajeros
## Parada 14 hay 33 pasajeros
## Parada 15 hay 38 pasajeros
## Parada 16 hay 42 pasajeros
## Parada 17 hay 45 pasajeros
## Parada 18 hay 47 pasajeros
## Parada 19 hay 48 pasajeros
## Parada 20 hay 51 pasajeros
## Parada 21 hay 52 pasajeros
## Parada 22 hay 56 pasajeros
## Parada 23 hay 58 pasajeros
## Parada 24 hay 60 pasajeros
## Parada 25 hay 60 pasajeros
## Parada 26 hay 63 pasajeros
## Parada 27 hay 65 pasajeros
## Parada 28 hay 65 pasajeros
## Parada 29 hay 65 pasajeros
## Parada 30 hay 67 pasajeros
## Parada 31 hay 70 pasajeros
## Parada 32 hay 72 pasajeros
## Parada 33 hay 74 pasajeros
## Parada 34 hay 75 pasajeros
## Bus lleno!
```

![plot of chunk unnamed-chunk-13](figure/unnamed-chunk-13.png) 


- - -

### d. Gente que también baja

Hacer una variante del código (de cualquiera de las partes anteriores) en la que además de subir personas, a partir de la parada 10 se bajen entre 1 y 5 pasajeros por parada. Tanto la subida y la bajada deben ejecutarse **antes** de determinar si se alcanzó el máximo estipulado de pasajeros y por lo tanto si debe dejar de detenerse el bus en las paradas.

Sugerencia: puede ser muy útil hacer un diagrama de flujo sencillo para planificar el código antes de escribirlo.

El siguiente es un ejemplo del resultado de aplicar los cambios que se piden en la función ``bus``:





```r
set.seed(11)
x <- bus(30, 60)
```

```
## Parada 1 hay 1 pasajeros
## Parada 2 hay 1 pasajeros
## Parada 3 hay 4 pasajeros
## Parada 4 hay 4 pasajeros
## Parada 5 hay 4 pasajeros
## Parada 6 hay 10 pasajeros
## Parada 7 hay 10 pasajeros
## Parada 8 hay 12 pasajeros
## Parada 9 hay 18 pasajeros
## Parada 10 hay 17 pasajeros
## Parada 11 hay 15 pasajeros
## Parada 12 hay 16 pasajeros
## Parada 13 hay 17 pasajeros
## Parada 14 hay 18 pasajeros
## Parada 15 hay 19 pasajeros
## Parada 16 hay 21 pasajeros
## Parada 17 hay 22 pasajeros
## Parada 18 hay 23 pasajeros
## Parada 19 hay 22 pasajeros
## Parada 20 hay 21 pasajeros
## Parada 21 hay 20 pasajeros
## Parada 22 hay 16 pasajeros
## Parada 23 hay 18 pasajeros
## Parada 24 hay 16 pasajeros
## Parada 25 hay 14 pasajeros
## Parada 26 hay 12 pasajeros
## Parada 27 hay 14 pasajeros
## Parada 28 hay 16 pasajeros
## Parada 29 hay 13 pasajeros
## Parada 30 hay 15 pasajeros
```

![plot of chunk unnamed-chunk-15](figure/unnamed-chunk-15.png) 

