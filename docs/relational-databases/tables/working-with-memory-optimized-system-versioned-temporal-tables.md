---
title: Trabalhando com tabelas temporais com controle de versão do sistema de otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 691d4f80-6754-43f5-8b43-d4facf08f6fc
caps.latest.revision: 12
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d339b84876fac50d01b602109f6c1b34f3567f97
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-memory-optimized-system-versioned-temporal-tables"></a>Trabalho com tabelas temporais com controle da versão do sistema com otimização de memória
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Este tópico discute como o trabalho com uma tabela temporal com controle da versão do sistema com otimização de memória é diferente do trabalho com uma tabela temporal com versão do sistema baseada em disco.  
  
> [!NOTE]  
>  O uso de tabelas temporais com otimização de memória só se aplica ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , não ao [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
## <a name="discovering-metadata"></a>Descoberta de Metadados  
 Para descobrir os metadados referentes a uma tabela temporal com controle de versão do sistema e otimização de memória, você precisa combinar as informações de [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) e [sys.internal_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md). Uma tabela temporal com controle da versão do sistema é apresentada como parent_object_id da tabela de histórico na memória interna  
  
 Este exemplo mostra como consultar e unir essas tabelas.  
  
```  
SELECT SCHEMA_NAME (T1.schema_id) as TemporalTableSchema  
   , OBJECT_NAME(IT.parent_object_id) as TemporalTableName  
   , T1.object_id as TemporalTableObjectId  
   , IT.Name as InternalHistoryStagingName   
   , SCHEMA_NAME (T2.schema_id) as HistoryTableSchema  
   , OBJECT_NAME (T1.history_table_id) as HistoryTableName   
FROM sys.internal_tables IT    
JOIN sys.tables T1   
   ON IT.parent_object_id = T1.object_id   
JOIN sys.tables T2   
   ON T1.history_table_id = T2.object_id   
WHERE T1.is_memory_optimized  = 1 AND T1.temporal_type = 2  
  
```  
  
## <a name="modifying-data"></a>Modificando dados  
 As tabelas temporais com controle da versão do sistema com otimização de memória podem ser modificadas por meio de procedimentos armazenados compilados nativamente que permitem converter tabelas não temporais com otimização de memória para versão do sistema e manter procedimentos existentes armazenados nativamente.  
  
 Este exemplo mostra como uma tabela criada anteriormente pode ser modificada no módulo compilado nativamente.  
  
```  
CREATE PROCEDURE dbo.UpdateFXCurrencyPair  
   (   
       @ProviderID int  
     , @CurrencyID1 int  
     , @CurrencyID2 int  
     , @BidRate decimal(8,4)  
     , @AskRate decimal(8,4)   
   )   
WITH NATIVE_COMPILATION, SCHEMABINDING  
   , EXECUTE AS OWNER   
AS    
   BEGIN ATOMIC WITH   
   (TRANSACTION ISOLATION LEVEL = SNAPSHOT  , LANGUAGE = N'English')   
      UPDATE dbo.FXCurrencyPairs SET AskRate = @AskRate, BidRate  = @BidRate   
     WHERE ProviderID = @ProviderID AND CurrencyID1 = @CurrencyID1 AND CurrencyID2 = @CurrencyID2   
END   
GO ;  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Criação de uma tabela temporal com controle da versão do sistema com otimização de memória](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)   
 [Monitorando tabelas temporais com controle da versão do sistema com otimização de memória](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)   
 [Considerações sobre desempenho com tabelas temporais com versão do sistema e otimização de memória](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)   
 [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)   
 [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Gerenciar a Retenção de Dados Históricos em Tabelas Temporais com Versão do Sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
