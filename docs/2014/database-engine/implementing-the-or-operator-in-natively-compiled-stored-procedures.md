---
title: Implementando o OR operador em procedimentos armazenados compilados nativamente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f2528e74-2b1c-48cb-861b-c4e57b51ac35
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 64de082cd12c967f3f3c90ca3cb99c51985ed41a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62778907"
---
# <a name="implementing-the-or-operator-in-natively-compiled-stored-procedures"></a>Implementando o operador OR em procedimentos armazenados compilados de modo nativo
  Não há suporte para os operadores OR nos predicados de consulta em procedimentos armazenados compilados de modo nativo. Como também não há suporte para os operadores NOT nos predicados de consulta em procedimentos armazenados compilados de modo nativo, os efeitos dos operadores OR não podem ser simulados apenas através do uso de operadores lógicos equivalentes. No entanto, os efeitos de um operador OR podem ser simulados com variáveis de tabela com otimização de memória.  
  
## <a name="or-operator-in-where-clause"></a>Operador OR na cláusula WHERE  
 Se você tiver um operador OR na cláusula WHERE, poderá usar a abordagem a seguir para simular seu comportamento:  
  
1.  Crie uma variável de tabela com otimização de memória usando o esquema apropriado. Isso requer um tipo de tabela com otimização de memória predefinido.  
  
2.  Começando com o operador OR de nível superior, separe a cláusula WHERE em duas partes de acordo com os predicados unidos pelo operador OR. Se houver mais de um operador OR em uma cláusula WHERE, talvez seja necessário fazer isso mais de uma vez. Repita essa etapa até que não reste nenhum operador OR. Por exemplo, se você tiver o seguinte predicado:  
  
    ```  
    pred1 OR (pred2 AND (pred3 OR pred4)) OR (pred5 AND pred6)  
    ```  
  
     Depois dessa etapa, você terá os seguintes predicados:  
  
    ```  
    pred1  
    pred5 AND pred6  
    pred2 AND pred3  
    pred2 AND pred4  
    ```  
  
3.  Executar uma consulta com cada uma das duas partes encontradas na etapa 2 como predicado. Insira o resultado de cada consulta na variável de tabela com otimização de memória criada na etapa 1.  
  
4.  Se necessário, remova as duplicatas da variável de tabela com otimização de memória.  
  
5.  Use o conteúdo da variável de tabela com otimização de memória como resultado da consulta.  
  
 O exemplo a seguir usa tabelas do banco de dados AdventureWorks2012 que foram atualizadas no [!INCLUDE[hek_2](../includes/hek-2-md.md)]. Para baixar os arquivos para este exemplo, acesse [bancos de dados AdventureWorks – 2012, 2008R2 e 2008](http://msftdbprodsamples.codeplex.com/releases/view/93587). Para aplicar [!INCLUDE[hek_2](../includes/hek-2-md.md)] código de exemplo AdventureWorks2012, acesse [exemplos de OLTP na memória do SQL Server 2014](https://msftdbprodsamples.codeplex.com/releases/view/114491).  
  
 Adicione o seguinte procedimento armazenado ao banco de dados. Converteremos esse procedimento armazenado para usar a compilação nativa.  
  
```  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesOrderDetail_ondisk  
  @SalesOrderId int = 0, @SalesOrderDetailId int = 0,   
  @CarrierTrackingNumber nvarchar(25) = N'', @ProductId int = 0,   
  @minUnitPrice money = 0, @maxUnitPrice money = 0  
AS BEGIN  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_ondisk s  
  WHERE  s.SalesOrderId = @SalesOrderId  
      OR s.SalesOrderDetailId = @SalesOrderDetailId  
      OR s.CarrierTrackingNumber = @CarrierTrackingNumber  
      OR s.ProductID = @ProductId  
      OR (s.UnitPrice > @minUnitPrice AND s.UnitPrice < @maxUnitPrice)  
END  
GO  
```  
  
 Após a conversão, o esquema da tabela e do procedimento armazenado será o seguinte:  
  
```  
CREATE TYPE Sales.fuzzySearchSalesOrderDetailType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  ModifiedDate datetime2(7) not null  
  INDEX ix_fuzzySearchSalesOrderDetailType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE TYPE Sales.fuzzySearchSalesOrderDetailTempType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  recordcount int not null  
  INDEX ix_fuzzySearchSalesOrderDetailTempType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesOrderDetail_inmem  
  @SalesOrderId int = 0, @SalesOrderDetailId int = 0,   
  @CarrierTrackingNumber nvarchar(25) = N'', @ProductId int = 0,   
  @minUnitPrice money = 0, @maxUnitPrice money = 0  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'ENGLISH')  
  
  DECLARE @retValue Sales.fuzzySearchSalesOrderDetailType  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.SalesOrderId = @SalesOrderId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.SalesOrderDetailId = @SalesOrderDetailId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.CarrierTrackingNumber COLLATE Latin1_General_BIN2 = @CarrierTrackingNumber COLLATE Latin1_General_BIN2   
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.ProductID = @ProductId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE (s.UnitPrice > @minUnitPrice AND s.UnitPrice < @maxUnitPrice)  
  
  -- After the above statements, there will be duplicates inside @retValue  
  -- Delete the duplicates from @retValue  
  DECLARE @duplicates Sales.fuzzySearchSalesOrderDetailTempType  
  
  INSERT INTO @duplicates (SalesOrderId, SalesOrderDetailId, recordcount)   
  SELECT SalesOrderId, SalesOrderDetailId, COUNT(*) AS recordCount  
  FROM @retValue  
  GROUP BY SalesOrderId, SalesOrderDetailId  
  
  -- Now we have one row per pair  
  -- clear and rebuild the result set  
  DELETE FROM @retValue  
  
  INSERT INTO @retValue  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN @duplicates d ON s.SalesOrderId = d.SalesOrderId AND s.SalesOrderDetailId = d.SalesOrderDetailId  
  
  -- After this every pair of (SalesOrderId, SalesOrderDetailId) in @retValue should be unique.  
  SELECT SalesorderId, SalesOrderDetailId, ModifiedDate FROM @retValue  
END  
GO  
```  
  
## <a name="or-operator-in-join-condition"></a>Operador OR na condição JOIN  
 Se você tiver um operador OR na condição JOIN de uma instrução SELECT, poderá usar a abordagem a seguir para simular seu comportamento. Se houver mais de um operador OR em uma condição JOIN ou várias condições JOIN com operadores OR, talvez seja necessário fazer isso mais de uma vez.  
  
 Se você tiver condições OUTER JOIN, poderá combinar essa solução com a solução das condições OUTER JOIN.  
  
1.  Crie uma variável de tabela com otimização de memória usando o esquema apropriado. Isso requer um tipo de tabela com otimização de memória predefinido.  
  
2.  Separe o predicado na condição JOIN em duas partes de acordo com os predicados unidos pelo operador OR. Se você tiver várias condições JOIN, talvez precise fazer isso em cada condição JOIN e criar um conjunto de combinações dos fragmentos resultantes. Por exemplo, se você tiver três condições JOIN com um operador OR em cada condição JOIN, talvez tenha os predicados 2x2x2=8.  
  
3.  Para cada predicado gerado pela etapa 2, crie uma consulta que inserirá o resultado na variável de tabela com otimização de memória criada na etapa 1.  
  
4.  Se necessário, remova as duplicatas da variável de tabela com otimização de memória.  
  
5.  Use o conteúdo da variável de tabela com otimização de memória como resultado da consulta.  
  
 O exemplo a seguir usa tabelas do banco de dados AdventureWorks2012 que foram atualizadas no [!INCLUDE[hek_2](../includes/hek-2-md.md)]. Para baixar os arquivos para este exemplo, acesse [bancos de dados AdventureWorks – 2012, 2008R2 e 2008](http://msftdbprodsamples.codeplex.com/releases/view/93587). Para aplicar [!INCLUDE[hek_2](../includes/hek-2-md.md)] código de exemplo AdventureWorks2012, acesse [exemplos de OLTP na memória do SQL Server 2014](https://msftdbprodsamples.codeplex.com/releases/view/114491).  
  
 Adicione o seguinte procedimento armazenado ao banco de dados. Converteremos esse procedimento armazenado para usar a compilação nativa. Esse exemplo usa condições INNER JOIN.  
  
```  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesSpecialOffers_ondisk  
  @SpecialOfferId int  
AS BEGIN  
  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_ondisk s  
  JOIN Sales.SpecialOffer_onDisk offer   
    ON s.SpecialOfferID = offer.SpecialOfferID   
    OR s.ProductID IN (SELECT ProductId FROM Sales.SpecialOfferProduct sop WHERE sop.SpecialOfferID = @SpecialOfferId)  
END  
```  
  
 Após a conversão, o esquema da tabela e do procedimento armazenado será o seguinte:  
  
```  
CREATE TYPE Sales.fuzzySearchSalesSpecialOffers_Type AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  SpecialOfferId int not null,  
  ModifiedDate datetime2(7) not null  
  INDEX ix_fuzzySearchSalesSpecialOffers_Type NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE TYPE Sales.fuzzySearchSalesSpecialOffers_TempType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  SpecialOfferId int not null,  
  recordcount int null  
  INDEX ix_fuzzySearchSalesSpecialOffers_TempType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesSpecialOffers_inmem  
  @SpecialOfferId int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'ENGLISH')  
  
  DECLARE @retValue Sales.FuzzySearchSalesSpecialOffers_Type  
  
  -- Find all special offers matching the conditions  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, SpecialOfferid, ModifiedDate)  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN Sales.SpecialOffer_inmem offer   
    ON s.SpecialOfferID = offer.SpecialOfferID  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, SpecialOfferid, ModifiedDate)  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN Sales.SpecialOfferProduct_inmem sop   
    ON sop.SpecialOfferId = @SpecialOfferId AND s.ProductID = sop.ProductId  
  
  -- Now we need to remove the duplicates from @matchingSpecialOffers  
  DECLARE @duplicates Sales.fuzzySearchSalesSpecialOffers_TempType  
  
  INSERT INTO @duplicates (SalesOrderId, SalesOrderDetailId, SpecialOfferid, recordcount)  
  SELECT SalesOrderId, SalesOrderDetailId, SpecialOfferId, COUNT(*)   
  FROM @retValue  
  GROUP BY SalesOrderId, SalesOrderDetailId, SpecialOfferId  
  
  -- now there should be no duplicates within @duplicate  
  -- use @duplicate for join.  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN @duplicates offer   
    ON    s.SalesOrderId = offer.SalesOrderId   
      AND s.SalesOrderDetailId = offer.SalesOrderDetailID   
      AND s.SpecialOfferId = offer.SpecialOfferId  
END  
GO  
```  
  
## <a name="side-effects"></a>Efeitos colaterais  
 Se houver mais de um operador OR na cláusula WHERE ou na condição JOIN, o número de consultas que você precisa executar para simular o comportamento pode aumentar exponencialmente. Isso pode reduzir o desempenho da consulta e aumentar o uso da memória devido à necessidade de uso das variáveis de tabela com otimização de memória.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de migração para procedimentos armazenados compilados nativamente](../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)  
  
  
