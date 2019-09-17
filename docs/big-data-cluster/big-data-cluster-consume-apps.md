---
title: Consumir aplicativos em clusters SQL Server Big Data
titleSuffix: SQL Server big data clusters
description: Consuma um aplicativo implantado no [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] uso de um serviço Web RESTful (versão prévia).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bd7d5e0093d3805679e59b542582c263dfd56c9c
ms.sourcegitcommit: 5a61854ddcd2c61bb6da30ccad68f0ad90da0c96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70978290"
---
# <a name="consume-an-app-deployed-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-using-a-restful-web-service"></a>Consumir um aplicativo implantado no [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] uso de um serviço Web RESTful

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como consumir um aplicativo implantado em um cluster de Big Data do SQL Server 2019 usando um serviço Web RESTful (versão prévia).

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster de Big Data do SQL Server 2019](deployment-guidance.md)
- [Utilitário de linha de comando azdata](deploy-install-azdata.md)
- Um aplicativo implantado usando [azdata](big-data-cluster-create-apps.md) ou a [Extensão de implantação de aplicativo](app-deployment-extension.md)

## <a name="capabilities"></a>Capacidades

Depois de implantar um aplicativo no [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], você pode acessar e consumir esse aplicativo usando um serviço Web RESTful. Isso permite a integração desse aplicativo usando outros aplicativos ou serviços (por exemplo, um aplicativo móvel ou site). A tabela a seguir descreve os comandos de implantação do aplicativo que você pode usar com **azdata** para obter informações sobre o serviço Web RESTful para seu aplicativo.

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

Descreva seu aplicativo executando um comando semelhante ao exemplo a seguir:

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

Uma das outras maneiras de obter essas informações é fazer com que clique com o botão direito do mouse em gerenciar no servidor em Azure Data Studio, onde você encontrará os pontos de extremidade dos serviços listados.

![Ponto de extremidade do ADS](media/big-data-cluster-consume-apps/ads_end_point.png)

## <a name="generate-a-jwt-access-token"></a>Gerar um token de acesso JWT

Para acessar o serviço Web RESTful para o aplicativo que você implantou, primeiro, você precisa gerar um token de acesso JWT. Abra a seguinte URL em seu navegador: `https://[IP]:[PORT]/docs/swagger.json` usando o endereço IP e a porta que você recuperou executando o comando `describe` acima. Você precisará entrar com as mesmas credenciais usadas para `azdata login`o.

Cole o conteúdo de `swagger.json` no [Editor de Swagger](https://editor.swagger.io) para entender quais métodos estão disponíveis:

![API Swagger](media/big-data-cluster-consume-apps/api_swagger.png)

Observe o método GET `app`, bem como o método POST `token`. Como a autenticação para aplicativos usa tokens JWT, você precisará obter um token My usando sua ferramenta favorita para fazer uma chamada post para o `token` método. Veja um exemplo de como fazer exatamente isso no [Postman](https://www.getpostman.com/):

![Token do Postman](media/big-data-cluster-consume-apps/postman_token.png)

O resultado dessa solicitação lhe dará um JWT `access_token`, que será necessário chamar a URL para executar o aplicativo.

## <a name="execute-the-app-using-the-restful-web-service"></a>Executar o aplicativo usando o serviço Web RESTful

> [!NOTE]
> Se desejar, você pode abrir a URL para o `swagger` que foi retornado quando você executou `azdata app describe --name [appname] --version [version]` em seu navegador, que deve ser semelhante a `https://[IP]:[PORT]/app/[appname]/[version]/swagger.json`. Você precisará fazer logon com as mesmas credenciais usadas para o `azdata login`. O conteúdo do `swagger.json` que você pode colar no [Editor de Swagger](https://editor.swagger.io). Você verá que o serviço Web expõe o método `run`. Observe também a URL base exibida na parte superior.

Você pode usar sua ferramenta favorita para chamar o método `run` (`https://[IP]:30778/api/app/[appname]/[version]/run`), passando os parâmetros no corpo da solicitação POST como json. Neste exemplo, usaremos o [postmaster](https://www.getpostman.com/). Antes de fazer a chamada, você precisará definir o `Authorization` como `Bearer Token` e colar o token recuperado anteriormente. Isso definirá um cabeçalho em sua solicitação. Veja a captura de tela abaixo.

![Cabeçalhos de execução de Postman](media/big-data-cluster-consume-apps/postman_run_1.png)

Em seguida, no corpo da solicitação, passe os parâmetros para o aplicativo que você está chamando e defina `content-type` como `application/json`:

![Corpo da execução do Postman](media/big-data-cluster-consume-apps/postman_run_2.png)

Ao enviar a solicitação, você receberá a mesma saída que recebeu quando executou o aplicativo por meio de `azdata app run`:

![Resultado da execução do Postman](media/big-data-cluster-consume-apps/postman_result.png)

Você chamou o aplicativo com êxito usando o serviço Web. Você pode seguir etapas semelhantes para integrar esse serviço Web ao seu aplicativo.

## <a name="next-steps"></a>Próximas etapas

Confira também mais amostras em [Amostras de implantação de aplicativo](https://aka.ms/sql-app-deploy).

Para obter mais informações [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]sobre o, consulte [o que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
