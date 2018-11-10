---
title: O que é um pool de computação de clusters de grandes dados SQL? | Microsoft Docs
description: Este artigo descreve o pool de computação em um cluster de big data do SQL Server de 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 6aa73c5881a4b6a17e190c26c15f97b3d8c79c14
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221792"
---
# <a name="what-is-a-sql-big-data-clusters-compute-pool"></a>O que é um pool de computação de clusters de grandes dados SQL?

Este artigo descreve a função do *pools de computação do SQL Server* em um cluster de big data de visualização de 2019 do SQL Server. Pools de computação fornecem recursos computacionais de escalabilidade horizontal para um cluster de big data. As seções a seguir descrevem a arquitetura e a funcionalidade de um pool de computação.

## <a name="compute-pool-architecture"></a>Arquitetura do pool de computação

Um pool de computação é feito de um ou mais pods em execução no Kubernetes de computação. A criação automatizada e o gerenciamento desses pods é coordenada pelo [instância mestre do SQL Server](concept-master-instance.md). Cada pod contém um conjunto de serviços de base e uma instância do mecanismo de banco de dados do SQL Server.

> [!NOTE]
> CTP 2.1 dá suporte apenas um pool de computação único por cluster.

## <a name="scale-out-groups"></a>Grupos de expansão

Um pool de computação pode agir como um grupo de escala horizontal do PolyBase para consultas distribuídas em fontes de dados diferentes, como HDFS, Oracle, MongoDB ou Teradata. Usando computação pods no Kubernetes, clusters de big data podem automatizar a criação e configuração de pods de computação para grupos de escala horizontal do PolyBase.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os clusters de grandes dados do SQL Server, consulte a visão geral a seguir:

- [Quais são os clusters do SQL Server 2019 grandes dados?](big-data-cluster-overview.md)
