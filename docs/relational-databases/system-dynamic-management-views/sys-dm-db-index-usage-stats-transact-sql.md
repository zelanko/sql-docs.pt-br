---
description: sys.dm_db_index_usage_stats (Transact-SQL)
title: sys. dm_db_index_usage_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_index_usage_stats_TSQL
- sys.dm_db_index_usage_stats
- sys.dm_db_index_usage_stats_TSQL
- dm_db_index_usage_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_index_usage_stats dynamic management view
ms.assetid: d06a001f-0f72-4679-bc2f-66fff7958b86
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8e5f1f9d5c4e313e81392d83b6d9ffdf98013880
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88374632"
---
# <a name="sysdm_db_index_usage_stats-transact-sql"></a>sys.dm_db_index_usage_stats (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna contas de tipos diferentes de operações de índice e a hora em que cada tipo de operação foi executada pela última vez.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, todas as linhas que contêm dados que não pertencem ao locatário conectado serão filtradas.  
  
> [!NOTE]  
>  **Sys. dm_db_index_usage_stats** não retorna informações sobre índices com otimização de memória. Para obter informações sobre o uso de índice com otimização de memória, consulte [Sys. dm_db_xtp_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md).  
  
> [!NOTE]  
>  Para chamar essa exibição de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use **Sys. dm_pdw_nodes_db_index_usage_stats**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_id**|**smallint**|ID do banco de dados no qual a tabela ou exibição é definida.|  
|**object_id**|**int**|ID da tabela ou exibição na qual o índice é definido.|  
|**index_id**|**int**|ID do índice.|  
|**user_seeks**|**bigint**|Número de buscas através de consultas de usuário.|  
|**user_scans**|**bigint**|Número de verificações por consultas de usuário que não usaram o predicado ' Seek '.|  
|**user_lookups**|**bigint**|Número de pesquisas de indicador através de consultas de usuário.|  
|**user_updates**|**bigint**|Número de atualizações através de consultas de usuário. Isso inclui inserir, excluir e atualizações que representam o número de operações realizadas, não as linhas reais afetadas. Por exemplo, se você excluir 1000 linhas em uma instrução, essa contagem será incrementada em 1|  
|**last_user_seek**|**datetime**|Hora da última busca de usuário.|  
|**last_user_scan**|**datetime**|Hora do último exame de usuário.|  
|**last_user_lookup**|**datetime**|Hora da última pesquisa de usuário.|  
|**last_user_update**|**datetime**|Hora da última atualização de usuário.|  
|**system_seeks**|**bigint**|Número de buscas através de consultas do sistema.|  
|**system_scans**|**bigint**|Número de exames através de consultas do sistema.|  
|**system_lookups**|**bigint**|Número de pesquisas através de consultas do sistema.|  
|**system_updates**|**bigint**|Número de atualizações através de consultas do sistema.|  
|**last_system_seek**|**datetime**|Hora da última busca do sistema.|  
|**last_system_scan**|**datetime**|Hora do último exame do sistema.|  
|**last_system_lookup**|**datetime**|Hora da última pesquisa do sistema.|  
|**last_system_update**|**datetime**|Hora da última atualização do sistema.|  
|pdw_node_id|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="remarks"></a>Comentários  
 Cada busca, exame, pesquisa ou atualização individual no índice especificado pela execução de uma consulta é contado como um uso desse índice e incrementa o contador correspondente nessa exibição. As informações são relatadas para operações causadas por consultas enviadas pelo usuário e operações causadas por consultas geradas internamente, como exames de coleta de estatísticas.  
  
 O contador **user_updates** indica o nível de manutenção no índice causado pelas operações de inserção, atualização ou exclusão na tabela ou exibição subjacente. Você pode usar essa exibição para determinar quais índices são pouco usados por seus aplicativos. Também é possível usar a exibição para determinar quais índices estão incorrendo em sobrecarga de manutenção. Se desejar, você pode descartar índices que incorrem em sobrecarga de manutenção, mas são pouco usados para consultas ou não são usados.  
  
 Os contadores são inicializados para esvaziar sempre que o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) é iniciado. Além disso, sempre que um banco de dados é desanexado ou desligado (por exemplo, porque AUTO_CLOSE está definido como ON), todas as linhas associadas a ele são removidas.  
  
 Quando um índice é usado, uma linha é adicionada a **sys.dm_db_index_usage_stats** se já não existir uma para ele. Quando a linha é adicionada, seus contadores são definidos como zero inicialmente.  
  
 Durante a atualização para [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] , [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , as entradas em sys. dm_db_index_usage_stats são removidas. A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] , as entradas são retidas como estavam antes do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .  
  
## <a name="permissions"></a>Permissões  
Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o  **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .  
  
## <a name="see-also"></a>Consulte Também  

 [Exibições e funções de gerenciamento dinâmico relacionadas ao índice &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys. dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys. Objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  


