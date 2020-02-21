---
title: Serviços de Machine Learning (Python, R)
titleSuffix: SQL Server Big Data Clusters
description: Saiba como executar scripts do Python e do R na instância mestra de Clusters de Big Data do SQL Server com Serviços de Machine Learning.
author: dphansen
ms.author: davidph
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
ms.openlocfilehash: e16304765e5f4a51feed4d3d59e790505baa740d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75252030"
---
# <a name="run-python-and-r-scripts-with-machine-learning-services-on-sql-server-big-data-clusters"></a>Executar scripts do Python e do R com Serviços de Machine Learning em Clusters de Big Data do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Você pode executar scripts do Python e do R na instância mestra de [Clusters de Big Data do SQL Server](big-data-cluster-overview.md) com [Serviços de Machine Learning](../advanced-analytics/index.yml).

> [!NOTE]
> Você também pode executar o código Java na instância mestra com as [Extensões de Linguagem do SQL Server](../language-extensions/language-extensions-overview.md). A conclusão das etapas abaixo habilitará também as Extensões de Linguagem.

## <a name="enable-machine-learning-services"></a>Habilitar Serviços de Machine Learning

O Serviços de Machine Learning são instalados por padrão em Clusters de Big Data e não exigem instalação separada.

Para habilitar Serviços de Machine Learning, execute esta instrução na instância mestra:

```sql
EXEC sp_configure 'external scripts enabled', 1
RECONFIGURE WITH OVERRIDE
GO
```

## <a name="enable-always-on-availability-groups"></a>Habilitar grupos de disponibilidade AlwaysOn

Se estiver usando Clusters de Big Data do SQL Server com [grupos de disponibilidade Always On](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md), você precisará executar algumas etapas adicionais para habilitar Serviços de Machine Learning.

1. Conecte-se à instância mestra e execute esta instrução:

    ```sql
    SELECT @@SERVERNAME
    ```

    Anote o nome do servidor. Neste exemplo, o nome do servidor para a instância mestra é **master-2**.

1. Em cada réplica no Grupo de Disponibilidade Always On no Cluster de Big Data, execute estes comandos `kubectl`:

    ```
    kubectl -n bdc expose pod master-0 --port=1533 --name=mymaster-0 --type=LoadBalancer

    kubectl -n bdc expose pod master-1 --port=1533 --name=mymaster-1 --type=LoadBalancer

    kubectl -n bdc expose pod master-2 --port=1533 --name=mymaster-2 --type=LoadBalancer
    ```

    Você deverá ver uma saída semelhante a esta:
    
    ```
    service/mymaster-0 exposed

    service/mymaster-1 exposed

    service/mymaster-2 exposed
    ```

1. Conecte-se a cada ponto de extremidade de réplica mestre e habilite a execução de script.

    Execute esta instrução:

    ```sql
    EXEC sp_configure 'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    GO
    ```

Agora você está pronto para executar scripts do Python e do R na instância mestra de Clusters de Big Data. Confira os guias de início rápido abaixo para executar seu primeiro script.

## <a name="next-steps"></a>Próximas etapas

+ [Início Rápido: Criar e executar scripts Python simples com os Serviços de Machine Learning do SQL Server](../advanced-analytics/tutorials/quickstart-python-create-script.md)
+ [Início Rápido: Criar e pontuar um modelo de previsão no Python com os Serviços de Machine Learning do SQL Server](../advanced-analytics/tutorials/quickstart-python-train-score-model.md)
+ [Início Rápido: Criar e executar scripts R simples com os Serviços de Machine Learning do SQL Server](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [Início Rápido: Criar e pontuar um modelo de previsão no R com os Serviços de Machine Learning do SQL Server](../advanced-analytics/tutorials/quickstart-r-train-score-model.md)
