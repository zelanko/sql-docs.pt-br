---
title: O que é o pool de armazenamento de clusters de grandes dados do SQL Server? | Microsoft Docs
description: Este artigo descreve o pool de armazenamento em um cluster de big data do SQL Server de 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: cbf9ff14ece1b33e1c271786bc96f0ac590b807e
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50050748"
---
# <a name="what-is-the-sql-server-big-data-clusters-storage-pool"></a>O que é o pool de armazenamento de clusters de grandes dados do SQL Server?

Este artigo descreve a função dos *pool de armazenamento do SQL Server* em um cluster de big data de visualização de 2019 do SQL Server. As seções a seguir descrevem a arquitetura e a funcionalidade de um pool de armazenamento do SQL.

## <a name="storage-pool-architecture"></a>Arquitetura do pool de armazenamento

O pool de armazenamento consiste em armazenamento compostos de nós do SQL Server no Linux, Spark e HDFS. Todos os nós de armazenamento em um cluster de big data SQL são membros de um cluster do HDFS.

![Arquitetura do pool de armazenamento](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>Responsabilidades

Nós de armazenamento serão responsáveis por:

- Ingestão de dados por meio do Spark.
- Armazenamento de dados no HDFS (formato Parquet). HDFS também fornece a persistência de dados, como dados do HDFS são distribuídos entre todos os nós de armazenamento no cluster de big data do SQL.
- Acesso a dados por meio de pontos de extremidade do HDFS e o SQL Server.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os clusters de grandes dados do SQL Server, consulte a visão geral a seguir:

- [Quais são os clusters do SQL Server 2019 grandes dados?](big-data-cluster-overview.md)
