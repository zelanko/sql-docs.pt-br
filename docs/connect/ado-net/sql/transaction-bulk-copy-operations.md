---
title: Transações e operações de cópia em massa
description: Descreve como executar uma operação de cópia em massa em uma transação, incluindo como fazer commit ou reverter a transação.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: f6f0cbc9-f7bf-4d6e-875f-ad1ba0b4aa62
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 82e7e9b5dcae2f3878104757823112022064d7e6
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80918515"
---
# <a name="transaction-and-bulk-copy-operations"></a>Transações e operações de cópia em massa

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Operações de cópia em massa podem ser executadas como operações isoladas ou como parte de uma transação de várias etapas. Essa última opção permite executar mais de uma operação de cópia em massa dentro da mesma transação, bem como executar outras operações de banco de dados (como inserções, atualizações e exclusões), podendo ainda confirmar ou reverter toda a transação.  
  
Por padrão, uma operação de cópia em massa é executada como uma operação isolada. A operação de cópia em massa ocorre de forma não transacionada, sem a oportunidade de revertê-la novamente. Se você precisar reverter toda ou parte da cópia em massa quando ocorrer um erro, poderá usar uma transação gerenciada por <xref:Microsoft.Data.SqlClient.SqlBulkCopy>, executar a operação de cópia em massa dentro de uma transação existente ou ser inscrito em uma **System.Transactions**<xref:System.Transactions.Transaction>.  
  
## <a name="performing-a-non-transacted-bulk-copy-operation"></a>Executando uma operação de cópia em massa não transacionada  
O aplicativo de Console a seguir mostra o que acontece quando uma operação de cópia em massa não transacionada encontra um erro na operação.  
  
No exemplo, cada tabela de origem e cada tabela de destino incluem uma coluna `Identity` denominada **ProductID**. O código prepara primeiro a tabela de destino excluindo todas as linhas e, em seguida, inserindo uma única linha cuja **ProductID** é conhecida por existir na tabela de origem. Por padrão, um novo valor para a coluna `Identity` é gerado na tabela de destino para cada linha adicionada. Neste exemplo, uma opção é definida quando a conexão é aberta, o que força o processo de carregamento em massa a usar os valores de `Identity` da tabela de origem.  
  
A operação de cópia em massa é executada com a propriedade <xref:Microsoft.Data.SqlClient.SqlBulkCopy.BatchSize%2A> definida como 10. Quando a operação encontra a linha inválida, uma exceção é lançada. Neste primeiro exemplo, a operação de cópia em massa é não transacionada. Todos os lotes copiados até o ponto do erro são confirmados; o lote que contém a chave duplicada é revertido e a operação de cópia em massa é interrompida antes de processar todos os outros lotes.  
  
> [!NOTE]
>  Essa amostra não será executada, a menos que você tenha criado as tabelas de trabalho conforme descrito em [Configuração de exemplo de cópia em massa](bulk-copy-example-setup.md). Esse código é fornecido para demonstrar a sintaxe para usar somente **SqlBulkCopy**. Se as tabelas de origem e destino estiverem localizadas na mesma instância do SQL Server, será mais fácil e mais rápido usar uma instrução `INSERT … SELECT` do Transact-SQL para copiar os dados.  
  
[!code-csharp[DataWorks SqlBulkCopyOpeions_Default#1](~/../sqlclient/doc/samples/SqlBulkCopyOptions_Default.cs#1)]
  
## <a name="performing-a-dedicated-bulk-copy-operation-in-a-transaction"></a>Como executar uma operação de cópia em massa dedicada em uma transação  
Por padrão, uma operação de cópia em massa é sua própria transação. Quando quiser executar uma operação de cópia em massa dedicada, crie uma instância do <xref:Microsoft.Data.SqlClient.SqlBulkCopy> com uma cadeia de conexão ou use um objeto <xref:Microsoft.Data.SqlClient.SqlConnection> existente sem uma transação ativa. Em cada cenário, a operação de cópia em massa cria e, em seguida, confirma ou reverte a transação.  
  
Você pode especificar explicitamente a opção <xref:Microsoft.Data.SqlClient.SqlBulkCopyOptions.UseInternalTransaction> no construtor de classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy> para explicitamente fazer com que uma operação de cópia em massa seja executada em sua própria transação, fazendo com que cada lote da operação de cópia em massa seja executado dentro de uma transação separada.  
  
> [!NOTE]
>  Como lotes diferentes são executados em diferentes transações, se ocorrer um erro durante a operação de cópia em massa, todas as linhas no lote atual serão revertidas, mas as linhas de lotes anteriores permanecerão no banco de dados.  
  
O aplicativo de console a seguir é semelhante ao exemplo anterior, com uma exceção: neste exemplo, a operação de cópia em massa gerencia suas próprias transações. Todos os lotes copiados até o ponto do erro são confirmados; o lote que contém a chave duplicada é revertido e a operação de cópia em massa é interrompida antes de processar todos os outros lotes.  
  
> [!IMPORTANT]
>  Essa amostra não será executada, a menos que você tenha criado as tabelas de trabalho conforme descrito em [Configuração de exemplo de cópia em massa](bulk-copy-example-setup.md). Esse código é fornecido para demonstrar a sintaxe para usar somente **SqlBulkCopy**. Se as tabelas de origem e destino estiverem localizadas na mesma instância do SQL Server, será mais fácil e mais rápido usar uma instrução `INSERT … SELECT` do Transact-SQL para copiar os dados.  
  
[!code-csharp[DataWorks SqlBulkCopyOptions_UseInternalTransaction#1](~/../sqlclient/doc/samples/SqlBulkCopyOptions_UseInternalTransaction.cs#1)]
  
## <a name="using-existing-transactions"></a>Usando transações existentes  
É possível especificar um objeto <xref:Microsoft.Data.SqlClient.SqlTransaction> existente como um parâmetro em um construtor <xref:Microsoft.Data.SqlClient.SqlBulkCopy>. Nessa situação, a operação de cópia em massa é executada em uma transação existente e nenhuma alteração é feita ao estado da transação (isto é, ela não é confirmada nem anulada). Isso permite que um aplicativo inclua a operação de cópia em massa em uma transação com outras operações de banco de dados. No entanto, uma exceção será lançada caso você não especifique um objeto <xref:Microsoft.Data.SqlClient.SqlTransaction>, passe uma referência nula e caso a conexão tenha uma transação ativa.  
  
Caso precise reverter toda a operação de cópia em massa porque ocorreu um erro. Ou caso a cópia em massa deva ser executada como parte de um processo maior que pode ser revertido, será possível fornecer um objeto <xref:Microsoft.Data.SqlClient.SqlTransaction> para o construtor <xref:Microsoft.Data.SqlClient.SqlBulkCopy>.  
  
O aplicativo de console a seguir é semelhante para o primeiro exemplo (não transacionado), com uma exceção: neste exemplo, a operação de cópia em massa está incluída em uma transação maior, externa. Quando ocorre o erro de violação de chave primária, a transação inteira é revertida e nenhuma linha é adicionada à tabela de destino.  
  
> [!IMPORTANT]
>  Essa amostra não será executada, a menos que você tenha criado as tabelas de trabalho conforme descrito em [Configuração de exemplo de cópia em massa](bulk-copy-example-setup.md). Esse código é fornecido para demonstrar a sintaxe para usar somente **SqlBulkCopy**. Se as tabelas de origem e destino estiverem localizadas na mesma instância do SQL Server, será mais fácil e mais rápido usar uma instrução `INSERT … SELECT` do Transact-SQL para copiar os dados.  
  
[!code-csharp[DataWorks SqlBulkCopy_ExternalTransaction#1](~/../sqlclient/doc/samples/SqlBulkCopy_ExternalTransaction.cs#1)]
  
## <a name="next-steps"></a>Próximas etapas
- [Operações de cópia em massa no SQL Server](bulk-copy-operations-sql-server.md)
