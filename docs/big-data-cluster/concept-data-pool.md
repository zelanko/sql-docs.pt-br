---
title: Quais são os pools de dados?
titleSuffix: SQL Server 2019 big data clusters
description: Este artigo descreve o pool de dados em um cluster de big data do SQL Server de 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 906b27c186668518702c7ab3a757e6eeb4e5b278
ms.sourcegitcommit: 715683b5fc7a8e28a86be8949a194226b72ac915
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58478221"
---
# <a name="what-are-data-pools-in-a-sql-server-2019-big-data-cluster"></a>Quais são os pools de dados em um cluster de big data do SQL Server 2019?

Este artigo descreve a função do *pools de dados do SQL Server* em um cluster de big data do SQL Server 2019 (visualização). As seções a seguir descrevem a arquitetura e a funcionalidade de um pool de dados SQL.

## <a name="data-pool-architecture"></a>Arquitetura do pool de dados

Um pool de dados consiste em uma ou mais instâncias de pool de dados do SQL Server. Instâncias do pool de dados SQL fornecem armazenamento persistente do SQL Server para o cluster. Um pool de dados é usado para ingerir dados de consultas SQL ou trabalhos do Spark. Para fornecer um melhor desempenho em grandes conjuntos de dados, os dados em um pool de dados são distribuídos em fragmentos entre as instâncias de pool de dados SQL de membro.

## <a name="scale-out-data-marts"></a>Armazéns de dados de expansão

Os pools de dados permitem a criação de armazéns de dados de expansão, onde dados externos de várias fontes são ingeridos no pool de dados. Porque os dados são distribuídos entre instâncias do pool de dados, consultas paralelas contra os dados coletados são mais eficientes.

![Armazém de dados de expansão](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os clusters de grandes dados do SQL Server, consulte os seguintes recursos:

- [Quais são os clusters do SQL Server 2019 grandes dados?](big-data-cluster-overview.md)
- [Workshop: Arquitetura de clusters de grandes dados do Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
