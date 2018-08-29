---
title: tran_version_store_space_usage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
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
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c13145dafb316d184d8a9b2a4986550abee90b81
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43111538"
---
# <a name="sysdmtranversionstorespaceusage-transact-sql"></a>sys.dm_tran_version_store_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

Retorna uma tabela que exibe o total de espaço em tempdb usado pelos registros de repositório de versão para cada banco de dados. **tran_version_store_space_usage** é eficiente e não é caro para ser executado, pois não navegue por meio de registros de repositório de versão individuais e retorna agregado consumido em tempdb por banco de dados de espaço de armazenamento de versão.
  
Cada registro com controle de versão é armazenado como dados binários, junto com algumas informações de rastreamento ou de status. Semelhante a registros em tabelas de banco de dados, os registros de armazenamento de versão são armazenados em páginas de 8.192 bytes. Se um registro exceder 8.192 bytes, ele será dividido em dois registros diferentes.  
  
Porque o registro com controle de versão é armazenado como binário, não há nenhum problema com agrupamentos diferentes de bancos de dados diferentes. Use **tran_version_store_space_usage** para monitorar e planejar tamanho de tempdb com base no uso de espaço de armazenamento a versão de bancos de dados em uma instância do SQL Server.
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID do banco de dados do banco de dados.|  
|**reserved_page_count**|**bigint**|Contagem total de páginas reservadas no tempdb para a versão armazenar os registros do banco de dados.|  
|**reserved_space_kb**|**bigint**|Espaço total usado em quilobytes em tempdb para a versão armazenar os registros do banco de dados.|  
  
## <a name="permissions"></a>Permissões  
Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   

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
  
