
### 8b. ¿Es decidible que la clausura Kleene de un lenguaje CE es CE?

$$L^* = \cup_{i \geq 0} L^i$$

La clave es saber como trabajar con $\Sigma$ infinitos y recorrer todos los casos.

Para esto es útil la función de pares:
-- Hacemos una matríz con todas las posibles opciones al cuadro

[i \ i] 1 2 3 4 5 ...
1 
2 
3
4
5
...

Recorro todos los valores yendo por las diagonales.

Una funcion de pares asigna el orden para ser recorrido un elemento de la matriz L^2 
Vimos <x,y> = 2^x(2j +1) - 1 

Si hubiera una upla de tamaño mayor al dos,
se pueden armar 2uplas de, por ejemplo, <x, y, z> --> <x, <y,z>> o <<x, y>, z>

### ¿Cómo armo L*? (y cuento su cardinalidad)

Dado L computable (por ejemplo regular), quiero enumerar L*

### Enumerar $L$:
> Puedo contar L observando todas las posibles cadenas $\Sigma^*$ aceptadas por $L$ y las ordeno primero por longitud y luego lexicográficamente.
> Observación la validacion de si $\alpha \in \Sigma^* \in L$ la veo con un AFD sobre el cual valido cada cadena ordenada peretenece a $L$ (esto es computable mediante la funcion \delta porque asumo que el autómata representa un lenguaje computable). 

- Prop: Seguro $L$ regular tiene un automata e infinitos equivalentes

### Enumerar $L^2$:
> Opción 1: Hago el producto cartesiano de \Sigma* y me fijo si está o no, lo ordeno por ejemplo tambien lexicográficamente.
> $$(u,v) \in L² \iff \delta(q_0, u) \in F \land \delta(q_0, v)$$
> Opción 2: Me construyo el autómata de L²  (ver cómo se construye un autómata para lenguajes concatenados)

### Enumerar $L^i$:
> Enumeramos $\Sigma^i$ con
> $$(u_1, ..., u_i) \in Li \iff \delta(q_0, u_j) \in F \text{ para } j\in[1..i] \land \delta(q_0, v)$$

### ¿Cómo simulo un Automata de Pila con una MT no deterministica?
> Usando una MT de dos cintas, uno para la pila y otro para las transiciones.

- $L$ libre de contexto es computable por su automata de pila

### Automata de Pila a MT deterministica (libre de contexto -> computable)

#### Automata de Pila $\rightarrow$ MT no deterministica
Mirando un autómata de pila podemos simularlo secuencialmente en paralelo con una MT no deterministica con una cantidad de cintas igual a la máxima cantiddad de remificaciones del programa (mirando la funcion de transicion). 

#### MT no deterministica $\rightarrow$ MT deterministica
Hay equivalencia entre maquinas de turing no deterministicas y deterministicas. La demostracion sale con múltiples cintas para una MT (MT de mas cintas reconocen el mismo lenguaje que una de 1 cinta). Por ejemplo, una MT de 20 cintas se puede simular con una MT de 1 cinta partiendola en 40 partes (porque tenemos 20 cintas y 20 cabezas, es el doble de clases de equivalencia del no deterministico)

Idea para enumerar computablemente $L^i$:
- Obtenemos el $j$-esimo elemento de $(\Sigma^*)^i$, el cual es una tupla $(u_1, ..., u_i)$. Si $\prod_{k=1}^i (u_k \in L)$ entonces $u_1,.., u_i \in L^i$.
- $(u_k \in L) \text{ es computable por la hipótesis de L c.e.}$
- Hicimos $f:\mathbb{N} \rightarrow \mathbb{N}$ total computable e la forma 
$f(j) = \begin{cases}
(u_1, ..., u_i) & \text {si } \prod_{k=1}^i (u_k \in L) \\
\lambda  & \text { sino}
\end{cases}$

## Computablemente enumerable Vs Computable:
> Computable enumerable: No podemos saber si un elemento cualquiera está o no, pero podemos dar un orden. No tengo el automata pero tengo una funcion que dice si $\u_k \in L$, la cual se puede colgar.
> Computable: Si podemos |saber si está o no sin quedarse colgado.

Una palabra que está en L^i i finito lo puedo hacer mirando la palabra y dividiendola en distintos i framentos (todas las posibles divisiones).

8a. Verdadero

8b. Verdadero

> Enumero (\Sigma*)^i y produzco sus palabras con el orden definido (funcion de pares).
> Veo $\prod_{k=1}^i (u_k \in L)$. Esta funcion se puede colgar, lo cual no hay problema por que me pide que sea ce.
> No corro f(t) para no tildarme en un L^i sino que uso f(<j, t>) = "la j esima tupla corrida por t pasos"
> 1. Uso la funcion de pares para tomar la siguiente tupla en el orden
> 2. Valido la pertenencia 
> En realidad la f lo vemos con triplas f(i,j,t) con u e L^i (doble funcion de pares)

8c. Verdadero

8d. Verdadero

8e. Verdadero
Armar una transicion lambda entre estados finales de automatas de pila

8f. Verdadero. Das vuelta la palabra y chequeas

8g. Con el mismo programa que hicimos en 2

Ej 9] 

proc Kolm(s):
    i = 0
    while ( true ) {
        if halt (i) == 0 and psi(i) == s
            return i
        i += 1
    }

9b) verdadero

9c) verdadero. 

Idea 1: Vas enumerando y te da cada iteracion un programa el numero de programa no es creciente necesariamente, me quedo con el subconjunto de programas con codigo creciente en ese orden. Vemos que es computable porque la busqueda está acotada hasta el numero que le toca.

Es falso que todos los automatas de pila no deterministico admiten los mismos q los no deterministicos.

10a) Verdadero.

10b) Es falso.

Sale con el contraejemplo de 
L1: a^n b^n c^k 
L2: a^n b^k c^k

L1 ^ L2: a^n b^n c^n no es libre de contexto

10c) Falso.

10d) Si viendo que la diferencia simétrica de vacío.

11. Dar un algoritmo que codeterminice un autómata finito.

Es co-no-deterministico si a un estado le llegan multiples flechas con mismo simbolo.

Para ver si es codoterministico:
- Dar vuelta las flechas (asumo 1 estado final e inicial)
- Determinizo y veo que este nuevo automata reconoce el lenguaje reverso.
- Luego vuelvo a darle vuelta a las flechas y tengo el reverso del reverso (el original) y co-deterministico (quizas ya no deterministico).

12. 
Producto cartesiano de $Q_a x Q_p$
Usar la pila por el uso de $P$
Para la nueva funcion de transicion validar 
- $\delta_p: Q_p \times (\Sigma \cup {\lambda}) \times \Gamma \rightarrow P(Q \times \Gamma) $
- $\delta_a: Q_a \times (\Sigma \cup {\lambda}) \rightarrow Q_a $
- $\delta_{nueva}: Q_p \times Q_a \times (\Sigma \cup {\lambda}) \times \Gamma \rightarrow P(Q \times \Gamma) \times Q_a $

$$\delta_{nueva}((p,q), a, z) = ((r,w) \in \delta_p(a,z), s \in \delta_a(q,a))$$