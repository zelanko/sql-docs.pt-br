---
title: sys. CHECK_CONSTRAINTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.check_constraints
- sys.check_constraints_TSQL
- check_constraints_TSQL
- check_constraints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.check_constraints catalog view
ms.assetid: 940ebc5e-44ba-4dae-8b29-da94f2d1d6c4
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 43ccc527143be26d4cee4d2e4ce55e8fb37d3abb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="syscheckconstraints-transact-sql"></a>sys.check_constraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contém uma linha para cada objeto que é uma restrição de verificação com **sys.objects.type** = 'c'.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**\<Colunas herdadas de sys. Objects >**||Para obter uma lista de colunas que essa exibição herda valores, consulte [sys. Objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**is_disabled**|**bit**|A restrição CHECK está desabilitada.|  
|**is_not_for_replication**|**bit**|A restrição CHECK foi criada com a opção NOT FOR REPLICATION.|  
|**is_not_trusted**|**bit**|A restrição CHECK não foi verificada pelo sistema para todas as linhas.|  
|**parent_column_id**|**Int**|0 indica uma restrição CHECK do nível da tabela.<br /><br /> O valor diferente de zero indica que esta é uma restrição CHECK em nível de coluna definida na coluna com o valor de ID especificado.|  
|**Definição**|**nvarchar(max)**|Expressão SQL que define esta restrição CHECK.|  
|**uses_database_collation**|**bit**|1 = A definição de restrição depende do agrupamento padrão do banco de dados para avaliação correta; caso contrário, 0. Tal dependência impede a alteração do agrupamento padrão do banco de dados.|  
|**is_system_named**|**bit**|1 = O nome foi gerado pelo sistema.<br /><br /> 0 = O nome foi fornecido pelo usuário.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
