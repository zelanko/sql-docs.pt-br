---
title: sys.dm_tran_version_store_space_usage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_space_usage_TSQL
- sys.dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_version_store_space_usage dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
caps.latest.revision: 10
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 9f1cbef003053c5bac2861fb0490710d882d3578
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmtranversionstorespaceusage-transact-sql"></a>sys.dm_tran_version_store_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

Retorna uma tabela que exibe o total de espaço em tempdb usado pelos registros de repositório de versão para cada banco de dados. **sys.dm_tran_version_store_space_usage** é eficiente e não é caro para ser executado, ele não navegar por meio de registros de repositório de versão individual, e retorna agregados espaço de armazenamento de versão consumido em tempdb por banco de dados.
  
Cada registro com controle de versão é armazenado como dados binários, junto com algumas informações de rastreamento ou de status. Semelhante a registros em tabelas de banco de dados, os registros de armazenamento de versão são armazenados em páginas de 8.192 bytes. Se um registro exceder 8.192 bytes, ele será dividido em dois registros diferentes.  
  
Porque o registro com controle de versão é armazenado como binário, não há nenhum problema com agrupamentos diferentes de bancos de dados diferentes. Use **sys.dm_tran_version_store_space_usage** para monitorar e planejar o tamanho de tempdb com base no uso de espaço do repositório de versão de bancos de dados em uma instância do SQL Server.
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**Int**|ID do banco de dados do banco de dados.|  
|**reserved_page_count**|**bigint**|Contagem total de páginas reservadas em tempdb para a versão armazenar os registros do banco de dados.|  
|**reserved_space_kb**|**bigint**|Espaço total usado em quilobytes em tempdb para a versão armazenar os registros do banco de dados.|  
  
## <a name="permissions"></a>Permissões  
Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   

## <a name="examples"></a>Exemplos  
A consulta a seguir pode ser usada para determinar o espaço consumido em tempdb, pelo repositório de versão de cada banco de dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância. 
  
```sql  
SELECT 
  DB_NAME(database_id) as 'Database Name',
  reserved_page_count,
  reserved_space_kb 
FROM sys.dm_tran_version_store_space_usage;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Database Name            reserved_page_count reserved_space_kb  
------------------------ -------------------- -----------  
msdb                      0                    0             
AdventureWorks2016        10                   80             
AdventureWorks2016DW      0                    0             
WideWorldImporters        20                   160             
```
 
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à transação &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
