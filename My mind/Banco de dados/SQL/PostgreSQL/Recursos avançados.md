
---
### Simple view 

Uma simple view é basicamente uma consulta SQL salva, literalmente um select pronto, e que se mantem atualizado com o banco.

create view [name] as [select...]               = Cria uma view
create or replece view [name] as [select...]    = Cria ou altera uma view
drop view [name]                                = Exclui uma view

---

### Materialized view  

Praticamente uma simple view, porém seus dados não se atualizam, ou seja, a ultima atualização será no momento de criação. Ela praticamente se torna independente do resto do banco.

create materialized view [name] as [select...]              = Cria uma view materializada
create or replece materialized view [name] as [select...]   = Cria ou altera uma view materializada
drop materialized view [name]                               = Exclui uma view materializada
Refresh materialized view [name]                            = Atualiza a view com os dados atuais

----------

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
----------
### Procedures

Procedure é uma função sem retorno.

call [nome()]                  = Chama/Executa a procedure
drop procedure [nome()]        = Deleta uma procedure

```
-- PROCEDURE 1: Adicionar ao estoque
CREATE OR REPLACE PROCEDURE adicionar_estoque(titulo_livro VARCHAR, quantidade INT)
LANGUAGE plpgsql AS $$
DECLARE
    livro_id INT;
BEGIN
    IF quantidade <= 0 THEN
        RAISE EXCEPTION 'A quantidade deve ser positiva.';
    END IF;

    SELECT id INTO livro_id FROM livros WHERE titulo = titulo_livro;
    IF NOT FOUND THEN
        RAISE EXCEPTION 'Livro não encontrado.';
    END IF;

    UPDATE livros SET estoque = estoque + quantidade WHERE id = livro_id;
    RAISE NOTICE 'Estoque atualizado com sucesso!';
END;
$$;
```

```
-- PROCEDURE 5: Registrar venda
CREATE OR REPLACE PROCEDURE registrar_venda(livro_id INT, qntd INT)
LANGUAGE plpgsql AS $$
DECLARE
    novo_estoque INT;
    preco_unit NUMERIC(10,2);
BEGIN
    IF qntd <= 0 THEN
        RAISE EXCEPTION 'Quantidade deve ser positiva.';
    END IF;

    UPDATE livros SET estoque = estoque - qntd
    WHERE id = livro_id AND estoque >= qntd
    RETURNING estoque, preco INTO novo_estoque, preco_unit;

    IF NOT FOUND THEN
        IF NOT EXISTS (SELECT 1 FROM livros WHERE id = livro_id) THEN
            RAISE EXCEPTION 'Livro não encontrado.';
        ELSE
            RAISE EXCEPTION 'Estoque insuficiente.';
        END IF;
    END IF;

    INSERT INTO Vendas (livro_id, qnt_venda, total_venda)
    VALUES (livro_id, qntd, preco_unit * qntd);
    RAISE NOTICE 'Venda registrada com sucesso.';
END;
$$;
```

#### Exceções

RAISE NOTICE           = Exibe uma mensagem
RAISE WARNING          = Exibe uma mensagem de problema que pode não ser fatal, mas merece atenção.
RAISE INFO             = Exibe uma mensagem menos importantes que um NOTICE.
RAISE LOG              = Exibe uma mensagem de log detalhadas
RAISE DEBUG            = Mensagens de depuração muito detalhadas.
RAISE EXCEPTION        = Exibe uma mensagem, e interrompe o processo.

------------
### Triggers

Uma Trigger (ou gatilho) é um bloco de código, geralmente uma função, que é executado automaticamente em resposta a um evento específico em uma tabela.

drop trigger [trigger] on [table]                    = Exclui uma trigger
alter table [table] disable trigger [trigger]        = Desativa uma trigger
alter table [table] enable trigger [trigger]         = Ativa uma trigger

 -=-=-=-=-=-=-=-=-=-=-[Exemplo 1]
```
CREATE OR REPLACE FUNCTION log_alteracao_preco()
RETURNS TRIGGER AS $$
BEGIN
    -- OLD: Variável especial que representa a linha ANTES da modificação (para UPDATE/DELETE)
    -- NEW: Variável especial que representa a linha DEPOIS da modificação (para INSERT/UPDATE)

    IF OLD.preco IS DISTINCT FROM NEW.preco THEN -- Verifica se o preço realmente mudou
        INSERT INTO historico_precos (
            produto_id,
            preco_antigo,
            preco_novo,
            data_alteracao,
            usuario_alteracao
        ) VALUES (
            NEW.id,
            OLD.preco,
            NEW.preco,
            NOW(),
            current_user -- Usuário que executou a operação
        );
    END IF;

    RETURN NEW; -- Importante: para triggers AFTER, geralmente RETURN NEW;
                -- Para triggers BEFORE, você pode modificar NEW e retornar NEW.
END;
$$ LANGUAGE plpgsql
```

```
CREATE TRIGGER trig_preco
AFTER UPDATE ON produtos            -- Quando deve disparar: DEPOIS de um UPDATE na tabela 'produtos'
FOR EACH ROW                        -- Para cada linha afetada pelo UPDATE
EXECUTE FUNCTION alteracao_preco() -- A função que será executada
```
-----

-=-=-=-=-=-=-=-=-=-=-[Exemplo 2]
```
CREATE OR REPLACE FUNCTION padronizar_usuario()
RETURNS TRIGGER AS $$
BEGIN
    -- Converte o email para minúsculas antes de inserir
    NEW.email := LOWER(NEW.email);

    -- Se data_cadastro não foi fornecida, preenche com a data/hora atual
    IF NEW.data_cadastro IS NULL THEN
        NEW.data_cadastro := NOW();
    END IF;

    RETURN NEW; -- É CRUCIAL retornar NEW para triggers BEFORE INSERT/UPDATE
                -- pois NEW é o registro que será realmente inserido/atualizado.
END;
$$ LANGUAGE plpgsql;
```

```
CREATE TRIGGER trigger_usuario
BEFORE INSERT ON usuarios           -- Dispara ANTES de cada INSERÇÃO na tabela 'usuarios'
FOR EACH ROW                        -- Para cada linha que está sendo inserida
EXECUTE FUNCTION padronizar_usuario();
```
-----------

-=-=-=-=-=-=-=-=-=-=-[Exemplo 3]
```
CREATE OR REPLACE FUNCTION limpar_itens_pedido()
RETURNS TRIGGER AS $$
BEGIN
    -- OLD.id_pedido refere-se ao ID do pedido que acabou de ser EXCLUÍDO.
    DELETE FROM itens_pedido
    WHERE id_pedido = OLD.id_pedido;

    RETURN OLD; -- Para triggers AFTER DELETE, geralmente se retorna OLD.
END;
$$ LANGUAGE plpgsql;
```

```
CREATE TRIGGER trig_limpar_itens_pedido
AFTER DELETE ON pedidos             -- Dispara DEPOIS de cada EXCLUSÃO na tabela 'pedidos'
FOR EACH ROW                        -- Para cada linha de pedido que foi excluída
EXECUTE FUNCTION limpar_itens_pedido();
```
-------------

-=-=-=-=-=-=-=-=-=-=-[Exemplo 4]
```
CREATE OR REPLACE FUNCTION registrar_data_conclusao()
RETURNS TRIGGER AS $$
BEGIN
    -- Verifica se o status mudou para 'concluido'
    -- E se o status anterior não era 'concluido' (evita atualizações repetidas)
    IF NEW.status = 'concluido' AND OLD.status IS DISTINCT FROM 'concluido' THEN
        UPDATE pedidos
        SET data_conclusao = NOW()
        WHERE id_pedido = NEW.id_pedido;
    END IF;

    RETURN NEW; -- Retorna NEW, que é o registro após a atualização.
END;
$$ LANGUAGE plpgsql;
```

```
CREATE TRIGGER trig_registrar_conclusao
AFTER UPDATE OF status ON pedidos   -- Dispara DEPOIS que a coluna 'status' da tabela 'pedidos' for ATUALIZADA
FOR EACH ROW                        -- Para cada linha cujo status foi alterado
EXECUTE FUNCTION registrar_data_conclusao();
```

Observações sobre OLD e NEW:
OLD: Contém a linha antes da operação. Disponível para UPDATE e DELETE.
NEW: Contém a linha depois da operação. Disponível para INSERT e UPDATE. Para triggers BEFORE INSERT ou BEFORE UPDATE, você pode modificar NEW antes que a linha seja salva no banco.