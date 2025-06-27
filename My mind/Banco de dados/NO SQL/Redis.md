
docker exec -it redis redis-cli      = inicinaliza

KEYS *  = Exibe todas as chaves valor

SET USER:111:NOME "Luke"

DBSIZE = Exibe quantas chaves existem

SET tempo "30 seg" EX 10  = Define uma chave valor com duração de 10 seg

TLL [chave]  = Exibe em tempo real a duração
se retornar 1 = chave não tem tempo de duração
se retornar 2 = chave não existe

SET XX = Altera a chave, se existir
SET NX = Cria a chave se não existir 

EXISTS [chave] = Exibe em numero se existe ou n

DEL [chave]    = deleta a chave "bruta, interrompe todo o servidor"
UNLINK [chave] = deleta a chave "suave, não interrompe outros processos"

RENAME [chave_antes chave_depois] = Renomeia uma chave

FLUSHALL = Limpa todo o banco

MSET [chaves] = Adiciona mais de uma chave por vez
MGET [chaves] = Exibe mais de uma chave

GETSET [chave] = Exibe o valor e depois atualiza o valor

KEYS "*-05*"  = Exibe onde tem esse numero
KEYS *-15-20*
.
?  = substitui qualquer informação antes e depois
* = substitui qualquer coisas antes e depois
[] = lista de caracter, e conteudo ou
^e = negação de letra
\  = escape

MSET sessao:1001:nome "Lucas" EX 600 sessao:1001:email "Lucas@exemplo.com" EX 600 sessao:1001:login "2025-05-20" EX 600 sessao:1002:nome "Amanda" EX 600 sessao:1002:email "Amanda@exemplo.com" EX 600 sessao:1002:login "2025-05-20" EX 600 sessao:1003:nome "João" EX 600 sessao:1003:email "João@exemplo.com" EX600 sessao:1003:login "2025-05-20" EX 600


config get databases = exibe a quantidade de servidores
dbsize = exibe a quantidade de cha
select [0-15] troca de servidor

SCAN 0 MATCH sessao:?:email count 10 = conta do zero ao 10, onde tem isso

HSET resultado:10-05-25:sena "ganhadores" 3 = Cria 

HSET user:123 email "marcelo@gmail.com" =  user fica com o campo email
HSET user:123 idade 33                  = user fica com o campo idade

HGET user:123 email = visualiza o campo
HGET user:123 idade = visualiza o campo

HMSET user:123 email "marcelo@gmail.com" idade 33 = Adiciona mais de um campo

HDEL user:123 email = Deleta o campo

HGETALL user:123 = Exibe todos os campos

RPUSH fila:pedidos pedidos:001 pedidos:002 pedido:003 pedido:004 cria uma lista
LRANGE fila:pedidos 0 -1 = exibe do começo ao fim

LPOP fila:pedidos = Remove o item a esquerda
RPOP fila:pedidos = Remove o item a direita

LPOP fila:pedidos  2 = Remove 2 itens a esquerda
RPOP fila:pedidos  2 = Remove 2 itens a direita

LLEN fila:pedidos = Retorna a quantidade de itens na fila

LTRIM fila:pedidos 1 2 = Mantém os intens que estão entre esse intervalo

LINDEX fila:pedidos 1 = Retorna o item dessa posição

-----

RPUSH historico:user:2001 home produtos sobre produtos contato produtos

LREM historico:user:2001 2 produtos = Remove os dois primeiros produtos
LREM historico:user:2001 -2 produtos = Remove os dois ultimos produtos
LREM historico:user:2001 0 produtos = Remove todos os produtos

LSET fila:pedidos 2 pedido:005 = Substitui o item na posicao 2 por esse

-----

SADD colaborador:101:skills "Python" "SQL" "MongoDB" = Lista sem repetidos
SMEMBERS colaborador:101:skills            = Lista os elementos
SISMEMBER colaborador:101:skills "Python"  = Busca um elemento
SINTER colaborador:101:skills colaborador:102:skills = Exibe a interseçãp
SUNION colaborador:101:skills colaborador:102:skills = Exibe a união
SDIF colaborador:101:skills colaborador:102:skills =  exibe o que tem só no 101

SREM colaborador:101:skills "sql" = Deleta um elemento
SRRANDMER colaborador:101:skills 2 = Exibe a quantidade de itens

SPOP colaborador:101:skills = Deleta um aleatória

SADD produtor:1001:vies user:1 user2: user:3
SKARD

----------------
ZADD ranking_vendedores [??] 1500 "Hugo"
ZADD ranking_vendedores [NX] 1800 "Bruna"
ZADD ranking_vendedores [INCR] 100 "Bruna"
ZADD ranking_vendedores [GT] 1200 "Maria"   = Atualiza if esse valor for maior que o atual
ZADD ranking_vendedores [LT] 1200 "Maria"   = Atualiza if esse valor for menor que o atual
ZSCORE ranking_vendedores Hugo              = Exibe o score da pessoa
ZRANK ranking_vendedores Hugo               = Exibe o rank da pessoa
ZREVRANK ranking_vendedores Hugo            = Exibe o rank da pessoa decrescente
ZREM ranking_vendedores Lucas               = Remove pelo nome
ZREMRANGERBYSCORE ranking_vendedores 0 1000 = Remove todos entre esse intervalo de score
ZREMRANGERBYRANK

ZCARD ranking_vendedores                    = Exibe a quantidade de nomes


ZRANGE ranking_vendedores 0 -1
ZRANGE ranking_vendedores 0 -1 WITHSCORES            = Crescente
ZRANGE ranking_vendedores 0 -1 REV WITHSCORES        = Decrescente

NX    = Adiciona se não existir
XX    = Atualiza se existir
CH    = Retorna o num de mudanças
INCR  = Incrementa o score do membro
GT    = Maior que
LT    = Menor que