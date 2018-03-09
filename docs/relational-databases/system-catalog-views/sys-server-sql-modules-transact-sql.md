---
title: sys.server_sql_modules (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.server_sql_modules
- sys.server_sql_modules_TSQL
- server_sql_modules_TSQL
- server_sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_sql_modules catalog view
ms.assetid: 9ef9a8b9-c470-4a61-b0c4-ee24ad871d63
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2056568390fc8fa7ca7e03ee7df8ace39627ca5f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysserversqlmodules-transact-sql"></a>sys.server_sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém o conjunto de módulos SQL para gatilhos do nível do servidor de tipo TR. Você pode associar essa relação a sys.server_triggers. A tupla (object_id) é a chave da relação.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Esta é uma referência FOREIGN KEY ao gatilho no nível do servidor onde o módulo foi definido.|  
|**definição**|**nvarchar(max)**|Texto SQL que define esse módulo.<br /><br /> NULL = Criptografado.|  
|**uses_ansi_nulls**|**bit**|O módulo foi criado com a opção SET ANSI NULLS definida como ON.|  
|**uses_quoted_identifier**|**bit**|O módulo foi criado com a opção SET QUOTED IDENTIFIER definida como ON.|  
|**execute_as_principal_id**|**int**|A identificação do servidor principal EXECUTE AS.<br /><br /> NULL por padrão ou se EXECUTE AS CALLER<br /><br /> ID da entidade especificada se EXECUTE AS SELF EXECUTE AS entidade-2 = EXECUTE AS OWNER.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
