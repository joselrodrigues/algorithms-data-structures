![Captura de pantalla 2023-04-17 a la(s) 16.14.05.png](attachment:45afb5d0-62e7-43a1-9765-578b15565e96.png)

## Common Big O Values

La notación Big O se utiliza para analizar y comparar algoritmos basándose en su eficiencia en términos de tiempo de ejecución y espacio de memoria. Esta notación permite identificar cómo el tiempo de ejecución y el espacio de memoria de un algoritmo pueden aumentar en función del tamaño de entrada 'n'. Es importante tener en cuenta que la notación Big O es una estimación del peor escenario posible, es decir, el tiempo máximo que podría tomar un algoritmo en función del tamaño de entrada.

A continuación, se muestran las complejidades más comunes en la notación Big O con una descripción más detallada:

O(1) - Constante: La complejidad del algoritmo no depende del tamaño de entrada. Independientemente de cuán grande o pequeño sea 'n', el tiempo de ejecución y el espacio de memoria permanecen constantes.

O(n) - Lineal: La complejidad del algoritmo aumenta de manera proporcional al tamaño de entrada. Si 'n' se duplica, el tiempo de ejecución y el espacio de memoria también se duplican. Un ejemplo común de complejidad O(n) es recorrer todos los elementos de una lista.

O(n^2) - Cuadrático: La complejidad del algoritmo aumenta al cuadrado del tamaño de entrada. Si 'n' se duplica, el tiempo de ejecución aumenta cuatro veces. Un ejemplo común de complejidad O(n^2) es el algoritmo de ordenación por burbuja.

O(log n) - Logarítmico: La complejidad del algoritmo aumenta logarítmicamente con respecto al tamaño de entrada. A medida que 'n' crece, el tiempo de ejecución y el espacio de memoria aumentan de manera más lenta. Un ejemplo común de complejidad O(log n) es la búsqueda binaria.

O(n log n) - Lineal-Logarítmica: La complejidad del algoritmo es una combinación de crecimiento lineal y logarítmico. Un ejemplo común de complejidad O(n log n) es el algoritmo de ordenación rápida (Quicksort).




### Performance tracker

https://rithmschool.github.io/function-timer-demo/


## Problem solving patterns

### Frecuency counter

El patrón Frequency Counter (Contador de Frecuencias) es una técnica de resolución de problemas comúnmente utilizada en algoritmos, especialmente en aquellos relacionados con la comparación de elementos en estructuras de datos como arreglos o cadenas. Este enfoque implica contar la frecuencia de aparición de elementos individuales en una estructura de datos y almacenar esos recuentos en una estructura de datos auxiliar, como un objeto o un mapa.

El objetivo principal del patrón Frequency Counter es evitar el uso de bucles anidados, lo que puede llevar a una complejidad de tiempo de ejecución alta, como O(n^2). Al utilizar un contador de frecuencias, la complejidad del tiempo de ejecución se reduce a menudo a O(n), lo que mejora significativamente la eficiencia del algoritmo.


```javascript
function same(arr1, arr2){
    if(arr1.length !== arr2.length){
        return false;
    }
    let frequencyCounter1 = {}
    let frequencyCounter2 = {}
    for(let val of arr1){
        frequencyCounter1[val] = (frequencyCounter1[val] || 0) + 1
    }
    for(let val of arr2){
        frequencyCounter2[val] = (frequencyCounter2[val] || 0) + 1        
    }
    console.log(frequencyCounter1);
    console.log(frequencyCounter2);
    for(let key in frequencyCounter1){
        if(!(key ** 2 in frequencyCounter2)){
            return false
        }
        if(frequencyCounter2[key ** 2] !== frequencyCounter1[key]){
            return false
        }
    }
    return true
}

same([1,2,3,2,5], [9,1,4,4,11])
```

    { '1': 1, '2': 2, '3': 1, '5': 1 }
    { '1': 1, '4': 2, '9': 1, '11': 1 }





    false



La función same toma dos arreglos como entrada, arr1 y arr2, y devuelve true si cada número en arr1 tiene un cuadrado correspondiente en arr2, con la misma frecuencia. De lo contrario, devuelve false. La función utiliza el concepto de contadores de frecuencia para realizar esta tarea de manera eficiente.

Aquí está el paso a paso de lo que hace la función:

Comprueba si la longitud de arr1 y arr2 es diferente. Si es así, devuelve false, ya que no pueden tener números cuadrados correspondientes en ese caso.
Crea dos objetos, frequencyCounter1 y frequencyCounter2, para almacenar la frecuencia de los números en arr1 y sus cuadrados en arr2, respectivamente.
Itera a través de arr1 y cuenta la frecuencia de cada número, almacenándola en frequencyCounter1.
Itera a través de arr2 y cuenta la frecuencia de cada número, almacenándola en frequencyCounter2.
Imprime en consola frequencyCounter1 y frequencyCounter2 para mostrar las frecuencias.
Itera a través de las claves en frequencyCounter1 y verifica si el cuadrado de la clave (key ** 2) está presente en frequencyCounter2. Si no lo está, devuelve false.
Si el cuadrado está presente en frequencyCounter2, verifica si la frecuencia del cuadrado en frequencyCounter2 es igual a la frecuencia del número original en frequencyCounter1. Si no es así, devuelve false.
Si todas las condiciones anteriores se cumplen, la función devuelve true.
En el ejemplo dado:


```bash
    same([1, 2, 3, 2, 5], [9, 1, 4, 4, 11])
```    
La función devuelve false. Esto se debe a que, aunque hay cuadrados correspondientes para algunos números (por ejemplo, 1, 2 y 3), el número 5 en arr1 no tiene un cuadrado correspondiente en arr2, y el número 11 en arr2 no tiene una raíz cuadrada en arr1. Además, la frecuencia de los números y sus cuadrados no coincide.

### Multiple pointers 

El patrón Multiple Pointers (Múltiples Punteros) es otra técnica de resolución de problemas utilizada en algoritmos, particularmente en aquellos que involucran estructuras de datos lineales como arreglos o cadenas. Este enfoque implica el uso de dos o más punteros, o variables que apuntan a diferentes posiciones dentro de la estructura de datos, para realizar comparaciones, búsquedas o cálculos sin necesidad de bucles anidados.

El objetivo principal del patrón Multiple Pointers es reducir la complejidad del tiempo de ejecución al evitar bucles anidados y, en su lugar, realizar operaciones utilizando punteros adicionales. Esto a menudo mejora la eficiencia del algoritmo, reduciendo la complejidad del tiempo de ejecución a O(n) o incluso O(log n) en algunos caso


```javascript
function countUniqueValues(arr){
    if(arr.length === 0) return 0;
    var i = 0;
    for(var j = 1; j < arr.length; j++){
        if(arr[i] !== arr[j]){
            i++;
            arr[i] = arr[j]
        }
    }
    return i + 1;
}
countUniqueValues([1,2,2,5,7,7,99])
```




    5



La función countUniqueValues toma un arreglo ordenado arr como entrada y devuelve la cantidad de valores únicos presentes en el arreglo. La función utiliza el patrón de Múltiples Punteros para lograr esto de manera eficiente.

Aquí está el paso a paso de lo que hace la función:

Si la longitud del arreglo es 0, devuelve 0, ya que no hay valores únicos en un arreglo vacío.
Crea dos punteros, i y j. Inicializa i en 0 y j en 1. Estos punteros se usarán para comparar los elementos adyacentes en el arreglo.
Comienza un bucle for que recorre el arreglo desde el segundo elemento hasta el último elemento (índice j).
Dentro del bucle, compara los elementos en las posiciones i y j. Si los elementos son diferentes (arr[i] !== arr[j]), significa que se ha encontrado un nuevo valor único.
Si se encuentra un nuevo valor único, incrementa i en 1 e iguala el elemento en la posición i al elemento en la posición j. Esto asegura que el arreglo esté actualizado con los valores únicos encontrados hasta ahora.
Si los elementos en las posiciones i y j son iguales, el bucle continúa con el siguiente índice j.
Repite los pasos 4-6 hasta que el bucle termine.
Devuelve i + 1, que representa la cantidad de valores únicos en el arreglo.
En el ejemplo proporcionado:
```bash
countUniqueValues([1, 2, 2, 5, 7, 7, 99])
```
La función devuelve 5, ya que hay 5 valores únicos en el arreglo: 1, 2, 5, 7 y 99. Al usar el patrón de Múltiples Punteros, la función evita bucles anidados y resuelve el problema con una complejidad de tiempo de ejecución de O(n).

### Sliding Window

El patrón Sliding Window (Ventana Deslizante) es una técnica de resolución de problemas utilizada en algoritmos que involucran estructuras de datos lineales, como arreglos o cadenas. Este enfoque consiste en crear una "ventana" o subconjunto de elementos dentro de la estructura de datos y desplazarla a lo largo de la estructura mientras se realizan cálculos o comparaciones en los elementos contenidos en la ventana. La ventana puede ser de tamaño fijo o variable, dependiendo del problema en cuestión.

El objetivo principal del patrón Sliding Window es mejorar la eficiencia del algoritmo al evitar la necesidad de recalcular ciertos valores o repetir operaciones en cada paso del proceso. En lugar de utilizar bucles anidados, que pueden llevar a una alta complejidad en el tiempo de ejecución (como O(n^2)), el patrón Sliding Window a menudo reduce la complejidad a O(n).


```javascript
function maxSubarraySum(arr, num){
  let maxSum = 0;
  let tempSum = 0;
  if (arr.length < num) return null;
  for (let i = 0; i < num; i++) {
    maxSum += arr[i];
  }
  tempSum = maxSum;
  for (let i = num; i < arr.length; i++) {
    tempSum = tempSum - arr[i - num] + arr[i];
    maxSum = Math.max(maxSum, tempSum);
  }
  return maxSum;
}

maxSubarraySum([2,6,9,2,1,8,5,6,3],3)
```




    19



La función maxSubarraySum toma un arreglo de números arr y un número entero num como argumentos, y devuelve la suma máxima de num elementos consecutivos en el arreglo. La función utiliza el patrón Sliding Window (Ventana Deslizante) para lograr esto de manera eficiente.

Aquí está el paso a paso de lo que hace la función:

Inicializa las variables maxSum y tempSum en 0. maxSum almacenará la suma máxima encontrada hasta ahora, mientras que tempSum almacenará la suma de los elementos en la ventana actual.
Si la longitud del arreglo arr es menor que num, no hay suficientes elementos para calcular una subsuma, por lo que la función devuelve null.
Utiliza un bucle for para calcular la suma de los primeros num elementos del arreglo y asigna este valor tanto a maxSum como a tempSum.
Comienza otro bucle for que recorre el arreglo desde el índice num hasta el final del arreglo.
En cada iteración del bucle, actualiza tempSum restando el primer elemento de la ventana actual (arr[i - num]) y sumando el siguiente elemento fuera de la ventana (arr[i]). Esto desliza la ventana hacia adelante.
Compara tempSum con maxSum y actualiza maxSum si tempSum es mayor, utilizando la función Math.max().
Repite los pasos 5 y 6 hasta que el bucle termine.
Devuelve maxSum, que representa la suma máxima de num elementos consecutivos en el arreglo.
En el ejemplo proporcionado:

```bash
maxSubarraySum([2, 6, 9, 2, 1, 8, 5, 6, 3], 3)
```
La función devuelve 19, ya que la suma máxima de 3 elementos consecutivos en el arreglo es 9 + 2 + 8 = 19. Al utilizar el patrón Sliding Window, la función evita bucles anidados y resuelve el problema con una complejidad de tiempo de ejecución de O(n).


```javascript

```
