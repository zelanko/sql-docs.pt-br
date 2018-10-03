---
title: syspolicy_policies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policies_TSQL
- syspolicy_policies
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policies view
ms.assetid: aecf35bb-187e-4f80-870f-48081b88974e
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: aec3b91a52667e0ef0801bd2532689e39ebf9ccb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845144"
---
# <a name="syspolicypolicies-transact-sql"></a>syspolicy_policies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe uma linha para cada política de gerenciamento baseado em políticas na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. syspolicy_policies pertence ao esquema dbo do banco de dados msdb. A tabela a seguir descreve as colunas na exibição syspolicy_policies.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|policy_id|**int**|Identificador da política.|  
|nome|**sysname**|O nome da política.|  
|condition_id|**int**|ID da condição imposta ou testada por esta política.|  
|root_condition_id|**int**|Somente para uso interno.|  
|date_created|**datetime**|Data e hora em que a política foi criada.|  
|execution_mode|**int**|Modo de avaliação para a política. Os valores possíveis são os seguintes:<br /><br /> 0 = Sob demanda<br /><br /> Este modo avalia a política quando especificado diretamente pelo usuário.<br /><br /> 1 = Ao alterar: impedir<br /><br /> Esse modo automatizado usa gatilhos DDL para impedir violações de política.<br /><br /> 2 = Ao alterar: log apenas<br /><br /> Este modo automatizado usa notificação de eventos para avaliar uma política quando ocorre uma alteração relevante e registra em log as violações de política.<br /><br /> 4 = Ao agendar<br /><br /> Este modo automatizado usa um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para avaliar periodicamente uma política. O modo registra as violações de política.<br /><br /> Observação: O valor 3 não é um valor possível.|  
|policy_category|**int**|A ID da categoria das políticas do Gerenciamento Baseado em Políticas ao qual esta política pertence. Será NULL se for o grupo de políticas padrão.|  
|schedule_uid|**uniqueidentifier**|Quando o execution_mode for Ao agendar, contém a ID da agenda; caso contrário, será NULL.|  
|descrição|**nvarchar(max)**|A descrição da política. A coluna de descrição é opcional e pode ser NULL.|  
|help_text|**nvarchar(4000)**|O texto de hiperlink que pertence a help_link.|  
|help_link|**nvarchar(2083)**|O hiperlink de ajuda adicional atribuído à política pelo criador da política.|  
|object_set_id|**int**|ID do conjunto de objetos que a política avalia.|  
|is_enabled|**bit**|Indica se a política está habilitada (1) ou desabilita (0) atualmente.|  
|job_id|**uniqueidentifier**|Quando o execution_mode está como Ao agendar, contém a ID de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que executa a política.|  
|created_by|**sysname**|Logon que criou a política.|  
|modified_by|**sysname**|Logon que modificou mais recentemente a política. É NULL se nunca foi modificada.|  
|date_modified|**datetime**|Data e hora em que a política foi criada. É NULL se nunca foi modificada.|  
  
## <a name="remarks"></a>Comentários  
 Quando você estiver solucionando problemas de gerenciamento baseado em políticas, consulte o [syspolicy_conditions](../../relational-databases/system-catalog-views/syspolicy-conditions-transact-sql.md) exibição para determinar se a política está habilitada. Essa exibição também indica quem criou ou alterou mais recentemente a política.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
## <a name="see-also"></a>Consulte também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Exibições de Gerenciamento Baseado em Políticas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
