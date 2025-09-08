---------

Uma Common Table Expression (CTE) é um conjunto de resultados nomeado temporário que você pode referenciar dentro de uma única instrução SQL (SELECT, INSERT, UPDATE, DELETE). Elas são úteis para quebrar consultas complexas em partes menores e mais legíveis.

--------
### Sintaxe básica

WITH nome_da_cte AS (
    -- Sua consulta para definir a CTE aqui
    SELECT coluna1, coluna2 FROM tabela
)

-- Agora você pode consultar a CTE
SELECT * FROM nome_da_cte WHERE alguma_condicao;

--------------
### Sintaxe avançada

WITH
cte1 AS (
    SELECT ...
),
cte2 AS (
    SELECT ... FROM cte1 -- Pode referenciar CTEs anteriores
)
SELECT * FROM cte2;

----------------
### Exemplo 1° de uso

-- Usando CTE para encontrar o total de vendas por categoria e, em seguida, usar essa informação para ranquear as categorias.

WITH VendasPorCategoria AS (
    SELECT categoria, SUM(valor) as total_vendas
    FROM Vendas
    GROUP BY categoria
)

SELECT categoria, total_vendas,
    RANK() OVER (ORDER BY total_vendas DESC) as rank_categoria
FROM VendasPorCategoria;

--------

