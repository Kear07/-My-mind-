------------------
### Lista

Uma coleção ordenada e mutável. Permite membros duplicados.

frutas = ["maçã", "banana", "cereja"]
números = [1, 5, 2, 8]

.append(item)              = Adiciona um item ao final da lista.
.insert(índice, item)      = Adiciona um item em uma posição específica.
.remove(item)              = Remove a primeira ocorrência de um item.
.pop(índice)               = Remove e retorna o item de uma posição (o último, se o índice não for especificado).
.sort()                    = Ordena a lista.
len(lista)                 = Retorna o número de itens.
lista[ 0 ]                 = Acessa o item pelo índice (primeiro item).
lista[1:3]                 = "Fatia" a lista, pegando um pedaço dela.

--------
### Tupla

Uma coleção ordenada e imutável. Permite membros duplicados.

coordenadas = (10, 20)
cores = ("vermelho", "verde", "azul")

count(item)           = Conta quantas vezes um item aparece.
.index(item)          = Retorna o índice da primeira ocorrência do item.
len(tupla)            = Retorna o número de itens.
tupla[1]              = Acessa o item pelo índice (segundo item).

Uma vez criada, você não pode alterar, adicionar ou remover itens.

-------------
### Dicionários

Uma coleção não ordenada mutável e indexada por chaves. Não permite chaves duplicadas.

pessoa = {"nome": "Ana", "idade": 25, "cidade": "São Paulo"}

dicionario['chave']                    = Acessa o valor associado à chave.
dicionario.get('chave')                = Acessa o valor de forma segura (retorna None se a chave não existir).
dicionario['nova_chave'] = valor       = Adiciona ou atualiza um par chave-valor.
del dicionario['chave']                = Remove um par chave-valor.
.keys()                                = Retorna uma lista com todas as chaves.
.values()                              = Retorna uma lista com todos os valores.
.items()                               = Retorna os pares (chave, valor), útil em loops for.

-------
### Sets

Uma coleção não ordenada e não indexada. Não permite membros duplicados.

numeros = {1, 2, 3, 4, 4, 5} # Resultado: {1, 2, 3, 4, 5}
set_vazio = set() # Para criar um set vazio, use a função set()

.add(item)                       = Adiciona um item ao conjunto.
.remove(item)                    = Remove um item (gera um erro se o item não existir).
.discard(item)                   = Remove um item (não gera erro se o item não existir).
.union(conjunto2) ou |           = Une dois conjuntos.
.intersection(conjunto2) ou &    = Retorna os itens em comum entre dois conjuntos.
.difference(conjunto2) ou -      = Retorna os itens que estão no primeiro conjunto, mas não no segundo.

----------
