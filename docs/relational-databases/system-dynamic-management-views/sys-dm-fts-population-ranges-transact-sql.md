---
description: sys.dm_fts_population_ranges (Transact-SQL)
title: sys.dm_fts_population_ranges (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_population_ranges
- sys.dm_fts_population_ranges_TSQL
- dm_fts_population_ranges_TSQL
- dm_fts_population_ranges
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_population_ranges dynamic management view
ms.assetid: 58d8564b-9c43-4965-a31c-2893890334ef
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ae7ec8d8a4dde2a30e86b5c6a47e2af4d0c6c73b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484628"
---
# <a name="sysdm_fts_population_ranges-transact-sql"></a>sys.dm_fts_population_ranges (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna informações sobre os intervalos específicos relacionados a uma população de índice de texto completo atualmente em andamento.  
   
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**memory_address**|**varbinary (8)**|Endereço de buffers de memória alocado para atividade relacionada a este subintervalo de uma população de índice de texto completo.|  
|**parent_memory_address**|**varbinary (8)**|Endereço de buffers de memória que representam o objeto pai de todos os intervalos de população relacionados a um índice de texto completo.|  
|**is_retry**|**bit**|Se o valor for 1, este subintervalo será responsável por repetir as linhas que encontraram erros.|  
|**session_id**|**smallint**|ID da sessão que está processando esta tarefa atualmente.|  
|**processed_row_count**|**int**|Número de linhas que foram processadas por este intervalo. O progresso é persistido e contado a cada cinco minutos, em vez de a cada confirmação de lote.|  
|**error_count**|**int**|Número de linhas que encontraram erros neste intervalo. O progresso é persistido e contado a cada cinco minutos, em vez de a cada confirmação de lote.|  
  
## <a name="permissions"></a>Permissões  

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nos objetivos do serviço básico, S0 e S1 do banco de dados SQL, e para bancos de dados em pools elásticos, o `Server admin` ou uma `Azure Active Directory admin` conta é necessária. Em todos os outros objetivos de serviço do banco de dados SQL, a `VIEW DATABASE STATE` permissão é necessária no banco de dados.   
 
## <a name="physical-joins"></a>Junções físicas  
 ![Junções significativas dessa exibição de gerenciamento dinâmico](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-population-ranges-1.gif "Junções significativas dessa exibição de gerenciamento dinâmico")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|dm_fts_population_ranges.parent_memory_address|dm_fts_index_population.memory_address|Muitos para um|  
  
## <a name="see-also"></a>Consulte Também  
  [Exibições e funções de gerenciamento dinâmico de pesquisa de texto completo e de pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  

