---
title: Dicas de ordem para operações de cópia em massa
description: Descreve como usar dicas de ordem em operações de cópia em massa.
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: c7365bdc6da75e04d019ca1a6a87b90dd8d4ec3c
ms.sourcegitcommit: 6b3569977b034554883a94d73d1c4df6e2f74fe2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2020
ms.locfileid: "85110098"
---
# <a name="order-hints-for-bulk-copy-operations"></a>Dicas de ordem para operações de cópia em massa

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

As operações de cópia em massa oferecem vantagens de desempenho significativas em relação a outros métodos para carregar dados em uma tabela do SQL Server. O desempenho pode ser aprimorado ainda mais usando as dicas de ordem. Especificar dicas de ordem para suas operações de cópia em massa pode diminuir o tempo de inserção de dados classificados em tabelas com índices clusterizados.

Por padrão, a operação Bulk Insert pressupõe que os dados de entrada não estejam ordenados. O SQL Server força um tipo intermediário desses dados antes de carregá-los em massa. Se você souber que os dados de entrada já estão classificados, poderá usar as dicas de ordem para informar a operação de cópia em massa sobre a ordem de classificação das colunas de destino que fazem parte de um índice clusterizado.
  
## <a name="adding-order-hints-to-a-bulk-copy-operation"></a>Adicionar dicas de ordem a uma operação de cópia em massa  
O exemplo a seguir copia dados em massa de uma tabela de origem no banco de dados de exemplo **AdventureWorks** para uma tabela de destino no mesmo banco de dados. Um objeto SqlBulkCopyColumnOrderHint é criado para definir a ordem de classificação para a coluna **ProductNumber** na tabela de destino. Em seguida, a dica de ordem é adicionada à instância SqlBulkCopy, que acrescentará o argumento da dica de ordem apropriado à consulta de `INSERT BULK` resultante.

[!code-csharp [SqlBulkCopy.ColumnOrderHint#1](~/../sqlclient/doc/samples/SqlBulkCopy_ColumnOrderHint.cs#1)]

## <a name="next-steps"></a>Próximas etapas
- [Operações de cópia em massa no SQL Server](bulk-copy-operations-sql-server.md)
