# Tema Segundo Parcial

### Funciones no computables y diagonalización

$$ f\text{ es computable } \iff \text{ existe programa en S++ que la computa } $$
$$\iff \text{ puedo expresar f como minimizacion o existencial acotado de un predicado P computable} $$

#### Predicados computables 
$\text{STEP}^{n}(e,t,x_1,...,x_n) : \N^{n+2} \rightarrow \N = \begin{cases} 
    1 & \text{si el programa e con los argumentos x1..xn termina tras t o menos pasos} \\
    0 & \text{cc}
\end{cases}$

$\text{SNAP}^{n}(e,t,x_1,...,x_n) : \N^{n+2} \rightarrow \N$
> Codifica la configuracion instantanea del programe de número e con entrada (x1..xn) en tiempo t

#### Interprete universal
$$\phi_e^{n}(x_1,...,x_n)$$

### Definición de HALT

$$\text{HALT}(x,y) = \begin{cases}
1 & \text{si } \phi_{y}(x) \downarrow \\
0 & \text{cc}
\end{cases}$$

$$\text{HALT}(x) = \begin{cases}
1 & \text{si } \phi_x(x) \downarrow \\
0 & \text{cc}
\end{cases}$$
 
### Demostrar que una funcion no es computable

#### Opción 1.
> [1] Aplicar reducción para que sea una funcion de una variable
> [2] Armo una funcion que dependa de la original y se indefina en algun caso.
> [3] Construyo un programa Q que computa la funcion negada
> [4] Evalúo Q con su código de programa y llego a un absurdo.

#### Opción 2.
Ver que una función no computable puede escribirse usando la función que queremos ver como no computable y otras operaciones si computables.

#### Opción 3. 
Definir a partir de la $f(n)$ dada una $g(n) = f(n) + 1$, asumiendo $f$ computable.
Ver que si $e$ es el numero del programa que codifica $g$, $g(e)$ lleva a una contradicción. 

### Teorema del parámetro

Para cada $n,m > 0$ hay una función total computable inyectiva $S_m^n : \N^{n+1}\rightarrow \N$ tal que:
$$\phi_y^{(n+m)}(x_1,..,x_m,u_1,..,u_n) = \phi_{S_m^n(u_1,..,u_n,y)}^{(m)}(x_1,...,x_m)$$

### Teorema de la recursión

Para toda $g:\N^{n+1} \rightarrow \N$ parcial computable, existen infinitos $e$ tal que
$$\phi_e^{(n)}(x_1,...,x_n) = g(e,x_1,...,x_n)$$

### Teorema punto fijo
Si $f:\N \rightarrow \N$ es computable, existe un $e$ tal que $\phi_{f(e)} = \phi_e$