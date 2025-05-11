# Lenguajes, Alfabetos

## Alfabetos

Alfabeto ($\Sigma$): Conjunto finito no vacio de simbolos

La palabra nula ($\lambda$) no tiene simbolos

Una palabra sobre el alfabeto $\Sigma$ es la concatenacion de elementos de una seq finita de simbolos.

### Clausulas de Alfabetos
- La clausula de Keene es:
    $\Sigma^* = \cup_{i>=0} \Sigma^i$
- La clausula de positiva es:
    $\Sigma^* = \cup_{i>=1} \Sigma^i$


Teo: La cantidad de lenguajes es no numerable.

$P(\Sigma^*) = \{ L \subset \Sigma^* \}$

#### Estructuras de cadenas:
* Dado un alfabeto $\Sigma$, toda cadena de $\Sigma^*$ corresponde a uno de los siguientes casos:
|-> $\lambda$
|-> $x \alpha$ con $x \in \Sigma, \alpha \in \Sigma^*$

#### Potencia de una cadena (n-esima potencia de un alfabeto Σ): 
Denota al conjunto de todas las cadenas de longitud exactamente n sobre Σ:
$$\alpha^0 = \lambda$$ $$\alpha^{n+1} = \alpha.\alpha^{n}$$

## Lenguajes

Lenguaje: Es un subconjunto de $\Sigma^*$ (culaquier forma de elegir un cjt de palabras da un lenguaje)

$\Lambda$: es el lenguaje que solo tiene a $\lambda$.

#### Operaciones sobre lenguajes: 
|-> Complemento: $L^c = \Sigma^* \ L$
|-> Union: $L_1 \cup L_2 = \{ \alpha \in \Sigma^* | \alpha \in L_1 \lor \alpha \in L_2 \}$
|-> Interseccion: ....
|-> Reverso: $L\subset \Sigma^* , L^r = \{ \alpha^r | \alpha \in L\}$
|-> Concatenacion: $L_1 . L_2 = \{ a.b | a \in L1 \land b \in L2 \}$
|-> Potencia: 
|--->    $L^0 = \Lambda$
|--->    $L^n = L. L^{n-1}$

#### Propiedades:
Tienen elemento neutro: la union, la interseccion, la concatenacion.
Tienen elemento absorbente la intersección y la concatenacion.
La concatenacion es asociativa pero no conmutativa.

### Demostraciones:
Se hacen con inducción estructural o sobre n en la estructura del lenguaje.

### Clausulas de Lenguajes
- La clausula de Keene es: 
    $L^* = \cup_{i>=0} L^i$
- La clausula de positiva es:
    $L^* = \cup_{i>=1} L^i$

### Prefijos, Sufijos, Subcadenas:
- ini(L)
- fin(L)
- sub(L)

### Definiciones
- Longitud