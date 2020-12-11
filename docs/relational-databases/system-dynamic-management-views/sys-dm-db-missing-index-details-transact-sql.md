---
description: sys.dm_db_missing_index_details (Transact-SQL)
title: sys.dm_db_missing_index_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bb253a26812d07a2527dc0a21a400906f1bb638a
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97321877"
---
# <a name="sysdm_db_missing_index_details-transact-sql"></a>sys.dm_db_missing_index_details (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna informações detalhadas sobre índices ausentes e exclusão de índices espaciais.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, todas as linhas que contêm dados que não pertencem ao locatário conectado serão filtradas.  

  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**index_handle**|**int**|Identifica um determinado índice ausente. O identificador é exclusivo no servidor. **index_handle** é a chave desta tabela.|  
|**database_id**|**smallint**|Identifica o banco de dados onde reside a tabela com o índice ausente.|  
|**object_id**|**int**|Identifica a tabela onde o índice está ausente.|  
|**equality_columns**|**nvarchar(4000)**|Lista separada por vírgulas de colunas que contribuem para os predicados de igualdade do formulário:<br /><br /> *tabela. coluna*  = *constant_value*|  
|**inequality_columns**|**nvarchar(4000)**|Lista separada por vírgulas de colunas que contribuem para predicados de desigualdade, por exemplo, predicados do formulário:<br /><br /> *tabela. coluna*  >  *constant_value*<br /><br /> Qualquer operador de comparação diferente de "=" expressa desigualdade.|  
|**included_columns**|**nvarchar(4000)**|Lista separada por vírgulas de colunas necessárias como colunas de cobertura para a consulta. Para obter mais informações sobre como abranger ou incluir colunas, consulte [criar índices com colunas incluídas](../../relational-databases/indexes/create-indexes-with-included-columns.md).<br /><br /> Para índices com otimização de memória (hash e não clusterizado com otimização de memória), ignore **included_columns**. Todas as colunas da tabela são incluídas em cada índice com otimização de memória.|  
|**instrução**|**nvarchar(4000)**|Nome da tabela onde o índice está ausente.|  
  
## <a name="remarks"></a>Comentários  
 As informações retornadas por **sys.dm_db_missing_index_details** serão atualizadas quando uma consulta for otimizada pelo otimizador de consulta e não persistirão. As informações do índice ausente são mantidas apenas até o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ser reiniciado. Os administradores de banco de dados devem periodicamente gerar cópias de backup de informações de índice ausente se quiserem mantê-las após o desligamento e a reinicialização do servidor.  
  
 Para determinar a quais grupos de índice ausente um determinado índice ausente pertence, você pode consultar a exibição de gerenciamento dinâmico **sys.dm_db_missing_index_groups** unindo-a por igualdade a **sys.dm_db_missing_index_details** com base na coluna **index_handle**.  

  >[!NOTE]
  >O conjunto de resultados para essa DMV é limitado a 600 linhas. Cada linha contém um índice ausente. Se você tiver mais de 600 índices ausentes, você deverá resolver os índices ausentes existentes para que possa exibir os mais recentes. 
  
## <a name="using-missing-index-information-in-create-index-statements"></a>Usando informações de índice ausente em instruções CREATE INDEX  
 Para converter as informações retornadas por **Sys.dm_db_missing_index_details** em uma instrução CREATE INDEX para os índices baseados em disco e com otimização de memória, as colunas de igualdade devem ser colocadas antes das colunas de desigualdade e, juntas, devem tornar a chave do índice. As colunas incluídas devem ser adicionadas à instrução CREATE INDEX com a cláusula INCLUDE. Para determinar uma ordem efetiva para as colunas desiguais, ordene-as com base em sua seletividade: liste as colunas mais seletivas primeiro (a mais à esquerda na lista de colunas).  
  
 Para obter mais informações sobre índices com otimização de memória, consulte [índices para tabelas de Memory-Optimized](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md).  
  
## <a name="transaction-consistency"></a>Consistência de transação  
 Se uma transação criar ou descartar uma tabela, as linhas contendo as informações de índice ausente sobre os objetos descartados serão removidas do objeto de gerenciamento dinâmico, preservando a consistência da transação.  
  
## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nos objetivos do serviço básico, S0 e S1 do banco de dados SQL, e para bancos de dados em pools elásticos, o `Server admin` ou uma `Azure Active Directory admin` conta é necessária. Em todos os outros objetivos de serviço do banco de dados SQL, a `VIEW DATABASE STATE` permissão é necessária no banco de dados.   

## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sys.dm_db_missing_index_columns ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.dm_db_missing_index_groups ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.dm_db_missing_index_group_stats ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
