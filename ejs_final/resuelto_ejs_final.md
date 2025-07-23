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
> biribiriasfse

¿Cómo valido $L(M) = \empty$?
>  aksdjiajdw


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
|-> $Q = \{(u, v, n, m) : u \in Q_1 \land v \in Q_2\}$
|-> $\delta(a, (u_1, v_1, n, m), (u_2, v_2, n+1, m+1)) \iff \delta_1(a, u_1, u_2) \land \delta_2(a, v_1, v_2)$
|-> $q_0 = (q_0^{(1)}, q_0^{(2)})$
|-> $F = \{ (u, v, n, m): u \in F_1 \land v \in F_2 \land n = m \}$

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
> Falso. Los autómatas de pila si pueden tener transiciones $\lambda$ ?????! (Duda)

5. Las maquinas de Turing determinısticas reconocen una cadena de longitud $n$ en exactamente $n$ transiciones.
> Falso. 

6. Sea $M$ un $AFD$ y sea $M^R$ el automata que resulta de revertir función de transición. $L(M)$ intersección $L(M^R)$ es regular.
> Verdadero. Sabemos que la intersección entre dos LR es LR y vale que $L^r$ es regular.

## Ejercicio 7. 

**Enunciado**
Decir Verdadero o Falso y justificar:

1. Toda funcion total de $\mathbb{N} \rightarrow \mathbb{N}$ es computable. 
> Falso. Por ejemplo `Halt'(x) = Halt(x,x)` 
> Duda: Halt en realidad es de $\mathbb{N} \rightarrow {0, 1}$, cambia la rsta?

2. El conjunto de funciones parcialmente computables de $\mathbb{N}$ en $\mathbb{N}$ es computablemente enumerable (c.e).
> Verdadero. Podemos listar estas funciones con numeros de programa las cuales pueden ser parcialmente computadas.

## Ejercicio 8.

**Enunciado**
Indicar V o F. Justificar:

1. La intersección de dos conjuntos c.e. es un conjunto c.e.
> Verdadero. Los conjuntos c.e. están cerrados por la unión e intersección. 

2. La clausura Kleene de un lenguaje c.e. es c.e.
> Verdadero.
Enumero $(\Sigma^*)^i$ y produzco sus palabras con el orden definido (funcion de pares).
Veo $\prod_{k=1}^i (u_k \in L)$. Esta funcion se puede colgar, lo cual no hay problema por que me pide que sea ce.
No corro $f(t)$ para no tildarme en un $L^i$ sino que uso $f(<j, t>) = \text{"la j esima tupla corrida por t pasos"}$
Primero uso la funcion de pares para tomar la siguiente tupla en el orden y despues valido la pertenencia.
En realidad la $f$ lo vemos con triplas $f(i,j,t)$ con $u \in L^i$ (doble funcion de pares)

3. La clausula de Kleene de un lenguaje computable es computable.
> Verdadero

4. La clausula de Kleene de un lenguaje regular es regular.
> Verdadero

5. La clausura de Kleene de un lenguaje libre de contexto es libre de contexto.
> Verdadero. Armar una transicion lambda entre estados finales de automatas de pila.

6. La reversa de un lenguaje computable es computable. 
> Verdadero. Invierto las cadenas y chequeo.

7. La reversa de un lenguaje ce es ce.
> Verdadero. Con el programa del ej 2.

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
Dado un autómata finito determinístico $A=(Q_A, \Sigma, \delta_A, q_0, F_A)$ y determinístico $P=(Q_P, \Sigma, \Gamma, \delta_p, p_0, F_P)$ dar un algoritmo que decida si el lenguaje $L(A) \cap L(P)$ es finito. Justificar correctitud.

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
Vemos que $L$ es LCC por ser union de dos LCC. aV
Vale que la unión de dos contadores es reconocible por un contador.
Vemos que $L^c$ no es reconocible por un contador mediante una propiedad más fuerte: 
$L \text{ LCC } \rightarrow L^c \text{ no es LCC}$. Luego si $L^c$ no es LCC no hay automata de pila que lo reconozca, mucho menos un contador.
Demo: Asumimos $L^c$ libre de contexto, luego su intersección con un lenguaje regular tambien es libre de contexto.
Por ejemplo $L^c \cap L(a^+b^+c^+)$ ...


B. Si dos lenguajes $L_A$ y $L_B$ son reconocidos por autómatas contadores, entonces el lenguaje de su unión también. 
> Verdadero.

C. Si dos lenguajes $L_A$ y $L_B$ son reconocidos por autómatas contadores, entonces el lenguaje de su intersección también.

D. Todos los lenguajes reconocibles por autómatas finitos  son reconocibles por autómatas contadores.

E. No todos los lenguajes reconocibles por un autómata contador son reconocibles por un autómata finito.

