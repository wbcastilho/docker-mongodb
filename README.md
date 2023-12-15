## Docker MongoDB
![GitHub last commit](https://img.shields.io/github/last-commit/AzeemIdrisi/PhoneSploit-Pro?logo=github)

### MongoDB
Descrição MOngoDB

### Insert
Inserir documento(s) de uma collection.

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

Exclui todos os documentos da collection
```
db.series.deleteMany({})
```

### Find
Realizar consultas

Retornar todos
```
db.series.find()
```

#### Projeção
> Como segundo parâmetro do método find temos a projeção que especifica quais campos serão exibidos. 
> Quando 1 é exibido e quando 0 não é exibido

Retornar todos onde serão exibidos apenas os campos Série e Ano de Lançamento
```
db.series.find({}, {"Série": 1, "Ano de lançamento": 1, "_id": 0})
```




