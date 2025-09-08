-----
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