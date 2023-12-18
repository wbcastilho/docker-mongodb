## Docker MongoDB
![GitHub last commit](https://img.shields.io/github/last-commit/AzeemIdrisi/PhoneSploit-Pro?logo=github)

### MongoDB
Descrição MOngoDB

### Softwares e utilitários
* mongosh
* MongoDB Compass
* NoSQLBooster for MongoDB
* mongodump
* mongorestore

### mongosh

### MongoDB Compass

### NoSQLBooster for MongoDB

### mongodump
É um utilitário que cria uma cópia do conteúdo de um banco de dados.

Realizar o backup de um banco de dados.
```
mongodump --db=Vendas
```

Realizar o backup de uma coleção específica, informando um novo diretório
```
mongodump --collection=Pedidos --db=Vendas --out=C:\Curso\backup\pedidos
```

Excluir coleções específicas do backup
```
mongodump --db=Vendas --excludeCollection=Pedidos 
```

Comprimir a saída
```
mongodump --gzip --db=Vendas 
```

### mongorestore
Importa dados de um arquivo gerado pelo mongodump ou outra entrada padrão.

Restaurar um banco de dados
```
mongorestore --db=Vendas C:\Curso\backup\Vendas\Vendas 
```

Restaurar um banco de dados com arquivos compactados
```
mongorestore --gzip  --nsInclude="Vendas.*" C:\Curso\backup\compactada
```

### Renomear collection
db.Endereco.renameCollection("endereco")

### Insert
Inserir documento(s) a uma collection.

#### InsertOne
Faz o insert de um documento.
```
db.clientes.insertOne(
     {      
       "nome": "Carolina Jéssica Daiane Vieira", 
       "cpf": "625.181.705-45", 
       "data_nascimento": {"$date":"1999-01-13T18:00:00.000-03:00"}, 
       "genero": "Feminino", 
       "profissao": "Professor nível médio na educação infantil", 
       "status_civil": "Casado(a)"
   }
)
```

#### InsertMany
Faz o insert de vários documentos.
```
db.clientes.insertOne([
    {      
       "nome": "Calebe Danilo Roberto Figueiredo", 
       "cpf": "028.796.232-60", 
       "data_nascimento": {"$date":"1986-10-01T18:00:00.000-03:00"}, 
       "genero": "Masculino", 
       "profissao": "Supervisor de vendas comercial", 
       "status_civil":"Viúvo(a)"
   },
   {       
       "nome": "Tomás Bruno Lima", 
       "cpf": "695.097.514-72", 
       "data_nascimento": {"$date":"1973-11-01T18:00:00.000-03:00"}, 
       "genero": "Masculino", 
       "profissao": "Operador de caixa", 
       "status_civil": "Separado(a)"
   }, 
   {       
       "nome": "Geraldo Benedito Ian Lopes", 
       "cpf": "845.939.560-05", 
       "data_nascimento": {"$date":"1977-06-01T18:00:00.000-03:00"},
       "genero": "Masculino", 
       "profissao": "Vigilante", 
       "status_civil": "Viúvo(a)"
   } 
])
```

### Update
Atualizar documento(s) de uma collection.

#### UpdateOne
Faz o update de um documento.
```
db.series.updateOne(
    {"Série": "Grimm"},
    {$set: {"Classificação": "16+"}}   
)
```

#### UpdateMany
Faz o update de vários documentos.
```
db.restaurant.updateMany(
    { violations: { $gt: 4 } },
    { $set: { "Review" : true } }
)
```

#### $unset
Altera o campo do documento
```
db.contas.updateOne({_id: 34}, {$set: {valor: "2000"}})
```

#### $unset
Remove o campo do documento
```
db.contas.updateOne({_id: 34}, {$unset: {valor: ""}})
```

#### $push
Operador $push, caso exista o campo ele atualiza e caso não exista ele cria.
```
db.clientes.updateOne({"_id": 1}, {$push: {seguros: "seguro de vida"}})
```

#### $rename
Operador que renomeia o campo cpf de todos os documentos da collection clientes de cpf para CPF
```
db.clientes.updateMany({}, {$rename: {"cpf": "CPF"}})
```

#### $inc
Operador que incrementa ou decrementa valores
```
db.contas.updateOne({cpf:"410.436.439-82"}, {$inc: {valor: -2000}})
```

#### findAndModify
Modifica e retorna um único documento de acordo com o filtro especificado na consulta.
```
db.contas.findAndModify({query: {_id:34}, update: {$unset: {valor:""}}})
```

Traz na consulta o valor já modificado devido ao new:true
```
db.contas.findAndModify(
    {
        query: {_id:34}, 
        update: {$unset: {valor:""}},
        new: true
    }
)
```

```
db.contas.findAndModify(
    {
        query: {valor: {$lt: 500}}, 
        sort: {valor: 1},
        update: {$inc: {valor: 1000}},
        new: true
    }
)
```

#### findOneAndUpdate
Atualiza um único documento com base nos critérios especificados no filtro da consulta.
```
db.contas.findOneAndUpdate(
    {_id: 34},
    {$set: {valor: 5145.86}},
    {returnNewDocument: true}
)
```

#### findOneAndReplace
Substitui um único documento de acordo com o filtro especificado na consulta.
```
db.clientes.findOneAndReplace(
    {_id: 34},
    {       
       "nome": "Geraldo Benedito Ian", 
       "cpf": "845.939.560-05", 
       "data_nascimento": {"$date":"1977-06-01T18:00:00.000-03:00"},
       "genero": "Masculino", 
       "profissao": "Operador", 
       "status_civil": "Viúvo(a)"
   } 
)
```

### Delete
Excluir documento(s) de uma collection.

#### DeleteOne
Exclui um único documento.
```
db.series.deleteOne(
    {"Série": "The Boys"}
)
```

#### DeleteMany
Exclui vários documentos.
```
db.series.deleteMany(
    {"Temporadas": 1}
)
```

Exclui todos os documentos da collection.
```
db.series.deleteMany({})
```

#### findOneAndDelete
Exclui um único documento com base nos critérios especificados na consulta e retorna como resultado o documento excluído.
```
db.contas.findOneAndDelete({valor: {$lt:100}}, {$sort:{valor:1}})
```

### Find
Realizar consultas.

Retornar todos os documentos.
```
db.series.find()
```

Retornar todos os documentos onde ano de lançamento igual a 2018.
```
db.series.find({"Ano de lnaçamento": 2018})
```

#### FindOne
Retorna o primeiro documento da collection.
```
db.series.findOne()
```

#### Projeção
> Como segundo parâmetro do método find temos a projeção que especifica quais campos serão exibidos. 
> Quando 1 é exibido e quando 0 não é exibido

Retornar todos onde serão exibidos apenas os campos Série e Ano de Lançamento
```
db.series.find({}, {"Série": 1, "Ano de lançamento": 1, "_id": 0})
```

#### count
Retorna a quantidade de documentos.
```
db.clientes.find().count()
```
```
db.clientes.count()
```

#### distinct
```
db.clientes.find().distinct("tipo")
```

#### limit
Cursor de modificação que exibe a quantidade de documentos especificados em limit.
```
db.series.find().limit(5)
```

#### sort
Cursor de modificação que realiza a ordenação de acordo com o campo especificado.
> Quando 1 é ascendente e -1 é descendente.
```
db.series.find().sort("Série": 1)
db.series.find().sort("Série": -1)
```

#### skip
Cursor de modificação que retorna os documentos a partir do número especificado.
db.series.find().skip(200)

#### Combinando cursores de modificação
db.series.find().sort("Série": 1).limit(5)skip(200)

#### $eq
Operador de comparação, igual a.
```
db.clientes.find({genero: "Masculino"})
db.clientes.find({"genero": {$eq: "Masculino"}})
```

#### $ne
Operador de comparação, diferente.
```
db.clientes.find({"genero": {$ne: "Masculino"}})
```

#### $gt
Operador de comparação, maior que.
```
db.contas.find({valor: {$gt: 9000}})
```

#### $gte
Operador de comparação, maior ou igual a.
```
db.contas.find({valor: {$gte: 9000}})
```

#### $lt
Operador de comparação, menor que.
```
db.contas.find({valor: {$lt: 9000}})
```

#### $lte
Operador de comparação, menor ou igual a.
```
db.contas.find({valor: {$lte: 9000}})
```

#### $in
Operador de comparação, caso o valor especificado exista no array passado.
```
db.clientes.find({"status_civil": {$in: ["Viúvo(a)", "Casado(a)"]}})
```

#### Combinando operadores de comparação
Exemplo comparação maior que 50 e menor que 100.
```
db.produtos.find({peso:{$gt:50, $lt:100}})
```

#### $and
Operador lógico e.
```
db.contas.find({
    $and: [
        {tipo: {$eq: "Conta salário"}},
        {valor: {$gt: 9000}}    
    ]
})
```

#### $or
Operador lógico ou.
```
db.contas.find({
    $or: [
        {tipo: {$eq: "Conta salário"}},
        {valor: {$gt: 9000}}    
    ]
})
```

#### $not
Operador lógico de negação.
```
db.contas.find({estado: {$not: {$eq: "SP"}}})
```

#### $exist
Operador de elemento, checa se o elemento existe no documento.
```
db.clientes.find({seguros: {$exists: true}})
```

#### $type
Operador de elemento, checa se o elemento é de um determinado tipo.
> O tipo 2 significa tipo string.
```
db.clientes.find({seguros: {$type: 2}})
```

#### $all
Operador de matriz
```
db.clientes.find({seguros: {$all: ["seguro de vida", "seguro para carro"]}})
```

#### $size
Operador de matriz que checa se um determinado campo possui um array de duas posições.
```
db.clientes.find({dependentes: {$size: 2}})
```

#### $slice
Operador de matriz que retorna um dos elementos do array na projeção.
```
db.clientes.find({dependentes: {$size: 2}}, {dependentes: {$slice:1}})
```

### Aggregate
* Agrupar valores de vários documentos
* Executar operações nos dados agrupados para retornar um único resultado
* Analisar as mudanças de dados ao longo do tempo

#### group
Agrupa por um campo especificado
```
db.contas.aggregate({$group: {_id:"$tipo"}})
```

#### $limit
```
db.contas.aggregate({$limit:5})
```

#### $skip
```
db.contas.aggregate({$skip:5})
```

#### $sort
```
db.contas.aggregate({$sort:{valor: -1}})
```

#### Combinar estágios no aggregate
```
db.contas.aggregate([{$skip:15}, {$limit:5}, {$sort:{valor: -1}}])
```

#### unwind 
Desconstroi a matriz a partir de um campo selecionado
```
db.clientes.aggregate([{$unwind:"$seguros"}])
```

#### sortByCount
```
db.clientes.aggregate([{$unwind:"$seguros"}, {$sortByCount:"$genero"}])
```

#### match 
Aplicar filtros
```
db.enderecos.aggregate([{$match:{cidade:"Recife"}}])
```

```
db.contas.aggregate([
    {
        $match: {
            $and: [
                {tipo: {$eq:"Conta salário"}}, 
                {valor:{$gt: 3500}}
            ]
        }
    }
])
```

#### $avg 
Operador acumulador que retorna média.
```
db.contas.aggregate({
    $group: {
        _id: "$tipo",
        media: {
            $avg: "$valor"
        }
    }
})
```

#### $max
Operador acumulador que retorna o valor máximo.
```
db.contas.aggregate({
    $group: {
        _id: "$tipo",
        valorMaximo: {
            $max: "$valor"
        }
    }
})
```

#### $min
Operador acumulador que retorna o valor mínimo.
```
db.contas.aggregate({
    $group: {
        _id: "$tipo",
        valorMinimo: {
            $min: "$valor"
        }
    }
})
```

#### $count
Operador acumulador que retorna o valor contagem.
```
db.contas.aggregate({
    $group: {
        _id: "$tipo",
        contagem: {
            $count:{}
        }
    }
})
```

#### $sum
Operador acumulador que retorna o valor total.
```
db.contas.aggregate({
    $group: {
        _id: "$tipo",
        Total: {
            $sum:"$valor"
        }
    }
})
```

#### Combinando operadores acumuladores
Retorna soma e média.
```
db.contas.aggregate({
    $group: {
        _id: "$tipo",
        Total: {
            $sum:"$valor"
        },
        Media: {
            $avg: "$valor"
        }
    }
})
```

Retornar Soma e Média e filtra.
```
db.contas.aggregate(
    { 
        $match: {tipo: "Conta poupança"}
    },
    {
        $group: {
            _id: "$tipo",
            Total: {
                $sum:"$valor"
            },
            Media: {
                $avg: "$valor"
            }
        }
    }
)
```

Retorna Soma, Média, Máximo e Mínimo.
```
db.contas.aggregate([
    {$group:{
        _id:null,
        Soma:{$sum:"$valor"},
        Media:{$avg:"$valor"},
        Maximo:{$max:"$valor"},
        Minimo:{$min:"$valor"}
    }
},{
    $project: {
      _id: 0    }  }
])
```

#### Formatando datas
```
db.alarmes.aggregate([
    {
        $project: {
            datetime: {
                $dateToString: {
                    format: "%d/%m/%Y %H:%M:%S",
                    date: "$datetime"
                }
            },
            company: 1,
            service: 1,
            type: 1,
            message: 1,
            value: 1,
            alarm: 1
        }
    },
    { $limit: 10},
    { $sort: {datetime: -1} }
])
```

#### $cond 
Operador condicional que dependendo da condição apresenta um determinado texto.
```
db.contas.aggregate([{
    $project: {
        cpf: 1,
        tipo: 1,
        valor: 1,
        valores: {
            $cond:[{$gte:["$valor", 8000]}, "VERDADEIRO", "FALSO"]
        }
    }
}])
```

#### $ifNull
Operador condicional que caso o valor seja null retorna o texto.
```
db.contas.aggregate([{
    $project: {
        valor: {
            $ifNull: ["$valor", "Não Espcificado"]
        }
    }
}])
```






