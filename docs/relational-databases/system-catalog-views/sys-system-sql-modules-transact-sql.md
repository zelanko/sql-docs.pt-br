---
title: sys. system_sql_modules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- system_sql_modules_TSQL
- sys.system_sql_modules
- sys.system_sql_modules_TSQL
- system_sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_sql_modules catalog view
ms.assetid: ad3548bc-4780-4821-b962-b421d52daed9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 349abe5ccc5fb36ee6c3568e97163e6eb665f633
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47594660"
---
# <a name="syssystemsqlmodules-transact-sql"></a>sys.system_sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha por objeto de sistema que contém um módulo definido em linguagem SQL. Objetos de sistema do tipo FN, IF, P, PC, TF, V têm um módulo SQL associado. Para identificar o objeto recipiente, você pode unir esta exibição à [sys. system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Número de identificação de objeto do objeto recipiente, exclusivo no banco de dados.|  
|**Definição**|**nvarchar(max)**|Texto SQL que define esse módulo.|  
|**uses_ansi_nulls**|**bit**|1 = O módulo foi criado com a opção de banco de dados SET ANSI_NULLS definida como ON.<br /><br /> Sempre retorna 1.|  
|**uses_quoted_identifier**|**bit**|1 = O módulo foi criado com SET QUOTED_IDENTIFIER como ON.<br /><br /> Sempre retorna 1.|  
|**is_schema_bound**|**bit**|0 = O módulo não foi criado com a opção SCHEMABINDING.<br /><br /> Sempre retorna 0.|  
|**uses_database_collation**|**bit**|0 = O módulo não depende do agrupamento padrão do banco de dados.<br /><br /> Sempre retorna 0.|  
|**is_recompiled**|**bit**|0 = O procedimento não foi criado com o uso da opção WITH RECOMPILE.<br /><br /> Sempre retorna 0.|  
|**null_on_null_input**|**bit**|0 = O módulo não foi criado para produzir uma saída NULL em nenhuma entrada NULL.<br /><br /> Sempre retorna 0.|  
|**execute_as_principal_id**|**int**|Sempre retorna NULL.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.all_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-sql-modules-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições do catálogo do objeto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
