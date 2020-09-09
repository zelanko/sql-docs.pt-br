---
description: sys.dm_db_missing_index_groups (Transact-SQL)
title: sys. dm_db_missing_index_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_groups
- sys.dm_db_missing_index_groups_TSQL
- dm_db_missing_index_groups
- dm_db_missing_index_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_groups dynamic management view
- missing indexes feature [SQL Server], sys.dm_db_missing_index_groups dynamic management view
ms.assetid: 9cc00acd-d83d-49f8-be72-5b2aebed246b
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 79c1cb3bf387af73e1505b8452cd44a1a5f55675
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542268"
---
# <a name="sysdm_db_missing_index_groups-transact-sql"></a>sys.dm_db_missing_index_groups (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Essa DMV retorna informações sobre índices ausentes em um grupo de índice específico, exceto os índices espaciais. 
  
 No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, todas as linhas que contêm dados que não pertencem ao locatário conectado serão filtradas.  
   
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**index_group_handle**|**int**|Identifica um grupo de índice ausente.|  
|**index_handle**|**int**|Identifica um índice ausente que pertence ao grupo especificado por **index_group_handle**.<br /><br /> Um grupo de índice contém apenas um índice.|  
  
## <a name="remarks"></a>Comentários  
 As informações retornadas por **sys.dm_db_missing_index_groups** serão atualizadas quando uma consulta for otimizada pelo otimizador de consulta e não persistirão. As informações do índice ausente são mantidas apenas até o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ser reiniciado. Os administradores de banco de dados devem periodicamente gerar cópias de backup de informações de índice ausente se quiserem mantê-las após o desligamento e a reinicialização do servidor.  
  
 Nenhuma coluna do conjunto de resultados de saída é uma chave, mas juntos eles formam uma chave de índice.  

  >[!NOTE]
  >O conjunto de resultados para essa DMV é limitado a 600 linhas. Cada linha contém um índice ausente. Se você tiver mais de 600 índices ausentes, você deverá resolver os índices ausentes existentes para que possa exibir os mais recentes.
  
## <a name="permissions"></a>Permissões  
 Para consultar essa exibição de gerenciamento dinâmico, os usuários devem receber a permissão VIEW SERVER STATE ou qualquer permissão que implique essa permissão.  
  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_db_missing_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys. dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys. dm_db_missing_index_group_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
