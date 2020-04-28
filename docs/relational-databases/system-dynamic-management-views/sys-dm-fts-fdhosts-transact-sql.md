---
title: sys. dm_fts_fdhosts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_fdhosts
- dm_fts_fdhosts_TSQL
- sys.dm_fts_fdhosts
- sys.dm_fts_fdhosts_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_fdhosts dynamic management view
- troubleshooting [SQL Server], full-text search
ms.assetid: d42a6334-4362-4361-83da-f8324fe55ec7
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 77bf96ee1cea4356e26d33fab9ab519e99ae0a60
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68265957"
---
# <a name="sysdm_fts_fdhosts-transact-sql"></a>sys.dm_fts_fdhosts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre a atividade atual do host (ou hosts) daemon do filtro da instância de servidor.  
  
 
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**fdhost_id**|**int**|ID do host daemon do filtro.|  
|**fdhost_name**|**nvarchar(120)**|Nome de host daemon do filtro.|  
|**fdhost_process_id**|**int**|ID de processo do Windows do host daemon do filtro.|  
|**fdhost_type**|**nvarchar(120)**|Tipo de documento que está sendo processado pelo host daemon do filtro, um de:<br /><br /> Thread único<br /><br /> Multi-thread<br /><br /> Documento enorme|  
|**max_thread**|**int**|Número de máximo de threads no host daemon do filtro.|  
|**batch_count**|**int**|Número de lotes que estão sendo processados no host daemon do filtro.|  
  
## <a name="permissions"></a>Permissões  

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   

## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o nome do host daemon do filtro e seu número máximo de threads. Ele também monitora quantos lotes estão sendo processados no daemon do filtro. Essa informação pode ser usada para diagnosticar o desempenho.  
  
```  
SELECT fdhost_name, batch_count, max_thread FROM sys.dm_fts_fdhosts;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico de pesquisa de texto completo e de pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Pesquisa de texto completo](../../relational-databases/search/full-text-search.md)  
  
  
