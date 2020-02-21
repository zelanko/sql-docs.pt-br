---
title: Configuração de exemplo de cópia em massa
description: Descreve as tabelas usadas nos exemplos de cópia em massa e fornece scripts SQL para criar as tabelas no banco de dados AdventureWorks.
ms.date: 09/30/2019
dev_langs:
- sql
ms.assetid: d4dde6ac-b8b6-4593-965a-635c8fb2dadb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 129dc64fc9bac2111cd0bc5cb61f3ce7f1d98ee1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247872"
---
# <a name="bulk-copy-example-setup"></a>Configuração de exemplo de cópia em massa

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

A classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy> pode ser usada para gravar dados somente em tabelas do SQL Server. Os exemplos de código mostrados neste tópico usam o banco de dados de exemplo do SQL Server, **AdventureWorks**. Para evitar a alteração das tabelas existentes, os exemplos de código gravam dados em tabelas que você deve criar primeiro.  
  
As tabelas **BulkCopyDemoMatchingColumns** e **BulkCopyDemoDifferentColumns** são baseadas na tabela **AdventureWorks** **Production.Products**. Nos exemplos de código que usam essas tabelas, os dados são adicionados da tabela **Production.Products** para uma dessas tabelas de exemplo. A tabela **BulkCopyDemoDifferentColumns** é usada quando o exemplo ilustra como mapear colunas de dados de origem para a tabela de destino; **BulkCopyDemoMatchingColumns** é usada na maioria dos outros exemplos.  
  
Alguns dos exemplos de código demonstram como usar uma classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy> para gravar em várias tabelas. Para esses exemplos, as tabelas **BulkCopyDemoOrderHeader** e **BulkCopyDemoOrderDetail** são usadas como as tabelas de destino. Essas tabelas são baseadas nas tabelas **Sales.SalesOrderHeader** e **Sales.SalesOrderDetail** no **AdventureWorks**.  
  
> [!NOTE]
>  Os exemplos de código **SqlBulkCopy** são fornecidos para demonstrar a sintaxe para usar o **SqlBulkCopy** apenas. Se as tabelas de origem e destino estiverem localizadas na mesma instância do SQL Server, será mais fácil e mais rápido usar uma instrução `INSERT … SELECT` do Transact-SQL para copiar os dados.  
  
## <a name="table-setup"></a>Configuração da tabela  
Para criar as tabelas necessárias para que os exemplos de código sejam executado corretamente, você deve executar as seguintes instruções Transact-SQL em um banco de dados do SQL Server.  
  
```sql
USE AdventureWorks  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoMatchingColumns]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoMatchingColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoMatchingColumns]([ProductID] [int] IDENTITY(1,1) NOT NULL,  
    [Name] [nvarchar](50) NOT NULL,  
    [ProductNumber] [nvarchar](25) NOT NULL,  
 CONSTRAINT [PK_ProductID] PRIMARY KEY CLUSTERED  
(  
    [ProductID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoDifferentColumns]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoDifferentColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoDifferentColumns]([ProdID] [int] IDENTITY(1,1) NOT NULL,  
    [ProdNum] [nvarchar](25) NOT NULL,  
    [ProdName] [nvarchar](50) NOT NULL,  
 CONSTRAINT [PK_ProdID] PRIMARY KEY CLUSTERED  
(  
    [ProdID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderHeader]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderHeader]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderHeader]([SalesOrderID] [int] IDENTITY(1,1) NOT NULL,  
    [OrderDate] [datetime] NOT NULL,  
    [AccountNumber] [nvarchar](15) NULL,  
 CONSTRAINT [PK_SalesOrderID] PRIMARY KEY CLUSTERED  
(  
    [SalesOrderID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderDetail]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderDetail]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderDetail]([SalesOrderID] [int] NOT NULL,  
    [SalesOrderDetailID] [int] NOT NULL,  
    [OrderQty] [smallint] NOT NULL,  
    [ProductID] [int] NOT NULL,  
    [UnitPrice] [money] NOT NULL,  
 CONSTRAINT [PK_LineNumber] PRIMARY KEY CLUSTERED  
(  
    [SalesOrderID] ASC,  
    [SalesOrderDetailID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
```  
  
## <a name="next-steps"></a>Próximas etapas
- [Operações de cópia em massa no SQL Server](bulk-copy-operations-sql-server.md)
