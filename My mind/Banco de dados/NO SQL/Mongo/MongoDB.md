show dbs          = mostra os databases 

show collections  = mostra as tables 

use nome          = cria um novo database 

db.dropDatabase() = exclui o database atual 

db. renameColletion


-=-=-=-=-=-=-=-=-=-=-CRUD-=-=-=-=-=-=-=-=-=-=- 

.insertOne()  = insere um documento 

.insertMany() = insere varios documentos 

.updateOne()  = atualiza o primeiro documento 

.updateMany() = atualiza todos documentos 

.deleteOne()  = deleta o primeiro documento 

.deleteMany() = deleta todos documentos 

.findOne()    = mostra o primeiro documento 

.find()       = mostra todos documentos


-=-=-=-=-=-=-=-=-=-=-=-=-USO-=-=-=-=-=-=-=-=-=-=-=-=- 

.insertOne({nome: "ana",idade: 18}) 

.insertMany([{nome: "ana"},{nome: "caio":}]) 

.updateOne({nome: "Luke"}, {$set:{nome: "Kear"}}) 

.updateMany({nome: "Luke"}, {$set:{nome: "Kear"}}) 

.deleteOne({ nome: "João" }) 

.deleteMany({ nome: "João" }) 

.findOne({status: "ativo"}) 

.find({status "ativo"})

=-=-=-=-=-=-OPERADORES-=-=-=-=-=-=- 

$and    = e 

$or     = ou 

$exists = existencia 

$type   = tipo 

$lt     = menor 

$lte    = menor ou igual 

$gt     = maior  

$gte    = maior ou igual 

$eq     = igual 

$ne     = diferente 

$not    = negação 

$in     = contém 

$nin    = não contém 

$inc    = acrescenta valor 

$min    = define um valor mínimo 

$max    = define um valor máximo


=-=-=-=-=-=-=-=-=-=-=-=-=-=USO-=-=-=-=-=-=-=-=-=-=-=-=-=- 

.find( {$and: [{ idade: 18}, {status: "ativo"}}] } ) 

.find( {$or: [{nome: "Juliana"} ,{nome: "Fernanda"}]} ) 

.find( {telefone: { $exists: true}} ) 

.find( {telefone: { $type: "string"}} ) 

.find( {media: { $lt: 7}} ) 

.find( {media: { $let: 7}} )  

.find( {media: { $gt: 7}} ) 

.find( {media: { $gte: 7}} ) 

.find( {idade: { $eq: 25 }} ) 

.find( {idade: { $ne: 25 }} ) 

.find( {idade: { $not: { $eq: 25 }}} ) 

.find( {categoria: { $in: ["eletrônico","vestuário"] }} ) 

.find( {categoria: { $nin: ["eletrônico","vestuário"] }} ) 

.find( {"escola.qnd_professores": {$not: {$lt: 10}}} ) 

.find( {preco: {$not: {$gte: 100, $lte: 500 }}} ) 

.find( {"escola.nome": /germinare business/i } ).count() 

.find( {} ).sort(saldo: -1)


Leitura 

- .findById() – Consulta um documento específico pelo seu _id. 
    
- .countDocuments() – Retorna a contagem de documentos que correspondem a um filtro. 
    
- .distinct() – Retorna valores únicos de um campo específico em todos os documentos que correspondem ao filtro. 
    
- .aggregate() – Executa operações de agregação, como somas, médias, agrupamentos, etc. 
    

  

Atualização 

- .findOneAndUpdate() – Encontra um documento e o atualiza em uma única operação atômica, retornando o documento antes ou depois da atualização. 
    
- .findOneAndReplace() – Substitui um documento específico e retorna o original ou o novo documento. 
    
- .findOneAndDelete() – Encontra um documento e o exclui, retornando-o antes da exclusão.
=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-UPDATES=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=- 

@filtro@ - @função@ 

( {cartao: {$exists: true}}, {$inc: {saldo: 100} )  ===== ( se o campo existe, adiciona 100 ) 

( {"cartao.status": "inativo"}, {$unset: {cartao: "" }} ) ===== ( se inativo, remove o campo ) 

( {}, {$rename: {"endereço": "endereco"}} ) ===== ( sem filtro, renomeia o campo ) 

( {idade: {$gt: 60}}, {$mul: {saldo: 1.1}} ) ===== ( if maior 60, multiplica o valor por 1.1 ) 

( {departamento: "TI"}, {$min: {salario: 5000 }} ) ===== ( if for "TI", todos acima de 5k ficam com 5k ) 

( {departamento: "TI"}, {$max: {salario: 2000 }} ) ===== ( if for "TI", todos abaixo de 2k ficam com 2k )

=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=OPERADORES ARRAY=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-= 

@filtro@ - @função@ 

( {nome: "Lamelo"}, {$pull: {emprestimo_tipo: "Consignado" }} ) ===== ( if for "Lamelo", retira o elemento do array) 

( {}, {$pullAll: {scores: [ 0, 5 ] }} ) ===== ( sem filtro", retira mais de um elemento do array) 

( {nome: "Jucelio"}, {$push: {emprestimo_tipo: "Pessoal" }} ) ===== ( if for "Jucelio", adciona o elemento no array) 

( {}, {$addToSet: {emprestimo_tipo: "Pessoal" }} ) ===== ( sem filtro, adciona o elemento se não existir no array) 

( {}, {$push: {scores: {$each: [ 1,3,5 ] }}} ) ===== ( sem filtro, adciona os elemento no array) 

( {}, {$addToSet: {scores: {$each: [ 1,3,5 ] }}} ) ===== ( sem filtro, adciona os elemento se não exisitr no array) 

( {nome: "Jucelio"}, {$pop: {emprestimo_tipo: 1 }} ) ===== ( if for "Jucelio", remove o ultimo elemento do array) 

( {nome: "Jucelio"}, {$pop: {emprestimo_tipo: -1 }} ) ===== ( if for "Jucelio", remove o primeiro elemento do array)

-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-FUNÇÃO AGGREGATE-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=- 

$match       = Filtra documentos. 

$sort        = Ordena os documentos. 

$limit       = Limita o número de documentos. 

$project     = Controla os campos a serem exibidos. 

$group       = Agrupa documentos e aplica funções de agregação. 

$avg         = Calcula a média de um campo. 

$count       = Conta o número de documentos. 

$sum         = Soma os valores de um campo. 

$unwind      = Desconstrói arrays. 

$sortByCount = Conta e ordena por quantidade em grupos. 

$skip        = Pula os n primeiros documentos 

{ $match: { idade:  18}} 

{ $sort:  { $idade: -1}} 

{ $limit: 3} 

{ $project: { nome: 1, idade: 1, _id: 0 }} 

{ $group: { _id: "$categoria", totalVendas: { $sum: "$preco" }}} 

{ $group: { _id: null, mediaIdade: { $avg: "$idade" }}} 

{ $count: "totalUsuarios"} 

{ $group: { _id: null, totalFaturado: { $sum: "$valor" }}} 

{ $unwind: "$seguros" } 

{ $skip: 5}


Distinct 

|   |   |
|---|---|
|Query:|.distinct("tipo")|

|   |   |
|---|---|
|Retorno:|[ 'Conta corrente', 'Conta poupança', 'Conta salário' ]|

|   |   |
|---|---|
|Explicação:|Exibi todos os valores diferentes que o array possui|

Distinct e $Length 

|   |   |
|---|---|
|Query:|.distinct("profissao").length()|
|Retorno:|3|

|   |   |
|---|---|
|Explicação:|Retorna quantas profissões diferente tem|

$All 

|   |   |
|---|---|
|Query:|.find({seguros: {$all: ["seguro de vida", "seguro para carro"]}}).count()|

|   |   |
|---|---|
|Explicação:|Exibi a quantidades de array que possui os 2 seguros|

$Group e $Count 

|   |   |
|---|---|
|Query:|.aggregate({$group: {_id: "$tipo", "Quantidade": {$count:{}}}})|

|   |   |
|---|---|
|Explicação:|Exibi quantos campos tipos existem|

$Sort e $limit 

|   |   |
|---|---|
|Query:|.find({}, {nome: 1, _id:0}).sort({data_nascimento:1}).limit(1)|
|Retorno:|[[ { nome: 'Alice Márcia Pereira' } ]|

|   |   |
|---|---|
|Explicação:|Ordena pelo nascimento , pega o primeiro resultado e exibi só o nome|


$Group, $Sum, $Avg, $Count, $Max, $Min, $Sort 

|   |   |
|---|---|
|Query:|aggregate([{ <br><br>$group: { _id: "$categoria",               -- Agrupa por categoria <br><br>totalVendas: { $sum: "$preco" },       -- Soma o valor de todas as vendas na categoria <br><br>mediaPreco: { $avg: "$preco" },        -- Calcula a média dos preços <br><br>quantidadeVendas: { $count: {} },     -- Conta o número de vendas <br><br>precoMaximo: { $max: "$preco" },   -- Encontra o preço máximo <br><br>precoMinimo: { $min: "$preco" }     -- Encontra o preço mínimo <br><br>}}, <br><br>{$sort: { totalVendas: -1 }}])|

|   |   |
|---|---|
|Explicação:|Agrupa por categoria de produto, calculando o total de vendas, a média de preços, o número de vendas, e os preços máximo e mínimo de cada categoria, e  ordena os resultados pela soma total das vendas de forma decrescente.|

$Unwind e $Project 

|   |   |
|---|---|
|Query:|aggregate([ <br><br>{$unwind: "$produtos" },   <br><br>{$project: { cliente: 1,  produto: "$produtos.nome", preco: "$produtos.preco" }}])|

|   |   |
|---|---|
|Explicação:|Desconstroi o array, exibi as informações do cleinte, nome e preco do produto|

$SortByCount 

|   |   |
|---|---|
|Query:|db.pedidos.aggregate([{ $sortByCount: "$produto" } ])|

|   |   |
|---|---|
|Explicação:|Conta a quantidade de cada produto e ordena|

{$lookup: { 

    from: "nome_da_colecao",           // Coleção que você quer relacionar 

    localField: "campo_local",         // Campo na coleção atual 

    foreignField: "campo_estrangeiro", // Campo correspondente na coleção relacionada 

    as: "alias_do_resultado"           // Nome do novo campo onde os dados relacionados serão armazenados 

}} 

$multiply = operação de * 

{$project: { 

    nome: 1, 

    faturamento_total: { $multiply: ["$preco", "$quantidade"] } 

}} 

$subtract = operação de - 

{$project: { 

     nome: 1, 

     preco_com_desconto: { $subtract: ["$preco", 200] }   

}} 

$divide = operação de / 

{$project: { 

     nome: 1, 

     peso_medio: { $divide: ["$peso_total", "$quantidade"] } 

}} 

$concat = operação de juntar 

{$project: { 

      nome_completo: { $concat: ["$primeiro_nome", " ", "$sobrenome"] } 

}} 

$round = arredonda 

{$project: { 

      nome: 1, 

      preco_arredondado: { $round: ["$preco", 2] } 

}} 

$trunc = remove as casas decimais 

{ 

    $project: { 

      nome: 1, 

      preco_truncado: { $trunc: "$preco" } 

}



|   |   |
|---|---|
|$split|Divide uma string em array com base em um delimitador.|

|   |   |
|---|---|
|$concat|Junta várias strings em uma só.|

|   |   |
|---|---|
|$substr|Extrai parte da string com base em posição e comprimento. (deprecated, prefira $substrBytes ou $substrCP)|

|   |   |
|---|---|
|$substrBytes|Extrai substring por bytes.|

|   |   |
|---|---|
|$substrCP|Extrai substring por pontos de código (recomendado p/ Unicode).|

|   |   |
|---|---|
|$toLower|Converte string para minúsculas.|

|   |   |
|---|---|
|$toUpper|Converte string para maiúsculas.|

|   |   |
|---|---|
|$trim|Remove espaços (ou caracteres especificados) do início e fim da string.|

|   |   |
|---|---|
|$ltrim|Remove apenas da esquerda.|

|   |   |
|---|---|
|$rtrim|Remove apenas da direita.|

|   |   |
|---|---|
|$strLenBytes|Tamanho da string em bytes.|

|   |   |
|---|---|
|$strLenCP|Tamanho da string em code points (correto p/ Unicode).|

|   |   |
|---|---|
|$indexOfBytes|Posição de substring (em bytes).|

|   |   |
|---|---|
|$indexOfCP|Posição de substring (em code points).|

|   |   |
|---|---|
|$replaceOne|Substitui a primeira ocorrência de um texto.|

|   |   |
|---|---|
|$replaceAll|Substitui todas as ocorrências de um texto.|

|   |   |
|---|---|
|$regexFind|Busca usando regex (retorna 1º match como objeto).|

|   |   |
|---|---|
|$regexFindAll|Retorna todas as ocorrências que batem com o regex.|

|   |   |
|---|---|
|$regexMatch|Retorna true/false se regex encontrar algo.|

( {}, {$pull: {fruits: {$in: [ "apples", "oranges" ] }}} ) ===== ( sem filtro", retira mais de um elemento do array) 

Totalmente subistituivel pelo pullall


$position Especifica uma posição para inserir um elemento {$push: {campo: elemento, $position: index} } 

$slice Limite o número de elementos de um array {$push: {campo: elemento, $slice: qnt} }  

$sort Ordena um array {$push: {campo: elemento, $sort: 1 ou -1} }


$setOnInsert


![[Pasted image 20250821152838.png]]