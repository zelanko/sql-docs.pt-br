---
title: Exibições do sistema, procedimentos armazenados, DMVs e tipos de espera para OLTP in-memory | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: efaa59e3-dbfa-407f-b1aa-cb0c6602ea17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 04b2d0fdd00d9f3001ce1687744a9ecd992f44dd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48144616"
---
# <a name="system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp"></a>Exibições do sistema, procedimentos armazenados, tipos de espera e DMVs para OLTP in-memory
  Este tópico fornece descrições breves e links para vários objetos de banco de dados que dão suporte a OLTP na memória.  
  
### <a name="system-views"></a>Exibições do sistema  
  
|Exibição do sistema|Description|Recurso de OLTP na memória|  
|-----------------|-----------------|-----------------------------|  
|[sys.data_spaces &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-data-spaces-transact-sql)|Verifica se um grupo de arquivos contém dados com otimização de memória.|As colunas a seguir exibem valores adicionais: **tipo** e **type_desc**.|  
|[sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)|Verifica se um índice está em uma tabela com otimização de memória.|As colunas a seguir exibem valores adicionais: **tipo** e **type_desc**.|  
|[sys.parameters &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-parameters-transact-sql)|Verifique se o parâmetro não é anulável (para uma execução mais eficiente de um procedimento armazenado compilado nativamente).|**is_nullable** coluna.|  
|[sys.all_sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-all-sql-modules-transact-sql)|Verifique se algum procedimento armazenado foi originalmente compilado.|**uses_native_compilation** coluna.|  
|[sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)|Verifique se algum procedimento armazenado foi originalmente compilado.|**uses_native_compilation** coluna.|  
|[table_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-table-types-transact-sql)|Verifique se uma tabela tem otimização de memória.|**is_memory_optimized** coluna.|  
|[sys.tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)|Verifica se uma tabela tem otimização de memória e verifica a configuração de durabilidade da tabela.|**durabilidade**, **durability_desc**, e **is_memory_optimized** colunas.|  
|[sys.hash_indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-hash-indexes-transact-sql)|Mostre os índices de hash de uma tabela com otimização de memória.|Específico para OLTP na memória.|  
  
### <a name="metadata-functions"></a>Funções de metadados  
  
|Função de metadados|Description|Recurso de OLTP na memória|  
|-----------------------|-----------------|-----------------------------|  
|[OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)|Verifica se os objetos de banco de dados tem otimização de memória.|**ExecIsWithNativeCompilation** e **TableIsMemoryOptimized** propriedades.<br /><br /> O **IsSchemaBound** propriedade dá suporte ao tipo de objeto Procedure (retorna 0 para procedimentos, em vez de NULL).|  
|[SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)|Verifica se um servidor dá suporte a OLTP na memória.|**Isxtpsupported não depende** propriedade.|  
  
### <a name="system-stored-procedures"></a>Procedimentos armazenados do sistema  
  
|Procedimento armazenado|Description|  
|----------------------|-----------------|  
|[sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql)|Associa um banco de dados de OLTP na memória para um pool de recursos.|  
|[sys.sp_xtp_checkpoint_force_garbage_collection &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-checkpoint-force-garbage-collection-transact-sql)|Inicia a coleta de lixo em um banco de dados de OLTP na memória.|  
|[sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql)|Habilita a coleta de estatísticas para procedimentos armazenados compilados nativamente.|  
|[sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql)|Habilita a coleta de estatísticas por consulta para procedimentos armazenados compilados nativamente.|  
|[sp_xtp_merge_checkpoint_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql)|Mescla dados e arquivos delta.|  
|[sys.sp_xtp_unbind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql)|Remove a associação entre um banco de dados e um pool de recursos.|  
  
## <a name="dynamic-management-views-dmvs"></a>DMVs (exibições de gerenciamento dinâmico)  
 Há várias DMVs para tabelas com otimização de memória.  
  
 Para obter detalhes, consulte [exibições de gerenciamento dinâmico tabela com otimização de memória &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql).  
  
## <a name="wait-types"></a>Tipo de espera  
 Há vários tipos de espera que dão suporte a OLTP na memória.  
  
 Para obter detalhes, consulte tipos que têm o prefixo de espera **WAIT_XTP**, e **XTPPROC** no [DM os_wait_stats &#40;Transact-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql) tópico.  
  
## <a name="see-also"></a>Consulte também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)   
 [Suporte ao Transact-SQL para OLTP in-memory](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
  
