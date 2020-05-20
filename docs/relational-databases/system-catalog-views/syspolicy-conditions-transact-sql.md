---
title: syspolicy_conditions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_conditions
- syspolicy_conditions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_conditions view
ms.assetid: af97d26c-4bd5-4b08-be51-8419e3b2832c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2f047007397eb302859f80bb5efe4b106a33ae61
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833800"
---
# <a name="syspolicy_conditions-transact-sql"></a>syspolicy_conditions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe uma linha para cada condição de gerenciamento baseado em políticas na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . syspolicy_conditions pertence ao esquema dbo no banco de dados msdb. A tabela a seguir descreve as colunas na exibição syspolicy_conditions.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|condition_id|**int**|Identificador desta condição. Cada condição representa uma coleção de uma ou mais expressões de condição.|  
|Nome|**sysname**|O nome da condição.|  
|date_created|**datetime**|Data e hora em que a condição foi criada.|  
|descrição|**nvarchar(max)**|A descrição da condição. A coluna de descrição é opcional e pode ser NULL.|  
|created_by|**sysname**|Logon que criou a condição.|  
|modified_by|**sysname**|Logon que modificou a condição mais recentemente. É NULL se nunca foi modificada.|  
|date_modified|**datetime**|Data e hora em que a condição foi criada. É NULL se nunca foi modificada.|  
|is_name_condition|**smallint**|Especifica se a condição é uma condição de nomeação.<br /><br /> 0 = a expressão de condição não contém a variável @Name.<br /><br /> 1 = a expressão de condição contém a variável @Name.|  
|faceta|**nvarchar(max)**|Nome da faceta na qual a condição é baseada.|  
|Expression|**nvarchar(max)**|A expressão dos estados da faceta.|  
|obj_name|**sysname**|O nome de objeto é atribuído a @Name quando a expressão de condição contém esta variável.|  
  
## <a name="remarks"></a>Comentários  
 Quando você estiver solucionando problemas de Gerenciamento Baseado em Políticas, consulte a exibição syspolicy_conditions para determinar quem criou e alterou pela última vez a condição.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
## <a name="see-also"></a>Consulte Também  
 [Administrar servidores usando o gerenciamento baseado em políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Exibições de Gerenciamento Baseado em Políticas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
