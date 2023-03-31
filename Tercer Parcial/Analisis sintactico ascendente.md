 Comenzamos por los elementos que tenemos en la frase que vamos a analizar y se va contruyendo hacia arriba hasta nuestro **NO TERMINAL** inicial.

## Desplazamiento y Reduccion
> A este tipo de analisis se le comoce como **LR**
> El proceso de construccion de hojas a raiz se le nombra reduccion de la cadena w para obtener el simbolo inicial
```
	Suponga
	S -> a A B e
	A -> A b c | b
	B -> d
```
Generar la cadena ***a b b c d e*** (estas son las hojas)
Queremos llegar a S que es el simbolo inicial


Para remplazar buscamos cual de las producciones aparecen en la cadena. Le colocamos al lado izquierdo el simbolo
```
	Remplazaremos b
	a A b c d e
```
```
	Remplazaremos A b c
	a A d e
```
```
	Remplazaremos d
	a A B e
```
```
	Remplazaremos a A B e
	S
```
### Mangos
Un mango es una subcadena que concuerda con el lado derecha de una produccion y cuya reduccion al no  terminal del lado izquierdo representa un paso a la inversa de una derivacion por la derecha

#### Ejercicio
Suponga la gramatica
```
	E -> E + E
	E -> E * E
	E -> ( E )
	E -> id
```
Emepezamos con una pila vacia
Pila | Entrada | Accion
```
	$ | Id1 + Id2 * Id3$ | desplazar  Id1
	
	$Id1 |  | reducir E -> id
	
	$E | + Id2 * Id3$ | desplazar +

	$E + | Id2 * Id3$  | desplazo Id2

	$E + Id2 | * Id3$ | reducir E -> id

	$E + E | * Id3$ | reducir E + E

	$E | * Id3$ | desplazar *

	$E * | Id3$ | desplazar Id3$

	$E * Id3 | $ | reducir E -> id

	$E * E | $ | reducir E -> E * E

	$E | $ | aceptar	
```

### Acciones
- Desplazar
- Reducir
- Aceptar
- Error
### Conflictos

No podriamos analizar si mi gramatica es ambigua 
#### Desplazar/Reduccion
Puse un simbolo que ya no pude reducir
#### Reduccion/Reduccion
No sabe cual reduccion elegir

#### Analisis de casos de Conflicto
![[Pasted image 20230303144442.png]]

### Gramatica de operadores
> Es aquella donde no puedo tener 2 NO TERMINALES consecutivos
> Pero sustituyendo A en medio se obtiene una gramatica de operadores

Suponga

```
	E -> E A E | ( E ) | - E | id
	A -> = | - | * | / | ^ 
```

Sustituyendo A
```
	E -> E + E | E - E | E * E | E / E | E ^ E | ( E ) | - E | id
```
Se planytea una tecnica para determinar la precedencia utilizando relaciones de precedencias distintas 

```
<.
=.
.>
```

```
+ <. * En este caso * es mas relevante que +
* =. /
* .> -
```
![[Pasted image 20230303145338.png]]

#### Ejercicio

```
	$ id + id * id $
	
	Resultado
	
	$ <. id .> + <. id .> * <. id .> $
```

### Sacamos el Mango

```
	Sea
	E -> E + E | E - E | E * E | E / E | E ^ E | ( E ) | - E | id
	$ <. id .> + <. id .> * <. id .> $
	
	Buscamos el primer .>
	$ | <.  id   .> | + <. id .> * <. id .> $
	Buscamos el primer <.
	$ | <. id .> | + <. id .> * <. id .> $
	Esta seccion puede ser sustituida por E ya que E -> id
	$ <. E .> + <. id .> * <. id .> $
	---
	El resultado sera
	$ <. E .> + <. E .> * <. E .> $
	$ <. E .> + <. E .> $
	Sacamos los NO TERMINALES

	$ eliminando .>
	$ <. + <. * .> $
```

## Analisis con automara LR ( 0 )
Entendemos como LR(0) que tiene un PUNTO en cierta posicion de la produccion

Se utilza
- Estados : Desplazar o reducir

### Funcion de cerradura
Se utiliza para generar estados

### SLR Modelo LR Simple
![[Pasted image 20230303151105.png]]
![[Pasted image 20230303151323.png]]


![[Pasted image 20230303151411.png]]

```
 E' -> E 
 E -> E + T | T
 T -> T * F | F
 E -> ( E ) | id
```

### Ejemplo de Mangos


## Inicio
Al querer realizar un analisis sintactico LR
1. Extender la gramatica
```
	E' -> E
```
2. Ordenar las producciones para obtener reducciones
```
	(1) 
```
3. Empezar a construir nuestros estados aplicando reglas de cerradura
```
```
4. Conseguir Primeros y Siguientes
5. Construccion de la tabla
```
I0
	E' -> .E
Buscamos donde este E.
en este caso en el cruce de 0 con E obtendremos\
I1
	E' -> E.
```
## Reglas
Si S' produce S. Si esta en Ii  , en el cruce de i con pesos ponemos "Acptar"
ir_A ponemos los cruces donde tenemos .S o .Terminal


## Ejemplo bueno

S -> aA

A -> b

``` 1ro
	S' -> S Agregamos S'
	S -> aA
	A -> b
```

``` 2do
	Io:
		Agarramos el primer no terminal y le agregamos el .
		S' -> . S
	si hay un . y no terminal -> agregamos todas las producciones de ese no terminal al estado
		S -> . a A
	I1:
		Recorremos el punto a la derecha
		S' -> S .
	I2:
		S -> a . A
		A -> . b
	I3:
		S -> a A .
	I4: 
		A -> b .
```

``` 3ro
	Enumeramos el numero de producciones, que es el numero de reducciones
	1 ) S -> aA
	2 ) A -> b
```

Regla de OK en el cruce de $ con el estado donde me encuentre que el . este al final de mi simbolo inicial

``` 4to
	P(S) : {a}
	P(A) : {b}
	S(S) : {$}
	S(A) : {$}
```

Reducciones buscar en todos mis estados donde se encuentra el ppunto al final 

Para desplazar, busco un . terminal y localizo el estado con la misma produccion pero terminal .

Ir a es buscar donde haya . No terminal y se convierta en No terminal .
```
	| a | b | $ | S | A |
	0 d2| - | - |  1|   |
	1 - | - | ok|
	2 - | d4| - |   |  3|
	3 - | - | r1|
	4 - | - | r2|
```

```
	pila | cadena | accion
	0    | ab$    | d2
	0a2  | b$     | d4
	0a2b4| $      | r2
	Sustituimos con 2 ) A -> b
	0a2A | $      | 
	Vemos que hay 2 con A
	0a2A3| $      | r1
	0S1  | $      | ok
```


