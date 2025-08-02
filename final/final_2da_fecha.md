# Final automatas y computabilidad

### Ejercicio 1.

**Enunciado**
Dada una expresion regular, dar un algoritmo que da una cota superior a la cantidad de estados del automata finito no deterministico con transiciones lambda que acepta el lenguaje dado por el regex pasado.

**Solución**

Vale el siguiente teorema..
> Teorema: Para cada expresion regular $r$ hay un AFND-λ $M$ con un solo estado final y sin transiciones de salida tal que $r = L(M)$.

Nos interesa acotar la cantidad de nuevos estados agregados para cada posible ER ($n(r)$), para eso hacemos inducción en la estructura de una expresión regular.

$$r = \empty | \lambda | a | r_1r_2 | r^* | r^+ | (r_1|r_2)$$

Casos base:
- Si $r=\empty$, con 1 estado basta.
- Si $r=\lambda$, con 1 estado basta.
- Si $r=a$, con 2 estados basta ($q_0 \xrightarrow{a} q_1$).

Paso inductivo:
- Si $r=r_1r_2$, sea $n(r_i)$ la cota necesaria de estados para cada uno, entonces basta con $n(r_1) + n(r_2)$ estados.
- Si $r=r^*$, entonces necesito $n(r*) = 2+n(r)$ estados (nuevo inicial y final con $\lambda$), porque el final no tendría flechas de salida.
- Si $r=r^+$, similarmente necesito dos estados.
- Si $r=r_1|r_2$, sea $n(r_i)$ la cota necesaria de estados para cada uno, entonces basta con $2+n(r_1)+n(r_2)$ estados.

Luego, el algoritmo podría ser:
- Descomponer iterativamente $r$ según su estructura y acotar recursivamente por 1 (o 2 según el caso) la cantidad de estados necesaria para representar la ER.

Esto es computar la funcion definida por induccion en la estructura de las ER:
$n(r) = \begin{cases}
    1 & \text{ si } r = \lambda \\
    1 & \text{ si } r = a \in \Sigma \\
    n(s)+n(t) & \text{ si } r = st \\
    n(s)+n(t)+2 & \text{ si } r = s|t \\
    n(r)+2 & \text{ si } r = r^* \\
    n(r)+2 & \text{ si } r = r^+ \\
\end{cases}$

Observaciones:
- Si $r=\empty$, entonces el unico estado no debe ser final, lo cual contradice el teorema, entonces este caso esta fuera del teorema.
- Si $r=\empty$, entonces cualquier autómata sin estados finales acepta $L(r)$. Podemos usar un estado inicial no final, luego $n(r)=1$.

### Ejercicio 2.

**Enunciado**
Demostrar Verdadero o Falso:
Sea $S^{++}$ el lenguaje de programacion de maquinas de Turing, llamamos $\psi_P^{(m)}(r_1, ..., r_m)$ a la funcion parcialmente computable que realiza el programa $P$ con entradas $r_1,...r_m$.
Sea $f: \mathbb{N} \rightarrow \mathbb{N}$, $f(n)=min\{ \#P : \psi_P^{(0)} = n \} = C(n)$. 
Entonces el conjunto $A \subset \mathbb{N} \times \mathbb{N}, A=\{ (n,p): p > f(n), n \geq 0 \}$ es computablemente enumerable.

**Solución**

Vemos que $f(n)$ da el código de programa más chico, con cero parametros, que devuelve $n$, es una **función de Kolmogorov**.

Además, $A$ representa las tuplas $(n,p)$, con $n \in \mathbb{N}_0$ y $p$ un programa mayor a ese número.

Recuerdo:
$$A \text{ ce } \iff \exists f: \mathbb{N} \rightarrow \mathbb{N} \text{ parcial computable tal que } A = \{ x: f(x)\downarrow \}$$

Veo que puedo encontrar una cota mínima de $p$ para cada $n$ simplemente armando el programa más sencillo
que devuelva $n$

``` c
// Sea P el código de programa de esto
X = 0;
while (X != N) {
    X++;
}
Y = X;
```

Luego $\forall m > P$ vale que $(N, m) \in A$.

Ahora, ¿cómo encuentro los $p<P$ que cumplen $(N, p) \in A$?
> Esto es chequear casos finitos, códigos de programa $P' = 0..P-1$.
 No obstante, no se si alguno de ellos se va a colgar al ejecutar $\psi_{P'}^{(0)}$.  
 Sin embargo, esto lo puedo hacer ejecutando todos los programas en paralelo (dovetailing).
 Cada vez que encuentro un programa $k \in 0..P-1$ que termina y devuelve $n$, como $k<P=C(n)$.
 Entonces, todos los $p'>k$ cumplen $p>f(n)$, luego $(n,p)\in A$.

