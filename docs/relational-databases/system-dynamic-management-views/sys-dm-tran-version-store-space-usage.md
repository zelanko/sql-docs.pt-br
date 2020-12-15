---
description: sys.dm_tran_version_store_space_usage (Transact-SQL)
title: sys.dm_tran_version_store_space_usage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2fb83ffddba629b35f60bc930dc1525af7037244
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474787"
---
# <a name="sysdm_tran_version_store_space_usage-transact-sql"></a>sys.dm_tran_version_store_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

Retorna uma tabela que exibe o espaço total em tempdb usado pelos registros de repositório de versão para cada banco de dados. a **Sys.dm_tran_version_store_space_usage** é eficiente e não cara para ser executada, pois não navega por registros de repositório de versão individuais e retorna o espaço de armazenamento de versão agregado consumido em tempdb por banco de dados.
  
Cada registro com versão é armazenado como dados binários, junto com algumas informações de status ou controle. Semelhante a registros em tabelas de banco de dados, os registros de armazenamento de versão são armazenados em páginas de 8.192 bytes. Se um registro exceder 8.192 bytes, ele será dividido em dois registros diferentes.  
  
Porque o registro com controle de versão é armazenado como binário, não há nenhum problema com ordenações diferentes de bancos de dados diferentes. Use **Sys.dm_tran_version_store_space_usage** para monitorar e planejar o tamanho do tempdb com base no uso do espaço do repositório de versão de bancos de dados em uma instância do SQL Server.
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID do banco de dados.|  
|**reserved_page_count**|**bigint**|Contagem total das páginas reservadas em tempdb para registros de repositório de versão do banco de dados.|  
|**reserved_space_kb**|**bigint**|Espaço total usado em kilobytes em tempdb para registros de repositório de versão do banco de dados.|  
  
## <a name="permissions"></a>Permissões  
Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   

## <a name="examples"></a>Exemplos  
A consulta a seguir pode ser usada para determinar o espaço consumido em tempdb, por repositório de versão de cada banco de dados em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância do. 
  
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
 
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à transação &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
