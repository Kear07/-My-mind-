
---
### Inicialização
 
docker exec -it redis redis-cli           = Inicia a interface de linha de comando do Redis 

----
### Comandos básicos

KEYS *                = Exibe todas as chaves armazenadas no banco.
KEYS "*-05*"            = Exibe chaves que contêm "-05-" em qualquer posição.
KEYS *-15-20*:          = Exibe chaves que contêm "-15-20-" em qualquer posição.
KEYS user:?:name      = Substitui um único caractere (coringa de um caractere). 
KEYS user:            = Substitui zero ou mais caracteres (coringa de múltiplos caracteres).  
KEYS user:[abc]       = Lista de caracteres. Ex: (user:a, user:b, user:c).
KEYS user:[^e]         = Negação de letra. Ex: (user:a, user:b, mas não user:e).
KEYS user\            = Caractere de escape para usar caracteres especiais.

DBSIZE                = Exibe o número de chaves existentes no banco.
EXISTS [chave]        = Verifica se uma chave existe.
DEL [chave]           = Deleta uma chave. 
UNLINK [chave]        = Deleta uma ou mais chaves de forma assíncrona.
RENAME [antiga nova]  = Renomeia uma chave.
FLUSHALL              = Limpa todos os bancos de dados.

---
### Gerenciamento de Bancos de Dados

O Redis pode ter múltiplos bancos de dados, numerados de 0 a 15 por padrão.

config get databases   = Exibe a quantidade de bancos de dados configurados.
SELECT [0-15]          = Troca para o banco de dados especificado.

----------
### Chaves com Tempo de Expiração (TTL)

Você pode definir um tempo de vida para suas chaves, após certo tempo, elas se excluirão.

SET [chave] "[valor]" EX [2] =  Define uma chave-valor com uma duração de [2] segundos.
TTL [chave]                  =  Exibe o tempo restante de uma chave em segundos.

Retorno -1: A chave existe, mas não tem tempo de duração definido
Retorno -2: A chave não existe.

---
### Manipulação de Chaves (SET Avançado)

SET [chave] "[valor]" XX   = Altera o valor da chave somente se ela já existir.
SET [chave] "[valor]" NX   = Cria a chave somente se ela não existir.
GETSET [chave] "[valor]"  = Retorna o valor atual da chave e, atualiza o seu valor.

SCAN 0 MATCH [padrão] COUNT [num] = Itera as chaves do banco de dados.
0                                 = Ordem/index onde vai começar a busca
MATCH [padrão]                    = Filtra as chaves (mesmos padrões de KEYS).
COUNT [numero]                    = Número de elementos a serem retornados por cada iteração.

----
### Comandos para Múltiplas Chaves (M)

MSET [chave1] "[valor1]" [chave2] "[valor2]"  = Adiciona ou atualiza múltiplas chaves de uma vez.
MGET [chave1 chave2]                          = Exibe os valores de múltiplas chaves.

Observação: EX para expiração só funciona diretamente com SET. Para MSET, você precisaria definir a expiração para cada chave individualmente.

--------
### Tipo de Dados: Hashes (H)

Hashes são como objetos ou dicionários, permitindo armazenar múltiplos campos e valores dentro de uma única chave.

HSET [key campo1] "[valor1]" [campo2] "[valor2]"   = Cria ou atualiza campos dentro de um hash.
Ex: HSET user:123 email "marcelo@gmail.com"  
EX: HSET user:123 idade 33 
(adiciona múltiplos campos à chave user:123)

HMSET [key campo1] "[valor1]" [campo2] "[valor2]"  = Adiciona ou atualiza múltiplos campos
Ex: HMSET user:123 email "marcelo@gmail.com" idade 33

HGET [chave campo]  = Visualiza o valor de um campo específico dentro de um hash.
Ex: HGET user:123 email

HDEL [chave campo]  = Deleta um campo de um hash.
Ex: HDEL user:123 email

HGETALL [chave]: Exibe todos os campos e valores de um hash.
Ex: HGETALL user:123

-----
### Tipo de Dados: Listas (L/R)

Listas são coleções ordenadas de strings. Você pode adicionar elementos no início ou no final da lista.

RPUSH [chave elemento1 elemento2]  = Adiciona um ou mais elementos ao final de uma lista.
Ex: RPUSH fila:pedidos pedidos:001 pedidos:002 pedido:003 pedido:004

LPUSH [chave elemento1 elemento2]  = Adiciona um ou mais elementos ao início de uma lista.
Ex: LPUSH fila:pedidos pedidos:001 pedidos:002 pedido:003 pedido:004

LRANGE [chave start stop]          = Exibe um intervalo de elementos de uma lista.
0: Primeiro elemento.
-1: Último elemento.
Ex: LRANGE fila:pedidos 0 -1 (exibe todos os elementos do começo ao fim).

LPOP [chave]                       = Remove e retorna o elemento no início da lista.
RPOP [chave]                       = Remove e retorna o ultimo elemento da lista.

LPOP [chave quantidade]            = Remove e retorna a [quantidade] de elementos no inicio 
RPOP [chave quantidade]            = Remove e retorna a [quantidade] de elementos no fim

LLEN [chave]                       = Retorna a quantidade de elementos em uma lista.

LTRIM [chave start stop]           = Mantém apenas os elementos dentro do intervalo.
Ex: LTRIM fila:pedidos 1 2 (mantém os itens que estão entre as posições 1 e 2).

LINDEX [chave posição]             = Retorna o elemento em uma posição específica da lista.
Ex: LINDEX fila:pedidos 1 (retorna o segundo elemento da lista).

LREM [chave count] "[valor]":      = Remove ocorrências de um [valor] de uma lista.

2: Remove os primeiros [2] elementos do inicio ao fim.
< 2: Remove os últimos [2] elementos do [valor] do fim ao inicio.
0: Remove todas as ocorrências do [valor].

LSET [chave index] "[novo_valor]"  = Substitui o elemento na posição [index] da lista.

----------
### Tipo de Dados: Sets (S)
Sets são coleções não ordenadas de strings únicas. Não permitem elementos duplicados.

SADD [chave] "[membro1]" "[membro2]"   = Adiciona um ou mais membros a um set.
Ex: SADD colaborador:101:skills "Python" "SQL" "MongoDB"

SMEMBERS [chave]                       = Lista todos os membros de um set.

SISMEMBER [chave] "[membro]"           = Verifica se um membro existe em um set.

SINTER [chave1 chave2]                 = Retorna a intercessão de membros nos sets.

SUNION [chave1 chave2]                 = Retorna a união de membros nos sets.

SDIFF [chave1 chave2]                  = Retorna os membros que estão somente na [chave1].

SREM [chave] "[membro1]" "[membro2]"   = Remove um ou mais membros de um set.

SRANDMEMBER [chave quantidade]         = Retorna um ou mais membros aleatórios de um set.

SPOP [chave]                           = Remove e retorna um membro aleatório de um set.

SCARD [chave]                          = Retorna a quantidade de membros em um set.

--------
### Tipo de Dados: Sorted Sets (Z)
Sorted Sets são coleções de membros únicos, onde cada membro está associado a uma pontuação (score) numérica. Os membros são armazenados em ordem crescente de score.

ZADD [chave score] "[membro]"      =  Adiciona um membro com um score a um sorted set.
Ex: ZADD ranking_vendedores 1500 "Hugo"

NX: Adiciona o membro somente se ele não existir.
Ex: ZADD ranking_vendedores NX 1800 "Bruna"
XX: Atualiza o score do membro somente se ele já existir.
CH: Retorna o número de membros que foram adicionados ou tiveram seus scores alterados 
INCR: Incrementa o score do membro pelo valor fornecido.
GT: Atualiza o score do membro somente se o novo score for maior que o score atual.
LT: Atualiza o score do membro somente se o novo score for menor que o score atual.

ZSCORE [chave] "[membro]"          = Exibe o score de um membro específico.

ZRANK [chave] "[membro]"           = Exibe o rank de um membro em ordem crescente de score.
ZREVRANK [chave] "[membro]"        = Exibe o rank de um membro em ordem decrescente de score.

ZREM [chave] "[membro]"            = Remove um membro.
ZREMRANGEBYSCORE [chave min max]   = Remove todos os membros cujo score está dentro do intervalo.
ZREMRANGEBYRANK [chave start stop] = Remove membros pelo seu rank.

ZCARD [chave]                      = Exibe a quantidade de membros.
ZRANGE [chave start stop]          = Exibe um intervalo de membros em ordem crescente de score.
0: Primeiro membro.
-1: Último membro.

ZRANGE [key start stop] WITHSCORES  = Exibe um intervalo de membros e os scores em ordem crescente.
ZRANGE [key start stop] REV WITHSCORES = Exibe um intervalo de membros e seus scores decrescente.

--------
### Tipo de Dados: Bitmaps
Bitmaps são uma forma eficiente de armazenar e manipular arrays de bits. Cada bit pode ser 0 ou 1.

SETBIT [chave offset valor]       = Seta o bit na posição offset (índice) como 0 ou 1.
Ex: SETBIT users:active 10 1      = Marca que o usuário com ID 10 está ativo.

GETBIT [chave offset]	      = Exibe o bit na posição offset.
Ex: GETBIT users:active 10    = Retorna 1 (usuário 10 está ativo).

BITCOUNT [chave]	          = Conta quantos bits estão em 1 
Ex: BITCOUNT users:active:    = Conta quantos bits estão em 1 

BITOP [operação destino chave1 chave2]  = Realiza operações bit a bit entre múltiplas chaves (AND, OR, XOR, NOT). O resultado é salvo em destino.

BITPOS [chave bit]	    = Encontra a posição do primeiro bit com o valor indicado (0 ou 1).

STRLEN [chave]	        = Retorna o tamanho da string armazenada na chave 




