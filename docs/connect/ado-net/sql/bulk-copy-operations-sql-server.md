---
title: Operações de cópia em massa no SQL Server
description: Descreve a funcionalidade de cópia em massa para o Provedor de Dados .NET para SQL Server.
ms.date: 09/30/2019
ms.assetid: 83a7a0d2-8018-4354-97b9-0b1d99f8342b
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: d038b0a67923d7c475011b8f3d141f7d64358f61
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247856"
---
# <a name="bulk-copy-operations-in-sql-server"></a>Operações de cópia em massa no SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

O Microsoft SQL Server inclui um utilitário de linha de comando popular chamado **bcp** para copiar rapidamente grandes arquivos em massa em tabelas ou exibições em bancos de dados do SQL Server. A classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy> permite escrever soluções de código gerenciado que fornecem funcionalidade semelhante. Há outras maneiras de carregar dados em uma tabela do SQL Server (instruções INSERT, por exemplo), mas <xref:Microsoft.Data.SqlClient.SqlBulkCopy> oferece uma vantagem de desempenho significativa sobre eles.  
  
Usando a classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy>, você pode executar:  
  
- Uma única operação de cópia em massa  
  
- Várias operações de cópia em massa  
  
- Uma operação de cópia em massa dentro de uma transação  
  
> [!NOTE]
>  Ao usar o .NET Framework versão 1.1 ou anterior (que não dá suporte à classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy>), você pode executar a instrução **BULK INSERT** do Transact-SQL no SQL Server usando o objeto <xref:Microsoft.Data.SqlClient.SqlCommand>.  
  
## <a name="in-this-section"></a>Nesta seção  
[Configuração de exemplo de cópia em massa](bulk-copy-example-setup.md)  
Descreve as tabelas usadas nos exemplos de cópia em massa e fornece scripts SQL para criar as tabelas no banco de dados AdventureWorks.  
  
[Operação únicas de cópia em massa](single-bulk-copy-operations.md)  
Descreve como fazer uma cópia em massa de dados em uma instância do SQL Server usando a classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy> e como executar a operação de cópia em massa usando instruções Transact-SQL e a classe <xref:Microsoft.Data.SqlClient.SqlCommand>.  
  
[Várias operações de cópia em massa](multiple-bulk-copy-operations.md)  
Descreve como realizar várias operações de cópia em massa de dados em uma instância do SQL Server usando a classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy>.  
  
[Transações e operações de cópia em massa](transaction-bulk-copy-operations.md)  
Descreve como executar uma operação de cópia em massa em uma transação, incluindo como fazer commit ou reverter a transação.  
  
## <a name="next-steps"></a>Próximas etapas
- [SQL Server e ADO.NET](index.md)
