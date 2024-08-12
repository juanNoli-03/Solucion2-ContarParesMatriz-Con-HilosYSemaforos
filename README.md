<div id="user-content-toc">
  <ul align="center">
    <summary><h1 style="display: inline-block">Contar cantidad de Pares de una Matriz utilizando Hilos/Threads + Semáforos</h1>
    <h1 style="display: inline-block">Programación Concurrente</h1>
    </summary>
  </ul>
</div>

---

Como bien dice en la descripción del repositorio y en el titulo del README, el programa permite contar la cantidad de pares de una matriz utilizando Hilos/Threads e implementando el uso de los denominados 
Semáforos/Semaphores. En el mismo, tambíen se incluye la solución de manera Secuencial para que la misma pueda ser comparada con la solución Concurrente. 

**EXPLICACIÓN ACERCA DEL FUNCIONAMIENTO DEL PROGRAMA:**

- En primer lugar debemos tener en cuenta que, al trabajar con Hilos, debemos buscar la manera de que los Hilos que generemos trabajen en distintas regiones de nuestra matriz, ya que, si trabajan en las mismas, se
  generaría el gran problema de la concurrencia que es nada más y nada menos que la aparición de las denominadas "Regiones Críticas". Para abordar este primer problema, debemos decidir si los hilos se van a encargar
  de una determinada cantidad de renglones o columnas. En mi caso, elegí columnas.

- En segundo lugar, una vez que se decide lo anterior, hay que determinar de cuantas columnas/renglones se van a encargar los Hilos. Con lo dicho me refiero a que si, por ejemplo, tengo 20 columnas y 5 hilos, bueno,
  en ese caso, voy a poder hacer 20/5 y eso me da un total de 4 columnas por Hilo. Sin embargo, no siempre da exacto y depende de la cantidad de Hilos y Columnas que uno elija. En mi caso, la cantidad de Hilos es
  igual a la cantidad de Nucleos Logicos (Hilos = Runtime.getRuntime().availableProcessors()) de mi computadora (16), pero puede ser la cantidad de Hilos que uno quiera, siempre y cuando no sea mayor a la cantidad
  de núcleos que la coputadora de uno posee.

- En tercer lugar, una vez que uno decidió en que región de la matriz va a trabajar cada Hilo con el objetivo de evitar "Regiones Críticas" hay que realizar el trabajo propiamente dicho, que es, contar la cantidad
  de pares dentro de la matriz. Para eso, debemos desarrollar el metodo run() que es el metodo al cual se dirige el Hilo cuando es lanzado mediante el metodo start(). Cuando se desarrolla el metodo run (), en este
  caso, hay que tener una consideración importante que es la siguiente: ¿Si cada Hilo trabaja en una región determinada de la matriz, como hacemos para acumular la cantidad de pares cuando encuentran a uno? Para
  resolver ese problema, hay varias soluciones. Como expliqué en la <a href="https://github.com/juanNoli-03/Solucion1-ContarParesMatriz-Con-Hilos/tree/master">***solución1***</a> una alternativa puede ser crear un
  acumulador propio por cada Hilo y que cada uno vaya acumulando las apariciones en dicho acumulador. Esta solución no esta mal, pero también existen otras alternativas. Otra alternativa puede ser implementar a los
  denominados "Semáforos" que sirven para poder gestionar el acceso a un recurso compartido para evitar "Regiones Criticas". Cuando uno hace semaforo.acquire() basicamente hace referencia a que el recurso está siendo
  utilizado por un Hilo: le resta uno al semáforo y hace que todos los demas Hilos, esperen a que el mismo se libere. Cuando el recurso es utilizado, se libera mediante el semaforo.release() sumandole uno al semáforo
  y permitiendole al primer Hilo de la cola acceder al recurso. De esta maera, mediante el uso de este recurso podemos lograr acumular la cantidad de pares dentro de un acumulador general al cual todos los Hilos van
  a poder acceder de manera individual gracias a la implementación de los Semáforos.
  
- Por último y no menos importante, una vez que los Hilos terminan su trabajo (salen del run()) no hay que unificar los resultados como antes, ya que, utilizamos un acumulador general donde los Hilos fueron contando
  los pares que encontraban. Dicho esto, lo ultimo que hay que hacer es mostrarlo.
  
***Espero que la explicación se haya entendido! Muchas gracias!***
