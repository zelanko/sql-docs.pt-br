---
title: Consumir aplicativos em clusters de Big Data
titleSuffix: SQL Server big data clusters
description: Consuma um aplicativo implantado no cluster de Big Data do SQL Server 2019 usando um serviço Web RESTful (versão prévia).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a2135ef64fb17eba62eab75b81739eda047167ab
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68419513"
---
# <a name="consume-an-app-deployed-on-sql-server-big-data-cluster-using-a-restful-web-service"></a>Consuma um aplicativo implantado no cluster de Big Data do SQL Server usando um serviço Web RESTful

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como consumir um aplicativo implantado em um cluster de Big Data do SQL Server 2019 usando um serviço Web RESTful (versão prévia).

## <a name="prerequisites"></a>Prerequisites

- [Cluster de Big Data do SQL Server 2019](deployment-guidance.md)
- [Utilitário de linha de comando mssqlctl](deploy-install-azdata.md)
- Um aplicativo implantado usando [azdata](big-data-cluster-create-apps.md) ou a [Extensão de implantação de aplicativo](app-deployment-extension.md)

## <a name="capabilities"></a>Funcionalidades

Depois de implantar um aplicativo em seu cluster de Big Data do SQL Server 2019 (versão prévia), você pode acessar e consumir esse aplicativo usando um serviço Web RESTful. Isso permite a integração desse aplicativo usando outros aplicativos ou serviços (por exemplo, um aplicativo móvel ou site). A tabela a seguir descreve os comandos de implantação do aplicativo que você pode usar com **azdata** para obter informações sobre o serviço Web RESTful para seu aplicativo.

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

Descreva seu aplicativo executando um comando semelhante ao seguinte:

```bash
azdata app describe --name addpy --version v1
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
    "app": "https://10.1.1.3:30777/api/app/addpy/v1",
    "swagger": "https://10.1.1.3:30777/api/app/addpy/v1/swagger.json"
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

Observe o endereço IP (neste exemplo, `10.1.1.3`) e o número da porta (`30777`) na saída.

## <a name="generate-a-jwt-access-token"></a>Gerar um token de acesso JWT

Para acessar o serviço Web RESTful para o aplicativo que você implantou, primeiro, você precisa gerar um token de acesso JWT. Abra a seguinte URL em seu navegador: `https://[IP]:[PORT]/api/docs/swagger.json` usando o endereço IP e a porta que você recuperou executando o comando `describe` acima. Você precisará fazer logon com as mesmas credenciais usadas para o `azdata login`.

Cole o conteúdo de `swagger.json` no [Editor de Swagger](https://editor.swagger.io) para entender quais métodos estão disponíveis:

![API Swagger](media/big-data-cluster-consume-apps/api_swagger.png)

Observe o método GET `app`, bem como o método POST `token`. Como a autenticação para aplicativos usa tokens JWT, você precisará obter um token usando sua ferramenta favorita para fazer uma chamada POST para o método `token`. Veja um exemplo de como fazer exatamente isso no [Postman](https://www.getpostman.com/):

![Token do Postman](media/big-data-cluster-consume-apps/postman_token.png)

O resultado dessa solicitação lhe dará um `access_token` JWT, que será necessário para chamar a URL para executar o aplicativo.

## <a name="execute-the-app-using-the-restful-web-service"></a>Executar o aplicativo usando o serviço Web RESTful

> [!NOTE]
> Se desejar, você pode abrir a URL para o `swagger` que foi retornado quando você executou `azdata app describe --name [appname] --version [version]` em seu navegador, que deve ser semelhante a `https://[IP]:[PORT]/api/app/[appname]/[version]/swagger.json`. Você precisará fazer logon com as mesmas credenciais usadas para o `azdata login`. O conteúdo do `swagger.json` que você pode colar no [Editor de Swagger](https://editor.swagger.io). Você verá que o serviço Web expõe o método `run`. Observe também a URL base exibida na parte superior.

Você pode usar sua ferramenta favorita para chamar o método `run` (`https://[IP]:30778/api/app/[appname]/[version]/run`), passando os parâmetros no corpo da solicitação POST como json. Neste exemplo, usaremos [Postman](https://www.getpostman.com/). Antes de fazer a chamada, você precisará definir o `Authorization` como `Bearer Token` e colar o token recuperado anteriormente. Isso definirá um cabeçalho em sua solicitação. Veja a captura de tela abaixo.

![Cabeçalhos de execução de Postman](media/big-data-cluster-consume-apps/postman_run_1.png)

Em seguida, no corpo da solicitação, passe os parâmetros para o aplicativo que você está chamando e defina `content-type` como `application/json`:

![Corpo da execução do Postman](media/big-data-cluster-consume-apps/postman_run_2.png)

Ao enviar a solicitação, você receberá a mesma saída que recebeu quando executou o aplicativo por meio de `azdata app run`:

![Resultado da execução do Postman](media/big-data-cluster-consume-apps/postman_result.png)

Você chamou o aplicativo com êxito usando o serviço Web. Você pode seguir etapas semelhantes para integrar esse serviço Web ao seu aplicativo.

## <a name="next-steps"></a>Próximas etapas

Confira também mais amostras em [Amostras de implantação de aplicativo](https://aka.ms/sql-app-deploy).

Para obter mais informações sobre os clusters de Big Data do SQL Server, confira [O que são clusters de Big Data do SQL Server 2019?](big-data-cluster-overview.md).
