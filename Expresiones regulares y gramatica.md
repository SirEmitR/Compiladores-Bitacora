
Conversion de un AFN a una gramatica
1. Para cada esytado *i* del AFN, crear un no terminal A~i~
2. Si el estado *i* tiene un atransicion al estado *j* con la entrada *a* , agregar la produccion Ai -> aAj. Si el estado *i* pasa al estado j con la entrada *epsilon*, agregar la produccion Ai -> Aj
3. Si *i* es un estado de aceptacon, agregar Ai -> *epsilon* 
4. Si *i* es el esyado inicial , hacer que Ai sea el simbolo inicial de la gramatica

