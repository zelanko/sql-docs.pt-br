---
title: sys. sql_modules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sql_modules_TSQL
- sql_modules
- sql_modules_TSQL
- sys.sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_modules catalog view
ms.assetid: 23d3ccd2-f356-4d89-a2cd-bee381243f99
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: af128c6c3b28c448111f49adf55c66c12ab4bbae
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33222087"
---
# <a name="syssqlmodules-transact-sql"></a>sys.sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada objeto que é um módulo de definido em linguagem SQL no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluindo nativamente compilado função escalar definida pelo usuário. Objetos de tipo P, RF, V, TR, FN, IF, TF e R têm um módulo SQL associado. Padrões autônomos, objetos de tipo D, também têm uma definição de módulo SQL nessa exibição. Para obter uma descrição desses tipos, consulte o **tipo** coluna o [sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) exibição do catálogo.  
  
 Para obter mais informações, consulte [Funções escalares definidas pelo usuário para OLTP in-memory](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**Int**|ID do objeto contentor. É exclusivo em um banco de dados.|  
|**Definição**|**nvarchar(max)**|Texto SQL que define esse módulo. Esse valor também pode ser obtido usando o [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) função interna.<br /><br /> NULL = Criptografado.|  
|**uses_ansi_nulls**|**bit**|O módulo foi criado com SET ANSI_NULLS ON.<br /><br /> Sempre será = 0 para regras e padrões.|  
|**uses_quoted_identifier**|**bit**|O módulo foi criado com SET QUOTED_IDENTIFIER ON.|  
|**is_schema_bound**|**bit**|O módulo foi criado com a opção SCHEMABINDING.<br /><br /> Sempre contém um valor de 1 para procedimentos armazenados compilados nativamente.|  
|**uses_database_collation**|**bit**|1 = A definição de módulo associada a esquema depende do agrupamento padrão do banco de dados para avaliação correta; caso contrário, 0. Tal dependência impede a alteração de agrupamento do banco de dados.|  
|**is_recompiled**|**bit**|Procedimento foi criado a opção WITH RECOMPILE.|  
|**null_on_null_input**|**bit**|O módulo foi declarado para produzir uma saída NULL em qualquer entrada NULL.|  
|**execute_as_principal_id**|**Int**|A identificação do principal de banco de dados EXECUTE AS.<br /><br /> NULL por padrão ou se EXECUTE AS CALLER.<br /><br /> ID da entidade especificada se EXECUTE AS SELF ou EXECUTE AS \<principal >.<br /><br /> -2 = EXECUTE AS OWNER.|  
|**uses_native_compilation**|**bit**|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].<br /><br /> 0 = não compilado originalmente<br /><br /> 1 = é compilado originalmente<br /><br /> O valor padrão é 0.|  
  
## <a name="remarks"></a>Remarks  
 A expressão SQL para uma restrição padrão, o objeto de tipo D, é encontrada na [default_constraints](../../relational-databases/system-catalog-views/sys-default-constraints-transact-sql.md) exibição do catálogo. A expressão SQL para uma restrição de verificação, o objeto do tipo C, é encontrada na [sys. CHECK_CONSTRAINTS](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md) exibição do catálogo.  
  
 Essa informação também está descrita em [sys.DM db_uncontained_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o nome, o tipo e a definição de cada módulo no banco de dados atual.  
  
```  
SELECT sm.object_id, OBJECT_NAME(sm.object_id) AS object_name, o.type, o.type_desc, sm.definition  
FROM sys.sql_modules AS sm  
JOIN sys.objects AS o ON sm.object_id = o.object_id  
ORDER BY o.type;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Consultando o catálogo de sistema do SQL Server perguntas Frequentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [OLTP na memória &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
