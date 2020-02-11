---
title: Exibições do sistema, procedimentos armazenados, DMVs e tipos de espera para OLTP na memória | Microsoft Docs
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
ms.openlocfilehash: d047cbc4fe3ba3f4945acd9da4f627a05992e779
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62842395"
---
# <a name="system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp"></a>Exibições do sistema, procedimentos armazenados, tipos de espera e DMVs para OLTP in-memory
  Este tópico fornece descrições breves e links para vários objetos de banco de dados que dão suporte a OLTP na memória.  
  
### <a name="system-views"></a>Exibições do sistema  
  
|Exibição do sistema|DESCRIÇÃO|Recurso de OLTP na memória|  
|-----------------|-----------------|-----------------------------|  
|[sys. data_spaces &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-data-spaces-transact-sql)|Verifica se um grupo de arquivos contém dados com otimização de memória.|As colunas a seguir exibem valores adicionais: **Type** e **type_desc**.|  
|[sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)|Verifica se um índice está em uma tabela com otimização de memória.|As colunas a seguir exibem valores adicionais: **Type** e **type_desc**.|  
|[sys.parameters &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-parameters-transact-sql)|Verifique se o parâmetro não é anulável (para uma execução mais eficiente de um procedimento armazenado compilado nativamente).|**IS_NULLABLE** coluna.|  
|[sys. all_sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-all-sql-modules-transact-sql)|Verifique se algum procedimento armazenado foi originalmente compilado.|**uses_native_compilation** coluna.|  
|[sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)|Verifique se algum procedimento armazenado foi originalmente compilado.|**uses_native_compilation** coluna.|  
|[sys. table_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-table-types-transact-sql)|Verifique se uma tabela tem otimização de memória.|**is_memory_optimized** coluna.|  
|[sys.tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)|Verifique se uma tabela tem otimização de memória e verifique a configuração de durabilidade de uma tabela.|**durabilidade**, **durability_desc**e **is_memory_optimized** colunas.|  
|[sys.hash_indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-hash-indexes-transact-sql)|Mostre os índices de hash de uma tabela com otimização de memória.|Específico para OLTP na memória.|  
  
### <a name="metadata-functions"></a>Funções de metadados  
  
|Função de metadados|DESCRIÇÃO|Recurso de OLTP na memória|  
|-----------------------|-----------------|-----------------------------|  
|[OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)|Verifica se os objetos de banco de dados tem otimização de memória.|Propriedades **ExecIsWithNativeCompilation** e **TableIsMemoryOptimized** .<br /><br /> A propriedade **IsSchemaBound** dá suporte ao tipo de objeto de procedimento (retorna 0 para procedimentos em vez de NULL).|  
|[SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)|Verifica se um servidor dá suporte a OLTP na memória.|Propriedade **IsXTPSupported** .|  
  
### <a name="system-stored-procedures"></a>Procedimentos armazenados do sistema  
  
|Procedimento armazenado|DESCRIÇÃO|  
|----------------------|-----------------|  
|[sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql)|Associa um banco de dados de OLTP na memória para um pool de recursos.|  
|[sys. sp_xtp_checkpoint_force_garbage_collection &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-checkpoint-force-garbage-collection-transact-sql)|Inicia a coleta de lixo em um banco de dados de OLTP na memória.|  
|[sys. sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql)|Habilita a coleta de estatísticas para procedimentos armazenados compilados nativamente.|  
|[sys. sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql)|Habilita a coleta de estatísticas por consulta para procedimentos armazenados compilados nativamente.|  
|[sys. sp_xtp_merge_checkpoint_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql)|Mescla dados e arquivos delta.|  
|[sys.sp_xtp_unbind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql)|Remove a associação entre um banco de dados e um pool de recursos.|  
  
## <a name="dynamic-management-views-dmvs"></a>DMVs (exibições de gerenciamento dinâmico)  
 Há várias DMVs para tabelas com otimização de memória.  
  
 Para obter detalhes, consulte [exibições de gerenciamento dinâmico da tabela com otimização de memória &#40;&#41;Transact-SQL ](/sql/relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql).  
  
## <a name="wait-types"></a>Tipo de espera  
 Há vários tipos de espera que dão suporte a OLTP na memória.  
  
 Para obter detalhes, consulte tipos de espera que são prefixados com **WAIT_XTP**e **XTPPROC** no tópico [Sys. dm_os_wait_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql) .  
  
## <a name="see-also"></a>Consulte Também  
 [O OLTP na memória &#40;a otimização na memória&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)   
 [Suporte ao Transact-SQL para OLTP in-memory](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
  
