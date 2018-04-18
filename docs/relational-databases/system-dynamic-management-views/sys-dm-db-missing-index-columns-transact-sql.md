---
title: sys.dm_db_missing_index_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_missing_index_columns_TSQL
- sys.dm_db_missing_index_columns_TSQL
- sys.dm_db_missing_index_columns
- dm_db_missing_index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_columns dynamic management function
- missing indexes feature [SQL Server], sys.dm_db_missing_index_columns dynamic management function
ms.assetid: 3b24e5ed-0c79-47e5-805c-a0902d0aeb86
caps.latest.revision: 40
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: da062527194387dbfbc2c2516722bbbad8faf304
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmdbmissingindexcolumns-transact-sql"></a>sys.dm_db_missing_index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre as colunas de tabela de banco de dados que estão ausentes em um índice, exceto os índices espaciais. **sys.DM db_missing_index_columns** é uma função de gerenciamento dinâmico.  

## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.dm_db_missing_index_columns(index_handle)  
```  
  
## <a name="arguments"></a>Argumentos  
 *index_handle*  
 Número inteiro que identifica exclusivamente um índice ausente. Pode ser obtido nos seguintes objetos de gerenciamento dinâmico:  
  
 [sys.dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)  
  
 [sys.dm_db_missing_index_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**column_id**|**Int**|ID da coluna.|  
|**column_name**|**sysname**|Nome da coluna da tabela.|  
|**column_usage**|**varchar(20)**|Como a coluna é usada pela consulta. Os valores possíveis e suas descrições são:<br /><br /> IGUALDADE: A coluna contribui com um predicado que expressa igualdade do formulário: <br />                        *table.column* = *constant_value*<br /><br /> Operador de DESIGUALDADE: A coluna contribui com um predicado que expressa desigualdade, por exemplo, um predicado do formulário: *tabela* > *constant_value*. Qualquer operador de comparação diferente de "=" expressa desigualdade.<br /><br /> INCLUIR: Coluna não é usada para avaliar um predicado, mas é usada por outro motivo, por exemplo, para cobrir uma consulta.|  
  
## <a name="remarks"></a>Remarks  
 Informações retornadas por **sys.DM db_missing_index_columns** é atualizada quando uma consulta for otimizada pelo otimizador de consulta e não é persistente. As informações do índice ausente são mantidas apenas até o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ser reiniciado. Os administradores de banco de dados devem periodicamente gerar cópias de backup de informações de índice ausente se quiserem mantê-las após o desligamento e a reinicialização do servidor.  
  
## <a name="transaction-consistency"></a>Consistência de transação  
 Se uma transação criar ou descartar uma tabela, as linhas contendo as informações de índice ausente sobre os objetos descartados serão removidas do objeto de gerenciamento dinâmico, preservando a consistência da transação.  
  
## <a name="permissions"></a>Permissões  
 Os usuários devem receber a permissão VIEW SERVER STATE ou qualquer permissão que implique que a permissão VIEW SERVER STATE consulte essa função de gerenciamento dinâmico.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir executa uma consulta na tabela `Address` e executa uma consulta usando a exibição de gerenciamento dinâmico `sys.dm_db_missing_index_columns` para retornar as colunas de tabela com índice ausente.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode  
FROM Person.Address  
WHERE StateProvinceID = 9;  
GO  
SELECT mig.*, statement AS table_name,  
    column_id, column_name, column_usage  
FROM sys.dm_db_missing_index_details AS mid  
CROSS APPLY sys.dm_db_missing_index_columns (mid.index_handle)  
INNER JOIN sys.dm_db_missing_index_groups AS mig ON mig.index_handle = mid.index_handle  
ORDER BY mig.index_group_handle, mig.index_handle, column_id;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
