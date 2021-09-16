# Mongo-DB-e-Spring-Data-MongoDB

### Start Docker Local
```shell
docker-compose  up
```

ou

```shell
docker run -d -p 27017:27017 --name mongo-rio-talks -e MONGO_INITDB_ROOT_USERNAME=mongoadmin -e MONGO_INITDB_ROOT_PASSWORD=secret mongo
```

# FIND

### mongoshel login

```shell
    mongosh "mongodb://127.0.0.1:27017" --username mongoadmin --password secret --authenticationDatabase admin
```

---
> A primeira é que não há um comando **criar** no MongoDB Shell.
> Para criar um banco de dados você usa o comando use. Se o banco de dados não existir, então o cluster do MongoDB irá criá-lo.

```shell
use nome_da_base_de_dados
```

---

> Isso é tudo o que você tem de fazer. O banco de dados é criado. Mas isso nos leva ao segundo ponto. Mesmo que o banco de dados exista, se você inserir o comando show dbs</strong>, ele se parecerá com isto:

```shell
show dbs
```

---

> Mas onde está a minha base que acabei de criar?
>
> O segundo ponto é que o banco de dados não é totalmente criado até que você coloque algo nele.
> Para adicionar um documento ao seu banco de dados, use o comando `db.**collection**.insert()`.

```shell
db.user.insert({nome: "José Ricardo da Silva Dainese", idade: 28})
```

---

> Agora, se você executar o comando show dbs, você verá seu banco de dados.

```shell
show dbs
```

---

>
> Trocar de database

```shell
use riotalks
```

---

> Fazer busca

```shell
db.usuario.find()
```

---

> Fazer busca filtrando

```shell
    db.usuario.find({"nome":"José Ricardo da Silva Dainese"})
```

---

> Ordenando crescente

```shell
    db.usuario.find().sort({"nome": 1})
```

---

> Ordenando decrescente

```shell
    db.usuario.find().sort({"nome": -1})
```

---

# GERENCIANDO USUÁRIOS

> Listar Usuários

```shell
db.getUsers()
{ users: [], ok: 1 }
```

---

> Gerenciar Usuários

```shell
db.createUser({user: "riotalks", pwd: "riotalks", roles: [{role:"readWrite", db:"riotalks"}]})
{ ok: 1 }
```

> Roles

### read

> Ler dados das bases de dados epecificadas exceto bases de dados de sistema.

### readWrite

> Ler e modificar dados das bases de dados epecificadas exceto bases de dados de sistema.

> Esta permissão da acesso as coleções abaixo

* collStats
* convertToCapped
* createCollection
* dbHash
* dbStats
* dropCollection
* createIndex
* dropIndex
* find
* insert
* killCursors
* listIndexes
* listCollections
* remove
* renameCollectionSameDB
* update

### dbAdmin

> Da a permissão de executar tarefas administrativas relacionadas a esquemas, indexação e dados estatisticos.
> Não da permissão para gerenciar usuaários e funções de usuários

### dbOwner

> Permite executar tarefas administrativas

### userAdmin

> Pode modificar as regras de acesso dos usuários

* changeCustomData
* changePassword
* createRole
* createUser
* dropRole
* dropUser
* grantRole
* revokeRole
* setAuthenticationRestriction
* viewRole
* viewUser
  [👉🏻 Veja Todas as Roles](https://docs.mongodb.com/manual/reference/built-in-roles/)

---

> Atualizar usuario

```shell

db.createUser({user: "josesd", pwd: "1234", roles: [{role:"readWrite", db:"riotalks"}]})


db.createUser({user: "user1", pwd: "user1", roles: [{role:"readWrite", db:"riotalks"}]})
db.auth("user1", "user1")
db.createUser({user: "user2", pwd: "user2", roles: [{role:"readWrite", db:"riotalks"}]})
db.updateUser("user1", { pwd: "123", roles: ["readWrite", "userAdmin"] });
db.createUser({user: "user2", pwd: "user2", roles: [{role:"readWrite", db:"riotalks"}]})
db.auth("user2", "user2")
db.createUser({user: "user3", pwd: "user3", roles: [{role:"readWrite", db:"riotalks"}]})

```

---

> Autenticar com Usuário

```shell
db.auth("josesd", "142022")
{ ok: 1 }
```

```shell
db.auth("jose", "00000")
MongoServerError: Authentication failed.
```

---

> Listar Usuários

```shell
db.getUsers()
{
  users: [
    {
      _id: 'test.jose',
      userId: UUID("a330867c-1987-4fc4-9495-c811cc962399"),
      user: 'josesd',
      db: 'test',
      roles: [ { role: 'readWrite', db: 'riotalks' } ],
      mechanisms: [ 'SCRAM-SHA-1', 'SCRAM-SHA-256' ]
    }
  ],
  ok: 1
}
```

---

> Deletar Usuário

```shell
db.dropUser("ze")
{ ok: 1 }
```

# Spring Data MongoDB

```java
Query query = new Query();
query.addCriteria(Criteria.where("id").is("iHA5GROvEF1Xe7BkPp7dY"));

Update update = new Update();
update.set("nome", "Carlos");
this.mongoTemplate.updateFirst(query, update, User.class);
````