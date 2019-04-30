---
title: Migrando colunas computadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 64a9eade-22c3-4a9d-ab50-956219e08df1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f5355af9adb2ae2a06fab1041b22959165dfaf2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63165048"
---
# <a name="migrating-computed-columns"></a>Criando colunas computadas
  As colunas computadas não têm suporte em tabelas com otimização de memória. No entanto, você pode simular uma coluna computada.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Migrando para OLTP na memória](migrating-to-in-memory-oltp.md)  
  
  
