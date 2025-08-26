
---------
### Gerenciamento

show dbs                                             = Lista todos os bancos de dados no servidor.
use [database]                                       = Troca para um banco de dados existente ou o cria se ele não existir.
db                                                   = Mostra o banco de dados atualmente em uso.
show collections                                     = Lista todas as collections (tabelas) no banco de dados atual.
db.dropDatabase()                                    = Apaga o banco de dados que você está usando atualmente.
db.[collection].renameCollection("[new_name]")       = Renomeia uma collection.

----
### CRUD Insert

"Sempre use db.[colletion] antes dos comandos"

.insertOne({ nome: "Ana", idade: 18, status: "ativo" })
.insertMany([ { nome: "Beto", idade: 25 }, { nome: "Caio", idade: 32 } ])

----
### CRUD Find

"Sempre use db.[colletion] antes dos comandos"

.find({})                                                                   = Um filtro vazio `{}` retorna tudo.
.find({ status: "ativo" })                                                  = Retorna todos os documentos que correspondem ao filtro. 

.findOne({ status: "ativo" })                                               = Retorna apenas o primeiro documento que corresponde ao filtro.
.findById("6e8f8f8f8f8f8f8f8f8f8f8f")                                       = Busca um documento específico pelo seu [_id]._
.countDocuments({ status: "ativo" })                                        = Conta quantos documentos correspondem ao filtro.

---
### CRUD Update

"Sempre use db.[colletion] antes dos comandos"

.updateOne( {nome: "Ana"}, {$set: {idade: 19 }} )                           = Atualiza o primeiro documento que corresponde ao filtro.
.updateMany( {status: "ativo"}, {$set: {ultima: new Date()}} )              = Atualiza **todos** os documentos que correspondem ao filtro.

-----
### CRUD Delete

"Sempre use db.[colletion] antes dos comandos"

.deleteOne( {nome: "Beto"} )                                                = Apaga o primeiro documento que corresponde ao filtro.
.deleteMany( {status: "inativo"} )                                          = Apaga todos os documentos que correspondem ao filtro.