---
title: sys. all_sql_modules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- all_sql_modules_TSQL
- sys.all_sql_modules
- all_sql_modules
- sys.all_sql_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_sql_modules catalog view
ms.assetid: 7477a3fe-afb3-44c8-bb2c-c6e1d9bdee6f
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6b21f7e2bbed731e29334be1a87f5089ccfc1145
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73981847"
---
# <a name="sysall_sql_modules-transact-sql"></a>sys.all_sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna a União de **Sys. sql_modules** e **Sys. system_sql_modules**.  
  
 A exibição retorna uma linha para cada função escalar definida pelo usuário compilada nativamente. Para obter mais informações, consulte [Funções escalares definidas pelo usuário para OLTP in-memory](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto contentor. É exclusivo em um banco de dados.|  
|**defini**|**nvarchar(max)**|Texto SQL que define esse módulo.<br /><br /> NULL = Criptografado|  
|**uses_ansi_nulls**|**bit**|O módulo foi criado com SET ANSI_NULLS ON.|  
|**uses_quoted_identifier**|**bit**|O módulo foi criado com SET QUOTED_IDENTIFIER ON.|  
|**is_schema_bound**|**bit**|O módulo foi criado com a opção SCHEMABINDING.|  
|**uses_database_collation**|**bit**|1 = A definição de módulo associada a esquema depende do agrupamento padrão do banco de dados para avaliação correta; caso contrário, 0. Essa dependência impede a alteração da ordenação padrão do banco de dados.|  
|**is_recompiled**|**bit**|O procedimento foi criado com a opção WITH RECOMPILE.|  
|**null_on_null_input**|**bit**|O módulo foi declarado para produzir uma saída NULL em qualquer entrada NULL.|  
|**execute_as_principal_id**|**int**|A identificação do principal de banco de dados EXECUTE AS.<br /><br /> NULL por padrão ou se EXECUTE AS CALLER.<br /><br /> ID da entidade de segurança especificada se executar como SELF ou EXECUTE \<as> principal.<br /><br /> -2 = EXECUTE AS OWNER.|  
|**uses_native_compilation**|bit|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> 0 = não compilado originalmente<br /><br /> 1 = é compilado originalmente<br /><br /> O valor padrão é 0.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]Para obter mais informações, consulte [configuração de visibilidade de metadados](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys. system_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-sql-modules-transact-sql.md)   
 [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
