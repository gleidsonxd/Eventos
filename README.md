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
curl -d "user=daniel@ifpb.gov.br&nome=Evento tal&servicos=[1,2,3]&lugar=[Patio]&dataIni=10/10/2010 09:00&dataFim=10/10/2010 12:00&desc=Descricao Tall" localhost:3000/createEvento

Retorna o ID do evento criado:
HTTP/1.1 200 Ok
{
 "id":"1"
 "message":"evento criado com sucesso"
}
```
---

###Update

O usuario que criar um evento tambem vai poder alterar esse evento. Para atualizar um
evento, deve-se enviar alguns parametros:

```
param nome,        String,          required, nome do evento
param servicos,    Array[Int],                id do serviço
param lugar,       Array[String],   required, nome do local, deve-se fazer um teste de msm locais na mesma data
param dataIni,     String,          required, no formato dd/MM/yyyy HH:mm
param dataFim,     String,          required, no formato dd/MM/yyyy HH:mm. Fazer validação das datas.
param desc,        String,                    a descrição do evento
param user,        String,                    email do usuario que criou o evento
param userU,       String,                    email do usuario que alterou o evento
```  

```
PUT /updateEvento
curl -d "user=user@email.com&nome=Evento_Mod tal&servicos=[1,2,3]&lugar=[Patio]
&dataIni=10/10/2010 09:00&dataFim=10/10/2010 12:00&desc=Descricao Tall_mod&userU=usermod@email.com" localhost:3000/updateEvento


Retorna o ID do evento alterado:
HTTP/1.1 200 Ok
{
 "id":"2"
 "message":"evento alterado com sucesso"
}
```
---
###DELETE

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

O usuario administrador vai poder alterar os serviços. Para atualizar um
serviço, deve-se enviar alguns parametros:

```
param nome,        String,      required, nome do evento
param tempo,       Int,         required, tempo para o servico ficar pronto. Tempo em dias
param coord,       String       required, nome da coordenacao que oferece o servico
```  

```
PUT /updateServico
curl -d "nome=Nome_Servico_Mod&tempo=20&coord=Coordenacao_eventos"localhost:3000/updateServico


Retorna o ID do serviço alterado:
HTTP/1.1 200 Ok
{
 "id":"2"
 "message":"serviço alterado com sucesso"
}
```
---
###Delete
###Read

##Usuario

###Create

Os usuarios do sistema vão se logar utilizando o email institucional, na primeira
que se logarem no sistema, irão completar seu cadastro no sistema. Para criar um
usuario, deve-se enviar alguns parametros:

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

O usuario vai poder alterar os dados do seu cadastro. Para atualizar um
usuario, deve-se enviar alguns parametros:

```
param nome,        String,      required, nome do usuario

```

```
PUT /updateUsuario
curl -d "nome=Nome_Usuario_Mod"localhost:3000/updateUsuario

Retorna a mensagem de sucesso:
HTTP/1.1 200 Ok
{
 
 "message":"Nome alterado com sucesso"
}
```
---
###Delete
###Read

##Lugar

###Create

É necessario cadastrar os lugares antes de se cadastrar um eventos. Para criar um
lugar, deve-se enviar alguns parametros:

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

O usuario administrado vai poder alterar os dados dos locais cadastrados. Para atualizar um
lugar, deve-se enviar alguns parametros:

```
param nome,        String,      required, nome do lugar
param qntPessoas,  Int,         required, quantidade de pessoas

```

```

PUT /updateLugar
curl -d "nome=Patio&qntPessoas=250"localhost:3000/updateLugar

Retorna o ID do lugar alterado:
HTTP/1.1 200 Ok
{
  "id":"1"
  "message":"Lugar alterado com sucesso"
}
```
---
###Delete
###Read
---

##Coordenação
###Create

É necessario cadastrar as coordenações antes de se cadastrar um serviço. Para criar uma 
coordenação, deve-se enviar alguns parametros:

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

O usuario administrado vai poder alterar os dados dos locais cadastrados. Para atualizar um
lugar, deve-se enviar alguns parametros:

```
param nome,        String,      required, nome da coordenação

```

```
PUT /updateCoord
curl -d "nome=Coordenacao_eventos"localhost:3000/updateCoord

Retorna o ID da coordenação alterada:
HTTP/1.1 200 Ok
{
  "id":"1"
  "message":"Coordenação alterada com sucesso"
}
```
---
###Delete
###Read
---
