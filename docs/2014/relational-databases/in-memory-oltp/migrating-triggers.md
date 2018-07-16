---
title: Migrando gatilhos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ad5385c5-5a50-40ca-a319-97d5606b8511
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 49dd8abf026cc3beffe30b0137abe643b29a97d8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37175350"
---
# <a name="migrating-triggers"></a>Migrando gatilhos
  Este tópico discute gatilhos DDL e DML, e tabelas com otimização de memória.  
  
 Os gatilhos LOGON são gatilhos definidos para serem disparados em eventos LOGON. Os gatilhos LOGON não afetam tabelas com otimização de memória.  
  
## <a name="ddl-triggers"></a>Gatilhos DDL  
 Os gatilhos DDL são gatilhos definidos para disparar quando uma instrução CREATE, ALTER, DROP, GRANT, DENY, REVOKE ou UPDATE STATISTICS é executada no banco de dados ou no servidor no qual está definida.  
  
 Você não pode criar tabelas com otimização de memória se o banco de dados ou o servidor tem um ou mais gatilhos DDL definidos em CREATE_TABLE ou em qualquer grupo de eventos que o inclua. Você não pode descartar uma tabela com otimização de memória se o banco de dados ou o servidor tem um ou mais gatilhos DDL definidos em DROP_TABLE ou em qualquer grupo de eventos que o inclua.  
  
 Você não pode criar procedimentos armazenados compilados de modo nativo quando há um ou mais gatilhos DDL em CREATE_PROCEDURE, em DROP_PROCEDURE ou em qualquer grupo de eventos que inclua esses eventos.  
  
## <a name="dml-triggers"></a>Gatilhos DML  
 Os gatilhos DML não podem ser definidos em tabelas com otimização de memória. No entanto, a OLTP em Memória permitirá atingir um efeito semelhante aos gatilhos DML se você usar explicitamente procedimentos armazenados para inserir, atualizar ou excluir dados. Se o sistema contiver consultas ad hoc, converta-as para usar esses procedimentos armazenados em vez de simular o efeito dos gatilhos DML.  
  
 Dependendo do evento de gatilho (FOR/AFTER ou INSTEAD OF), você pode incluir o conteúdo do gatilho no procedimento armazenado apropriado que executa INSERT, UPDATE ou DELETE nessa tabela. Por exemplo, ao migrar um gatilho AFTER INSERT, você pode modificar o procedimento armazenado que executa a operação de inserção, incluindo o conteúdo do gatilho após a instrução INSERT apropriada.  
  
 Você pode usar um procedimento armazenado interpretado ou um procedimento armazenado compilado de modo nativo. A maioria das construções [!INCLUDE[tsql](../../includes/tsql-md.md)] em um procedimento armazenado interpretado podem ser executadas em uma tabela com otimização de memória. Entretanto, apenas um subconjunto de construções [!INCLUDE[tsql](../../includes/tsql-md.md)] tem suporte em procedimentos armazenados compilados de modo nativo. Para obter informações sobre o suporte ao [!INCLUDE[tsql](../../includes/tsql-md.md)] em tabelas com otimização de memória, consulte [Accessing Memory-Optimized Tables Using Interpreted Transact-SQL](accessing-memory-optimized-tables-using-interpreted-transact-sql.md). Para obter informações sobre o suporte ao [!INCLUDE[tsql](../../includes/tsql-md.md)] em procedimentos armazenados compilados de modo nativo, consulte [Transact-SQL Constructs Not Supported by In-Memory OLTP](transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
 Veja a seguir um exemplo simples de simulação do comportamento do gatilho DML em uma tabela com otimização de memória.  
  
 O banco de dados contém os seguintes objetos, incluídos no script como instruções CREATE TABLE, CREATE TRIGGER e CREATE PROCEDURE:  
  
```tsql  
CREATE TABLE OrderDetails  
(  
   OrderId int not null primary key,  
   ProductId int not null,  
   SalePrice money not null,  
   Quantity int not null,  
   Total money not null,  
   IsDeleted bit not null DEFAULT (0)  
)  
GO  
  
CREATE TRIGGER tr_order_details_insteadof_insert  
ON OrderDetails  
INSTEAD OF INSERT AS  
BEGIN  
   DECLARE @pid int, @qty_buy int, @qty_remain int  
   SELECT @pid = ProductId, @qty_buy = Quantity FROM inserted  
   SELECT @qty_remain = Quantity FROM Inventory WHERE ProductId = @pid  
   IF (@qty_remain <= @qty_buy)  
      THROW 51000, N'Insufficient inventory!', 1  
   ELSE  
   BEGIN  
      INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)   
      SELECT OrderId, ProductId, SalePrice, Quantity, Total FROM inserted  
      UPDATE Inventory SET Quantity = Quantity - @qty_buy WHERE ProductId = @pid  
   END  
END  
GO  
  
CREATE TRIGGER tr_order_details_after_update  
ON OrderDetails  
AFTER UPDATE AS  
BEGIN  
   INSERT INTO UpdateNotifications (OrderId, UpdateTime) SELECT OrderId, GETDATE() FROM inserted     
END  
GO  
  
CREATE PROCEDURE sp_insert_order_details   
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @total money  
AS BEGIN  
   INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)  
   VALUES (@OrderId, @ProductId, @SalePrice, @Quantity, @total)  
END  
GO  
  
CREATE PROCEDURE sp_update_order_details_by_id  
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @Total money  
AS BEGIN  
   UPDATE dbo.OrderDetails   
   SET ProductId = @ProductId, SalePrice = @SalePrice, Quantity = @Quantity, Total = @total  
   WHERE OrderId = @OrderId  
END  
GO  
```  
  
 Os seguintes objetos são funcionalmente equivalentes ao estado de pré-migração:  
  
```tsql  
CREATE TABLE OrderDetails  
(  
   OrderId int not null PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 1048576),  
   ProductId int not null,  
   SalePrice money not null,  
   Quantity int not null,  
   Total money not null,  
   IsDeleted bit not null DEFAULT (0)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
GO  
  
CREATE TABLE Inventory  
(  
   ProductId int not null PRIMARY KEY NONCLUSTERED,  
   Quantity int not null  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
GO  
  
CREATE TABLE UpdateNotifications  
(  
   OrderId int not null,  
   UpdateTime datetime2 not null  
   CONSTRAINT pk_updateNotifications PRIMARY KEY NONCLUSTERED (OrderId, UpdateTime)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
GO  
  
CREATE PROCEDURE sp_insert_order_details   
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @total money  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'English')  
   DECLARE @qty_remain int  
   SELECT @qty_remain = Quantity FROM dbo.Inventory WHERE ProductId = @ProductId  
   IF (@qty_remain <= @Quantity)  
      THROW 51000, N'Insufficient inventory!', 1  
   ELSE  
   BEGIN  
      INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)   
      VALUES (@OrderId, @ProductId, @SalePrice, @Quantity, @total)  
      UPDATE dbo.Inventory SET Quantity = Quantity - @Quantity WHERE ProductId = @ProductId  
   END  
END  
GO  
  
CREATE PROCEDURE sp_update_order_details_by_id  
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @Total money  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'English')  
   UPDATE dbo.OrderDetails   
   SET ProductId = @ProductId, SalePrice = @SalePrice, Quantity = @Quantity, Total = @total  
   WHERE OrderId = @OrderId  
   INSERT INTO dbo.UpdateNotifications (OrderId, UpdateTime) VALUES (@OrderId, GETDATE())  
END  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Migrando para OLTP na memória](migrating-to-in-memory-oltp.md)  
  
  
