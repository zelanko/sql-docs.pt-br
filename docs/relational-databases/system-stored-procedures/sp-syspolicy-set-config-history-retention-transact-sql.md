---
title: sp_syspolicy_set_config_history_retention (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_set_config_history_retention_TSQL
- sp_syspolicy_set_config_history_retention
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_set_config_history_retention
ms.assetid: 2574898a-e724-4447-b96c-ff778471339d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 49c45013b02bd6c1e6a49d229d6c9be6ad635964
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752752"
---
# <a name="sp_syspolicy_set_config_history_retention-transact-sql"></a>sp_syspolicy_set_config_history_retention (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Especifica o número de dias durante os quais manter o histórico de avaliação de políticas para o Gerenciamento Baseado em Políticas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syspolicy_set_config_history_retention [ @value = ] value  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @value = ] value`É o número de dias para reter o histórico do gerenciamento baseado em políticas. o *valor* é **sqlvariant**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Você deve executar sp_syspolicy_set_config_history_retention no contexto do banco de dados de sistema msdb.  
  
 Se *Value* for definido como 0, o histórico não será removido automaticamente.  
  
 Para exibir o valor atual de retenção de histórico, execute a consulta a seguir:  
  
```  
SELECT current_value FROM msdb.dbo.syspolicy_configuration  
WHERE name = 'HistoryRetentionInDays'  
```  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de banco de dados fixa PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Possível elevação de credenciais: os usuários na função PolicyAdministratorRole podem criar gatilhos de servidor e agendar execuções de políticas que possam afetar a operação da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por exemplo, os usuários da função PolicyAdministratorRole podem criar uma política que impeça a criação da maioria dos objetos no [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Devido a essa possível elevação de credenciais, a função PolicyAdministratorRole deve ser concedida somente a usuários que são confiáveis com o controle da configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir define a retenção do histórico de avaliação de política como 28 dias.  
  
```  
EXEC msdb.dbo.sp_syspolicy_set_config_history_retention @value = 28;  
  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do gerenciamento baseado em políticas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_syspolicy_configure](../../relational-databases/system-stored-procedures/sp-syspolicy-configure-transact-sql.md)  
  
  
