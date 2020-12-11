---
description: sys.dm_fts_outstanding_batches (Transact-SQL)
title: sys.dm_fts_outstanding_batches (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_outstanding_batches
- dm_fts_outstanding_batches_TSQL
- sys.dm_fts_outstanding_batches_TSQL
- sys.dm_fts_outstanding_batches
dev_langs:
- TSQL
helpviewer_keywords:
- troubleshooting [SQL Server], full-text search
- sys.dm_fts_outstanding_batches dynamic management view
ms.assetid: c4d697ed-c906-4c28-b137-036a25e13c84
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 98faf34f1af430bfe870f8a9ea91fb1d751f0b52
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97323805"
---
# <a name="sysdm_fts_outstanding_batches-transact-sql"></a>sys.dm_fts_outstanding_batches (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna informações sobre cada lote de indexação de texto completo.  
  
  |Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID do banco de dados|  
|catalog_id|**int**|Identificação do catálogo de texto completo.|  
|table_id|**int**|ID da tabela que contém o índice de texto completo.|  
|batch_id|**int**|ID do Lote|  
|memory_address|**varbinary (8)**|O endereço de memória do objeto do lote.|  
|crawl_memory_address|**varbinary (8)**|Endereço de memória do objeto de rastreamento (objeto pai).|  
|memregion_memory_address|**varbinary (8)**|Endereço de memória da região de memória da memória de compartilhamento de saída do host daemon do filtro (fdhost.exe).|  
|hr_batch|**int**|O código de erro mais recente do lote.|  
|is_retry_batch|**bit**|Indica se este é um lote de repetição:<br /><br /> 0 = Não<br /><br /> 1 = Sim|  
|retry_hints|**int**|Tipo de repetição necessária para o lote:<br /><br /> 0 = Nenhuma repetição<br /><br /> 1 = Repetição de multi-thread<br /><br /> 2 = Repetição de thread único<br /><br /> 3 = Repetição de único e multi-thread<br /><br /> 5 = Repetição final de multi-thread<br /><br /> 6 = Repetição final de thread único<br /><br /> 7 = Repetição final de único e multi-thread|  
|retry_hints_description|**nvarchar(120)**|Descrição do tipo de repetição necessária:<br /><br /> SEM REPETIÇÃO<br /><br /> REPETIÇÃO DE MULTI-THREAD<br /><br /> REPETIÇÃO DE THREAD ÚNICO<br /><br /> REPETIÇÃO DE ÚNICO E MULTI-THREAD<br /><br /> REPETIÇÃO FINAL DE MULTI-THREAD<br /><br /> REPETIÇÃO FINAL DE THREAD ÚNICO<br /><br /> REPETIÇÃO FINAL DE ÚNICO E MULTI-THREAD|  
|doc_failed|**bigint**|Número de documentos do lote que falharam.|  
|batch_timestamp|**timestamp**|O valor do carimbo de data/hora obtido quando o lote foi criado.|  
  
## <a name="permissions"></a>Permissões  

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nos objetivos do serviço básico, S0 e S1 do banco de dados SQL, e para bancos de dados em pools elásticos, o `Server admin` ou uma `Azure Active Directory admin` conta é necessária. Em todos os outros objetivos de serviço do banco de dados SQL, a `VIEW DATABASE STATE` permissão é necessária no banco de dados.   
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir localiza o número de lotes que está sendo processado para cada tabela na instância de servidor.  
  
```  
SELECT database_id, table_id, COUNT(*) AS batch_count FROM sys.dm_fts_outstanding_batches GROUP BY database_id, table_id ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico de pesquisa de texto completo e de pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Pesquisa de texto completo](../../relational-databases/search/full-text-search.md)  
  
  
