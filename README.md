= Mini TP - Memoria y Planificadores 
Adrián Romero <adrian.agustin.romero@proton.me>; Dylan Ponce <dylan18ponce2323@gmail.com>
:revdate: {docdate}
:revremark: COM-02
:version-label!:
:title-page:
:title-logo-image: image::image/ungs.png[]
:source-highlighter: coderay

== Memoria

En el presente trabajo práctico se analizan conceptos fundamentales de administración de memoria en sistemas operativos, aplicados a un entorno basado en una Raspberry Pi con arquitectura de 32 bits y sistema operativo Raspbian Buster Lite. A partir del consumo de memoria de un proceso de usuario, se busca comprender el funcionamiento de la paginación y su impacto en el uso de la memoria.

El sistema considerado utiliza un esquema de paginación con un tamaño de página de 8 KB. Dado que se trata de una arquitectura de 32 bits, las direcciones virtuales tienen una longitud total de 32 bits, lo cual permite analizar cómo se distribuyen entre número de página y desplazamiento

=== a) ¿Cuántos bits se necesitan para dar un número de página del proceso ejecutable_A?

Para responder esta pregunta, es necesario analizar cómo se compone una dirección virtual en un sistema paginado.

El tamaño de página es de 8 KB, lo que equivale a 8192 bytes, es decir, 
2¹³. Esto implica que se requieren 13 bits para representar el desplazamiento (offset) dentro de una página.

Dado que la dirección virtual total es de 32 bits, los bits restantes se destinan al número de página. Por lo tanto, se obtiene: 
32 - 13 = 19 bits

En consecuencia, se necesitan 19 bits para el número de página.

=== b) ¿Cuántos bits se necesitan para el desplazamiento dentro de un frame?

El desplazamiento dentro de un frame depende directamente del tamaño de la página.

Dado que el tamaño de página es de 8 KB (equivalente a 2¹³ bytes), se requieren 13 bits para poder direccionar cualquier posición dentro de una página.

Por lo tanto, el desplazamiento dentro del frame se representa con 13 bits.

=== c) ¿Cuántas páginas se asignan al proceso ejecutable_A?

El proceso ejecutable_A consume 128.05 MB de memoria. Para determinar la cantidad de páginas necesarias, primero se convierte este valor a kilobytes:

128.05 * 1024 = 131123.2 KB

Luego, se divide por el tamaño de página (8 KB):

131123.2 / 8 = 16390.4

Dado que no es posible asignar fracciones de página, se debe redondear hacia arriba. Por lo tanto, el proceso requiere un total de 16391 páginas.

=== d) ¿Hay fragmentación? Justificar.

Sí, existe fragmentación interna.

Esto se debe a que el tamaño del proceso no es múltiplo exacto del tamaño de página, lo que provoca que la última página asignada no se utilice completamente.

En este caso, solo se utilizan 3.2 KB de la última página, quedando sin usar 4.8 KB. Este espacio desperdiciado constituye la fragmentación interna del sistema.

Demostración:
A partir del cálculo previo, se obtiene que el proceso requiere un total de 16390.4 páginas. Esto implica que 16390 páginas se encuentran completamente utilizadas, mientras que la última página solo se ocupa parcialmente, en un 0.4 de su capacidad.

Dado que cada página tiene un tamaño de 8 KB, la porción utilizada de la última página es:

0.4 × 8 KB = 3.2 KB

Por lo tanto, el espacio restante dentro de esa página, que no es utilizado por el proceso, se obtiene restando este valor al tamaño total de una página:

8 KB − 3.2 KB = 4.8 KB

Este espacio no utilizado corresponde a la fragmentación interna, ya que pertenece a memoria asignada al proceso pero que no puede ser aprovechada.

=== En conclusion

Durante la resolución de este ejercicio no se presentaron mayores dificultades en el desarrollo de los cálculos. Sin embargo, como grupo se identificaron ciertas dudas en la interpretación de los enunciados y en la comprensión de algunos conceptos teóricos necesarios para su correcta aplicación. Estas dificultades fueron superadas mediante la revisión de los contenidos vistos en clase, lo que permitió resolver adecuadamente el punto de memoria.

== Planificadores
