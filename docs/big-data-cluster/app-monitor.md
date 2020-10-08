---
title: Monitorar aplicativos com o Painel do Grafana e azdata
titleSuffix: SQL Server Big Data Clusters
description: Monitorar aplicativos com azdata e Grafana no cluster de Big Data do SQL Server 2019.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 08/16/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fa5ae6a8834659f7a1098cd9d8fbaee6beef359e
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725030"
---
# <a name="monitor-applications-with-azdata-and-grafana-dashboard"></a>Monitorar aplicativos com o Painel do Grafana e azdata

O Grafana é uma das melhores ferramentas de virtualização nativas de nuvem e pode ser usado para fornecer várias métricas de monitoramento de seu aplicativo em execução no Kubernetes.  

Este artigo descreve como monitorar um aplicativo em um Cluster de Big Data do SQL Server.

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster de Big Data do SQL Server 2019](deployment-guidance.md)
- [Utilitário de linha de comando azdata](../azdata/install/deploy-install-azdata.md)

## <a name="capabilities"></a>Funcionalidades

No SQL Server 2019, você pode criar, excluir, descrever, inicializar, listar, executar e atualizar seu aplicativo. A tabela a seguir descreve os comandos de implantação de aplicativos que você pode usar com o **azdata**.

|Comando |Descrição |
|:---|:---|
|`azdata bdc endpoint list` | Lista os pontos de extremidade para o cluster de Big Data. |


Use o exemplo a seguir para listar o ponto de extremidade do **Painel do Grafana**:

```bash
azdata bdc endpoint list --endpoint-name metricsui 
```

A saída fornecerá o ponto de extremidade, e você poderá usar o nome de usuário e a senha do cluster para fazer logon. 

![Painel do Grafana](media/big-data-cluster-monitor-apps/grafana-dashboard-endpoint.png)


Ao abrir o painel, vá para  **Métricas de Aplicativos de Host** para ver mais informações sobre seu aplicativo e gerenciá-lo.  

![Métricas de aplicativos de host](media/big-data-cluster-monitor-apps/host-apps-metrics.png)


Para obter mais informações sobre um único pod do aplicativo (em alguns casos, você tem várias cópias do seu aplicativo), vá para  **Métricas de Pods de Host**  e escolha o pod específico. Você obterá uma exibição das métricas da seguinte maneira:  

![Métricas de pods de host](media/big-data-cluster-monitor-apps/host-pods-metrics.png) 


## <a name="next-steps"></a>Próximas etapas

Confira exemplos adicionais em [Amostras de Implantação de Aplicativo](https://aka.ms/sql-app-deploy).

Para obter mais informações sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).