---
title: Consumir aplicativos em clusters de big data
titleSuffix: SQL Server 2019 big data clusters
description: Consuma um aplicativo implantado em um cluster de big data de 2019 do SQL Server usando um serviço web RESTful (visualização).
author: jeroenterheerdt
ms.author: jterh
manager: craigg
ms.date: 03/18/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.reviewer: rothja
ms.openlocfilehash: bc55e90ad8aced555858008bc77715299a064b2a
ms.sourcegitcommit: 1a182443e4f70f4632617cfef4efa56d898e64e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58342839"
---
# <a name="consume-an-app-deployed-on-sql-server-big-data-cluster-using-a-restful-web-service"></a>Consumir um aplicativo implantado no cluster de big data do SQL Server usando um serviço web RESTful

Este artigo descreve como consumir um aplicativo implantado em um cluster de big data de 2019 do SQL Server usando um serviço web RESTful (visualização).

## <a name="prerequisites"></a>Prerequisites

- [Cluster de big data do SQL Server de 2019](deployment-guidance.md)
- [Utilitário de linha de comando mssqlctl](deploy-install-mssqlctl.md)
- Um aplicativo implantado usando um [ `mssqlctl` ](big-data-cluster-create-apps.md) ou o [implantar o aplicativo de extensão](app-deployment-extension.md)

## <a name="capabilities"></a>Recursos

Depois de ter implantado um aplicativo para seu cluster de big data do SQL Server 2019 (visualização), você pode acessar e consumir um aplicativo usando um serviço web RESTful. Isso permite a integração do aplicativo de outros aplicativos ou serviços (por exemplo, um aplicativo móvel ou site). A tabela a seguir descreve os comandos de implantação do aplicativo que você pode usar com **mssqlctl** para obter informações sobre o serviço web RESTful do seu aplicativo.

|Comando |Descrição |
|:---|:---|
|`mssqlctl app describe` | Descreva o aplicativo. |

Você pode obter ajuda com o `--help` parâmetro como no exemplo a seguir:

```bash
mssqlctl app describe --help
```

As seções a seguir descrevem como recuperar um ponto de extremidade para um aplicativo e como trabalhar com o serviço web RESTful para integração de aplicativos.

## <a name="retrieve-the-endpoint"></a>Recuperar o ponto de extremidade

O **mssqlctl aplicativo descrevem** comando fornece informações detalhadas sobre o aplicativo, incluindo o ponto de extremidade em seu cluster. Isso normalmente é usado por um desenvolvedor de aplicativo para compilar um aplicativo usando o cliente do swagger e usando o serviço Web para interagir com o aplicativo de maneira RESTful.

Descreva seu aplicativo ao executar um comando semelhante ao seguinte:

```bash
mssqlctl app describe --name addpy --version v1
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

Anote o endereço IP (`10.1.1.3` neste exemplo) e o número da porta (`30777`) na saída.

## <a name="generate-a-jwt-access-token"></a>Gerar um token de acesso JWT

Para acessar o serviço web RESTful para o aplicativo você implantou pela primeira vez para gerar um token de acesso JWT. Abra a seguinte URL no seu navegador: `https://[IP]:[PORT]/api/docs/swagger.json` usando o endereço IP e porta em execução que você recuperou o `describe` comando acima. Você terá que fazer logon com as mesmas credenciais usadas para `mssqlctl login`.

Cole o conteúdo da `swagger.json` para o [Editor do Swagger](https://editor.swagger.io) para entender quais métodos estão disponíveis:

![API Swagger](media/big-data-cluster-consume-apps/api_swagger.png)

Observe que o `app` método GET, bem como a `token` método POST. Como a autenticação para aplicativos usa tokens JWT é necessário obter um token meu usando sua ferramenta favorita para fazer uma chamada POST para o `token` método. Aqui está um exemplo de como fazer isso [Postman](https://www.getpostman.com/):

![Postman Token](media/big-data-cluster-consume-apps/postman_token.png)

O resultado dessa solicitação lhe dará um JWT `access_token`, que você precisará chamar a URL para executar o aplicativo.

## <a name="execute-the-app-using-the-restful-web-service"></a>Execute o aplicativo usando o serviço web RESTful

> [!NOTE]
> Se você quiser, você pode abrir a URL para o `swagger` que foi retornado quando você executou `mssqlctl app describe --name [appname] --version [version]` em seu navegador, que deve ser semelhante ao `https://[IP]:[PORT]/api/app/[appname]/[version]/swagger.json`. Você terá que fazer logon com as mesmas credenciais usadas para `mssqlctl login`. O conteúdo a `swagger.json` você pode colar em [Editor do Swagger](https://editor.swagger.io). Você verá que o serviço web expõe o `run` método.

Você pode usar sua ferramenta favorita para chamar o `run` método (`https://[IP]:[PORT]/api/app/[appname]/[version]/run`), passando os parâmetros no corpo da solicitação POST como json. Neste exemplo usaremos [Postman](https://www.getpostman.com/). Antes de fazer a chamada, você precisará definir a `Authorization` para `Bearer Token` e cole o token que você recuperou anteriormente. Isso definirá um cabeçalho em sua solicitação. Consulte a captura de tela abaixo.

![Postman executar cabeçalhos](media/big-data-cluster-consume-apps/postman_run_1.png)

Em seguida, no corpo de solicitações, passar parâmetros para o aplicativo que você está chamando e defina as `content-type` para `application/json`:

![Corpo de execução do postman](media/big-data-cluster-consume-apps/postman_run_2.png)

Quando você envia a solicitação, você receberá a mesma saída de forma que quando você executou o aplicativo por meio de `mssqlctl app run`:

![Resultado da execução de postman](media/big-data-cluster-consume-apps/postman_result.png)

Agora você ter chamado com êxito o aplicativo por meio do serviço web. Você pode seguir etapas semelhantes para integrar esse web service em seu aplicativo.

## <a name="next-steps"></a>Próximas etapas

Você também pode conferir exemplos adicionais no [exemplos de implantar o aplicativo](https://aka.ms/sql-app-deploy).

Para obter mais informações sobre clusters de grandes dados do SQL Server, consulte [quais são os clusters do SQL Server 2019 big data?](big-data-cluster-overview.md).
