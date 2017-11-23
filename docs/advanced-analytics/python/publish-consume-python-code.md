---
title: "Publicar e consumir o código Python | Microsoft Docs"
ms.custom: 
ms.date: 11/09/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: b060d27376b17709bd0f3fc8f39b8e01a6702e6b
ms.sourcegitcommit: ec5f7a945b9fff390422d5c4c138ca82194c3a3b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/11/2017
---
# <a name="publish-and-consume-python-web-services"></a>Publicar e consumir serviços web do Python

Você pode implantar um solução de Python de trabalho para um serviço web usando o recurso de operacionalização no servidor de aprendizado de máquina do Microsoft. Este tópico descreve as etapas para publicar com êxito e, em seguida, executar sua solução.

O público-alvo deste artigo é cientistas de dados que desejam saber como publicar modelos ou código Python como serviços web hospedados no servidor de aprendizado de máquina do Microsoft. O artigo também explica como os aplicativos podem consumir o o código ou modelos. Este artigo pressupõe que você tiver experiência em Python.

> [!IMPORTANT]
>
> Esse exemplo foi desenvolvido para a versão do Python que está incluído no aprendizado de máquina Server (autônomo) e usa recursos na versão do servidor de aprendizado de máquina **9.1.0**.
 > 
 > Clique no link a seguir para ver o mesmo exemplo, republicado usando as bibliotecas mais recentes no servidor de aprendizado de máquina. Consulte [implantar e gerenciar serviços web no Python](https://docs.microsoft.com/machine-learning-server/operationalize/python/how-to-deploy-manage-web-services).

**Aplica-se a: Microsoft R Server (autônomo)**

## <a name="overview-of-workflow"></a>Visão geral do fluxo de trabalho

O fluxo de trabalho de publicação para consumir um serviço web de Python pode ser resumido da seguinte maneira:

1. Atender a [pré-requisito](#prereq) de gerar a biblioteca de cliente do Python do documento principal Swagger de API.
2. Adicione lógica de autenticação e de cabeçalho para o seu script de Python.
3. Criar uma sessão de Python, prepare o ambiente e criar um instantâneo para preservar o ambiente.
4. Publicar o serviço web e inserir esse instantâneo.
5. Testar o serviço web, consumi-las na sua sessão.
6. Gerencie esses serviços.

![Fluxo de trabalho de swagger](./media/data-scientist-python-workflow.png)

Este artigo descreve cada etapa do fluxo de trabalho e inclui o código Python de exemplo usando o conjunto de dados íris.

## <a name="sample-code"></a>Código de exemplo

Esse código de exemplo supõe que foram satisfeitas a [pré-requisitos](#prereq) para gerar uma biblioteca de cliente do Python de que Swagger de arquivo e que você usou Autorest.

Após o bloco de código, você encontrará instruções passo a passo com descrições mais detalhadas do processo de conclusão.

> [!IMPORTANT]
> Este exemplo usa o local `admin` conta para autenticação. No entanto, você deve substituir as credenciais e [método de autenticação](#python-auth) configurado pelo seu administrador.

```python
##################################################
##       IMPORT GENERATED CLIENT LIBRARY        ##
##################################################

# Import the generated client library. 

import deployrclient

# This example is intended for use with Microsoft R Server 9.0.1. 
# If you are using a newer version of Machine Learning Server, 
# use the mrs_server library instead.

##################################################
##              AUTHENTICATION                  ##
##################################################

#Using client library generated from Autorest
#Create client instance and point it at an R Server. 
#In this case, R Server is local.
client = deployrclient.DeployRClient("http://localhost:12800")
# To use ML Server, replace with mrs_server.MRSServer()

#Define the login request and provide credentials 
#Update values with the connection parameters from your admin
login_request = deployrclient.models.LoginRequest("<<your-username>>","<<your-password>>")

#Make a call to the /login API. 
#Store the returned an access token in a variable.
token_response = client.login(login_request)

#Add the returned access token to the headers variable.
headers = {"Authorization": "Bearer {0}".format(token_response.access_token)}

#Verify that the server is running.
#Remember to include `headers` in all requests!
status_response = client.status(headers) 
print(status_response.status_code)


##################################################
##        CREATE SESSION, MODEL, SNAPSHOT       ##
##################################################

#Since already logged in, create a Python session.
#Define session using name (`Session 1`) and `runtime_type="Python"`.
#Remember to specify the Python runtime type.
create_session_request = deployrclient.models.CreateSessionRequest("Session 1", runtime_type="Python")

#Make the call to start the session. 
#Remember to include headers in all method calls to the server.
#Returns a session ID.
response = client.create_session(create_session_request, headers) 
   
#Store the session ID in a variable called `session_id` 
#to be able to identify it later at execution time.
session_id = response.session_id

#Create model - Import SVM and datasets from the SciKit-Learn library
execute_request = deployrclient.models.ExecuteRequest("from sklearn import svm\nfrom sklearn import datasets")
execute_response = client.execute_code(session_id,execute_request, headers)
#Report if it was a success
execute_response.success
   
#Define the untrained Support Vector Classifier (SVC) object
#and the dataset to be preloaded.
execute_request = deployrclient.models.ExecuteRequest("clf=svm.SVC()\niris=datasets.load_iris()\nnames={0:'I. setosa',1:'I. versicolor',2:'I. virginica'}")
#Now, go create the object and preload Iris Dataset in R Server
execute_response = client.execute_code(session_id,execute_request, headers)
#Report if it was a success
execute_response.success
   
#Define two rows from the Iris Dataset as a sample for scoring
workspace_object = deployrclient.models.WorkspaceObject("species_1",[7,3.2,4.7,1.4])
workspace_object_2 = deployrclient.models.WorkspaceObject("species_2",[3,2.6,3,2.5])

#Define how to train the classifier model; what to predict; what to return
execute_request = deployrclient.models.ExecuteRequest(
    "clf.fit(iris.data, iris.target)\n"+
    "result=clf.predict(species_1)\n"+
    "other_result=clf.predict(species_2)",
    [workspace_object,workspace_object_2], #Input
    ["result", "other_result"]) #Output

#Now, go train that model on the Iris Dataset in R Server
execute_response = client.execute_code(session_id,execute_request, headers)

#If successful, print name and result of each output parameter. Else, print error.
if(execute_response.success):
    for result in execute_response.output_parameters:
        print("{0}: {1}".format(result.name,result.value))
else:
    print (execute_response.error_message)

#Create a snapshot of the current session
response = client.create_snapshot(session_id, deployrclient.models.CreateSnapshotRequest("Iris Snapshot"), headers)
#Return the snapshot ID for reference when you publish later.
response.snapshot_id
#If you forget the ID, list snapshots to get the ID again.
for snapshot in client.list_snapshots(headers):
    print(snapshot)

##################################################
##        PUBLISH AS A SERVICE IN PYTHON        ##
##################################################

#Define a web service that determines the iris species by scoring 
#a vector of sepal length and width, petal length and width

#Set `flower_data` for the sepal and petal length and width
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
#Set `iris_species` for the species of iris
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "vector")

#Define the publish request for the web service and its arguments.
#Specify the code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
       code = "iris_species = [names[x] for x in clf.predict(flower_data)]", 
       input_parameter_definitions = [flower_data], 
       output_parameter_definitions = [iris_species],
       runtime_type = "Python",
       snapshot_id = response.snapshot_id)

#Publish the service using the specified name (iris), version (V1.0)
client.publish_web_service_version("Iris", "V1.0", publish_request, headers)

##################################################
##           CONSUME SERVICE IN PYTHON          ##
##################################################

# Inspect holdings and metadata for service Iris V1.0.
for service in client.get_web_service_version("Iris","V1.0", headers):
    #print service metadata (description, who published,...)
    print(service)
    #Print input and output parameters as defined in service definition object
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))

#Import the requests library to make requests on the server
import requests
#Import the JSON library to use for pretty printing of json responses
import json

#Create a requests `Session` object.
s = requests.Session()

#Record the R Server endpoint URL hosting the web services you created before
url = "http://localhost:12800"

#Give the request.Session object the authentication headers 
#so you don't have to repeat it with each request.
s.headers = headers

#Retrieve the service-specific swagger file using the requests library.
swagger_resp = s.get(url+"/api/Iris/V1.0/swagger.json")

#Either, download service-specific swagger file using the json library.
with open('iris_swagger.json','w') as f:
   (json.dump(client.get_web_service_swagger("Iris","V1.0",headers),f, indent = 1))

#Or, print just what you need from the Swagger file, 
#such as the routing paths for the endpoints to be consumed.
print(json.dumps(swagger_resp.json()["paths"], indent = 1, sort_keys = True))

#Or, print input and output parameters as defined in the Swagger.io format
print("Input")
print(json.dumps(swagger_resp.json()["definitions"]["InputParameters"], indent = 1, sort_keys = True))
print("Output")
print(json.dumps(swagger_resp.json()["definitions"]["WebServiceResult"], indent = 1, sort_keys = True))

#Make the request to consume the service using these flower_data inputs
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[7,3.2,4.7,1.4]})
#Print the output
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Use input from another Iris species.
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[3,2.6,3,2.5]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Use input from another Iris species.
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

##################################################
##          MANAGE SERVICES IN PYTHON           ##
##################################################

#Define what needs to be updated. Here we add a description.
#Be sure to specify the runtime_type again.
update_request = deployrclient.models.PublishWebServiceRequest(
    description = "Determines iris species using length and width of sepal and petal", runtime_type = "Python")
#Now update it by specifying the service name and version number
client.patch_web_service_version("Iris", "V1.0", update_request, headers)

#Or, publish another version of the web service, but this time 
#the service returns the species as a string instead of list of strings.
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "string")
 
#Define the publish request for the service and its arguments.
#Specify the changed code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
    code = "iris_species = [names[x] for x in clf.predict(flower_data)][0]",
    description = "Determines the species of iris, based on Sepal Length, Sepal Width, Petal Length and Petal Width",
    input_parameter_definitions = [flower_data],
    output_parameter_definitions = [iris_species],
    runtime_type = "Python",
    snapshot_id = response.snapshot_id)
 
#Now, publish the service with version (V2.0)
client.publish_web_service_version("Iris", "V2.0", publish_request, headers)
 
#Make request to consume service using these flower_data inputs; print output
resp = s.post(url+"/api/Iris/V2.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Return the list of all existing web services.
for service in client.get_all_web_services(headers):
    #print the service information
    print(service)
    #Print each input and output parameter
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))

#Delete the second version we just published.
client.delete_web_service_version("Iris","V2.0",headers)
```

## <a name="walkthrough"></a>Passo a passo

Esta seção descreve como o código funciona em mais detalhes.


### <a name="prereq"></a>Etapa 1. Criar bibliotecas de cliente de pré-requisito

Antes de começar a publicar seu Python código e modelos thorugh Microsoft Server de aprendizado de máquina, você deve gerar uma biblioteca de cliente usando o documento de Swagger fornecido nesta versão.

1. Instale um gerador de código de Swagger em seu computador local e se familiarizar com ele. Você o usará para gerar as bibliotecas de cliente de API em Python. Ferramentas populares incluem [Azure AutoRest](https://github.com/Azure/autorest) (requer o Node. js) e [Swagger Codegen](https://github.com/swagger-api/swagger-codegen). 

2. Baixe o arquivo Swagger que contém os principais APIs para sua versão do servidor de aprendizado de máquina. Esse arquivo contém um modelo de Swagger define a lista de recursos REST e as operações que podem ser chamadas nesses recursos. Você pode encontrar esse arquivo em `https://microsoft.github.io/deployr-api-docs/swagger/<version>/rserver-swagger-<version>.json`, onde `<version>` é o número de versão do servidor de R de 3 dígitos. 

   Por exemplo, para R Server 9.1 você deve baixar de: https://microsoft.github.io/deployr-api-docs/9.1.0/swagger/rserver-swagger-9.1.0.json

3. Gerar a biblioteca de cliente gerado estaticamente, passando o `rserver-swagger-<version>.json` o arquivo para o gerador de código Swagger e especificar o idioma desejado. Nesse caso, você deve especificar Python.  

    Por exemplo, se você usar AutoRest para gerar uma biblioteca de cliente do Python, pode ser algo como este, em que o número de 3 dígitos representa o número de versão do servidor de R:
    
    `AutoRest.exe -Input rserver-swagger-9.1.0.json -CodeGenerator Python  -OutputDirectory C:\Users\rserver-user\Documents\Python`

4. Você também pode fornecer alguns cabeçalhos personalizados e fazer outras alterações antes de usar o cliente gerada stub de biblioteca. Consulte o [Interface de linha de comando](https://github.com/Azure/autorest/blob/master/docs/user/cli.md) documentação no GitHub para obter detalhes sobre as diferentes opções de configuração e de preferências, como renomear o namespace.
   
5. Explore a biblioteca principal do cliente para ver as diversas chamadas de API, que você pode fazer. 

    Em nosso exemplo, Autorest gerado alguns diretórios e arquivos para a biblioteca de cliente do Python em seu sistema local. Por padrão, o namespace (e diretório) são `deployrclient` e pode ter esta aparência:
   
   ![Caminho de saída Autorest](./media/data-scientist-python-autorest.png)

    Para esse namespace padrão, a biblioteca de cliente é chamada `deploy_rclient.py`. Se você abrir esse arquivo em seu IDE como o Visual Studio, você verá algo assim:
   
   ![Biblioteca de cliente do Python](./media/data-scientist-python-client-library.png)


### <a name="step-2-add-authentication-and-header-logic"></a>Etapa 2. Adicionar lógica de autenticação e de cabeçalho

Tenha em mente que todas as APIs exigem autenticação. Portanto, todos os usuários devem autenticar ao fazer uma API chamada usando o `POST /login` API ou por meio do Azure Active Directory (AAD). 

Para simplificar esse processo, os tokens de acesso de portador são emitidos para que os usuários não precisam fornecer suas credenciais para cada chamada.  Esse token de portador é um token de segurança leve que concede o acesso de "portador" a um recurso protegido: nesse caso, as APIs do servidor de aprendizado de máquina. Depois que um usuário for autenticado, o aplicativo deve validar o token de portador do usuário para garantir que a autenticação foi bem-sucedida para as partes planejadas. Para saber mais sobre como gerenciar esses tokens, consulte [Tokens de acesso de segurança](https://msdn.microsoft.com/microsoft-r/operationalize/security-access-tokens).

Antes de você interage com os principais APIs, primeiro autenticar, obter acesso de portador de token usando o [método de autenticação](https://msdn.microsoft.com/microsoft-r/operationalize/security-authentication) configurado pelo seu administrador e, em seguida, incluí-lo em cada cabeçalho de cada solicitação subsequente:

1. Começar importando a biblioteca de cliente para tornar acessível a partir de sua preferência Python editor de código, como Jupyter, Visual Studio, o código de VS ou iPython.

   Especifique o diretório pai da biblioteca do cliente. Em nosso exemplo, a biblioteca de cliente gerada Autorest está sob `C:\Users\rserver-user\Documents\Python\deployrclient`:

   ```python
   # Import the generated client library
   import deployrclient
   ```

2. Adicione a lógica de autenticação ao seu aplicativo para definir uma conexão do computador local para o servidor de aprendizado de máquina, forneça as credenciais, captura o token de acesso, adicione esse token para o cabeçalho. Você, em seguida, usar esse cabeçalho para todas as solicitações subsequentes.  Use o método de autenticação, definido pelo administrador: conta de administrador básico, / LDAP do Active Directory (AD/LDAP) ou do Azure Active Directory (AAD).

   **LDAP/AD ou `admin` autenticação de conta**

   Chamar o `POST /login` API para autenticar. Passe o `username` e `password` para o administrador local, ou se o Active Directory é ativado, passar as informações de conta do LDAP. Por sua vez, o servidor de aprendizado de máquina emite um token de portador/acesso. Depois de autenticado, o usuário não precisa mais fornecer as credenciais novamente, desde que o token ainda é válido e um cabeçalho é enviado com cada solicitação. Se você não souber suas configurações de conexão, entre em contato com seu administrador.

   ```python
   #Using client library generated from Autorest
   #Create client instance and point it at an R Server. 
   #In this case, R Server is local.
   client = deployrclient.DeployRClient("http://localhost:12800")
   
   #Define the login request and provide credentials. 
   #Update values with the connection parameters from your admin.
   login_request = deployrclient.models.LoginRequest("<<your-username>>","<<your-password>>")
   #Make a call to the /login API. 
   #Store the returned an access token in a variable.
   token_response = client.login(login_request)
   ```

   **Autenticação do Active Directory (AAD) do Azure**

   Passar as credenciais AAD, a autoridade e o ID do cliente. Por sua vez, AAD emite o [token de acesso de portador](https://msdn.microsoft.com/microsoft-r/operationalize/security-access-tokens). Depois de autenticado, o usuário não precisa mais fornecer as credenciais novamente, desde que o token ainda é válido e um cabeçalho é enviado com cada solicitação. Se você não souber suas configurações de conexão, entre em contato com seu administrador.

   ```python
   #Import the AAD authentication library
   import adal
   
   #Define the login request and provide credentials. 
   #Use the AAD connection parameters provided by your admin.
   url = "http://localhost:12800"
   authuri = https://login.windows.net,
   tenantid = "<<AAD_DOMAIN>>", 
   clientid = "<<NATIVE_APP_CLIENT_ID>>", 
   resource = "<<WEB_APP_CLIENT_ID>>", 
   
   #Acquire authentication token using AAD Device Code Login
   context = adal.AuthenticationContext(authuri+'/'+tenantid, api_version=None)
   code = context.acquire_user_code(resource, clientid)
   print(code['message'])
   token = context.acquire_token_with_device_code(resource, code, clientid)
   #The authentication code returned must be entered at https://aka.ms/devicelogin 
   ```     

3. Adicionar o `Bearer` acessar token e verifique se o servidor de aprendizado de máquina está sendo executado.  Esse token foi retornado durante a autenticação e **devem ser incluídos em cada cabeçalho de solicitação subsequente**. Este exemplo usa a biblioteca de cliente gerada pelo Autorest.

   > [!IMPORTANT]
   > Todas as chamadas de API devem ser autenticada. Portanto, lembre-se de incluir cabeçalhos de tokens para cada solicitação única.

   ```python
   #Add the returned access token to the headers variable.
   headers = {"Authorization": "Bearer {0}".format(token_response.access_token)}
   
   #Verify that the server is running.
   #Remember to include `headers` in every request!
   status_response = client.status(headers) 
   print(status_response.status_code)
   ```

### <a name="step-3-prepare-session-and-code"></a>Etapa 3. Preparar a sessão e código

Após a autenticação, você pode iniciar uma sessão de Python e criar um modelo para publicar mais tarde. Você pode incluir qualquer código Python ou modelos em um serviço web. Depois de configurar seu ambiente de sessão, você pode salvá-lo mesmo como um instantâneo, você pode recarregar a sessão que você tinha antes. 

> [!IMPORTANT]
> Lembre-se de incluir `headers` em cada solicitação.

1. Crie uma sessão de Python no servidor de R. Certifique-se de especificar um nome e a linguagem Python (`runtime_type="Python"`).  Se você não definir o tipo de tempo de execução para Python, o padrão é R.

   Esta é a continuação do exemplo usando a biblioteca de cliente gerada por Autorest:

   ```python
   #Since already logged in, create a Python session.
   #Define session using name (`Session 1`) and `runtime_type="Python"`.
   #Remember to specify the Python runtime type.
   create_session_request = deployrclient.models.CreateSessionRequest("Session 1", runtime_type="Python")
   
   #Make the call to start the session. 
   #Remember to include headers in every method call to the server.
   #Returns a session ID.
   response = client.create_session(create_session_request, headers) 
   
   #Store the session ID in a variable called `session_id` 
   #to be able to identify it later at execution time.
   session_id = response.session_id
   ```

2. Criar ou chamar um modelo em Python que você usará como um serviço web

   Neste exemplo, vamos treinar um Saiba SciKit suporte vetor máquinas (SVM) modelo em íris Dataset em uma instância remota do servidor de aprendizado de máquina.  Este conjunto de dados está disponível na [scikit-Saiba site](http://scikit-learn.org/stable/auto_examples/datasets/plot_iris_dataset.html).

   ```python
   #Import SVM and datasets from the SciKit-Learn library
   execute_request = deployrclient.models.ExecuteRequest("from sklearn import svm\nfrom sklearn import datasets")
   execute_response = client.execute_code(session_id,execute_request, headers)
   #Report if it was a success
   execute_response.success
   
   #Define the untrained Support Vector Classifier (SVC) object
   #and the dataset to be preloaded.
   execute_request = deployrclient.models.ExecuteRequest("clf=svm.SVC()\niris=datasets.load_iris()\nnames={0:'I. setosa',1:'I. versicolor',2:'I. virginica'}")
   #Now, go create the object and preload Iris Dataset in R Server
   execute_response = client.execute_code(session_id,execute_request, headers)
   #Report if it was a success
   execute_response.success
   
   #Define two rows from the Iris Dataset as a sample for scoring
   workspace_object = deployrclient.models.WorkspaceObject("species_1",[7,3.2,4.7,1.4])
   workspace_object_2 = deployrclient.models.WorkspaceObject("species_2",[3,2.6,3,2.5])

   #Define how to train the classifier model; what to predict; what to return
   execute_request = deployrclient.models.ExecuteRequest(
       "clf.fit(iris.data, iris.target)\n"+
       "result=clf.predict(species_1)\n"+
       "other_result=clf.predict(species_2)",
       [workspace_object,workspace_object_2], #Input
       ["result", "other_result"]) #Output

   #Now, go train that model on the Iris Dataset in R Server
   execute_response = client.execute_code(session_id,execute_request, headers)

   #If successful, print name and result of each output parameter. Else, print error.
   if(execute_response.success):
       for result in execute_response.output_parameters:
           print("{0}: {1}".format(result.name,result.value))
   else:
       print (execute_response.error_message)
   ```

3. Criar um instantâneo desse Python sessão para esse ambiente pode ser salvo no serviço da web e reproduzido na consomem tempo. Instantâneos são úteis quando você precisa de um ambiente preparado que inclui determinadas bibliotecas de objetos, modelos, arquivos e artefatos. Instantâneos de salvam o espaço de trabalho inteiro e o diretório de trabalho. No entanto, ao publicar, você pode usar somente os instantâneos que você criou.

   ```python
   #Create a snapshot of the current session.
   response = client.create_snapshot(session_id, deployrclient.models.CreateSnapshotRequest("Iris Snapshot"), headers)
   
   #Return the snapshot ID for reference when you publish later.
   response.snapshot_id
   
   #If you forget the ID, list snapshots to get the ID again.
   for snapshot in client.list_snapshots(headers):
       print(snapshot)
   ```

  > [!NOTE] 
   > Enquanto os instantâneos também podem ser usados ao publicar um serviço web para dependências de ambiente, ele pode ter um impacto no desempenho do tempo de consumo.  Para um desempenho ideal, considere cuidadosamente o tamanho do instantâneo e certifique-se de que você mantenha apenas os objetos de espaço de trabalho, você precisa e limpar o restante. Em uma sessão, você pode usar o Python `del` função ou [o `deleteWorkspaceObject` solicitação API](https://microsoft.github.io/deployr-api-docs/#delete-workspace-object) para remover objetos desnecessários. 

### <a name="step-4-publish-the-model"></a>Etapa 4. Publicar o modelo 

Depois de sua biblioteca de cliente foi gerada e você construiu a lógica de autenticação em seu aplicativo, você pode interagir com os principais APIs para criar uma sessão de Python, criar um modelo e, em seguida, publicar um serviço web usando esse modelo.

Alguns itens a lembrar:

+ Você deve ser autenticado antes de fazer qualquer chamada de API. Portanto, incluir `headers` em todas as solicitações.
+ Para garantir que o serviço web é registrado como um serviço do Python, certifique-se de especificar `runtime_type="Python"`. Se você não definir o tipo de tempo de execução para Python, o padrão é R.
+ Pontuação requer um vetor com comprimento sépala, largura sépala, comprimento pétala e largura da pétala

O código a seguir publica o modelo SVM como um serviço web de Python. Esse serviço da web gera uma categoria prevista com base nos valores passados para ele.

```python
   #Set `flower_data` for the sepal and petal length and width
   flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
   #Set `iris_species` for the species of iris
   iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "vector")
   
   #Define the publish request for the web service and its arguments.
   #Specify the code, inputs, outputs, and snapshot.
   #Don't forget to set runtime_type="Python"`.
   publish_request = deployrclient.models.PublishWebServiceRequest(
       code = "iris_species = [names[x] for x in clf.predict(flower_data)]", 
       input_parameter_definitions = [flower_data], 
       output_parameter_definitions = [iris_species],
       runtime_type = "Python",
       snapshot_id = response.snapshot_id)

   #Publish the service using the specified name (iris), version (V1.0)
   client.publish_web_service_version("Iris", "V1.0", publish_request, headers)
```

### <a name="step-5-consume-the-web-service"></a>Etapa 5. Consumir o serviço web

Esta seção demonstra como utilizar o serviço na mesma sessão do qual ele foi criado.

1. Na mesma sessão, obter as ações de serviço e os metadados para o serviço.

   ```python
   # Inspect holdings and metadata for service Iris V1.0.
   for service in client.get_web_service_version("Iris","V1.0", headers):
       #print service metadata (description, who published,...)
       print(service)
       #Print input and output parameters as defined in service definition object
       print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
       print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))
   ```

2. Examine as ações de serviço e se preparar para consumir. 
   ```python
   #Import the requests library to make requests on the server
   import requests
   #Import the JSON library to use for pretty printing of json responses
   import json

   #Create a requests `Session` object.
   s = requests.Session()

   #Record the R Server endpoint URL hosting the web services you created
   url = "http://localhost:12800"

   #Include the request.Session object in the authentication headers.
   #By doing so, you don't need to repeat it with each request.
   s.headers = headers

   # Retrieve the service-specific Swagger file using the requests library.
   swagger_resp = s.get(url+"/api/Iris/V1.0/swagger.json")

   #You can download a service-specific Swagger file using the json library.
   with open('iris_swagger.json','w') as f:
      (json.dump(client.get_web_service_swagger("Iris","V1.0",headers),f, indent = 1))

   #Or, you can print just what you need from the Swagger file. 
   #This example gets the routing paths for the endpoints to be consumed.
   print(json.dumps(swagger_resp.json()["paths"], indent = 1, sort_keys = True))

   #You can also print input and output parameters as defined in the Swagger.io format
   print("Input")
   print(json.dumps(swagger_resp.json()["definitions"]["InputParameters"], indent = 1, sort_keys = True))
   print("Output")
   print(json.dumps(swagger_resp.json()["definitions"]["WebServiceResult"], indent = 1, sort_keys = True))
   ```

3. Consumir o serviço, fornecendo alguns entrada e obter a espécie de íris. 
   ```python
   #Make the request to consume the service using these flower_data inputs
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[7,3.2,4.7,1.4]})
   #Print the output
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))

   ##Use input from another Iris species.
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[3,2.6,3,2.5]})
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))

   ##Use input from another Iris species.
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[5.1,3.5,1.4,.2]})
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))
   ```

## <a name="managing-the-services"></a>Gerenciamento de serviços

Agora que você criou um serviço web, você pode atualizar, excluir ou republicar desse serviço. Você também pode listar todos os serviços da web que são hospedados usando R Server (ou servidor de aprendizado de máquina).

### <a name="update-a-web-service"></a>Atualizar um serviço web

 Neste exemplo, podemos atualizar o serviço para adicionar uma descrição útil para as pessoas que podem consumir esse serviço.

```python
#Define what needs to be updated. Here we add a description.
#Be sure to specify the runtime_type again.
update_request = deployrclient.models.PublishWebServiceRequest(
    description = "Determines iris species using length and width of sepal and petal", runtime_type = "Python")
#Now update it by specifying the service name and version number
client.patch_web_service_version("Iris", "V1.0", update_request, headers)
```

Você pode atualizar um serviço da web para alterar o código, modelo, descrição, entradas, saídas e muito mais.

### <a name="publish-another-version"></a>Outra versão de publicação

Neste exemplo, o serviço retornará a espécie de íris como uma cadeia de caracteres em vez de como uma lista de cadeias de caracteres.

```python
#Publish another version of the web service, but this time 
#the service returns the species as a string instead of list of strings.
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "string")
 
#Define the publish request for the service and its arguments.
#Specify the changed code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
    code = "iris_species = [names[x] for x in clf.predict(flower_data)][0]",
    description = "Determines the species of iris, based on Sepal Length, Sepal Width, Petal Length and Petal Width",
    input_parameter_definitions = [flower_data],
    output_parameter_definitions = [iris_species],
    runtime_type = "Python",
    snapshot_id = response.snapshot_id)
 
#Now, publish the service with version (V2.0)
client.publish_web_service_version("Iris", "V2.0", publish_request, headers)
 
#Make request to consume service using these flower_data inputs; print output
resp = s.post(url+"/api/Iris/V2.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))
```

Você pode usar esse padrão para publicar várias versões do mesmo serviço da web. 

### <a name="list-services"></a>Listar serviços

Este exemplo obtém uma lista de todos os serviços da web, incluindo aqueles criados por outros usuários ou em idiomas diferentes.

```python
#Return the list of all existing web services.
for service in client.get_all_web_services(headers):
    #print the service information
    print(service)
    #Print each input and output parameter
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))
``` 

### <a name="delete-services"></a>Excluir serviços

Neste exemplo, podemos excluir a segunda versão do serviço web que acabou de ser publicados.

```python
#Delete the second version we just published.
client.delete_web_service_version("Iris","V2.0",headers)
```

Você pode excluir qualquer serviço que você criou. Você pode excluir os serviços de terceiros somente se você está atribuído a uma função que tenha as permissões apropriadas.