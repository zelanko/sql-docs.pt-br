---
title: O que é o pool de armazenamento?
titleSuffix: SQL Server 2019 big data clusters
description: Este artigo descreve o pool de armazenamento em um cluster de big data do SQL Server de 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 7dfb89103bb83fc77c590e5c5b5984cbd96b197d
ms.sourcegitcommit: 715683b5fc7a8e28a86be8949a194226b72ac915
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58477921"
---
# <a name="what-is-the-storage-pool-sql-server-2019-big-data-clusters"></a>O que é o pool de armazenamento (clusters de big data de 2019 do SQL Server)?

Este artigo descreve a função dos *pool de armazenamento do SQL Server* em um cluster de big data do SQL Server 2019 (visualização). As seções a seguir descrevem a arquitetura e a funcionalidade de um pool de armazenamento do SQL.

## <a name="storage-pool-architecture"></a>Arquitetura do pool de armazenamento

O pool de armazenamento consiste em armazenamento compostos de nós do SQL Server no Linux, Spark e HDFS. Todos os nós de armazenamento em um cluster de big data SQL são membros de um cluster do HDFS.

![Arquitetura do pool de armazenamento](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>Responsabilidades

Nós de armazenamento serão responsáveis por:

- Ingestão de dados por meio do Spark.
- Armazenamento de dados no HDFS (formato Parquet). HDFS também fornece a persistência de dados, como dados do HDFS são distribuídos entre todos os nós de armazenamento no cluster de big data do SQL.
- Acesso a dados por meio de pontos de extremidade do HDFS e o SQL Server.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os clusters de grandes dados do SQL Server, consulte os seguintes recursos:

- [Quais são os clusters do SQL Server 2019 grandes dados?](big-data-cluster-overview.md)
- [Workshop: Arquitetura de clusters de grandes dados do Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
