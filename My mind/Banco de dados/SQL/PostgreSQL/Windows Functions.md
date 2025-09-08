----------

As Funções de Janela permitem que você execute cálculos em um conjunto de linhas (uma "janela") que estão relacionadas à linha atual. Diferente das funções de agregação, elas retornam um valor para cada linha, com base na janela definida.

------
### RANK()

SELECT id, produto, categoria, valor,
    RANK() OVER (PARTITION BY categoria ORDER BY valor DESC) as rank_por_categoria
FROM Vendas;

No exemplo acima, vemos que na query ela está rankeando os produtos pela categoria, 
e depois coloca em ordem decrescente o campo "valor".
Se duas linhas tiverem o mesmo valor na coluna ORDER BY, elas recebem o mesmo rank.

------------------
### ROW_NUMBER()

SELECT id, produto, categoria, valor,
    ROW_NUMBER() OVER (PARTITION BY categoria ORDER BY valor DESC) as row_num_por_categoria
FROM Vendas;

No exemplo acima, vemos que na query ela está ordenando os produtos pela categoria, 
e depois coloca em ordem decrescente o campo "valor".
Se duas linhas tiverem o mesmo valor na coluna ORDER BY, elas não recebem o mesma ordem.

----------
### LAG()

LAG(coluna_a_acessar, offset, valor_padrao)

1 = A coluna cujo valor você quer da linha anterior.
2 = offset: Quantas linhas para trás olhar (1 é a linha imediatamente anterior).
3 = valor_padrao (opcional): O valor a ser retornado se não houver linha anterior (no exemplo, 0.00). Se omitido, retorna NULL

SELECT id, produto, valor, data_venda,
    LAG(valor, 1, 0.00) OVER (PARTITION BY produto ORDER BY data_venda) as valor_venda_anterior
FROM Vendas;

A função LAG() permite acessar dados de uma linha anterior dentro da mesma partição, com base na ordem especificada.
É muito útil para comparar um valor com o valor da linha anterior (ex: calcular a diferença entre vendas de um mês e o mês anterior).

---------
### FIRST_VALUE() e LAST_VALUE()

FIRST_VALUE() retorna o valor da primeira linha em uma partição (com base na ORDER BY). 
LAST_VALUE() retorna o valor da última linha em uma partição.

SELECT
    id, produto, categoria, valor,
    FIRST_VALUE(valor) OVER (PARTITION BY categoria ORDER BY valor DESC) as maior_valor_na_categoria,
    LAST_VALUE(valor) OVER (PARTITION BY categoria ORDER BY valor DESC ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) as menor_valor_na_categoria
FROM Vendas;

Na query acima, vemos um filtro por categoria, onde o "First_value" retorna o valor do maior produto dentro daquela categoria
e o "Last_value" retorna o valor do menor produto dentro daquela categoria.
Essa linhas ficam se duplicam .
No "last_value" devemos usar mais essas variaveis para tudo ocorrer bem

------------
