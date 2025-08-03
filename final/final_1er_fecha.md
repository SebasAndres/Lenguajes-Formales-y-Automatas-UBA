# Final LFAyC (Fecha 1)

## Ejercicio 1.

**Enunciado**
Sea $\Sigma$ un alfabeto, $w=a_1..a_n \in \Sigma^*$.
$shift(w) = a_2..a_na_1$.
Dado un lenguaje $L \subset \Sigma^*$
$Shift(w)=\{ shift(w): w\in L \}$

Decidir:
a) $L \text{ regular} \rightarrow Shift(L) \text{ regular}$
b) $L \text{ LCC} \rightarrow Shift(L) \text{ LCC}$.

**Solución**

[A] *Verdadero* 
Podemos armar un autómata convirtiendo el original para que esto suceda.
El autómata queda de la siguiente forma:
$M=\langle \Sigma', Q', q_0', \sigma', F'\rangle$
Con:
    $\Sigma'=\Sigma$
    $Q' = Q \times \# \text{posibles simbolos iniciales } \cup \{q_0', q_f'\}$
    $q_0' = q_0'$
    $F'=\{ q_f' \}$
    $\delta' \text{ que cumpla los siguientes requisitos.. }$

La idea es que desde el primer estado inicial, para cada primer transición no $\lambda$ alcanzable desde $q_0$,
replicar el autómata, cambiar la transición por una $\lambda$ y extender un nuevo estado final único, al que cada estado final de las réplicas va a transicionar con la letra que originó la réplica. Esto es, si por ejemplo la primer transición era $a\in\Sigma$, entonces el anterior estado final va a apuntar al nuevo único $q_f'\in F'$ con el símbolo $a$.

[A] *Verdadero* 
La misma idea es válida, con algunas refinaciones.
Para cada símbolo inicial se replica el autómata, se cambia esa transición por una $\lambda | Z_0$ y se agrega en cada estado final $q_f$ de la réplica generada por el símbolo $a$ la transición $\delta(q_f, a, r) = (q_{f'}, \lambda) \text{ para } \forall r\in\Gamma$

## Ejercicio 2.
**Enunciado**
$A$ cjt. infinito ce de $\mathbb{N}$. Dar cjtos infinitos disjuntos de $A$.

**Solución**
Como $A$ es computable enumerable e infinito, existe una enumeración efectiva sin repeticiones de sus elementos:
$$A=\{a_1, a_2, ...\} \text{ con } a_i \neq a_j \iff j \neq i$$

Podemos definir $A_1, A_2$ como:
$A_1 = \{ a_{2i} : \forall i\in \mathbb{N}_0\}$
$A_2 = \{ a_{2i+1} : \forall i\in \mathbb{N}_0\}$

Es decir, $A_1$ contiene los elementos de $A$ en posiciones pares de la enumeración, y $A_2$ los de posiciones impares.
Luego vale que $A_1 \cap A_2 = \empty$, por lo tanto son disjuntos.
Además, como $A$ es infinito entonces $A_i$ lo son también.
