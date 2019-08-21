---
title: O que são pools de computação?
titleSuffix: SQL Server big data clusters
description: Este artigo descreve o pool de computação em [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]um.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6156d23fa55690224cd6df82e5f4bafe10e4d1ab
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653082"
---
# <a name="what-are-compute-pools-in-a-sql-server-big-data-cluster"></a>O que são pools de computação em um cluster de Big Data do SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve a função dos *Pools de computação do SQL Server* em um cluster de Big Data da versão prévia do SQL Server 2019. Os pools de computação fornecem recursos computacionais de expansão para um cluster Big Data. As seções a seguir descrevem a arquitetura e a funcionalidade de um pool de computação.

## <a name="compute-pool-architecture"></a>Arquitetura do pool de computação

Um pool de computação é composto por um ou mais pods de computação em execução no Kubernetes. A criação e o gerenciamento automatizados desses pods são coordenados pela [Instância mestre do SQL Server](concept-master-instance.md). Cada pod contém um conjunto de serviços básicos e uma instância do mecanismo de banco de dados do SQL Server.

## <a name="scale-out-groups"></a>Grupos de expansão

Um pool de computação pode atuar como um grupo de escala horizontal do PolyBase para consultas distribuídas entre diferentes fontes de dados, como HDFS, Oracle, MongoDB ou Terradata. Usando pods de computação no Kubernetes, os clusters de Big Data podem automatizar a criação e a configuração de pods de computação para os grupos de escala horizontal do PolyBase.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], consulte os seguintes recursos:

- [O que [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]são?](big-data-cluster-overview.md)
- [Workshop: Arquitetura [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] da Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
