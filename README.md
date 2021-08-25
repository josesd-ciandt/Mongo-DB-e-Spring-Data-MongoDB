# Mongo-DB-e-Spring-Data-MongoDB

# FIND
### mongoshel login

```shel   
    mongosh "mongodb://127.0.0.1:27017" --username mongoadmin --password secret --authenticationDatabase admin
```

### trocar de database

```shel   
    use riotalks
```

### fazer busca

```shel   
    db.usuario.find()
```

### fazer busca filtrando

```shel   
    db.usuario.find({"nome":"José Ricardo da Silva Dainese"})
```

### ordenando crescente

```shel   
    db.usuario.find().sort({"nome": 1})
```
### ordenando decrescente

```shel   
    db.usuario.find().sort({"nome": -1})
```

# GERENCIANDO USUÁRIOS

## Listar Usuários
```shel  
db.getUsers()
{ users: [], ok: 1 }
```
## Gerenciar Usuários
```shel  
db.createUser({user: "josesd", pwd: "142022", roles: [{role:"readWrite", db:"riotalks"}]})
{ ok: 1 }
```

## Autenticar com Usuário
```shel  
db.auth("josesd", "142022")
{ ok: 1 }
```

```shel  
db.auth("josesd", "142021")
MongoServerError: Authentication failed.
```

## Listar Usuários
```shel  
db.getUsers()
{
  users: [
    {
      _id: 'test.josesd',
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


### Deletar Usuário

```shel   
db.dropUser("ze")
{ ok: 1 }
```

