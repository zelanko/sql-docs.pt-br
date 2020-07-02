---
title: sys. plan_guides (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.planguides_TSQL
- plan_guides
- sys.planguides
- plan_guides_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.plan_guides catalog view
ms.assetid: 3dde0397-ef6f-4b3f-8250-3f25584eb62b
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 390b7d0c1fd34827580562b16074028465cb8ae3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85678414"
---
# <a name="sysplan_guides-transact-sql"></a>sys.plan_guides (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Contém uma linha para cada guia de plano no banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**plan_guide_id**|**int**|Identificador exclusivo do guia de plano no banco de dados.|  
|**name**|**sysname**|Nome do guia de plano.|  
|**create_date**|**datetime**|Date e hora de criação do guia de plano.|  
|**modify_date**|**Horário**|Data da última modificação do guia de plano.|  
|**is_disabled**|**bit**|1 = Guia de plano desabilitado.<br /><br /> 0 = Guia de plano habilitado.|  
|**query_text**|**nvarchar(max)**|Texto da consulta na qual o guia de plano é criado.|  
|**scope_type**|**tinyint**|Identifica o escopo do guia de plano.<br /><br /> 1 = OBJECT<br /><br /> 2 = SQL<br /><br /> 3 = TEMPLATE|  
|**scope_type_desc**|**nvarchar(60)**|Descrição do escopo do guia de plano.<br /><br /> OBJECT<br /><br /> SQL<br /><br /> TEMPLATE|  
|**scope_object_id**|**Int**|object_id do objeto que definirá o escopo do guia de plano se o escopo for OBJECT.<br /><br /> NULL se o guia de plano não tiver nenhum escopo para OBJECT.|  
|**scope_batch**|**nvarchar(max)**|Texto em lotes, se **scope_type** for SQL.<br /><br /> NULL se tipo de lote não for SQL.<br /><br /> Se NULL e **scope_type** for SQL, o valor de **query_text** se aplicará.|  
|**parameters**|**nvarchar(max)**|A cadeia de caracteres que define a lista de parâmetros associada ao guia de plano.<br /><br /> NULL = Nenhuma lista de parâmetros está associada ao guia de plano.|  
|**raízes**|**nvarchar(max)**|Dicas da cláusula OPTION associadas ao guia de plano.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
  
