# MONGODB

# para disparar o banco
C:\Program Files\MongoDB\Server\3.6\bin>mongod

# para entrar no modo consulta por comand line
mongo 

# seta o banco que o mongo vai consultar
use dbaula3

# find sort decrescente
db.aluno.find().sort({"nome":-1})

# find sort crescente
db.aluno.find().sort({"nome":1})

# find por campo
db.aluno.find({"nome":"Rodrigo"})

# conta quantos registros tem
db.aluno.find().count()

# mostra todos
db.aluno.find()

# mostra mais bonitinho
db.aluno.find().pretty()

# lista os usuarios da base
db.getUsers()

# cria um usuário com regras de permissão em um dado banco
db.createUser({user:"rodrigo",pwd:"123",roles:[{role:"readWrite",db:"dbaula4"}]})

# roles existentes
ROLE--------DESCRIÇÃO DESSE PERFIL

read--------Você consegue ler todos os dados de um determinado banco de dados utilizando find

readWrite---Você consegue fazer CRUD em um ou mais bancos de dados específicos

dbAdmin-----Esse perfil é administrador de um banco de dados específico

root--------Pode fazer qualquer coisa no seu banco de dados


# verifica se usuário pode autenticar se retornar 1 pode, senão retorna 0 e ERROR: authentication failed
db.auth("rodrigo","123")

# cria usuário setando o base de dados customData 
db.createUser({user:"rodroga",pwd:"123",customData:{db:"dbaula4"},roles:[{role:"readWrite",db:"dbaula4"}]})


# importar arquivo csv

mongoimport -d dbaula5 -c ubs --type csv --file ubs.csv --headerline

# buscar quantidade limite de registro

db.ubs.find().limit(2).pretty()

# buscar campo onde contém ocidental, independente do que tem antes ou depois do que está escrito.

db.ubs.find({"municipio":/OCIDENTAL/})

# update field

db.colect.update({"name": "trocado"},{$set:{"idade":37}})

# MLAB free 500mg

## To connect using the mongo shell:

mongo ds227199.mlab.com:27199/teruelrodrigo -u <dbuser> -p <dbpassword>
  
## To connect using a driver via the standard MongoDB URI (what's this?):

mongodb://<dbuser>:<dbpassword>@ds227199.mlab.com:27199/teruelrodrigo

  
use teruelrodrigo

db.colect.find().pretty()

# Criar index para melhorar resposta da busca

db.aula8.createIndex({"roles.functionalities.name": 1})

# ver os Index

db.colect.getIndexes()

# drop Index (REMOÇÃO DA INDEX)

db.colect.dropIndex({"roles.functionalities.name": 1})
  
# agrega grupo campos comuns e soma amount

db.order.aggregate([
    {$group : { _id : "$cust_id", total : {$sum : "$amount"}}}
])

# agregando escolhendo match específico

db.order.aggregate([
    {$match : {status: "B"}},
    {$group : { _id : "$cust_id", total : {$sum : "$amount"}}}
])

# distinct

db.order.distinct("cust_id")