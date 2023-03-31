## Gramtica
Conjunto de producciones que definen las reglas sintacticas de un lenguaje
## Recursividad
El **No terminal** esta a la izquiera de la produccion
### Eliminar recursividad
```
	F -> FhF | Fd | x
```
Selecciono los que no tienen recursividad
```
	F -> xF'
```
Seleccionamos los que tienen recursividad y los reescribimos
```
	F' -> hFF' | dFF' | epsilon
```
## Factorizacion
```
	H -> kHv | kr | kHr
```
Encontramos el **factor comun** 
```
	k
```
Reescribimos diciendo que el no terminal produce su **factor comun**
```
	H -> kH'
```
Generamos H' omitiendo H
```
	H' -> Hv | r | Hr
```


