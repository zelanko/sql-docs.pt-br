---
title: Várias operações de cópia em massa
description: Descreve como realizar várias operações de cópia em massa de dados em uma instância do SQL Server usando a classe SqlBulkCopy.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 5ad12f94-7459-4a93-a421-4160d1a90715
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 6cc373224f4df437665cc48edb78ff81b85b8ac1
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452137"
---
# <a name="multiple-bulk-copy-operations"></a>Várias operações de cópia em massa

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Você pode executar várias operações de cópia em massa usando uma única instância de uma classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy>. Se os parâmetros da operação forem alterados entre as cópias (por exemplo, o nome da tabela de destino), você deve atualizá-los antes de qualquer chamada subsequentes, para qualquer um dos métodos **WriteToServer**, conforme demonstrado no exemplo a seguir. A menos que explicitamente alterados, todos os valores de propriedade permanecem como estavam na operação de cópia em massa anterior para determinada instância.  
  
> [!NOTE]
>  A execução de várias operações de cópia em massa usando a mesma instância de <xref:Microsoft.Data.SqlClient.SqlBulkCopy> é geralmente mais eficiente do que usar uma instância separada para cada operação.  
  
Se você executar várias operações de cópia em massa usando o mesmo objeto <xref:Microsoft.Data.SqlClient.SqlBulkCopy>, não haverá restrições se as informações de origem ou de destino forem iguais ou diferentes em cada operação. No entanto, você deve garantir que as informações de associação da coluna sejam definidas corretamente sempre que você gravar no servidor.  

## <a name="example"></a>Exemplo

> [!IMPORTANT]
>  Essa amostra não será executada, a menos que você tenha criado as tabelas de trabalho conforme descrito em [Configuração de exemplo de cópia em massa](bulk-copy-example-setup.md). Esse código é fornecido para demonstrar a sintaxe para usar somente **SqlBulkCopy**. Se as tabelas de origem e destino estiverem localizadas na mesma instância do SQL Server, será mais fácil e mais rápido usar uma instrução `INSERT … SELECT` do Transact-SQL para copiar os dados.  
  
[!code-csharp[DataWorks SqlBulkCopy_._ColumnMappingOrdersDetails#1](~/../sqlclient/doc/samples/SqlBulkCopy_ColumnMappingOrdersDetails.cs#1)]
  
## <a name="next-steps"></a>Próximas etapas
- [Operações de cópia em massa no SQL Server](bulk-copy-operations-sql-server.md)
