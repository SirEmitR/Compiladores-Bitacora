
S -> iEtS | i E t S e S | a
Para factorzar utilizamos los terminos
```
	i E t S 
```

## Funciones
```

	instr -> id(lista-expr)
	lista-expr -> lista-expr, expr | expr

```
En este caso eliminamos la recursividad por la izquierda ya que **lista -expr** es recursiva
```
	lista-expr -> expr lista-expr'
	lista-expr' -> , expr lista-expr'
```

```
	I -> i E t I | i E t I e2 I | O
	I -> i E t I I' | O
	I' -> epsilon | epsilon I
```

```
	S -> Sb | Sbd | epsilon
	S -> Sb S' | epsilon
	S' -> epsilon | d

	S -> S''
	S'' -> bS'S'' | epsilon
```

### Ejercicio 
