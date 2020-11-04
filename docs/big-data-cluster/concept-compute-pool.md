---
title: O que são pools de computação?
titleSuffix: SQL Server big data clusters
description: Este artigo descreve o pool de computação em um cluster de Big Data do SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 10/15/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b07b1480412dc8dd67535f58fcc4d223a9e91baa
ms.sourcegitcommit: ab9ddcc16fdfc245cf9a49d1e90bb1ffe3958c38
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2020
ms.locfileid: "92914312"
---
# <a name="what-are-compute-pools-in-a-sql-server-big-data-cluster"></a>O que são pools de computação em um cluster de Big Data do SQL Server?

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo descreve a função dos *pools de computação do SQL Server* em um cluster de Big Data do SQL Server. Os pools de computação fornecem recursos computacionais de expansão para um cluster de Big Data do SQL Server. Eles são usados para descarregar o trabalho computacional ou os conjuntos de resultados intermediários da instância mestra do SQL Server. As seções a seguir descrevem a arquitetura, a funcionalidade e os cenários de uso de um pool de computação.

Você também pode assistir a este vídeo de cinco minutos para obter uma introdução aos pools de computação:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Overview-Big-Data-Cluster-Compute-Pool/player?WT.mc_id=dataexposed-c9-niner]

## <a name="compute-pool-architecture"></a>Arquitetura do pool de computação

Um pool de computação é composto por um ou mais pods de computação em execução no Kubernetes. A criação e o gerenciamento automatizados desses pods são coordenados pela [Instância mestre do SQL Server](concept-master-instance.md). Cada pod contém um conjunto de serviços básicos e uma instância do mecanismo de banco de dados do SQL Server.

![Arquitetura do pool de computação](media/concept-compute-pool/compute-pool-architecture.png)

## <a name="scale-out-groups"></a>Grupos de expansão

Um pool de computação pode funcionar como um grupo de expansão do PolyBase para consultas distribuídas em diferentes fontes de dados externas, como o SQL Server, o Oracle, o MongoDB, o Teradata e o HDFS. Usando pods do computação no Kubernetes, os clusters de Big Data do SQL Server podem automatizar a criação e a configuração de pods de computação para os grupos de escala horizontal do PolyBase.

## <a name="compute-pool-scenarios"></a>Cenários de pool de computação

Entre os cenários em que o pool de computação é usado estão:

- Cenários em que as consultas enviadas à instância mestra usam uma ou mais tabelas localizadas no [pool de armazenamento](concept-storage-pool.md).

- Cenários em que as consultas enviadas à instância mestra usam uma ou mais tabelas com a distribuição round robin localizada no [pool de dados](concept-data-pool.md).

- Cenários em que as consultas enviadas à instância mestra usam tabelas **particionadas** com fontes de dados externas do SQL Server, do Oracle, do MongoDB e do Teradata. Para esse cenário, a dica de consulta OPTION (FORCE SCALEOUTEXECUTION) precisa estar habilitada.

- Cenários em que as consultas enviadas à instância mestra usam uma ou mais tabelas localizadas na [camada do HDFS](hdfs-tiering.md).

Entre os cenários em que o pool de computação **não** é usado estão:

- Cenários em que as consultas enviadas à instância mestra usam uma ou mais tabelas em um cluster HDFS externo do Hadoop.

- Cenários em que as consultas enviadas à instância mestra usam uma ou mais tabelas no Armazenamento de Blobs do Azure.

- Cenários em que as consultas enviadas à instância mestra usam tabelas **não particionadas** com fontes de dados externas do SQL Server, do Oracle, do MongoDB e do Teradata.

- Cenários em que a dica de consulta OPTION (DISABLE SCALEOUTEXECUTION) está habilitada.

- Cenários em que as consultas enviadas à instância mestra se aplicam a bancos de dados localizados na instância mestra.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira os seguintes recursos:

- [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
- [Workshop: Arquitetura dos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] da Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
