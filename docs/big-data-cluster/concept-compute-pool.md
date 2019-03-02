---
title: Quais são os pools de computação?
titleSuffix: SQL Server 2019 big data clusters
description: Este artigo descreve o pool de computação em um cluster de big data do SQL Server 2019 (visualização).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 272f10cfed8f7cd1b07633b81642323a8c74b6d7
ms.sourcegitcommit: 56fb7b648adae2c7b81bd969de067af1a2b54180
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2019
ms.locfileid: "57227128"
---
# <a name="what-are-compute-pools-in-a-sql-server-2019-big-data-cluster"></a>Quais são os pools de computação em um cluster de big data do SQL Server 2019?

Este artigo descreve a função do *pools de computação do SQL Server* em um cluster de big data de visualização de 2019 do SQL Server. Pools de computação fornecem recursos computacionais de escalabilidade horizontal para um cluster de big data. As seções a seguir descrevem a arquitetura e a funcionalidade de um pool de computação.

## <a name="compute-pool-architecture"></a>Arquitetura do pool de computação

Um pool de computação é feito de um ou mais pods em execução no Kubernetes de computação. A criação automatizada e o gerenciamento desses pods é coordenada pelo [instância mestre do SQL Server](concept-master-instance.md). Cada pod contém um conjunto de serviços de base e uma instância do mecanismo de banco de dados do SQL Server.

## <a name="scale-out-groups"></a>Grupos de expansão

Um pool de computação pode agir como um grupo de escala horizontal do PolyBase para consultas distribuídas em fontes de dados diferentes, como HDFS, Oracle, MongoDB ou Teradata. Usando computação pods no Kubernetes, clusters de big data podem automatizar a criação e configuração de pods de computação para grupos de escala horizontal do PolyBase.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os clusters de grandes dados do SQL Server, consulte a visão geral a seguir:

- [Quais são os clusters do SQL Server 2019 grandes dados?](big-data-cluster-overview.md)
