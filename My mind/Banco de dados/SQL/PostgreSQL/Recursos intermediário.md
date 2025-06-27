----
### Filtro básico para 1 coluna

select [*] from table [where id = 1]           

### Filtro avançado para + 1 coluna

SELECT
  colun [FILTER] ([WHERE] status = 'ativo'),
  colun [FILTER] ([WHERE] status = 'inativo') 
FROM table

### Argumentos 

=                                                = Argumento "igual"
AND                                              = Argumento "e"
OR                                               = Argumento "ou"
IN                                               = Argumento "em"
NOT	                                             = Argumento "negação"
BETWEEN [x] AND [y]                              = Argumento "entre x e y"
IS NULL                                          = Argumento "é nulo"
IS NOT NULL                                      = Argumento "não é nulo"


----
### Relacionamentos no select

SELECT [t1.nome] FROM [table1 t1]
JOIN [table2 t2] ON [t1.id] = [t2.table1_id]

JOIN                                             = Somente a interseção
LEFT JOIN                                        = Todos da table da esquerda 
RIGHT JOIN                                       = Todos da table da direita
FULL JOIN                                        = Pega de ambas as tables
SELF JOIN	                                     = Pega a própria table

--------------


group
order by


funções de agregação