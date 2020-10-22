---
title: Executar aplicativos usando o azdata
titleSuffix: SQL Server Big Data Clusters
description: Executar aplicativos com azdata nos clusters de Big Data do SQL Server 2019.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 08/16/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 13639627081a9bb9cb1309bcd0793653c7900ac8
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257266"
---
# <a name="run-apps-with-azdata---sql-server-big-data-clusters"></a>Executar aplicativos com azdata – Clusters de Big Data do SQL Server 2019

Este artigo descreve como executar um aplicativo nos Clusters de Big Data do SQL Server.

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster de Big Data do SQL Server 2019](deployment-guidance.md)
- [[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]](../azdata/install/deploy-install-azdata.md)

## <a name="capabilities"></a>Funcionalidades

No SQL Server 2019, você pode criar, excluir, descrever, inicializar, listar, executar e atualizar seu aplicativo. A tabela a seguir descreve os comandos de implantação de aplicativos que você pode usar com o **azdata**.

|Comando |Descrição |
|:---|:---|
|`azdata app describe` | Descrever o aplicativo. |
|`azdata app run` | Executar o aplicativo. |


As seções a seguir descrevem esses comandos mais detalhadamente.


## <a name="run-an-app"></a>Executar um aplicativo

Se o aplicativo estiver em um estado `Ready`, use-o executando-o com os parâmetros de entrada especificados. Use a seguinte sintaxe para executar um aplicativo:

```bash
azdata app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

O seguinte comando de exemplo demonstra o comando de execução:

```bash
azdata app run --name add-app --version v1 --inputs x=1,y=2
```

Se a execução for bem-sucedida, você deverá ver a saída especificada quando o aplicativo foi criado. A saída a seguir é um exemplo.

```json
{
  "changedFiles": [],
  "consoleOutput": "",
  "errorMessage": "",
  "outputFiles": {},
  "outputParameters": {
    "result": 3
  },
  "success": true
}
```


## <a name="describe-an-app"></a>Descrever um aplicativo

O comando describe fornece informações detalhadas sobre o aplicativo, incluindo o ponto de extremidade no cluster. Normalmente, isso é usado por um desenvolvedor de aplicativos para criar um aplicativo usando o cliente do Swagger e usando o serviço Web para interagir com o aplicativo de maneira semelhante ao RESTful. Confira mais informações em [Consumir aplicativos em clusters de Big Data](app-consume.md).

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
    "app": "https://10.1.1.3:30080/api/app/add-app/v1",
    "swagger": "https://10.1.1.3:30080/api/app/add-app/v1/swagger.json"
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

Explore como integrar os aplicativos implantados no [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] em seus próprios aplicativos em [Consumir aplicativos em clusters de Big Data](app-consume.md) para obter mais informações. Confira também mais amostras em [Amostras de implantação de aplicativo](https://aka.ms/sql-app-deploy).

Para obter mais informações sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).