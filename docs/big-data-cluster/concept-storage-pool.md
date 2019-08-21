---
title: O que é o pool de armazenamento?
titleSuffix: SQL Server big data clusters
description: Este artigo descreve o pool de armazenamento em um cluster de Big Data do SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ead6c2ceeecbdfb3466bd4475978b139a0d2ddde
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652242"
---
# <a name="what-is-the-storage-pool-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>O que é o pool de[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]armazenamento ()?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve a função do *pool de armazenamento SQL Server* em um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. As seções a seguir descrevem a arquitetura e a funcionalidade de um pool de armazenamento do SQL.

## <a name="storage-pool-architecture"></a>Arquitetura do pool de armazenamento

O pool de armazenamento é composto por nós de armazenamento compostos pelo SQL Server em Linux, pelo Spark e pelo HDFS. Todos os nós de armazenamento em um cluster de Big Data do SQL são membros de um cluster do HDFS.

![Arquitetura do pool de armazenamento](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>Responsabilidades

Os nós de armazenamento são responsáveis por:

- Ingestão de dados por meio do Spark.
- Armazenamento de dados no HDFS (formato Parquet). O HDFS também fornece persistência de dados, pois os dados do HDFS são distribuídos em todos os nós de armazenamento no cluster de Big Data do SQL.
- Acesso a dados por meio dos pontos de extremidade do HDFS e do SQL Server.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], consulte os seguintes recursos:

- [O que [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]são?](big-data-cluster-overview.md)
- [Workshop: Arquitetura [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] da Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
