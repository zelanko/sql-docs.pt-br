---
title: sys. edge_constraints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.edge_constraints
- edge_constraints
- SQL Graph
- edge_constraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.edge_constraints catalog view
ms.assetid: 0f782d2f-7126-46ab-85b7-bcba44862231
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6b05b73b3de7cc9707a89830d56bb54f1dc33c6f
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919722"
---
# <a name="sysedge_constraints-transact-sql"></a>sys. edge_constraints (Transact-SQL)
[!INCLUDE[sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

Contém uma linha para cada objeto que é uma restrição de borda. 
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||Para obter uma lista de colunas que essa exibição herda, consulte [Sys. objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**is_disabled**|**bit**|1 = a restrição de borda é disbled.<br /><br /> 0 = a restrição de borda está habilitada.|  
|**is_not_trusted**|**bit**|1 = a restrição de borda não foi verificada pelo sistema.<br /><br /> 0 = a restrição de borda foi verificada pelo sistema.|  
|**delete_referential_action**|**tinyint**|Ação referencial que foi definida nesta restrição de borda.<br /><br />0 = nenhuma ação.|  
|**delete_referential_action_desc**|**nvarchar(60)**|Descrição da ação referencial que foi definida nesta restrição de borda.<br /><br />NO_ACTION|  
|**is_system_named**|**bit**|1 = o nome da restrição de borda foi gerado pelo sistema.<br /><br />0 = o nome da restrição de borda foi fornecido pelo usuário.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
