---
title: sp_change_agent_profile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_change_agent_profile
- sp_change_agent_profile_TSQL
helpviewer_keywords:
- sp_change_agent_profile
ms.assetid: e73acf8d-0be8-4197-ba11-fe798d0e2820
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1d4dedd9a7451daa97b3e1ad130f7f6dd95d8dd9
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823496"
---
# <a name="sp_change_agent_profile-transact-sql"></a>sp_change_agent_profile (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Altera um parâmetro de um perfil de agente de replicação armazenado no [MSagent_profiles &#40;tabela&#41;Transact-SQL](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) . Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_change_agent_profile [ @profile_id = ] profile_id   
        , [ @property = ] 'property'   
        , [ @value = ] 'value'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id`É a ID do perfil. *profile_id* é **int**, sem padrão.  
  
`[ @property = ] 'property'`É o nome da propriedade. a *Propriedade* é **sysname**, sem padrão.  
  
`[ @value = ] 'value'`É o novo valor da propriedade. o *valor* é **nvarchar (3000)**, sem padrão.  
  
 Essa tabela descreve as propriedades de perfil que podem ser alteradas.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**ndescrição**|Descrição do perfil.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_change_agent_profile** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_change_agent_profile**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_agent_profile](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_drop_agent_profile](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_agent_profile](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
