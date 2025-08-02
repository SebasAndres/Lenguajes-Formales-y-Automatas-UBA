# Resueltos final

## Ejercicio 1.
**Enunciado**: 
    Dar un algoritmo que decida si dos expresiones regulares denotan el mismo lenguaje. Justificar la correctitud.

**Solución**: 
    Sean $M_1$ y $M_2$ dos autómatas finitos.
    Queremos un algoritmo para ver si $L(M_1) = L(M_2)$
    Vemos que:
        Si $L(M_1) = L(M_2) \rightarrow L(M_1) \Delta L(M_2) = \empty$    
    Ademas:
        $L(M_1) \Delta L(M_2) = (L(M_1) - L(M_2)) \cup (L(M_2) - L(M_1))$ 
    Donde:
        $L_i - L_j$: Se computa como ...
        $L_i \cup L_j$: Se computa como ...

## Ejercicio 2.
**Enunciado**: 
    Dar dos algoritmos distintos para determinar si el lenguaje aceptado por un autómata finito dado es el conjunto de todas las cadenas del alfabeto. Justificar cada uno.

**Solución**: 

[1] Algoritmo 1:
 Para un autómata $M=<Q, \Sigma, \delta, q_0, F>$ queremos ver si $L(M) = \Sigma^*$.
 Vale que:
    Si $L(M) = \Sigma^* \rightarrow L(M)^c = \empty$
 Entonces basta en calcular $L(M)^c$.

¿Cómo calculo $L(M)^c$?
> Ver resumen parcial 1 (armado del autómata).

¿Cómo valido $L(M) = \empty$?
>  Manual. Es ver si el estado inicial o los estados finales no son alcanzables por transiciones no lambda desde el inicial.


[2] Algoritmo 2:
1. Eliminar los estados no alcanzables del grafo.
2. Vemos si hay algun estado final en los alcanzables (si lo hay entonces $L$ no es vació).
3. Entre los estados alcanzables nos quedamos con los finales $q_{f} \in F$ y vemos que deben cumplir:
    $$q_i \in F \iff \forall a \in \Sigma. \delta(q_f, a) \in F $$


## Ejercicio 3.
**Enunciado**
    Dar un algoritmo que determine si un lenguaje regular dado es infinito. Justificar.

**Solución**:

*Algoritmo 1:*

$L$ es infinito si tiene al menos 1 ciclo alcanzable por un camino que llega hasta un estado final.
Para detectarlo, podemos correr el autómata con DFS y anotar los estados visitados, si pasamos nuevamente por un nodo entonces hay un ciclo. 
En particular, si en el camino nos encontramos con un estado final, entonces el lenguaje es infinito.
Para evitar que siempre caigamos en la misma rama, podríamos alternar las ramas por las que empezamos si sabemos que hay un ciclo que no llega a estado final.

*Algoritmo 2:*

Vale la siguiente propiedad:
$$L \text{ es infinito } \iff \exists w \in L, N \leq |w| < 2N, \text { siendo N la constante del lema de Pumping}$$
Ya que implica que podemos bombear infinitas veces una subcadena de $w$, lo que la hace infinita.
Entonces, podemos geneVrar todas las posibles cadenas de $\Sigma$ con longitud entre $N$ y $2N$ y ver si alguna pertenece a $L$. Si al menos 1 pertenece, entonces $L$ es infinito.

¿Cómo obtengo la $N$ del lema de pumping?
|-> En Lenguajes Regulares es $|a|$.

## Ejercicio 4.
**Enunciado**
¿Cuántos autómatas finitos deterministas con dos estados pueden construirse sobre el alfabeto $\{0,1\}$?

**Solución**
$$\text{posiblesEstadosFinales} \times \text{posiblesEstadosIniciales} \times \text{posiblesFuncionesDeTransicion}$$

$$2^2 * 2 * 2^4 = 2^7$$

Donde la cantidad de funciones de transición sale por la propiedad:
$\# \{ \mathbb{f}: \mathbb{A} \rightarrow \mathbb{B} \} = |B|^{|A|}$

Luego, en este caso $\delta: Q \times \Sigma \rightarrow Q$
Entonces $\# f = |Q|^{|Q|*|\Sigma|} = 2^{2*2} = 2^4$

## Ejercicio 5.
**Enunciado**
Sean $L_1$ y $L_2$ lenguajes regulares incluidos en $\Sigma^∗$. 
Hacer un AFD con dos cintas de entrada que reconoce el lenguaje $L = \{ (u,v) : u \in L_1, v \in L_2, |u| = |v| \}$

**Solución**
$L_1 = <Q_1, \Sigma, \delta_1, q_0^{(1)}, F_1>$ 
$L_2 = <Q_2, \Sigma, \delta_2, q_0^{(2)}, F_2>$ 

$M = <Q, \Sigma, \delta, q_0, F>$ 
- $Q = Q_1 \times Q_2$
- $\Sigma = \Sigma \times \Sigma$
- $q_0 = (q_0^{1}, q_0^{2})$
- $\delta : Q \times (\Sigma \times \Sigma) \rightarrow Q$
- $\delta((q_1, q_2), (a,b)) = (\delta_1(q_1, a), \delta_2(q_2, b))$
- $F' = F_1 \times F_2$

## Ejercicio 6.

**Enunciado**
Decir Verdadero o Falso y justificar:

1. Para cada $AF$ hay infinitos $AFD$ que reconocen el mismo lenguaje.
> Verdadero. Es tan simple como agregar estados inalcanzables.

2. Si $L$ es libre de contexto (LLC), todo subconjunto de $L$ es libre de contexto.
> Falso. Un contraejemplo es: $L = \{ a^n b^k c^n | n \geq 1 \}$ es LCC pero 
    $L' = \{ a^n b^n c^n | n \geq 1 \}$

3. Los automatas finitos determinısticos reconocen una cadena de longitud $n$ en exactamente $n$ transiciones.
> Verdadero. Si es deterministico no tiene transiciones lambda.

4. Los automatas de pila determinısticos reconocen una cadena de longitud $n$ en exactamente $n$ transiciones.
> Falso. Los autómatas de pila pueden tener transiciones $\lambda$ por definición.

5. Las maquinas de Turing determinısticas reconocen una cadena de longitud $n$ en exactamente $n$ transiciones.
> Falso. A diferencia de un autómata finito (AFD) o un autómata de pila determinista (APD) que solo pueden moverse en una dirección sobre la entrada y típicamente leen cada símbolo una vez, una MT puede mover su cabeza en ambas direcciones. Esto significa que puede leer el mismo símbolo de la cinta múltiples veces, realizando muchas transiciones adicionales.

6. Sea $M$ un $AFD$ y sea $M^r$ el automata que resulta de revertir función de transición. $L(M)$ intersección $L(M^r)$ es regular.
> Verdadero. Sabemos que la intersección entre dos LR es LR y vale que $L^r$ es regular.

## Ejercicio 7. 

**Enunciado**
Decir Verdadero o Falso y justificar:

1. Toda funcion total de $\mathbb{N} \rightarrow \mathbb{N}$ es computable. 
> Falso. Por ejemplo `Halt'(x) = Halt(x,x)` y también se ve por cardinalidad.

2. El conjunto de funciones parcialmente computables de $\mathbb{N}$ en $\mathbb{N}$ es computablemente enumerable (c.e).
> Verdadero. Podemos listar estas funciones con numeros de programa las cuales pueden ser parcialmente computadas.

## Ejercicio 8.

**Enunciado**
Indicar V o F. Justificar:

1. La intersección de dos conjuntos c.e. es un conjunto c.e.
> Verdadero. Los conjuntos c.e. están cerrados por la unión e intersección. 

2. La clausura Kleene de un lenguaje c.e. es c.e.
> Verdadero.

La demostración se basa en construir una máquina de Turing que enumera las palabras de $L^*$. Lo hace generando sistemáticamente todas las tuplas finitas de palabras de $\Sigma^*$, verificando si todas las palabras de una tupla pertenecen a $L$ mediante una simulación paralela del enumerador de $L$, y si es así, imprimiendo su concatenación. Como $L$ es c.e., su "verificación" (aceptación) es semi-decidible. Esta construcción garantiza que todas las palabras de $L^*$ sean eventualmente enumeradas, probando que $L^*$ es c.e. La clave está en manejar la no terminación potencial de la verificación de $w \in L$ mediante simulaciones paralelas truncadas.

La enumeración sistemática de tuplas se puede lograr usando funciones de emparejamiento (pares, triplas, etc.). Por ejemplo, el conjunto de todas las tuplas finitas de números naturales es enumerable.

La función $f(i, j, t)$ mencionada en el esbozo representa esta simulación: ejecuta la $j$-ésima palabra en la consideración de $L^i$ durante $t$ pasos. Al iterar sobre $i, j, t$, eventualmente se simularán todas las palabras necesarias por suficientes pasos para aceptarlas si pertenecen a $L$.

#### Enumeración de Tuplas de Palabras de $\Sigma^*$

Queremos enumerar todas las tuplas finitas de palabras de $\Sigma^*$, es decir, $\bigcup_{i=0}^{\infty} (\Sigma^*)^i$.
*   **Paso 1: Codificación de una tupla fija.** Sea $i \ge 1$. Una $i$-tupla de palabras $(w_1, w_2, \ldots, w_i) \in (\Sigma^*)^i$ se puede codificar como una $i$-tupla de índices naturales $(n(w_1), n(w_2), \ldots, n(w_i)) \in \mathbb{N}^i$. Esta tupla de índices se puede codificar en un solo número natural usando la función de emparejamiento para $i$-tuplas, digamos $\text{code}_i(n(w_1), \ldots, n(w_i)) \in \mathbb{N}$.
*   **Paso 2: Codificación de tuplas de cualquier longitud.** Una tupla de longitud variable $(w_1, \ldots, w_i)$ se puede codificar como $\langle i, \text{code}_i(n(w_1), \ldots, n(w_i)) \rangle \in \mathbb{N}$.
*   **Paso 3: Enumeración.** Podemos enumerar todas las tuplas posibles simplemente enumerando los números naturales $t = 0, 1, 2, \ldots$. Para cada número $t$, "decodificamos" $t$ para obtener la longitud de la tupla $i$ y su código interno $c$. Luego, decodificamos $c$ para obtener los índices $n(w_1), \ldots, n(w_i)$, y finalmente usamos la función inversa $n^{-1}$ para obtener las palabras $w_1, \ldots, w_i$. Este proceso puede no ser sobre ni inyectivo si nuestras codificaciones no son perfectas, pero garantiza que cada tupla finita sea generada eventualmente.

**Relación con la Función $f(i, j, t)$ del Esbozo Original:**
*   La idea de $f(i, j, t)$ es una forma de implementar la simulación paralela.
*   $i$: Longitud de la tupla actual que se está considerando.
*   $j$: Índice (según alguna enumeración fija de las $i$-tuplas) de la tupla específica de palabras $(w_1, \ldots, w_i)$ que se está evaluando.
*   $t$: Número de pasos que se ejecuta cada simulación $M_L(w_k)$.
*   El algoritmo itera sobre $i=0, 1, 2, \ldots$. Para cada $i$, itera sobre $j=1, 2, \ldots$ (todas las $i$-tuplas). Para cada par $(i, j)$, itera sobre $t=1, 2, \ldots$.
*   En la iteración $(i, j, t)$, se decodifica $j$ para obtener la $j$-ésima $i$-tupla $(w_1, \ldots, w_i)$. Luego se simula $M_L(w_k)$ por $t$ pasos para cada $k=1, \ldots, i$.
*   Si para todos los $k$, la simulación de $M_L(w_k)$ ha aceptado dentro de los $t$ pasos (o en iteraciones anteriores), entonces $w_1, \ldots, w_i \in L$. Se calcula $w = w_1 \ldots w_i$ y se imprime.


3. La clausula de Kleene de un lenguaje computable es computable.
> Verdadero. 

```
Algoritmo Decididor_L^*(w):
Entrada: Cadena w ∈ Σ*
Salida: Acepta si w ∈ L^*, Rechaza si w ∉ L^*

1. Si w = ε (la cadena vacía), entonces aceptar.
    (Porque ε ∈ L^0 ⊆ L^* por definición).

2. Si w ≠ ε:
    a. Sea n = |w| (longitud de w).
    b. Generar todas las particiones posibles de w en subcadenas no vacías.
        (Una partición de w = a_1...a_n es una secuencia de índices 0 = i_0 < i_1 < ... < i_{k-1} < i_k = n,
        que define las subcadenas w_1 = a_{i_0+1}...a_{i_1}, ..., w_k = a_{i_{k-1}+1}...a_{i_k}).
        El número de tales particiones es finito (es 2^{n-1}).

    c. Para cada partición w = w_1 w_2 ... w_k (donde k ≥ 1 y cada w_i ≠ ε):
        i.  Para cada subcadena w_j (desde j=1 hasta k):
            - Ejecutar la máquina D_L sobre la entrada w_j.
            - Como D_L es un decididor, se detiene.
            - Si D_L rechaza w_j, entonces esta partición no es válida.
            Salir del bucle para las subcadenas (probar con la siguiente partición).
        ii. Si D_L aceptó todas las subcadenas w_1, w_2, ..., w_k:
            - Entonces w = w_1 w_2 ... w_k es una concatenación de cadenas de L.
            - Por lo tanto, w ∈ L^*.
            - Aceptar w.

3. Si después de revisar todas las particiones finitas posibles de w,
    ninguna resultó en que todas sus subcadenas fueran aceptadas por D_L,
    entonces w no se puede escribir como una concatenación de cadenas de L.
    Por lo tanto, w ∉ L^*.
    Rechazar w.
```

4. La clausula de Kleene de un lenguaje regular es regular.
> Verdadero. Los lenguajes regulares están cerrados por unión.

5. La clausura de Kleene de un lenguaje libre de contexto es libre de contexto.
> Verdadero. Armar una transicion lambda entre estados finales de automatas de pila.

6. La reversa de un lenguaje computable es computable. 
> Verdadero. Invierto las cadenas y chequeo.

7. La reversa de un lenguaje ce es ce.
> Verdadero. Con el programa del ej 2. Enumeras las cadenas y las invertis.

## Ejercicio 9.

**Enunciado**
Decir Verdadero o Falso y justificar:

1. Si $\text{halt}: \mathbb{N}^2 \rightarrow \mathbb{N}$ fuera computable, entonces la complejidad de Kolmogorov $C: \mathbb{N} \rightarrow \mathbb{N}$ lo sería. $C(s) = \min \{ \#(P) : \psi_P^{(0)} = s\}$  

~~~c
int Kolm(int s){
    i = 0;
    while (true) {
        if (halt(i) == 0 and _psi(i) == s)
            return i;
        i += 1;
    }
}
~~~

2. La pertenencia de una palabra a un lenguaje computable es computable.
> Verdadero.

3. Todo conjunto infinito c.e. tiene un subconjunto infinito computable.
> Verdadero.

Idea (no entendi mucho): Vas enumerando y te da cada iteracion un programa, el numero de programa no es creciente necesariamente, me quedo con el subconjunto de programas con codigo creciente en ese orden. Vemos que es computable porque la busqueda está acotada hasta el numero que le toca.

## Ejercicio 10.

**Enunciado**
Sea APD $P=(Q, \Sigma, \delta, \Gamma, q_0, F)$ y AP $S=(Q', \Sigma', \delta', \Gamma, q_0', F')$. Indicar V o F y justificar.

1. $L(P) \cup L(S) \text{ es libre de contexto}$ 
> Verdadero.

2. $L(P) \cap L(S) \text{ es libre de contexto}$
> Falso.
Sale con el contraejemplo de 
$L_1= a^n b^n c^k$
$L_2= a^n b^k c^k$
Pero:
$L_1 \cap L_2 = a^n b^n c^n$ no es libre de contexto

3. Para todo AP hay un APD que reconoce el mismo lenguaje.
> Falso.
La clase de lenguajes reconocidos por Autómatas de Pila Determinísticos (APD) es estrictamente menor que la clase de lenguajes reconocidos por Autómatas de Pila No Determinísticos (AP).
Autómatas de Pila No Determinísticos (AP o APN): Reconocen exactamente la clase de lenguajes libres de contexto (LC).
Autómatas de Pila Determinísticos (APD): Reconocen una subclase propia de los lenguajes libres de contexto, a veces llamados lenguajes libres de contexto determinísticos o LDCD (Del inglés, Deterministic Context-Free Languages)

4. Es decidible si dos AFs reconocen el mismo lenguaje o no.
> Verdadero. Viendo que la diferencia simétrica de vacío.

## Ejercicio 11.

**Enunciado**
Dar un algoritmo que codeterminice un autómata finito.

**Solución**
Es co-no-deterministico si a un estado le llegan multiples flechas con mismo simbolo.

Para ver si es co-deterministico:
- Dar vuelta las flechas (asumo 1 estado final e inicial)
- Determinizo y veo que este nuevo automata reconoce el lenguaje reverso.
- Luego vuelvo a darle vuelta a las flechas y tengo el reverso del reverso (el original) y co-deterministico (quizas ya no deterministico).

## Ejercicio 12.

**Enunciado**
Dado un autómata finito determinístico $A=(Q_A, \Sigma, \delta_A, q_0, F_A)$ y un autómata de pila determinístico $P=(Q_P, \Sigma, \Gamma, \delta_p, p_0, F_P)$ dar un algoritmo que decida si el lenguaje $L(A) \cap L(P)$ es finito. Justificar correctitud.

**Solución**
Vamos a ver que los autómatas de pila determinísticos están cerrados bajo intersección con los lenguajes regulares. El autómata resultante es un autómata de pila determinístico.

1. Calcular $A \cap P$.
2. Vemos si el lenguaje es finito con el algoritmo del Ej2. Se puede acotar la constante de pumping para LCC con otro algoritmo mencionado eb las teóricas.
3. Armamos el automata resultante:
$M=(Q_P \times Q_A, \Sigma, \Gamma, \delta_M, (q_0,p_0), F_P\times F_A)$
Con:
$\delta_M((q,p),a,z) = ((q_1,p_1),\gamma)$
Para:
$(q_1,p_1) \in Q_P \times Q_A$,
$\gamma \in \Gamma^*$,
$\delta_A(p,a) = p_1$,
$\delta_P(q,a,z) = (q_1, \gamma)$,

Vemos que $\delta_A((q_0,p_0), w, z_0) \in F_P \times F_A \iff w\in L(A) \cap L(P)$

## Ejercicio 13.

Un automata de pila no determinístico, $(Q, \Sigma, \Gamma, \delta, q_0, Z_0, F)$ es un contador si $\Gamma = {Z_0, I}$ el símbolo $Z_0$ representa el valor del cero y e $I$ representa el valor 1. En cada transición el autómata solamente puede consultar si el contador es 0 o no. El contador no puede volverse negativo, por lo que no puede restar el valor 1 de un contador que actualmente es 0.

**Enunciado**
Demostrar V o F:

A. Si un lenguaje es reconocible por un autómata contador, entonces el lenguaje complemento también.

> Falso. Un contraejemplo puede ser:
$$L=\{ a^i b^j c^k | i,j,k \geq 0 \land (i \neq j \lor i \neq k) \}
=\{ a^i b^j c^k | i,j,k \geq 0 \land i \neq j\} \cup \{ a^i b^j c^Ek | i,j,k \geq 0 \land i \neq k\} = L_1 \cup L_2$$
Vemos que $L$ es LCC por ser union de dos LCC. 
Vale que la unión de dos contadores es reconocible por un contador.
Vemos que $L^c$ no es reconocible por un contador mediante una propiedad más fuerte: 
$L \text{ LCC } \rightarrow L^c \text{ no es LCC}$. Luego si $L^c$ no es LCC no hay automata de pila que lo reconozca, mucho menos un contador.
Demo: Asumimos $L^c$ libre de contexto, luego su intersección con un lenguaje regular tambien es libre de contexto.
Por ejemplo $L^c \cap L(a^+b^+c^+)$ ...


B. Si dos lenguajes $L_A$ y $L_B$ son reconocidos por autómatas contadores, entonces el lenguaje de su unión también. 
> Verdadero.

C. Si dos lenguajes $L_A$ y $L_B$ son reconocidos por autómatas contadores, entonces el lenguaje de su intersección también.
> Verdadero.
Los **autómatas contadores** (también llamados *counter automata*) son una forma limitada de **máquinas de Turing** que, además del control finito, tienen uno o más contadores que pueden incrementarse, decrementarse y compararse con cero. Son más poderosos que los autómatas finitos y los autómatas con pila, pero menos poderosos que las máquinas de Turing completas (dependiendo de la cantidad de contadores).

Una propiedad importante de estos autómatas es que el **conjunto de lenguajes reconocidos por autómatas contadores es cerrado bajo intersección**.

Demo: Dados..
* $L_A$ es reconocido por un autómata contador $M_A$
* $L_B$ es reconocido por un autómata contador $M_B$

Podemos construir un nuevo autómata contador $M$ que **simule en paralelo** ambos autómatas $M_A$ y $M_B$, utilizando contadores independientes para cada uno (o combinando los contadores en una sola máquina si es necesario), y acepte una palabra solo si **ambos** autómatas la aceptan. Esto es similar a cómo se hace en la construcción del producto para autómatas finitos o de pila.

Por lo tanto:
$$
L_A, L_B \in \text{Counter Automata Languages} \quad \Rightarrow \quad L_A \cap L_B \in \text{Counter Automata Languages}
$$

Por ejemplo, se puede codificar el contador $a$ y $b$ con $n = 2^a 3^b$.

D. Todos los lenguajes reconocibles por autómatas finitos  son reconocibles por autómatas contadores.
> Verdadero, si ignora el contador.

E. No todos los lenguajes reconocibles por un autómata contador son reconocibles por un autómata finito.
> Verdadero. Por ejemplo $L = a^n b^n$ no es regular pero puede ser aceptado por un AP contador.

