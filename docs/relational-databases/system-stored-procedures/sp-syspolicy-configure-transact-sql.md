---
title: sp_syspolicy_configure (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_configure
- sp_syspolicy_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_configure
ms.assetid: 70c10922-9345-4190-ba69-808a43f760da
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: b9ae7fdde89c9f927fbc56a9ca395138c264e931
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63001412"
---
# <a name="spsyspolicyconfigure-transact-sql"></a>sp_syspolicy_configure (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define configurações de Gerenciamento Baseado em Políticas, como, por exemplo, se o Gerenciamento Baseado em Políticas é habilitado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syspolicy_configure [ @name = ] 'name'  
    , [ @value = ] value  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'` É o nome da configuração que você deseja configurar. *nome da* está **sysname**, é necessário e não pode ser nulo ou uma cadeia de caracteres vazia.  
  
 *nome* pode ser qualquer um dos seguintes valores:  
  
-   'Enabled' - Determina se o Gerenciamento Baseado em Políticas é habilitado.  
  
-   'HistoryRetentionInDays' - Especifica o número de dias que o histórico de avaliação de política deve ser mantido. Se definido com 0, o histórico não será removido automaticamente.  
  
-   'LogOnSuccess' - Especifica se o Gerenciamento Baseado em Políticas registra em log avaliações de política com êxito.  
  
`[ @value = ] value` É o valor que está associado com o valor especificado para *nome*. *valor* está **sql_variant**e é necessária.  
  
-   Se você especificar 'Enabled' para *nome*, você pode usar qualquer um dos seguintes valores:  
  
    -   0 = Desabilita o Gerenciamento Baseado em Políticas.  
  
    -   1 = Habilita o Gerenciamento Baseado em Políticas.  
  
-   Se você especificar 'HistoryRententionInDays' para *nome*, especifique o número de dias como um valor inteiro.  
  
-   Se você especificar 'LogOnSuccess' para *nome*, você pode usar qualquer um dos seguintes valores:  
  
    -   0 = Registra em log somente as avaliações de política com falha.  
  
    -   1 = Registra em log as avaliações de política com êxito e com falha.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Você deve executar sp_syspolicy_configure no contexto do banco de dados de sistema msdb.  
  
 Para exibir os valores atuais dessas configurações, consulte a exibição do sistema msdb.dbo.syspolicy_configuration.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de banco de dados fixa PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Possível elevação de credenciais: Os usuários na função PolicyAdministratorRole podem criar gatilhos de servidor e agendar execuções de políticas que podem afetar a operação da instância da [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por exemplo, os usuários da função PolicyAdministratorRole podem criar uma política que impeça a criação da maioria dos objetos no [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Devido a essa possível elevação de credenciais, a função PolicyAdministratorRole deve ser concedida somente para usuários que sejam confiáveis no controle da configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir habilita o Gerenciamento Baseado em Políticas.  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'Enabled'  
, @value = 1;  
  
GO  
```  
  
 O exemplo seguinte define a retenção de histórico de política em 14 dias.  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'HistoryRetentionInDays'  
, @value = 14;  
  
GO  
```  
  
 O exemplo seguinte configura Gerenciamento Baseado em Políticas para registrar em log as avaliações de política com êxito e com falha.  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'LogOnSuccess'  
, @value = 1;  
  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de gerenciamento baseado em políticas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_set_config_enabled &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-enabled-transact-sql.md)   
 [sp_syspolicy_set_config_history_retention &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-history-retention-transact-sql.md)   
 [sp_syspolicy_set_log_on_success &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-log-on-success-transact-sql.md)  
  
  
