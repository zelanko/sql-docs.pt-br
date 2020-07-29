---
title: O que são pools de dados?
titleSuffix: SQL Server big data clusters
description: Este artigo descreve o pool de dados em um cluster de Big Data do SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 547f3e14d0e73b944cc7bde31f657dbf4ad49d41
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773665"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>O que são pools de dados em um cluster de Big Data do SQL Server?

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo descreve a função dos *Pools de dados do SQL Server* em um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. As seções a seguir descrevem a arquitetura e a funcionalidade de um pool de dados do SQL.

Este vídeo de 5 minutos apresenta pools de dados e mostra como consultar dados de pools de dados:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Querying-Data-from-Big-Data-Cluster-Data-Pool/player?WT.mc_id=dataexposed-c9-niner]

## <a name="data-pool-architecture"></a>Arquitetura do pool de dados

Um pool de dados é composto por uma ou mais instâncias de pool de dados do SQL Server. As instâncias de pool de dados do SQL fornecem armazenamento persistente no SQL Server para o cluster. Um pool de dados é usado para ingerir dados de consultas SQL ou de trabalhos do Spark. Para fornecer um melhor desempenho em grandes conjuntos de dados, os dados em um pool de dados são distribuídos em fragmentos entre as instâncias membro do pool de dados do SQL.

## <a name="scale-out-data-marts"></a>Data marts de expansão

Os pools de dados permitem a criação de data marts de expansão, em que dados externos de várias fontes são incluídos no pool de dados. Como os dados são distribuídos entre instâncias do pool de dados, consultas paralelas em relação aos dados organizados são mais eficientes.

![Data mart de expansão](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira os seguintes recursos:

- [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
- [Workshop: Arquitetura dos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] da Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
