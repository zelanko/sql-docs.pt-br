---
title: Migrando colunas computadas | Microsoft Docs
description: Saiba como simular colunas computadas em tabelas com otimização de memória. Avalie se a funcionalidade de coluna computada é necessária após a migração.
ms.custom: ''
ms.date: 12/17/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 64a9eade-22c3-4a9d-ab50-956219e08df1
author: MightyPen
ms.author: genemi
monikerRange: =sql-server-2016
ms.openlocfilehash: 95f920fc8648ed646f1056c9d334ee831651f5e2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465367"
---
# <a name="migrating-computed-columns"></a>Criando colunas computadas

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

As colunas computadas não têm suporte em tabelas com otimização de memória. No entanto, você pode simular uma coluna computada.

Do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] em diante, há suporte para colunas computadas em índices e tabelas com otimização de memória.

Considere a necessidade da persistência de suas colunas computadas ao migrar as tabelas baseadas em disco para as tabelas com otimização de memória. As diferentes características de desempenho das tabelas com otimização de memória e dos procedimentos armazenados compilados nativamente podem negar a necessidade da persistência.  
  
## <a name="non-persisted-computed-columns"></a>Colunas computadas não persistentes  
 Para simular os efeitos de uma coluna computada não persistente, crie uma exibição na tabela com otimização de memória. Na instrução SELECT que define a exibição, adicione a definição de coluna computada à exibição. A não ser em um procedimento armazenado compilado nativamente, as consultas que usam valores da coluna computada devem ler a exibição. Nos procedimentos armazenados compilados nativamente, você deve atualizar qualquer instrução select, update ou delete de acordo com sua definição de coluna computada.  
  
```sql  
-- Schema for the table dbo.OrderDetails:  
-- OrderId int not null primary key,  
-- ProductId int not null,  
-- SalePrice money not null,  
-- Quantity int not null,  
-- Total money not null  
--  
-- Total is computed as SalePrice * Quantity and is not persisted.  
CREATE VIEW dbo.v_order_details AS  
   SELECT  
      OrderId,  
      ProductId,  
      SalePrice,  
      Quantity,  
      Quantity * SalePrice AS Total  
   FROM dbo.order_details  
```  
  
## <a name="persisted-computed-columns"></a>Colunas computadas persistentes  
 Para simular os efeitos de uma coluna computada persistente, crie um procedimento armazenado para inserção na tabela e outro procedimento armazenado para atualizar a tabela. Ao inserir ou atualizar a tabela, chame esses procedimentos armazenados para executar essas tarefas. Nos procedimentos armazenados, calcule o valor do campo computado de acordo com as entradas, praticamente da mesma maneira que a coluna computada é definida na tabela baseada em disco original. Em seguida, insira ou atualize a tabela conforme necessário no procedimento armazenado.  
  
```sql  
-- Schema for the table dbo.OrderDetails:  
-- OrderId int not null primary key,  
-- ProductId int not null,  
-- SalePrice money not null,  
-- Quantity int not null,  
-- Total money not null  
--  
-- Total is computed as SalePrice * Quantity and is persisted.  
-- we need to create insert and update procedures to calculate Total.  

CREATE PROCEDURE sp_insert_order_details   
@OrderId int, @ProductId int, @SalePrice money, @Quantity int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (LANGUAGE = N'english', TRANSACTION ISOLATION LEVEL = SNAPSHOT)  

-- compute the value here.   
-- this stored procedure works with single rows only.  
-- for bulk inserts, accept a table-valued parameter into the stored procedure  
-- and use an INSERT INTO SELECT statement.  

DECLARE @total money = @SalePrice * @Quantity  
INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)  
VALUES (@OrderId, @ProductId, @SalePrice, @Quantity, @total)  
END  
GO  
  
CREATE PROCEDURE sp_update_order_details_by_id  
@OrderId int, @ProductId int, @SalePrice money, @Quantity int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (LANGUAGE = N'english', TRANSACTION ISOLATION LEVEL = SNAPSHOT)  

-- compute the value here.   
-- this stored procedure works with single rows only.  

DECLARE @total money = @SalePrice * @Quantity  
UPDATE dbo.OrderDetails   
SET ProductId = @ProductId, SalePrice = @SalePrice, Quantity = @Quantity, Total = @total  
WHERE OrderId = @OrderId  
END  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Migrando para OLTP na memória](./plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)  
  
