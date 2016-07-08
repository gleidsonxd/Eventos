# Eventos


Para criar um evento, deve-se enviar alguns parametros:

```
param nome,        String,      required, nome do evento
param servicos,    Array[Int],            id do serviço
param lugar,       String,      required, nome do local, deve-se fazer um teste de msm locais na mesma data
param dataIni,     String,      required, no formato dd/MM/yyyy HH:mm
param dataFim,     String,      required, no formato dd/MM/yyyy HH:mm. Fazer validação das datas.
param desc,        String,                a descrição do sistema
param user,        String,                email do usuario que está solicitando a criação do evento
```  
  

```
POST /createEvento
curl -d "user=daniel@ifpb.gov.br&nome=Evento tal&servicos=[1,2,3]&lugar=Patio&dataIni=10/10/2010 09:00&dataFim=10/10/2010 12:00&desc=Descricao Tall" localhost:3000/createEvento

Retorna o ID do evento criado:
HTTP/1.1 200 Ok
{
 "id":"1"
 "message":"evento criado com sucesso"
}
```
