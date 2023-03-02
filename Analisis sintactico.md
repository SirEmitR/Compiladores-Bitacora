## Manejo de errores
Objetivo:
- Informar de errores con claridad y exactitud
- Recuperarse del error al continuar
- No retrasar programas correctos

### Metodos
- LL 
	>Left Left
- LR
	>Left Rigth

## Estategias de recuperacion
- Modo panico
	Desechar simbolos de entrada hasta encontrar un componente lexico de sincronizacion
	Adecuado para cuando no hay errores multiples en la misma proposicion
- A nivel de fase
	Corregir con alguna cadena que permita continuar
- Produccion de error
- Correccion global

## Gramatica

Consiste en un conjunto de ***producciones*** que contienen ***terminales*** y ***no terminales*** y uno de ellos es reconocido como ***termino inicial***.

La sintaxis puede especificarse mediante gramaticas libres de contexto
	Aplicamos el algoritmo **BNF** - ***Backus Naur Form*** (libre de contexto)
	
Una gramtica permita  una evolucion iterativa de un lenguaje
Hya tres tipos de analizadores sintacticos para gramaticas
- Metodos universales: 
	>No son eficientes porque deben considerar muchas cosas
- ***Metodos desendentes***
	>Contruyen el arbol de la raiz a las hojas
- ***Metodos acendentes***
	> Comienza construccion del arbol de las hojas hacia la raiz

Los arboles no necesariamente se construyen como elementos no lineales sino que siguen representaciones  jererquicas que permiten la siguiente fase.

### Representacion de gramaticas
Para indicar la sintaxis de un ciclo **while**, por ejemplo podria generalizarse como 
```
	while (condicion) {(sentencia;)+}
```
> El token ***while*** indica basicamente por donde debemos comenzar a buscar las sintaxis de la sentencia

~~~
	E -> Expresion
	F -> Factor
	T -> Termino
	
	E -> E + T | T
	T -> T * F | F
	F -> (E) | id
~~~

### Gramatica LR
Significa que podemos sustituir un termino por otro

**Una gramtica es ambigua si puedo generar dos arboles o mas en una misma expresion**

~~~
	E -> E + E | E * E | (E) | id
~~~
La ambiguedad genera expresiones iguales, pero sin embargo obtendremos resultados difrerentes

~~~
	E 
	E + E
	id  E * E
		id  id
~~~

Gramatica de IF

instruccion -> **if** (expr) instruccion **else** instruccion

if , else son terminales 
instruccion y expr son variables sintacticas que pueden cambiar su valor en su totalidad

#### Producciones
Indican como se descrben combinar los terminales y no terminales para formar cadenas
Cada produccion se forma de:
- NO terminal 
- Simbolo de produccion (::=)
- Cuerpo
	- Combinaciones de terminales y/o no terminales
~~~
	E -> + T E
~~~
**E** es el termino inicial

#### Terminales
Generalmente los terminales se represnetan como 
- letras minusculas del alfabeto ***a, b, c***
- Operadores **+**, *
- Simbolos de puntuacion como parentesis, coma
- Digitos 
- Cadenas en negritas como **if** o **id**

#### No terminales
Generalmente los simbolos no terminales se representan como
- Letras mayusculas del alfabeto ***A, B, C***
- La letra S que, al aparecer, por lo heneral es el simbolo inicial
- Nombres en *cursiva* y minusculas como *expr* o *instr*

#### Terminles y no terminales
- Las ultimas letras del alfabeto en mayuscula ***X, Y, Z***
- Letras del alfabeto griego

Buscando id + id
~~~
	E 
	E + E
	id + E
	id + id
~~~

Buscando -id*(id+id)
~~~
	Gramtica: E -> E + E | E * E | - E | (E) | id

	E
	E * E
	- E * (E)
	- id * (E + E)
		  (id + id)
~~~


## Gramatica 