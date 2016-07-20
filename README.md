# Eventos API

##Eventos

###Create

Para criar um evento, deve-se enviar alguns parametros:

```
param nome,        String,          required, nome do evento
param servicos,    Array[Int],                id do serviço
param lugar,       Array[String],   required, nome do local, deve-se fazer um teste de msm locais na mesma data
param dataIni,     String,          required, no formato dd/MM/yyyy HH:mm
param dataFim,     String,          required, no formato dd/MM/yyyy HH:mm. Fazer validação das datas.
param desc,        String,                    a descrição do sistema
param user,        String,                    email do usuario que está solicitando a criação do evento
```  
  
```
POST /createEvento
curl -d "user=user@email.com&nome=Evento tal&servicos=[1,2,3]&lugar=[Patio]&dataIni=10/10/2010 09:00&dataFim=10/10/2010 12:00&desc=Descricao Tall" localhost:3000/createEvento

Retorna o ID do evento criado:
HTTP/1.1 200 Ok
{
 "id":"1"
 "message":"evento criado com sucesso"
}
```
---

###Update

O usuario que criar um evento tambem vai poder alterar esse evento. Para atualizar um evento, deve-se enviar alguns parametros:

```
param id           Int              required, id do evento
param nome,        String,          required, nome do evento
param servicos,    Array[Int],                id do serviço
param lugar,       Array[String],   required, nome do local, deve-se fazer um teste de msm locais na mesma data
param dataIni,     String,          required, no formato dd/MM/yyyy HH:mm
param dataFim,     String,          required, no formato dd/MM/yyyy HH:mm. Fazer validação das datas.
param desc,        String,                    a descrição do evento
param userU,       String,                    email do usuario que alterou o evento
```  

```
PUT /updateEvento
curl -d "id=2&&nome=Evento_Mod tal&servicos=[1,2,3]&lugar=[Patio]
&dataIni=10/10/2010 09:00&dataFim=10/10/2010 12:00&desc=Descricao Tall_mod&userU=usermod@email.com" localhost:3000/updateEvento


Retorna o ID do evento alterado:
HTTP/1.1 200 Ok
{
 "id":"2"
 "message":"evento alterado com sucesso"
}
```
---
###Delete

Um usuario pode apagar um evento que ele criou.

```
DELETE /deleteEvento
curl -X DELETE localhost:3000/deleteEvento/2

Retorna a mensagem de sucesso:
HTTP/1.1 200 Ok
{
 
 "message":"Evento excluido com sucesso"
}
```
---
###Read

O usuario vai poder ver os detalhes dos eventos que criou.Para ver um evento, deve-se acessar a URL:

```
GET/eventos/2

curl localhost:3000/eventos/2

Retorna o JSON:
HTTP/1.1 200 Ok
{
  "eventos":[
    {
      "nome":"nome_evento",
      "servicos":[1,2,3],
      "lugar":["Patio","Auditorio 1"],
      "dataIni":"10/10/2010 09:00",
      "dataFim":"10/10/2010 12:00",
      "desc": "Descricao Tall",
      "user": "user@email.com"
      }
    ]
  }

```
---
###List
O usuario vai poder ver todos os eventos cadastrados.Para ver os eventos, deve-se acessar a URL:

```
GET/eventos

curl localhost:3000/eventos

Retorna o JSON:
HTTP/1.1 200 Ok
{
  "eventos":[
    {
      "nome":"nome_evento",
      "servicos":[1,2,3],
      "lugar":["Patio","Auditorio 1"],
      "dataIni":"10/10/2010 09:00",
      "dataFim":"10/10/2010 12:00",
      "desc": "Descricao Tall",
      "user": "user@email.com"
      },
    {
      "nome":"nome_evento2",
      "servicos":[1,2],
      "lugar":["Patio"],
      "dataIni":"11/10/2010 09:00",
      "dataFim":"12/10/2010 12:00",
      "desc": "Descricao",
      "user": "user2@email.com"
      }
    {
      "nome":"nome_evento3",
      "servicos":[1,2,3,4],
      "lugar":["Patio"],
      "dataIni":"12/10/2010 09:00",
      "dataFim":"13/10/2010 12:00",
      "desc": "Descricao",
      "user": "user1@email.com"
      }
    ]
  }

```
---

##Serviço

###Create

Um serviço é alocado para os eventos. Eles compoem as coisas necessárias para que o evento aconteça. Exemplo: banner, folder, divulgação no site do instituto, filmagens, etc.
Se for criar um evento que precise de um serviço, é necessário criar os serviços primeiro e enviar os ids para o método de criar eventos.
Os serviços não são obrigatórios para a criação de um evento. Os eventos podem ser independentes.
Para criar um serviço, deve-se enviar alguns parametros:

```
param nome,        String,      required, nome do evento
param tempo,       Int,         required, tempo para o servico ficar pronto. Tempo em dias
param coord,       String       required, nome da coordenacao que oferece o servico
```  

```
POST /createServico
curl -d "nome=Nome_Servico&tempo=15&coord=Coordenacao_eventos"localhost:3000/createServico

Retorna o ID do servico criado:
HTTP/1.1 200 Ok
{
 "id":"1"
 "message":"servico criado com sucesso"
}
```
---
###Update

O usuario administrador vai poder alterar os serviços. Para atualizar um serviço, deve-se enviar alguns parametros:

```
param nome,        String,      required, nome do evento
param tempo,       Int,         required, tempo para o servico ficar pronto. Tempo em dias
param coord,       String       required, nome da coordenacao que oferece o servico
```  

```
PUT /updateServico
curl -d "id=2&nome=Nome_Servico_Mod&tempo=20&coord=Coordenacao_eventos"localhost:3000/updateServico


Retorna o ID do serviço alterado:
HTTP/1.1 200 Ok
{
 "id":"2"
 "message":"serviço alterado com sucesso"
}
```
---
###Delete

Um usuario administrador pode apagar um serviço.

```
DELETE /deleteServico
curl -X DELETE localhost:3000/deleteServico/2

Retorna a mensagem de sucesso:
HTTP/1.1 200 Ok
{
 
 "message":"Serviço excluido com sucesso"
}
```
---
###Read

O administrador vai poder ver um serviço específico.Para ver um serviço, deve-se acessar a URL:

```
GET/servicos/1

curl localhost:3000/servicos/1

Retorna o JSON:
HTTP/1.1 200 Ok
{
  "servicos":[
    {
      "nome":"serv1",
      "tempo":15,
      "coord":"coord eventos",
      }    
    ]
  }

```
---
###List

O administrador vai poder ver todos os serviços cadastrados.Para ver os serviços, deve-se acessar a URL:

```
GET/servicos

curl localhost:3000/servicos

Retorna o JSON:
HTTP/1.1 200 Ok
{
  "servicos":[
    {
      "nome":"serv1",
      "tempo":15,
      "coord":"coord eventos",
      },
    {
      "nome":"serv2",
      "tempo":25,
      "coord":"coord 2",
      }
    {
      "nome":"serv3",
      "tempo":30,
      "coord":"coord 3",
      }
    ]
  }

```
---
##Usuario

###Create

Os usuarios do sistema vão se logar utilizando o email institucional, na primeira que se logarem no sistema, irão completar seu cadastro no sistema. Para criar um usuario, deve-se enviar alguns parametros:

```
param nome,        String,      required, nome do usuario
param email,       String,      required, email do usuario
```

```
POST /createUsuario
curl -d "nome=Nome_Usuario&email=usuario@email.com"localhost:3000/createUsuario

Retorna a mensagem de sucesso:
HTTP/1.1 200 Ok
{
  "message":"Usuario criado com sucesso"
}
```
---
###Update

O usuario vai poder alterar os dados do seu cadastro. Para atualizar um usuario, deve-se enviar alguns parametros:

```
param nome,        String,      required, nome do usuario

```

```
PUT /updateUsuario
curl -d "id=2&nome=Nome_Usuario_Mod"localhost:3000/updateUsuario

Retorna a mensagem de sucesso:
HTTP/1.1 200 Ok
{
 
 "message":"Nome alterado com sucesso"
}
```
---
###Delete

Um usuario administrador pode apagar um usuario.

```
DELETE /deleteUsuario
curl -X DELETE localhost:3000/deleteUsuario/2

Retorna a mensagem de sucesso:
HTTP/1.1 200 Ok
{
 
 "message":"Usuario excluido com sucesso"
}
```
---
###Read

O administrador vai poder ver os dados de um usuário específico. Para ver um usuário, deve-se acessar a URL:

```
GET/usuarios/1

curl localhost:3000/usuarios/1

Retorna o JSON:
HTTP/1.1 200 Ok
{
  "usuarios":[
    {
      "nome":"nome_user",
      "email":"user@email.com",
      }    
    ]
  }

```
---
###List

O administrador vai poder ver todos os usuários cadastrados. Para ver os usuários, deve-se acessar a URL:

```
GET/usuarios

curl localhost:3000/usuarios

Retorna o JSON:
HTTP/1.1 200 Ok
{
  "usuarios":[
    {
      "nome":"nome_user",
      "email":"user@email.com",
      },
    {
      "nome":"nome_user2",
      "email":"user2@email.com",
      },
    {
      "nome":"nome_user3",
      "email":"user3@email.com",
      }    
    ]
  }

```
---
##Lugar

###Create

É necessario cadastrar os lugares antes de se cadastrar um eventos. Para criar um lugar, deve-se enviar alguns parametros:

```
param nome,        String,      required, nome do lugar
param qntPessoas,  Int,         required, quantidade de pessoas
```

```
POST /createLugar
curl -d "nome=Patio&qntPessoas=150"localhost:3000/createLugar

Retorna o ID do lugar criado:
HTTP/1.1 200 Ok
{
  "id":"1"
  "message":"Lugar criado com sucesso"
}
```
---
###Update

O usuario administrador vai poder alterar os dados dos locais cadastrados. Para atualizar um lugar, deve-se enviar alguns parametros:

```
param nome,        String,      required, nome do lugar
param qntPessoas,  Int,         required, quantidade de pessoas

```

```

PUT /updateLugar
curl -d "id=1&nome=Patio&qntPessoas=250"localhost:3000/updateLugar

Retorna o ID do lugar alterado:
HTTP/1.1 200 Ok
{
  "id":"1"
  "message":"Lugar alterado com sucesso"
}
```
---
###Delete

Um usuario administrador pode apagar um lugar cadastrado.

```
DELETE /deleteLugar
curl -X DELETE localhost:3000/deleteLugar/2

Retorna a mensagem de sucesso:
HTTP/1.1 200 Ok
{
 
 "message":"Lugar excluido com sucesso"
}
```
---
###Read

O administrador vai poder ver os dados de um lugar específico. Para ver um lugar, deve-se acessar a URL:

```
GET/lugares/1

curl localhost:3000/lugares/1

Retorna o JSON:
HTTP/1.1 200 Ok
{
  "lugares":[
    {
      "nome":"nome_lugar",
      "qntPessoas":100,
      }       
    ]
  }

```
---
###List

O administrador vai poder ver todos os lugares cadastrados. Para ver os lugares, deve-se acessar a URL:

```
GET/lugares

curl localhost:3000/lugares

Retorna o JSON:
HTTP/1.1 200 Ok
{
  "lugares":[
    {
      "nome":"nome_lugar",
      "qntPessoas":100,
      },
    {
      "nome":"nome_lugar2",
      "qntPessoas":140,
      },
    {
      "nome":"nome_lugar3",
      "qntPessoas":150,
      }    
    ]
  }

```
---

##Coordenação
###Create

É necessario cadastrar as coordenações antes de se cadastrar um serviço. Para criar uma coordenação, deve-se enviar alguns parametros:

```
param nome,        String,      required, nome da coordenação
```

```
POST /createCoord
curl -d "nome=Coordenacao_eventos"localhost:3000/createCoord

Retorna o ID da coordenação criada:
HTTP/1.1 200 Ok
{
  "id":"1"
  "message":"Coordenação criada com sucesso"
}
```
---
###Update

O usuario administrado vai poder alterar os dados dos locais cadastrados. Para atualizar um lugar, deve-se enviar alguns parametros:

```
param nome,        String,      required, nome da coordenação

```

```
PUT /updateCoord
curl -d "id=1&nome=Coordenacao_eventos"localhost:3000/updateCoord

Retorna o ID da coordenação alterada:
HTTP/1.1 200 Ok
{
  "id":"1"
  "message":"Coordenação alterada com sucesso"
}
```
---
###Delete

Um usuario administrador pode apagar uma coordenação cadastrada.

```
DELETE /deleteCoord
curl -X DELETE localhost:3000/deleteCoord/2

Retorna a mensagem de sucesso:
HTTP/1.1 200 Ok
{
 
 "message":"Coordenação excluida com sucesso"
}
```
---
###Read

O administrador vai poder ver os dados de uma coordenação específica. Para ver uma coordenação, deve-se acessar a URL:

```
GET/coord/1

curl localhost:3000/coord/1

Retorna o JSON:
HTTP/1.1 200 Ok
{
  "coords":[
    {
      "nome":"coord_eventos"      
      }       
    ]
  }

```
---
###List

O administrador vai poder ver todas as coordenações cadastradas. Para ver as coordenações, deve-se acessar a URL:

```
GET/coords

curl localhost:3000/coords

Retorna o JSON:
HTTP/1.1 200 Ok
{
  "coords":[
    {
      "nome":"coord_eventos"      
      } 
    {
      "nome":"coord2"      
      } 
    {
      "nome":"coord3"      
      }       
    ]
  }

```
---
