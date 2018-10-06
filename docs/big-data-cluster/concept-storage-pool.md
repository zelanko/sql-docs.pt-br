---
title: O que é o pool de armazenamento de clusters de grandes dados do SQL Server? | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 100ce09f7066a6df33d7b1daaf50db50bda4ed03
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48795772"
---
# <a name="what-is-the-sql-server-big-data-clusters-storage-pool"></a>O que é o pool de armazenamento de clusters de grandes dados do SQL Server?

Este artigo descreve a função dos *pool de armazenamento do SQL Server* em um servidor de SQL 2019 visualizar o cluster de Big Data. As seções a seguir descrevem a arquitetura e a funcionalidade de um pool de armazenamento do SQL.

## <a name="storage-pool-architecture"></a>Arquitetura do pool de armazenamento

O pool de armazenamento consiste em armazenamento compostos de nós do SQL Server no Linux, Spark e HDFS. Todos os nós de armazenamento em um cluster de Big Data do SQL são membros de um cluster do HDFS.

![Arquitetura do pool de armazenamento](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>Responsabilidades

Nós de armazenamento serão responsáveis por:

- Ingestão de dados por meio do Spark.
- Armazenamento de dados no HDFS (formato Parquet). HDFS também fornece a persistência de dados, como dados do HDFS são distribuídos entre todos os nós de armazenamento do cluster de Big Data do SQL.
- Acesso a dados por meio de pontos de extremidade do HDFS e o SQL Server.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os clusters de grandes dados do SQL Server, consulte a visão geral a seguir:

- [O que é o SQL Server 2019 clusters de big data?](big-data-cluster-overview.md)
