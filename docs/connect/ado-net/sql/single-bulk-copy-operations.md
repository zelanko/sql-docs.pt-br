---
title: Operação únicas de cópia em massa
description: Descreve como fazer uma cópia em massa de dados em uma instância do SQL Server usando a classe SqlBulkCopy e como executar a operação de cópia em massa usando instruções Transact-SQL e a classe SqlCommand.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 5e7ff0be-3f23-4996-a92c-bd54d65c3836
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 1029d9a0121b23963ccfc12582bd9d9cc7fd6cd6
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896594"
---
# <a name="single-bulk-copy-operations"></a>Operação únicas de cópia em massa

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

A abordagem mais simples para a execução de uma operação de cópia em massa do SQL Server é executar uma única operação em um banco de dados. Por padrão, uma operação de cópia em massa é executada como uma operação isolada: a operação de cópia ocorre de forma não transacionada, sem a oportunidade de disponibilizá-la de volta.  
  
> [!NOTE]
>  Se você precisar reverter toda ou parte da cópia em massa quando ocorrer um erro, poderá usar uma transação gerenciada <xref:Microsoft.Data.SqlClient.SqlBulkCopy> ou executar a operação de cópia em massa dentro de uma transação existente. **SqlBulkCopy** também funcionará com <xref:System.Transactions> se a conexão for inscrita (implícita ou explicitamente) em uma transação de **System.Transactions**.  
>   
>  Para obter mais informações, veja [Operações de cópia em massa e transação](transaction-bulk-copy-operations.md).  
  
As etapas gerais para executar uma operação de cópia em massa são:  
  
1. Conectar-se ao servidor de origem e obter os dados a serem copiados. Os dados também podem vir de outras fontes, desde que possam ser recuperados de um objeto <xref:System.Data.IDataReader> ou <xref:System.Data.DataTable>.  
  
2. Conecte-se ao servidor de destino (a menos que você queira que **SqlBulkCopy** estabeleça uma conexão para você).  
  
3. Crie um objeto <xref:Microsoft.Data.SqlClient.SqlBulkCopy>, configurando as propriedades necessárias.  
  
4. Defina a propriedade **DestinationTableName** para indicar a tabela de destino para a operação BULK INSERT.  
  
5. Chame um dos métodos **WriteToServer**.  
  
6. Opcionalmente, atualize as propriedades e chame **WriteToServer** novamente, conforme necessário.  
  
7. Chame <xref:Microsoft.Data.SqlClient.SqlBulkCopy.Close%2A> ou encapsule as operações de cópia em massa em uma instrução `Using`.  
  
> [!CAUTION]
>  É recomendável que os tipos de dados da coluna de origem e destino correspondam. Se os tipos de dados não corresponderem, o **SqlBulkCopy** tentará converter cada valor de origem para o tipo de dados de destino usando as regras empregadas por <xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>. As conversões podem afetar o desempenho e também podem resultar em erros inesperados. Por exemplo, um tipo de dados `Double` pode ser convertido em um tipo de dados `Decimal` na maior parte das vezes, mas não sempre.  
  
## <a name="example"></a>Exemplo  
O aplicativo de console a seguir demonstra como carregar dados usando a classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy>. Neste exemplo, um <xref:Microsoft.Data.SqlClient.SqlDataReader> é usado para copiar dados da tabela **Production.Product** no banco de dados **AdventureWorks** do SQL Server em uma tabela semelhante no mesmo banco de dados.  
  
> [!IMPORTANT]
>  Essa amostra não será executada, a menos que você tenha criado as tabelas de trabalho conforme descrito em [Configuração de exemplo de cópia em massa](bulk-copy-example-setup.md). Esse código é fornecido para demonstrar a sintaxe para usar somente **SqlBulkCopy**. Se as tabelas de origem e destino estiverem localizadas na mesma instância do SQL Server, será mais fácil e mais rápido usar uma instrução `INSERT … SELECT` do Transact-SQL para copiar os dados.  
  
[!code-csharp[DataWorks SqlBulkCopy_WriteToServer#1](~/../sqlclient/doc/samples/SqlBulkCopy_WriteToServer.cs#1)]
  
## <a name="performing-a-bulk-copy-operation-using-transact-sql-and-the-command-class"></a>Como executar uma operação de cópia em massa usando Transact-SQL e a classe command  
O exemplo a seguir ilustra como usar o método <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> para executar a instrução BULK INSERT.  
  
> [!NOTE]
>  O caminho do arquivo da fonte de dados é relativo ao servidor. O processo do servidor deve ter acesso a esse caminho para que a operação de cópia em massa seja bem-sucedida.  
  
```csharp  
using (SqlConnection connection = New SqlConnection(connectionString))  
{  
string queryString =  "BULK INSERT Northwind.dbo.[Order Details] " +  
    "FROM 'f:\mydata\data.tbl' " +  
    "WITH ( FORMATFILE='f:\mydata\data.fmt' )";  
connection.Open();  
SqlCommand command = new SqlCommand(queryString, connection);  
  
command.ExecuteNonQuery();  
}  
```  
  
## <a name="next-steps"></a>Próximas etapas
- [Operações de cópia em massa no SQL Server](bulk-copy-operations-sql-server.md)
