---
title: Consumir aplicativos
titleSuffix: SQL Server Big Data Clusters
description: Consuma um aplicativo implantado em Clusters de Big Data do SQL Server usando um serviço Web RESTful.
author: cloudmelon
ms.author: melqin
ms.reviewer: bilia
ms.date: 06/22/2020
ms.metadata: seo-lt-2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 45161a879adadb0de78c4b2b0d3c62a5c2e18f55
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85719061"
---
# <a name="consume-an-app-deployed-on-big-data-clusters-2019-using-a-restful-web-service"></a>Consumir um aplicativo implantado em [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] usando um serviço Web RESTful

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo descreve como consumir um aplicativo implantado em um cluster de Big Data do SQL Server usando um serviço Web RESTful.

## <a name="prerequisites"></a>Prerequisites

- [Cluster de Big Data do SQL Server](deployment-guidance.md)
- [Utilitário de linha de comando azdata](deploy-install-azdata.md)
- Um aplicativo implantado usando [azdata](big-data-cluster-create-apps.md) ou a [Extensão de implantação de aplicativo](app-deployment-extension.md)

> [!NOTE]
> Quando o arquivo de especificação YAML do aplicativo especifica uma agenda, o aplicativo será disparado por meio de um trabalho cron. Se o cluster de Big Data for implantado no OpenShift, o início do trabalho cron exigirá recursos adicionais. Confira os detalhes sobre [considerações de segurança no OpenShift](concept-application-deployment.md#app-deploy-security) para obter instruções específicas.

## <a name="capabilities"></a>Funcionalidades

Depois de implantar um aplicativo em seu [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], você pode acessar e consumir esse aplicativo usando um serviço Web RESTful. Isso permite a integração desse aplicativo usando outros aplicativos ou serviços (por exemplo, um aplicativo móvel ou site). A tabela a seguir descreve os comandos de implantação do aplicativo que você pode usar com **azdata** para obter informações sobre o serviço Web RESTful para seu aplicativo.

|Comando |Descrição |
|:---|:---|
|`azdata app describe` | Descrever o aplicativo. |

Obtenha ajuda com o parâmetro `--help` como no seguinte exemplo:

```bash
azdata app describe --help
```

As seções a seguir descrevem como recuperar um ponto de extremidade para um aplicativo e como trabalhar com o serviço Web RESTful para integração de aplicativos.

## <a name="retrieve-the-endpoint"></a>Recuperar o ponto de extremidade

O comando **azdata app describe** fornece informações detalhadas sobre o aplicativo, incluindo o ponto de extremidade no cluster. Normalmente, isso é usado por um desenvolvedor de aplicativos para criar um aplicativo usando o cliente do Swagger e usando o serviço Web para interagir com o aplicativo de maneira semelhante ao RESTful.

Descreva seu aplicativo executando um comando semelhante ao seguinte exemplo:

```bash
azdata app describe --name add-app --version v1
```

```json
{
  "input_param_defs": [
    {
      "name": "x",
      "type": "int"
    },
    {
      "name": "y",
      "type": "int"
    }
  ],
  "links": {
    "app": "https://10.1.1.3:30080/app/addpy/v1",
    "swagger": "https://10.1.1.3:30080/app/addpy/v1/swagger.json"
  },
  "name": "add-app",
  "output_param_defs": [
    {
      "name": "result",
      "type": "int"
    }
  ],
  "state": "Ready",
  "version": "v1"
}
```

Observe o endereço IP (neste exemplo, `10.1.1.3`) e o número da porta (`30080`) na saída.

Uma das outras maneiras de obter essas informações é clicando com o botão direito do mouse em Gerenciar no servidor no Azure Data Studio, em que você encontrará os pontos de extremidade dos serviços listados.

![Ponto de extremidade do ADS](media/big-data-cluster-consume-apps/ads_end_point.png)

## <a name="generate-a-jwt-access-token"></a>Gerar um token de acesso JWT

Para acessar o serviço Web RESTful para o aplicativo que você implantou, primeiro, você precisa gerar um token de acesso JWT. A URL para o token de acesso depende da versão do cluster de Big Data. 

|Versão |URL|
|------------|------|
|GDR1|  `https://[IP]:[PORT]/docs/swagger.json`|
|CU1 e posteriores| `https://[IP]:[PORT]/api/v1/swagger.json`|

 Considerando a saída do exemplo anterior: versão CU4 e o endereço IP do controlador (10.1.1.3 no exemplo) e o número da porta (30080), a URL seria assim: 
 
 ```bash
    https://10.1.1.3 :30080/api/v1/swagger.json
```
 
> Para obter informações sobre a versão, confira [Histórico de versões](release-notes-big-data-cluster.md#release-history).

Abra a URL adequada em seu navegador usando o endereço IP e a porta que você recuperou executando o comando [`describe`](#retrieve-the-endpoint) acima. Entre com as mesmas credenciais usadas para o `azdata login`.

Cole o conteúdo de `swagger.json` no [Editor de Swagger](https://editor.swagger.io) para entender quais métodos estão disponíveis:

![API Swagger](media/big-data-cluster-consume-apps/api_swagger.png)

Observe que o `app` é o método GET e para obter o `token` usaria o método POST. Como a autenticação para aplicativos usa tokens JWT, você precisará obter um token usando sua ferramenta favorita para fazer uma chamada POST para o método `token`. Com o mesmo exemplo, a URL para obter o token JWT se pareceria com o seguinte:

 ```bash
    https://10.1.1.3 :30080/api/v1/token
```


Veja um exemplo de como fazer exatamente isso no [Postman](https://www.getpostman.com/):

![Token do Postman](media/big-data-cluster-consume-apps/postman_token.png)


A saída dessa solicitação lhe dará um `access_token` JWT, que será necessário para chamar a URL para executar o aplicativo.

## <a name="execute-the-app-using-the-restful-web-service"></a>Executar o aplicativo usando o serviço Web RESTful

Há maneiras várias maneiras de consumir um aplicativo no BDC: você pode optar por usar [o comando azdata app run](big-data-cluster-create-apps.md). Esta seção demonstrará como usar ferramentas para desenvolvedores comuns, como o Postman, para executar o aplicativo. 

Você pode abrir a URL para o `swagger` que foi retornado quando você executou `azdata app describe --name [appname] --version [version]` em seu navegador, que deve ser semelhante a `https://[IP]:[PORT]/app/[appname]/[version]/swagger.json`. 

> [!NOTE]
> Você precisará fazer logon com as mesmas credenciais usadas para o `azdata login`. Com o mesmo exemplo, o comando ficaria assim:

 ```bash
    azdata app describe --name add-app --version v1
```

O conteúdo do `swagger.json` que você pode colar no [Editor de Swagger](https://editor.swagger.io). Você verá que o serviço Web expõe o método `run` e nos bastidores ele passou pelo proxy de aplicativo, que é uma API Web que autentica usuários e roteia as solicitações para os aplicativos. Observe que a URL base é exibida na parte superior. Você pode usar a ferramenta de sua escolha para chamar o método `run` (`https://[IP]:30778/api/app/[appname]/[version]/run`), passando os parâmetros no corpo da solicitação POST como JSON. 


Neste exemplo, usaremos [Postman](https://www.getpostman.com/). Antes de fazer a chamada, você precisará definir o `Authorization` como `Bearer Token` e colar o token recuperado anteriormente. Isso definirá um cabeçalho em sua solicitação. Veja a captura de tela abaixo.

![Cabeçalhos de execução de Postman](media/big-data-cluster-consume-apps/postman_run_1.png)

Em seguida, no corpo da solicitação, passe os parâmetros para o aplicativo que você está chamando e defina `content-type` como `application/json`:

![Corpo da execução do Postman](media/big-data-cluster-consume-apps/postman_run_2.png)

Ao enviar a solicitação, você receberá a mesma saída que recebeu quando executou o aplicativo por meio de `azdata app run`:

![Resultado da execução do Postman](media/big-data-cluster-consume-apps/postman_result.png)

Você chamou o aplicativo com êxito usando o serviço Web. Você pode seguir etapas semelhantes para integrar esse serviço Web ao seu aplicativo.


## <a name="next-steps"></a>Próximas etapas

Confira também mais amostras em [Amostras de implantação de aplicativo](https://aka.ms/sql-app-deploy).

Para obter mais informações sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
