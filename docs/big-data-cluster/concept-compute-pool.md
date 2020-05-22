---
title: O que são pools de computação?
titleSuffix: SQL Server big data clusters
description: Este artigo descreve o pool de computação em um cluster de Big Data do SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: be8766f00a8c6b4d9fd47c976c5a2e1235cacd41
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606338"
---
# <a name="what-are-compute-pools-in-a-sql-server-big-data-cluster"></a>O que são pools de computação em um cluster de Big Data do SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve a função dos *pools de computação do SQL Server* em um cluster de Big Data do SQL Server. Os pools de computação fornecem recursos computacionais de expansão para um cluster Big Data. As seções a seguir descrevem a arquitetura e a funcionalidade de um pool de computação.

Você também pode assistir a este vídeo de cinco minutos para obter uma introdução aos pools de computação:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Overview-Big-Data-Cluster-Compute-Pool/player?WT.mc_id=dataexposed-c9-niner]


## <a name="compute-pool-architecture"></a>Arquitetura do pool de computação

Um pool de computação é composto por um ou mais pods de computação em execução no Kubernetes. A criação e o gerenciamento automatizados desses pods são coordenados pela [Instância mestre do SQL Server](concept-master-instance.md). Cada pod contém um conjunto de serviços básicos e uma instância do mecanismo de banco de dados do SQL Server.

## <a name="scale-out-groups"></a>Grupos de expansão

Um pool de computação pode funcionar como um grupo de escala horizontal do PolyBase para consultas distribuídas em diferentes fontes de dados – como HDFS, Oracle, MongoDB ou Teradata. Usando pods de computação no Kubernetes, os clusters de Big Data podem automatizar a criação e a configuração de pods de computação para os grupos de escala horizontal do PolyBase.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira os seguintes recursos:

- [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
- [Workshop: Arquitetura dos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] da Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
