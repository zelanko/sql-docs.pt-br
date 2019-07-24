---
title: Consumir aplicativos em clusters Big Data
titleSuffix: SQL Server big data clusters
description: Consuma um aplicativo implantado no SQL Server 2019 Big Data cluster usando um serviço Web RESTful (versão prévia).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a2135ef64fb17eba62eab75b81739eda047167ab
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419513"
---
# <a name="consume-an-app-deployed-on-sql-server-big-data-cluster-using-a-restful-web-service"></a>Consumir um aplicativo implantado no cluster SQL Server Big Data usando um serviço Web RESTful

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como consumir um aplicativo implantado em um cluster SQL Server 2019 Big Data usando um serviço Web RESTful (versão prévia).

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster SQL Server 2019 Big Data](deployment-guidance.md)
- [utilitário de linha de comando mssqlctl](deploy-install-azdata.md)
- Um aplicativo implantado usando [azdata](big-data-cluster-create-apps.md) ou a [extensão de implantação de aplicativo](app-deployment-extension.md)

## <a name="capabilities"></a>Capacidades

Depois de implantar um aplicativo em seu SQL Server 2019 Big Data cluster (versão prévia), você pode acessar e consumir esse aplicativo usando um serviço Web RESTful. Isso permite a integração desse aplicativo de outros aplicativos ou serviços (por exemplo, um aplicativo móvel ou site). A tabela a seguir descreve os comandos de implantação de aplicativo que você pode usar com o **azdata** para obter informações sobre o serviço Web RESTful para seu aplicativo.

|Comando |Descrição |
|:---|:---|
|`azdata app describe` | Descreva o aplicativo. |

Você pode obter ajuda com o `--help` parâmetro como no exemplo a seguir:

```bash
azdata app describe --help
```

As seções a seguir descrevem como recuperar um ponto de extremidade para um aplicativo e como trabalhar com o serviço Web RESTful para integração de aplicativos.

## <a name="retrieve-the-endpoint"></a>Recuperar o ponto de extremidade

O comando **azdata app Descreva** fornece informações detalhadas sobre o aplicativo, incluindo o ponto de extremidade no cluster. Normalmente, isso é usado por um desenvolvedor de aplicativo para criar um aplicativo usando o cliente do Swagger e usando o WebService para interagir com o aplicativo de maneira RESTful.

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

Observe o endereço IP (`10.1.1.3` neste exemplo) e o número da porta (`30777`) na saída.

## <a name="generate-a-jwt-access-token"></a>Gerar um token de acesso JWT

Para acessar o serviço Web RESTful para o aplicativo que você implantou, primeiro, você precisa gerar um token de acesso JWT. Abra a seguinte URL no seu navegador: `https://[IP]:[PORT]/api/docs/swagger.json` usando o endereço IP e a porta que você recuperou executando o `describe` comando acima. Você precisará fazer logon com as mesmas credenciais usadas para `azdata login`o.

Cole o conteúdo do `swagger.json` no editor do [Swagger](https://editor.swagger.io) para entender quais métodos estão disponíveis:

![Swagger de API](media/big-data-cluster-consume-apps/api_swagger.png)

Observe o `app` método Get, bem como o `token` método post. Como a autenticação para aplicativos usa tokens JWT, você precisará obter um token My usando sua ferramenta favorita para fazer uma chamada post para `token` o método. Aqui está um exemplo de como fazer exatamente isso no [postmaster](https://www.getpostman.com/):

![Token do postmaster](media/big-data-cluster-consume-apps/postman_token.png)

O resultado dessa solicitação lhe dará um JWT `access_token`, que será necessário chamar a URL para executar o aplicativo.

## <a name="execute-the-app-using-the-restful-web-service"></a>Executar o aplicativo usando o serviço Web RESTful

> [!NOTE]
> Se desejar, você pode abrir a URL para o `swagger` que foi retornado quando você executou `azdata app describe --name [appname] --version [version]` em seu navegador, que deve ser semelhante a. `https://[IP]:[PORT]/api/app/[appname]/[version]/swagger.json` Você precisará fazer logon com as mesmas credenciais usadas para `azdata login`o. O conteúdo do que `swagger.json` você pode colar no [Editor do Swagger](https://editor.swagger.io). Você verá que o serviço Web expõe o `run` método. Observe também a URL base exibida na parte superior.

Você pode usar sua ferramenta favorita para chamar o `run` método (`https://[IP]:30778/api/app/[appname]/[version]/run`), passando os parâmetros no corpo da solicitação post como JSON. Neste exemplo, usaremos o [postmaster](https://www.getpostman.com/). Antes de fazer a chamada, você precisará definir o `Authorization` para `Bearer Token` e colar o token recuperado anteriormente. Isso definirá um cabeçalho em sua solicitação. Consulte a captura de tela abaixo.

![Cabeçalhos de execução do postmaster](media/big-data-cluster-consume-apps/postman_run_1.png)

Em seguida, no corpo de solicitações, passe os parâmetros para o aplicativo que você está chamando e defina `content-type` como `application/json`:

![Corpo da execução do postmaster](media/big-data-cluster-consume-apps/postman_run_2.png)

Ao enviar a solicitação, você receberá a mesma saída que fez quando executou o aplicativo por meio `azdata app run`de:

![Resultado da execução do postmaster](media/big-data-cluster-consume-apps/postman_result.png)

Você agora chamou com êxito o aplicativo por meio do serviço Web. Você pode seguir etapas semelhantes para integrar esse serviço Web em seu aplicativo.

## <a name="next-steps"></a>Próximas etapas

Você também pode conferir exemplos adicionais em [exemplos de implantação de aplicativo](https://aka.ms/sql-app-deploy).

Para obter mais informações sobre clusters de Big Data SQL Server, consulte [o que são SQL Server 2019 Big data clusters?](big-data-cluster-overview.md).
