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
### Group by

SELECT [cidade], [COUNT(id_cliente)] AS [total_clientes]
FROM [clientes]
GROUP BY [cidade];

GROUP BY
O comando GROUP BY é usado para agrupar linhas que têm os mesmos valores em uma ou mais colunas. Isso é frequentemente combinado com funções de agregação

---------------------

### Order by

ORDER BY é usado para classificar o conjunto de resultados de uma consulta em ordem crescente ou decrescente, com base em uma ou mais colunas.

SELECT [coluna1, coluna2] FROM [tabela]
ORDER BY [coluna_para_ordenar ASC | DESC]

ASC (Ascendente): Ordena do menor para o maior (padrão se nada for especificado).
DESC (Descendente): Ordena do maior para o menor.

---------
### Funções de agregação

Funções de Agregação realizam um cálculo em um conjunto de valores (um grupo de linhas) e retornam um único valor.

COUNT()  = Conta o número de linhas ou valores não nulos.
SUM()	 = Calcula a soma total de uma coluna numérica.
AVG()	 = Calcula a média de uma coluna numérica.
MIN()	 = Encontra o menor valor em uma coluna.
MAX()	 = Encontra o maior valor em uma coluna.

Ex: 
SELECT COUNT(*) AS [total_pedidos] FROM pedidos     = Conta quantos pedidos existem

-------
### Union

Os operadores UNION e UNION ALL são usados para combinar o conjunto de resultados de duas ou mais instruções SELECT em um único conjunto de resultados.

union     = Junta as colunas, evitando as duplicidades
union all = Junta as coluna

SELECT [coluna1], [coluna2] FROM [tabela1]
UNION | UNION ALL
SELECT [coluna1], [coluna2] FROM [tabela2]