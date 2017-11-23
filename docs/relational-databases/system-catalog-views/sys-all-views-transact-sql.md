---
title: all_views (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.all_views_TSQL
- sys.all_views
- all_views
- all_views_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.all_views catalog view
ms.assetid: d8829213-fce2-41c6-9ab2-aaab5836c941
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7cd9b1ea568222bc0309048d6c785833f03f14b7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysallviews-transact-sql"></a>sys.all_views (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Mostra o UNION de todas as exibições definidas pelo usuário e de sistema.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**\<herdado colunas >**||Para obter uma lista de colunas que essa exibição herda valores, consulte [sys. Objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**is_replicated**|**bit**|1 = A exibição é replicada.|  
|**has_replication_filter**|**bit**|1 = A exibição tem um filtro de replicação.|  
|**has_opaque_metadata**|**bit**|1 = A opção VIEW_METADATA especificada para exibição. Para obter mais informações, veja [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).|  
|**has_unchecked_assembly_data**|**bit**|1 = A tabela contém dados persistentes que dependem de um assembly cuja definição foi alterada durante o último ALTER ASSEMBLY. Será redefinido como 0 depois do próximo DBCC CHECKDB ou DBCC CHECKTABLE bem-sucedido.|  
|**with_check_option**|**bit**|1 = WITH CHECK OPTION foi especificado na definição de exibição.|  
|**is_date_correlation_view**|**bit**|1 = A exibição foi criada automaticamente pelo sistema para armazenar informações de correlação entre colunas de data e hora. A criação dessa exibição foi habilitada ao definir DATE_CORRELATION_OPTIMIZATION como **ON**.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [ALTER ASSEMBLY &#40; Transact-SQL &#41;](../../t-sql/statements/alter-assembly-transact-sql.md)   
 [DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)  
  
  
