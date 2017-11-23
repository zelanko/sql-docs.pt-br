---
title: syspolicy_conditions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syspolicy_conditions
- syspolicy_conditions_TSQL
dev_langs: TSQL
helpviewer_keywords: syspolicy_conditions view
ms.assetid: af97d26c-4bd5-4b08-be51-8419e3b2832c
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a0628b0913358fd5fb80f3c36fbcf8e5a5c05170
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="syspolicyconditions-transact-sql"></a>syspolicy_conditions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe uma linha para cada condição do gerenciamento baseado em políticas na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. syspolicy_conditions pertence ao esquema dbo do banco de dados msdb. A tabela a seguir descreve as colunas na exibição syspolicy_conditions.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|condition_id|**int**|Identificador desta condição. Cada condição representa uma coleção de uma ou mais expressões de condição.|  
|name|**sysname**|O nome da condição.|  
|date_created|**datetime**|Data e hora em que a condição foi criada.|  
|descrição|**nvarchar(max)**|A descrição da condição. A coluna de descrição é opcional e pode ser NULL.|  
|created_by|**sysname**|Logon que criou a condição.|  
|modified_by|**sysname**|Logon que modificou a condição mais recentemente. É NULL se nunca foi modificada.|  
|date_modified|**datetime**|Data e hora em que a condição foi criada. É NULL se nunca foi modificada.|  
|is_name_condition|**smallint**|Especifica se a condição é uma condição de nomeação.<br /><br /> 0 = a expressão de condição não contém a variável @Name.<br /><br /> 1 = a expressão de condição contém a variável @Name.|  
|faceta|**nvarchar(max)**|Nome da faceta na qual a condição é baseada.|  
|Expressão|**nvarchar(max)**|A expressão dos estados da faceta.|  
|obj_name|**sysname**|O nome de objeto é atribuído a @Name quando a expressão de condição contém esta variável.|  
  
## <a name="remarks"></a>Comentários  
 Quando você estiver solucionando problemas de Gerenciamento Baseado em Políticas, consulte a exibição syspolicy_conditions para determinar quem criou e alterou pela última vez a condição.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
## <a name="see-also"></a>Consulte também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Exibições de Gerenciamento Baseado em Políticas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
