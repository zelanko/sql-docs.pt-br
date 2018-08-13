---
title: sys.dm_db_missing_index_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: e1c1ff768f69cebb4ec8195326c644260d154c80
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39536676"
---
# <a name="sysdmdbmissingindexdetails-transact-sql"></a>sys.dm_db_missing_index_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações detalhadas sobre índices ausentes e exclusão de índices espaciais.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, cada linha que contém os dados que não pertencem ao locatário conectado será filtrada.  

  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**index_handle**|**int**|Identifica um determinado índice ausente. O identificador é exclusivo no servidor. **index_handle** é a chave dessa tabela.|  
|**database_id**|**smallint**|Identifica o banco de dados onde reside a tabela com o índice ausente.|  
|**object_id**|**int**|Identifica a tabela onde o índice está ausente.|  
|**equality_columns**|**nvarchar(4000)**|Lista separada por vírgulas de colunas que contribuem para os predicados de igualdade do formulário:<br /><br /> *table.column* =*constant_value*|  
|**inequality_columns**|**nvarchar(4000)**|Lista separada por vírgulas de colunas que contribuem para predicados de desigualdade, por exemplo, predicados do formulário:<br /><br /> *table.column* > *constant_value*<br /><br /> Qualquer operador de comparação diferente de "=" expressa desigualdade.|  
|**included_columns**|**nvarchar(4000)**|Lista separada por vírgulas de colunas necessárias como colunas de cobertura para a consulta. Para obter mais informações sobre como cobrir ou colunas incluídas, consulte [criar índices com colunas incluídas](../../relational-databases/indexes/create-indexes-with-included-columns.md).<br /><br /> Para índices com otimização de memória (hash e otimização de memória não clusterizado), ignore **included_columns**. Todas as colunas da tabela são incluídas em cada índice com otimização de memória.|  
|**instrução**|**nvarchar(4000)**|Nome da tabela onde o índice está ausente.|  
  
## <a name="remarks"></a>Remarks  
 Informações retornadas por **DM db_missing_index_details** é atualizada quando uma consulta for otimizada pelo otimizador de consulta e não é persistente. As informações do índice ausente são mantidas apenas até o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ser reiniciado. Os administradores de banco de dados devem periodicamente gerar cópias de backup de informações de índice ausente se quiserem mantê-las após o desligamento e a reinicialização do servidor.  
  
 Para determinar qual índice ausente grupos a um determinado índice ausente é parte do, você pode consultar a **db_missing_index_groups** exibição de gerenciamento dinâmico por pertence com **DM db_missing_index_details**  com base em de **index_handle** coluna.  

  >[!NOTE]
  >Conjunto de resultados para essa DMV são limitado a 600 linhas. Cada linha contém um índice ausente. Se você tiver mais de 600 índices ausentes, você deve tratar os índices ausentes existentes para que você possa exibir, em seguida, as mais recentes. 
  
## <a name="using-missing-index-information-in-create-index-statements"></a>Usando informações de índice ausente em instruções CREATE INDEX  
 Para converter as informações retornadas por **DM db_missing_index_details** em uma instrução CREATE INDEX para índices com otimização de memória tanto baseadas em disco, as colunas iguais devem ser colocadas antes das colunas desiguais e juntos elas devem gerar a chave do índice. As colunas incluídas devem ser adicionadas à instrução CREATE INDEX com a cláusula INCLUDE. Para determinar uma ordem efetiva para as colunas desiguais, ordene-as com base em sua seletividade: liste as colunas mais seletivas primeiro (a mais à esquerda na lista de colunas).  
  
 Para obter mais informações sobre índices com otimização de memória, consulte [índices para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md).  
  
## <a name="transaction-consistency"></a>Consistência de transação  
 Se uma transação criar ou descartar uma tabela, as linhas contendo as informações de índice ausente sobre os objetos descartados serão removidas do objeto de gerenciamento dinâmico, preservando a consistência da transação.  
  
## <a name="permissions"></a>Permissões

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` permissão no banco de dados.   

## <a name="see-also"></a>Consulte também  
 [sys.dm_db_missing_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
