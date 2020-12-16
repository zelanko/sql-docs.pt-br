---
title: Expressão CASE em um procedimento armazenado compilado nativamente
description: Os módulos T-SQL compilados nativamente dão suporte a expressões CASE em algumas versões do SQL Server. Este exemplo implementa a expressão CASE em uma consulta.
ms.custom: seo-dt-2019
ms.date: 11/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2f82db01-da7e-4a7d-8bc0-48b245e6f768
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 10dac4fb1068e42d296c5091da5e7c9ff6d96eec
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460449"
---
# <a name="implementing-a-case-expression-in-a-natively-compiled-stored-procedure"></a>Implementando uma expressão CASE em um procedimento armazenado compilado nativamente
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**Aplica-se a:** [!INCLUDE[ssSDSFull_md](../../includes/sssdsfull-md.md)] e ao SQL Server começando pelo [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]

Há suporte para expressões CASE em módulos T-SQL compilados nativamente. O exemplo a seguir demonstra uma maneira de usar a expressão CASE em uma consulta. 

``` 
-- Query using a CASE expression in a natively compiled stored procedure.
CREATE PROCEDURE dbo.usp_SOHOnlineOrderResult  
   WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
   AS BEGIN ATOMIC WITH  (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE=N'us_english')  
   SELECT   
      SalesOrderID,   
      CASE (OnlineOrderFlag)   
      WHEN 1 THEN N'Order placed online by customer'  
      ELSE N'Order placed by sales person'  
      END  
   FROM Sales.SalesOrderHeader_inmem
END  
GO  
  
EXEC dbo.usp_SOHOnlineOrderResult  
GO  
``` 

**Aplica-se a:** [!INCLUDE[ssSQL14-md](../../includes/ssSQL14-md.md)] e ao SQL Server começando pelo [!INCLUDE[ssSQL15-md](../../includes/ssSQL15-md.md)]

  *Não* há suporte para expressões CASE em módulos T-SQL compilados nativamente. O exemplo a seguir mostra uma maneira de implementar a funcionalidade de uma expressão CASE em um procedimento armazenado compilado nativamente.  
  
 Os exemplos de código usam uma variável de tabela para construir um único conjunto de resultados. Isso é adequado somente durante o processamento de um número de linhas limitado, porque ela envolve a criação de uma cópia adicional das linhas de dados.  
  
 Você deve testar o desempenho dessa solução alternativa.  
  
```  
-- original query  
SELECT   
   SalesOrderID,   
   CASE (OnlineOrderFlag)   
   WHEN 1 THEN N'Order placed online by customer'  
   ELSE N'Order placed by sales person'  
   END  
FROM Sales.SalesOrderHeader_inmem  
  
--  workaround for CASE in natively compiled stored procedures  
--  use a table for the single resultset  
CREATE TYPE dbo.SOHOnlineOrderResult AS TABLE  
(  
   SalesOrderID uniqueidentifier not null index ix_SalesOrderID,  
     OrderFlag nvarchar(100) not null  
) with (memory_optimized=on)  
go  
  
-- natively compiled stored procedure that includes the query  
CREATE PROCEDURE dbo.usp_SOHOnlineOrderResult  
   WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
   AS BEGIN ATOMIC WITH  
      (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE=N'us_english')  
  
   -- table variable for creating the single resultset  
   DECLARE @result dbo.SOHOnlineOrderResult  
  
   -- CASE OnlineOrderFlag=1  
   INSERT @result   
   SELECT SalesOrderID, N'Order placed online by customer'  
      FROM Sales.SalesOrderHeader_inmem  
      WHERE OnlineOrderFlag=1  
  
   -- ELSE  
   INSERT @result   
   SELECT SalesOrderID, N'Order placed by sales person'  
      FROM Sales.SalesOrderHeader_inmem  
      WHERE OnlineOrderFlag!=1  
  
   -- return single resultset  
   SELECT SalesOrderID, OrderFlag FROM @result  
END  
GO  
  
EXEC dbo.usp_SOHOnlineOrderResult  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de migração para procedimentos armazenados compilados nativamente](./a-guide-to-query-processing-for-memory-optimized-tables.md)   
 [Construções do Transact-SQL sem suporte pelo OLTP na memória](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
