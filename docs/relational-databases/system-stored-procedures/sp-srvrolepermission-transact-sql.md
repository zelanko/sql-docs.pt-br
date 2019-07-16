---
title: sp_srvrolepermission (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_srvrolepermission_TSQL
- sp_srvrolepermission
dev_langs:
- TSQL
helpviewer_keywords:
- sp_srvrolepermission
ms.assetid: 5709667f-e3e4-48a2-93ec-af5e22a2ac58
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6613c4e94ce8c802e45fe003ac73e51b3f38072b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032814"
---
# <a name="spsrvrolepermission-transact-sql"></a>sp_srvrolepermission (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe as permissões de uma função de servidor fixa.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_srvrolepermission [ [ @srvrolename = ] 'role']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @srvrolename = ] 'role'` É o nome da função de servidor fixa para a qual são retornadas permissões. *função* está **sysname**, com um padrão NULL. Se nenhuma função for especificada, as permissões de todas as funções de servidor fixas serão retornadas. *função* pode ter um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**sysadmin**|Administradores de sistema|  
|**securityadmin**|Administradores de segurança|  
|**serveradmin**|Administradores de servidor|  
|**setupadmin**|Administradores de configuração|  
|**processadmin**|Administradores de processo|  
|**diskadmin**|Administradores de disco|  
|**dbcreator**|Criadores de banco de dados|  
|**bulkadmin**|Pode executar instruções BULK INSERT|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**ServerRole**|**sysname**|Nome de uma função de servidor fixa|  
|**Permissão**|**sysname**|Permissão associada **ServerRole**|  
  
## <a name="remarks"></a>Comentários  
 As permissões listadas incluem as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem ser executadas e outras atividades especiais que podem ser realizadas por membros da função de servidor fixa. Para exibir uma lista de funções de servidor fixas, execute **sp_helpsrvrole**.  
  
 O **sysadmin** função de servidor fixa tem as permissões de todas as outras funções de servidor fixa.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir retorna as permissões associadas à função de servidor fixa `sysadmin`.  
  
```  
EXEC sp_srvrolepermission 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpsrvrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
