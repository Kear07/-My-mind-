-------
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