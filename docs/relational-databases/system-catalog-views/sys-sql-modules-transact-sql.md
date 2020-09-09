---
description: sys.sql_modules (Transact-SQL)
title: sys. sql_modules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/06/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fef38d2e060e8b9442a29fb83e821de0e93822b5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551355"
---
# <a name="syssql_modules-transact-sql"></a>sys.sql_modules (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna uma linha para cada objeto que é um módulo definido pela linguagem SQL no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , incluindo a função escalar definida pelo usuário e compilada nativamente. Objetos de tipo P, RF, V, TR, FN, IF, TF e R têm um módulo SQL associado. Padrões autônomos, objetos de tipo D, também têm uma definição de módulo SQL nessa exibição. Para obter uma descrição desses tipos, consulte a coluna **Type** na exibição do catálogo [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) .  
  
 Para obter mais informações, consulte [Funções escalares definidas pelo usuário para OLTP in-memory](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto contentor. É exclusivo em um banco de dados.|  
|**defini**|**nvarchar(max)**|Texto SQL que define esse módulo. Esse valor também pode ser obtido usando o [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) função interna.<br /><br /> NULL = Criptografado.|  
|**uses_ansi_nulls**|**bit**|O módulo foi criado com SET ANSI_NULLS ON.<br /><br /> Sempre será = 0 para regras e padrões.|  
|**uses_quoted_identifier**|**bit**|O módulo foi criado com SET QUOTED_IDENTIFIER ON.|  
|**is_schema_bound**|**bit**|O módulo foi criado com a opção SCHEMAbinding.<br /><br /> Sempre contém um valor de 1 para procedimentos armazenados compilados nativamente.|  
|**uses_database_collation**|**bit**|1 = A definição de módulo associada a esquema depende do agrupamento padrão do banco de dados para avaliação correta; caso contrário, 0. Essa dependência impede a alteração do agrupamento padrão do banco de dados.|  
|**is_recompiled**|**bit**|O procedimento foi criado com a opção recompile.|  
|**null_on_null_input**|**bit**|O módulo foi declarado para produzir uma saída NULL em qualquer entrada NULL.|  
|**execute_as_principal_id**|**Int**|A identificação do principal de banco de dados EXECUTE AS.<br /><br /> NULL por padrão ou se EXECUTE AS CALLER.<br /><br /> ID da entidade de segurança especificada se executar como SELF ou EXECUTE AS \<principal> .<br /><br /> -2 = EXECUTE AS OWNER.|  
|**uses_native_compilation**|**bit**|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].<br /><br /> 0 = não compilado originalmente<br /><br /> 1 = é compilado originalmente<br /><br /> O valor padrão é 0.|  
|**is_inlineable**|**bit**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssqlv15-md.md)] e posterior.<br/><br />Indica se o módulo é inlineável ou não. A inlineização se baseia nas condições especificadas [aqui](../user-defined-functions/scalar-udf-inlining.md#inlineable-scalar-udfs-requirements).<br /><br /> 0 = não embutido<br /><br /> 1 = é inlineável. <br /><br /> Para UDFs escalares, o valor será 1 se o UDF for inlineável e 0 caso contrário. Ele sempre contém um valor de 1 para TVFs embutido e 0 para todos os outros tipos de módulo.<br />|  
|**inline_type**|**bit**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssqlv15-md.md)] e posterior.<br /><br />Indica se a inalinhamento está ativada para o módulo no momento. <br /><br />0 = a inalinhamento está desativada<br /><br /> 1 = a inalinhamento está ativada.<br /><br /> Para UDFs escalares, o valor será 1 se o inlining estiver ativado (explicitamente ou implicitamente). O valor sempre será 1 para TVFs embutidos e 0 para outros tipos de módulo.<br />|  

  
## <a name="remarks"></a>Comentários  
 A expressão SQL para uma restrição padrão, objeto do tipo D, é encontrada na exibição de catálogo [Sys. default_constraints](../../relational-databases/system-catalog-views/sys-default-constraints-transact-sql.md) . A expressão SQL para uma restrição de verificação, objeto do tipo C, é encontrada na exibição de catálogo [Sys. check_constraints](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md) .  
  
 Essas informações também são descritas em [Sys. dm_db_uncontained_entities &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md).  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes sobre o catálogo do sistema SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
