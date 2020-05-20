---
title: sys. dm_db_missing_index_group_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_group_stats_TSQL
- sys.dm_db_missing_index_group_stats
- dm_db_missing_index_group_stats_TSQL
- dm_db_missing_index_group_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_group_stats dynamic management view
- missing indexes feature [SQL Server], sys.dm_db_missing_index_group_stats dynamic management view
ms.assetid: c2886986-9e07-44ea-a350-feeac05ee4f4
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e91971d13b26d6a156307b2a0288de236456c880
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828081"
---
# <a name="sysdm_db_missing_index_group_stats-transact-sql"></a>sys.dm_db_missing_index_group_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações resumidas sobre grupos de índices ausentes, excluindo índices espaciais.  
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, todas as linhas que contêm dados que não pertencem ao locatário conectado serão filtradas.  
    
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**group_handle**|**int**|Identifica um grupo de índices ausentes. Esse identificador é exclusivo no servidor.<br /><br /> As outras colunas fornecem informações sobre todas as consultas para as quais o índice no grupo é considerado ausente.<br /><br /> Um grupo de índice contém apenas um índice.|  
|**unique_compiles**|**bigint**|Número de compilações e recompilações que se beneficiariam deste grupo de índice ausente. Compilações e recompilações de muitas consultas diferentes podem contribuir para esse valor de coluna.|  
|**user_seeks**|**bigint**|Número de buscas geradas por consultas de usuário para as quais o índice recomendado no grupo poderia ter sido usado.|  
|**user_scans**|**bigint**|Número de exames gerados por consultas de usuário para as quais o índice recomendado no grupo poderia ter sido usado.|  
|**last_user_seek**|**datetime**|Data e hora da última busca gerada por consultas de usuário para as quais o índice recomendado no grupo poderia ter sido usado.|  
|**last_user_scan**|**datetime**|Data e hora do último exame gerado por consultas de usuário para as quais o índice recomendado no grupo poderia ter sido usado.|  
|**avg_total_user_cost**|**float**|Custo médio das consultas de usuário que poderia ser reduzido pelo índice no grupo.|  
|**avg_user_impact**|**float**|Benefício da porcentagem média que as consultas de usuário poderiam experimentar se esse grupo de índices ausentes fosse implementado. O valor indica que o custo da consulta ficaria na média dessa porcentagem se esse grupo de índices ausentes fosse implementado.|  
|**system_seeks**|**bigint**|Número de buscas geradas por consultas de sistema, como consultas de estatística automáticas, para as quais o índice recomendado no grupo poderia ter sido usado. Para obter mais informações, consulte [classe de evento auto stats](../../relational-databases/event-classes/auto-stats-event-class.md).|  
|**system_scans**|**bigint**|Número de exames gerados por consultas de sistema para as quais o índice recomendado no grupo poderia ter sido usado.|  
|**last_system_seek**|**datetime**|Data e hora da última busca gerada no sistema por consultas de sistema para as quais o índice recomendado no grupo poderia ter sido usado.|  
|**last_system_scan**|**datetime**|Data e hora do último exame gerado no sistema por consultas de sistema para as quais o índice recomendado no grupo poderia ter sido usado.|  
|**avg_total_system_cost**|**float**|Custo médio das consultas de sistema que poderia ser reduzido pelo índice no grupo.|  
|**avg_system_impact**|**float**|Benefício de porcentagem média que as consultas de sistema poderiam experimentar se esse grupo de índices ausentes fosse implementado. O valor indica que o custo da consulta ficaria na média dessa porcentagem se esse grupo de índices ausentes fosse implementado.|  
  
## <a name="remarks"></a>Comentários  
 Informações retornadas por **sys.dm_db_missing_index_group_stats** são atualizadas por todas as execuções de consulta, não por todas as compilações ou recompilações de consulta. As estatísticas de uso não são persistentes e só serão mantidas até o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ser reiniciado. Os administradores de banco de dados devem periodicamente gerar cópias de backup de informações de índice ausente se quiserem manter as estatísticas de uso após o desligamento e a reinicialização do servidor.  

  >[!NOTE]
  >O conjunto de resultados para essa DMV é limitado a 600 linhas. Cada linha contém um índice ausente. Se você tiver mais de 600 índices ausentes, você deverá resolver os índices ausentes existentes para que possa exibir os mais recentes.
  
## <a name="permissions"></a>Permissões  
 Para consultar essa exibição de gerenciamento dinâmico, os usuários devem receber a permissão VIEW SERVER STATE ou qualquer permissão que implique essa permissão.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como usar a exibição de gerenciamento dinâmico **sys.dm_db_missing_index_group_stats**.  
  
### <a name="a-find-the-10-missing-indexes-with-the-highest-anticipated-improvement-for-user-queries"></a>a. Localizar os 10 índices ausentes com o aperfeiçoamento antecipado mais alto para consultas de usuário  
 A consulta seguinte determina quais os 10 índices ausentes que produziriam o aperfeiçoamento cumulativo antecipado mais alto, em ordem decrescente, para consultas de usuário.  
  
```  
SELECT TOP 10 *  
FROM sys.dm_db_missing_index_group_stats  
ORDER BY avg_total_user_cost * avg_user_impact * (user_seeks + user_scans)DESC;  
```  
  
### <a name="b-find-the-individual-missing-indexes-and-their-column-details-for-a-particular-missing-index-group"></a>B. Localizar os índices ausentes individuais e seus detalhes de coluna de um determinado grupo de índice ausente  
 A consulta seguinte determina quais índices ausentes fazem parte de um determinado grupo de índices ausentes e exibe os detalhes de sua coluna. Por esse exemplo, o identificador de grupo de índices ausentes é 24.  
  
```  
SELECT migs.group_handle, mid.*  
FROM sys.dm_db_missing_index_group_stats AS migs  
INNER JOIN sys.dm_db_missing_index_groups AS mig  
    ON (migs.group_handle = mig.index_group_handle)  
INNER JOIN sys.dm_db_missing_index_details AS mid  
    ON (mig.index_handle = mid.index_handle)  
WHERE migs.group_handle = 24;  
```  
  
 Esta consulta fornece o nome do banco de dados, do esquema e da tabela em que um índice está ausente. Fornece também os nomes das colunas que deveriam ser usadas para a chave de índice. Ao gravar a instrução CREATE INDEX DDL para implementar índices ausentes, liste as colunas de igualdade primeiro e desigualdade na cláusula ON \< *table_name*> da instrução CREATE index. As colunas incluídas devem ser listadas na cláusula INCLUDE da instrução CREATE INDEX. Para determinar uma ordem efetiva para as colunas iguais, ordene-as com base em sua seletividade, listando as colunas mais seletivas primeiro (a mais à esquerda na lista de colunas).  
  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_db_missing_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys. dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys. dm_db_missing_index_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
  
