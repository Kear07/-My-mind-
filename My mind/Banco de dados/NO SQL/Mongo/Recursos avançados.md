
-------

### Aggregate

"Sempre use db.[colletion] antes dos comandos"

.aggregate([ {$match: {status: "ativo", idade: {$gte: 18 }}} ])                = Filtra os documentos.
.aggregate([ {$group: {id: "$categoria", total: {$sum: "$preco" }}} ])         = Agrupa por um campo.
.aggregate([ {$project: {nome: 1, idade: 1, id: 0 }} ])                        = Seleciona, exclui ou cria campos.
.aggregate([ {$sort: {idade: -1 }} ])                                          = Ordena por campo (-1 para decrescente, 1 para crescente).
.aggregate([ {$limit: 10 } ])                                                  = Retorna apenas os 10 primeiros documentos.
.aggregate([ {$skip: 5 } ])                                                    = Pula os 5 primeiros documentos.
.aggregate([ {$unwind: "$tags" } ])                                            = Transforma um array em vários documentos, um para cada elemento. 
.aggregate([ {$lookup: {from: "outra_colecao", localField: "id_local", foreignField: "id_fk", as: "new_campo" }} ])   = Join
.aggregate([ {$count: "totalDeDocumentos" } ])                                 = Conta os documentos no pipeline
.aggregate([  ])
.aggregate([  ])


##### Operadores de Expressão (usados em `$group`)

    
    - `$sum`: Soma valores. `{ totalVendas: { $sum: "$preco" } }`
        
    - `$avg`: Calcula a média. `{ mediaIdade: { $avg: "$idade" } }`
        
    - `$max`: Valor máximo. `{ precoMaximo: { $max: "$preco" } }`
        
    - `$min`: Valor mínimo. `{ precoMinimo: { $min: "$preco" } }`
        
- **Matemáticos (em `$project`):**
    
    - `$multiply`: `{ faturamento: { $multiply: [ "$preco", "$quantidade" ] } }`
        
    - `$subtract`: `{ precoFinal: { $subtract: [ "$preco", "$desconto" ] } }`
        
    - `$divide`: `{ media: { $divide: [ "$total", "$itens" ] } }`
        
    - `$round`: `{ precoAprox: { $round: [ "$preco", 2 ] } }` (Arredonda para 2 casas decimais)
        
- **Strings (em `$project`):**
    
    - `$concat`: `{ nomeCompleto: { $concat: [ "$primeiro_nome", " ", "$sobrenome" ] } }`
        
    - `$toUpper`: `{ nome_maiusculo: { $toUpper: "$nome" } }`
        
    - `$toLower`: `{ nome_minusculo: { $toLower: "$nome" } }`
        
    - `$split`: `{ partes_nome: { $split: [ "$nomeCompleto", " " ] } }`



-----

### Índices

.createIndex( {campo: 1} )                                                = Cria um índice ascendente no `campo`. Use `-1` para descendente.
.createIndex( {campoA: 1, campoB: -1} )                                   = Cria um índice composto.
.getIndexes()                                                             = Lista todos os índices da collection.
.dropIndex("nome_indice")                                                 = Apaga um índice específico.