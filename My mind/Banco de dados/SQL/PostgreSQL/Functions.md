-----
### Funções

Elas podem receber parâmetros de entrada, executar lógica (consultas, cálculos, manipulação de dados) e retornar um resultado.
```
CREATE OR REPLACE FUNCTION nome_da_funcao (parametro1 tipo, parametro2 tipo, ...)
RETURNS tipo_de_retorno AS $$
BEGIN
    -- Lógica da função
    RETURN valor_ou_tabela; 
END;
$$ LANGUAGE plpgsql;
```

select * from [nome()]          = Chama uma função
drop function [nome()]          = Deleta uma função

##### Parâmetros 

[nome] Tipo                     = Um parâmetro tem um nome e um tipo, "ex: idade 10"
 
#### Retorno

returns void                    = Sem retorno
returns tipo                    = Retorna um tipo/variavel ou mais
returns record                  = Retorna uma linha, "ex: nome, sobrenome, idade"
returns setof                   = Retorna uma coluna/tabela com valores
returns table([table...])       = Retorna uma tabela, especifique os campos

----------
#### Exemplos de funções
```
-- FUNÇÃO 1: Total de livros em estoque
CREATE OR REPLACE FUNCTION total_livro_estoque()
RETURNS INT AS $$
DECLARE
    total INT;
BEGIN
    SELECT SUM(estoque) INTO total FROM livros;
    RETURN COALESCE(total, 0);
END;
$$ LANGUAGE plpgsql;
```
Return colalesce(total, 0)  = Retorna o total, se for null, retorna 0 

```
-- FUNÇÃO 2: Listar autores e número de livros
CREATE OR REPLACE FUNCTION listar_autores_livros2()
RETURNS TABLE (autor VARCHAR, quantidade_livros BIGINT) AS $$
BEGIN
    RETURN QUERY
    SELECT a.nome, COUNT(la.livro_id)
    FROM autores a
    LEFT JOIN livrosautores la ON la.autor_id = a.id
    GROUP BY a.nome
    ORDER BY COUNT(la.livro_id) DESC;
END;
$$ LANGUAGE plpgsql;
```

```
CREATE OR REPLACE FUNCTION calcular_dobro(numero_original INT)
RETURNS INT AS $$
DECLARE
    -- Declara uma variável inteira para guardar o resultado
    resultado_dobro INT;
BEGIN
    -- Multiplica o número original por 2 e guarda na variável
    resultado_dobro := numero_original * 2;

    -- Retorna o valor que está na variável
    RETURN resultado_dobro;
END;
$$ LANGUAGE plpgsql;
```