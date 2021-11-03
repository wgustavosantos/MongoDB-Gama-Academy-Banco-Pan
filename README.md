# Atividade MongoDB
Você deve criar um banco de dados novo (database) e uma coleção com um nome pertinente, de acordo com os dados e tema que você escolher. Os seguintes comandos devem ser feitos e entregues:
- Inserção de documentos
- Atualização de documentos
- Exclusão de documentos
- Consulta com projeção
- Consulta utilizando combinação entre os seletores
- Consulta paginada e ordenada (utilizar ignorar , limitar e classificar )

#### Criando o banco de dados

```use Locadora```

![image](https://github.com/wgustavosantos/MongoDB-Gama-Academy-Banco-Pan/blob/main/prints/use%20Locadora.PNG)

O banco não irá ser listado caso não contenha nenhuma coleção criada, porém, ele está selecionado.

#### Criando a coleção filmes

```db.createCollection('filmes')```

![image](https://github.com/wgustavosantos/MongoDB-Gama-Academy-Banco-Pan/blob/main/prints/cria%C3%A7%C3%A3o%20da%20cole%C3%A7%C3%A3o.PNG)

#### Inserindo um documento na coleção filmes

```
db.filmes.insertOne({ nome: "Stalker", diretor: "Andrei Tarkovsky", ano: NumberInt(1979), genero: "drama/ficcao cientifica", classificacao: "12 anos", status: "disponivel"})
```

![image](https://github.com/wgustavosantos/MongoDB-Gama-Academy-Banco-Pan/blob/main/prints/InsertOne.PNG)

#### Inserindo vários documentos na coleção filmes

```
db.filmes.insertMany([
	{nome: "2001 - Uma Odisseia no Espaco", diretor: "Stanley Kubrick", ano: NumberInt(1968), genero: "drama/ficcao cientifica", classificacao: "12 anos", status: "disponivel"},
	{nome: "Her", diretor: "Spike Jonze", ano: NumberInt(2013), genero: "drama/ficcao cientifica", classificacao: "14 anos", status: "disponivel"},
	{nome: "O Sétimo Selo", diretor: "Ingmar Bergman", ano: NumberInt(1957), genero: "drama/fantasia", classificacao: "12 anos", status: "disponivel"},
	{nome: "Taxi Driver", diretor: "Martin Scorsese", ano:NumberInt(1976), genero: "drama", classificacao: "14 anos", status: "indisponivel"},
	{nome: "Trainspotting - Sem Limites", diretor: "Danny Boyle", ano:NumberInt(1996), genero: "Drama/Humor negro", classificacao: "16 anos", status: "indisponivel"},
	{nome: "Interestelar", diretor: "Christopher Nolan", ano: NumberInt(2014), genero: "drama/ficcao cientifica", classificacao: "14 anos", status: "disponivel"},
	{nome: "A Rede Social", diretor: "David Fincher", ano: NumberInt(2011), genero: "Ficcao Historica", classificacao: "14 anos", status: "indisponivel"}
])
```
#### Consultando todos os documentos da coleção
```db.filmes.find()```

#### CONSULTA COM PROJEÇÃO - Mostrando apenas a field nome
"_id": 0 -> retorna a consulta sem o Objectld

```db.getCollection('filmes').find({}, {nome: 1, "_id": 0})```


![image](https://github.com/wgustavosantos/MongoDB-Gama-Academy-Banco-Pan/blob/main/prints/Consultando%20a%20fild%20nome%20sem%20_id.PNG)

``` db.getCollection('filmes').find({}, {nome: 1}) ``` -> retorna com o objectld

![image](https://github.com/wgustavosantos/MongoDB-Gama-Academy-Banco-Pan/blob/main/prints/Consultando%20a%20fild%20nome%20com%20_id.PNG)

#### CONSULTA COM PROJEÇÃO - Mostrando somente as fields com filmes disponíveis

``` db.getCollection('filmes').find({status:"disponivel"}) ```

![image](https://github.com/wgustavosantos/MongoDB-Gama-Academy-Banco-Pan/blob/main/prints/filds%20com%20filmes%20disponiveis.PNG)

#### UPDATE - Atualizando o a field filme Her de "disponivel" para "indisponível"

``` db.filmes.updateOne({nome: "Her"  },{$set: {status: "indisponivel" } } ) ```

![image](https://github.com/wgustavosantos/MongoDB-Gama-Academy-Banco-Pan/blob/main/prints/Her.PNG)

#### UPDATE em vários - Atualizando fields, caso não exista a field especificada, o MongoDB criará 
No caso, criou a field "NoEstoque" do tipo boolean, atribuindo o valor true para todos, no caso, todos os "filmes" do banco estão no estoque da "locadora"

```db.filmes.updateMany({}, {$set: {NoEstoque: true} } )```

![image](https://github.com/wgustavosantos/MongoDB-Gama-Academy-Banco-Pan/blob/main/prints/Update%20em%20v%C3%A1rios.PNG)

#### DELETE
```db.filmes.deleteOne({nome: "Trainspotting - Sem Limites"} )```

#### CONSULTA COM PROJEÇÃO - Mostrando filmes produzidos após os anos 2000 incluido o ano 2000 e ignorando 1 resultado
db.getCollection('filmes').find({ano: {$gte: 2000},}) -> Consultando. 

skip(1) -> ignorando 1 resultado

```db.getCollection('filmes').find({ano: {$gte: 2000},}).skip(1)```

![image](https://github.com/wgustavosantos/MongoDB-Gama-Academy-Banco-Pan/blob/main/prints/Pos2Kskip1.PNG)

#### CONSULTA COM PROJEÇÃO - Mostrando filmes produzidos antes dos anos 2000 incluido o ano 2000 e limitando a 2 resultados
db.getCollection('filmes').find({ano: {$lte: 2000},}) -> Consultando.

limit(2) -> ignorando 1 resultado

```db.getCollection('filmes').find({ano: {$lte: 2000},}).limit(2)```

![image](https://github.com/wgustavosantos/MongoDB-Gama-Academy-Banco-Pan/blob/main/prints/Antes2Klimit2.PNG)

#### CONSULTA COM PROJEÇÃO - Mostrando filmes por ano de produção em ordem decrescente

```db.getCollection('filmes').find().sort({ano: -1})```

![image](https://github.com/wgustavosantos/MongoDB-Gama-Academy-Banco-Pan/blob/main/prints/decrescente.PNG)

