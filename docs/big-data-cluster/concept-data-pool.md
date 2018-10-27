---
title: O que é um pool de dados de clusters de grandes dados SQL? | Microsoft Docs
description: Este artigo descreve o pool de dados em um cluster de big data do SQL Server de 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: bf47aa1734e2b1a849fb8333da9c914ea4244f41
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50050758"
---
# <a name="what-is-a-sql-big-data-clusters-data-pool"></a>O que é um pool de dados de clusters de grandes dados SQL?

Este artigo descreve a função do *pools de dados do SQL Server* em um cluster de big data de visualização de 2019 do SQL Server. As seções a seguir descrevem a arquitetura e a funcionalidade de um pool de dados SQL.

## <a name="data-pool-architecture"></a>Arquitetura do pool de dados

Um pool de dados consiste em uma ou mais instâncias de pool de dados do SQL Server. Instâncias do pool de dados SQL fornecem armazenamento persistente do SQL Server para o cluster. Um pool de dados é usado para ingerir dados de consultas SQL ou trabalhos do Spark. Para fornecer um melhor desempenho em grandes conjuntos de dados, os dados em um pool de dados são distribuídos em fragmentos entre as instâncias de pool de dados SQL de membro.

## <a name="scale-out-data-marts"></a>Armazéns de dados de expansão

Os pools de dados permitem a criação de armazéns de dados de expansão, onde dados externos de várias fontes são ingeridos no pool de dados. Porque os dados são distribuídos entre instâncias do pool de dados, consultas paralelas contra os dados coletados são mais eficientes.

![Armazém de dados de expansão](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os clusters de grandes dados do SQL Server, consulte a visão geral a seguir:

- [Quais são os clusters do SQL Server 2019 grandes dados?](big-data-cluster-overview.md)
