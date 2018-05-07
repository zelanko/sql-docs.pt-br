---
title: sys.dm_db_missing_index_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_details
- dm_db_missing_index_details
- sys.dm_db_missing_index_details_TSQL
- dm_db_missing_index_details_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- missing indexes feature [SQL Server], sys.dm_db_missing_index_details dynamic management view
- sys.dm_db_missing_index_details dynamic management view
ms.assetid: ced484ae-7c17-4613-a3f9-6d8aba65a110
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0bfe8e6ce05b89d5c069521f88526b771386c94c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmdbmissingindexdetails-transact-sql"></a>sys.dm_db_missing_index_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações detalhadas sobre índices ausentes e exclusão de índices espaciais.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, cada linha que contém os dados que não pertencem ao locatário conectado será filtrada.  

  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**index_handle**|**Int**|Identifica um determinado índice ausente. O identificador é exclusivo no servidor. **index_handle** é a chave dessa tabela.|  
|**database_id**|**smallint**|Identifica o banco de dados onde reside a tabela com o índice ausente.|  
|**object_id**|**Int**|Identifica a tabela onde o índice está ausente.|  
|**equality_columns**|**nvarchar(4000)**|Lista separada por vírgulas de colunas que contribuem para os predicados de igualdade do formulário:<br /><br /> *table.column* =*constant_value*|  
|**inequality_columns**|**nvarchar(4000)**|Lista separada por vírgulas de colunas que contribuem para predicados de desigualdade, por exemplo, predicados do formulário:<br /><br /> *table.column* > *constant_value*<br /><br /> Qualquer operador de comparação diferente de "=" expressa desigualdade.|  
|**included_columns**|**nvarchar(4000)**|Lista separada por vírgulas de colunas necessárias como colunas de cobertura para a consulta. Para obter mais informações sobre como cobrir ou colunas incluídas, consulte [criar índices com colunas incluídas](../../relational-databases/indexes/create-indexes-with-included-columns.md).<br /><br /> Para índices com otimização de memória (hash e otimização de memória não clusterizado), ignorar **included_columns**. Todas as colunas da tabela são incluídas em cada índice com otimização de memória.|  
|**instrução**|**nvarchar(4000)**|Nome da tabela onde o índice está ausente.|  
  
## <a name="remarks"></a>Remarks  
 Informações retornadas por **sys.DM db_missing_index_details** é atualizada quando uma consulta for otimizada pelo otimizador de consulta e não é persistente. As informações do índice ausente são mantidas apenas até o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ser reiniciado. Os administradores de banco de dados devem periodicamente gerar cópias de backup de informações de índice ausente se quiserem mantê-las após o desligamento e a reinicialização do servidor.  
  
 Para determinar qual índice ausente um determinado índice ausente de grupos é parte do, você pode consultar o **db_missing_index_groups** exibição de gerenciamento dinâmico, unindo com **sys.DM db_missing_index_details**  com base no **index_handle** coluna.  
  
## <a name="using-missing-index-information-in-create-index-statements"></a>Usando informações de índice ausente em instruções CREATE INDEX  
 Para converter as informações retornadas por **sys.DM db_missing_index_details** em uma instrução CREATE INDEX para índices com otimização de memória e baseadas em disco, as colunas iguais devem ser colocadas antes das colunas desiguais e juntos elas devem gerar a chave do índice. As colunas incluídas devem ser adicionadas à instrução CREATE INDEX com a cláusula INCLUDE. Para determinar uma ordem efetiva para as colunas desiguais, ordene-as com base em sua seletividade: liste as colunas mais seletivas primeiro (a mais à esquerda na lista de colunas).  
  
 Para obter mais informações sobre índices com otimização de memória, consulte [índices para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md).  
  
## <a name="transaction-consistency"></a>Consistência de transação  
 Se uma transação criar ou descartar uma tabela, as linhas contendo as informações de índice ausente sobre os objetos descartados serão removidas do objeto de gerenciamento dinâmico, preservando a consistência da transação.  
  
## <a name="permissions"></a>Permissões

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   

## <a name="see-also"></a>Consulte também  
 [sys.dm_db_missing_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
