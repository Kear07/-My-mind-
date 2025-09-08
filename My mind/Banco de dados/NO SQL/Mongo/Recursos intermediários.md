-----
### Operadores de consulta lógicos (find e match)

"Sempre use db.[colletion] antes dos comandos"

.find( {$and: [{preco: { $lt: 50 }}, {estoque: {$gt: 0}} ]} )                      = Operador and "e".
.find( {$or: [{categoria: "A"}, {categoria: "B"} ]} )                              = Operador or "ou".
.find( {preco: {$not: { $gt: 50 }}} )                                              = Operador not "negação".

-------
### Operadores de consulta de comparação (find e match)

"Sempre use db.[colletion] antes dos comandos"

.find( {idade: {$eq: 25 }} )                                                       = Operador eq "igual a". 
.find( {status: {$ne: "inativo"}} )                                                = Operador ne "diferente de".
.find( {idade: {$gt: 18 }} )                                                       = Operador gt "maior que".
.find( {idade: {$gte: 18}} )                                                       = Operador gte "maior ou igual".
.find( {preco: {$lt: 100}} )                                                       = Operador lt "menor que".
.find( {preco: {$lte: 100}} )                                                      = Operador lte "menor ou igual".
.find( {categoria: {$in: ["eletrônico", "vestuário"] }} )                          = Operador in "está contido em".
.find( {categoria: {$nin: ["alimentício", "limpeza"] }} )                          = Operador nin "não está contido em".

----
### Operadores de consulta de elementos (find e match)

"Sempre use db.[colletion] antes dos comandos"

.find( {telefone: {$exists: true}} )                                               = Operador exists "verifica se o campo existe".
.find( {telefone: {$type: "string"}} )                                             = Operador type "verifica o tipo do valor do campo".

--------
### Operadores de Atualização (update)

"Sempre use db.[colletion] antes dos comandos"

.updateOne( {_id: 1}, {$set: {nome: "Carlos"}} )                                  = Define ou adiciona um campo._
.updateOne( {_id: 1}, {$unset: {telefone: ""}} )                                  = Remove um campo._
.updateMany( {}, {$rename: {"endereço": "endereco"}} )                           = Renomeia um campo.
.updateOne( {_id: 1 }, {$inc: {saldo: 100}} )                                     = Incrementa um valor numérico._
.updateOne( {_id: 1}, {$mul: {saldo: 1.1}} )                                      = Multiplica um valor numérico._
.updateOne( {_id: 1}, {$min: {salario: 5000}} )                                   = Atualiza se o valor for menor que o mínimo._
.updateOne( {_id: 1 }, {$max: {pontuacao: 1000 }} )                               = Atualiza se o valor for maior que o máximo.

----
### Arrays

"Sempre use db.[colletion] antes dos comandos"

.updateOne( {_id: 1}, {$push: {hobbies: "leitura" }} )                            = Adiciona um elemento ao array._
.updateOne( {_id: 1}, {$push: {scores: { $each: [ 1,3,5 ] }}} )                   = Para adicionar múltiplos valores._
.updateOne( {_id: 1}, {$addToSet: {hobbies: "leitura"}} )                         = Adiciona apenas se o elemento não existir._
.updateOne( {_id: 1}, {$pop: {scores: 1}} )                                       = Remove o último elemento ou `-1` para o primeiro._
.updateOne( {_id: 1 }, {$pull: {hobbies: "pesca"}} )                              = Remove todas as ocorrências de um valor._
.updateOne( {_id: 1}, {$pullAll: {scores: [ 0, 5 ] }} )                           = Remove todas as ocorrências de múltiplos valores.