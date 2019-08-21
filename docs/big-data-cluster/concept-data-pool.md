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
ms.openlocfilehash: bfd4d9d6ca24599a2297799555f53a83c6601420
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652262"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>O que são pools de dados em um cluster de Big Data do SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve a função de *pools de dados SQL Server* em um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. As seções a seguir descrevem a arquitetura e a funcionalidade de um pool de dados do SQL.

## <a name="data-pool-architecture"></a>Arquitetura do pool de dados

Um pool de dados é composto por uma ou mais instâncias de pool de dados do SQL Server. As instâncias de pool de dados do SQL fornecem armazenamento persistente no SQL Server para o cluster. Um pool de dados é usado para ingerir dados de consultas SQL ou de trabalhos do Spark. Para fornecer um melhor desempenho em grandes conjuntos de dados, os dados em um pool de dados são distribuídos em fragmentos entre as instâncias membro do pool de dados do SQL.

## <a name="scale-out-data-marts"></a>Data marts de expansão

Os pools de dados permitem a criação de data marts de expansão, em que dados externos de várias fontes são incluídos no pool de dados. Como os dados são distribuídos entre instâncias do pool de dados, consultas paralelas em relação aos dados organizados são mais eficientes.

![Data mart de expansão](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], consulte os seguintes recursos:

- [O que [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]são?](big-data-cluster-overview.md)
- [Workshop: Arquitetura [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] da Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
