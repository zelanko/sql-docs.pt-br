---
title: sp_help_operator (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_operator
- sp_help_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_operator
ms.assetid: caedc43d-44b8-415a-897e-92923f6de3b8
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc89c5f6689b64aea7be0410850f373d75d876e6
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sphelpoperator-transact-sql"></a>sp_help_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Relata informações sobre os operadores definidos para o servidor.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_operator  
     { [ @operator_name = ] 'operator_name'   
     | [ @operator_id = ] operator_id }  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@operator_name=** ] **'***operator_name***'**  
 O nome do operador. *operator_name* é **sysname**. Se *operator_name* não é especificado, serão retornadas informações sobre todos os operadores.  
  
 [ **@operator_id=** ] *operator_id*  
 O número de identificação do operador para o qual as informações são solicitadas. *operator_id*é **int**, com um padrão NULL.  
  
> [!NOTE]  
>  O *operator_id* ou *operator_name* devem ser especificados, mas não é possível especificar ambos.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**id**|**Int**|Número de identificação do operador.|  
|**name**|**sysname**|Nome do operador.|  
|**enabled**|**tinyint**|Operador está disponível para receber qualquer notificação:<br /><br /> **1** = Sim<br /><br /> **0** = No|  
|**email_address**|**nvarchar(100)**|Endereço de email do operador.|  
|**last_email_date**|**Int**|Data em que o operador foi notificado pela última vez por email.|  
|**last_email_time**|**Int**|Hora em que o operador foi notificado pela última vez por email.|  
|**pager_address**|**nvarchar(100)**|Endereço de pager do operador.|  
|**last_pager_date**|**Int**|Data em que o operador foi notificado pela última vez por pager.|  
|**last_pager_time**|**Int**|Hora em que o operador foi notificado pela última vez por pager.|  
|**weekday_pager_start_time**|**Int**|O início do período durante o qual o operador está disponível para receber notificações de pager em um dia da semana.|  
|**weekday_pager_end_time**|**Int**|O fim do período durante o qual o operador está disponível para receber notificações de pager em um dia da semana.|  
|**saturday_pager_start_time**|**Int**|O início do período durante o qual o operador está disponível para receber notificações de pager aos sábados.|  
|**saturday_pager_end_time**|**Int**|O fim do período durante o qual o operador está disponível para receber notificações de pager aos sábados.|  
|**sunday_pager_start_time**|**Int**|O início do período durante o qual o operador está disponível para receber notificações de pager aos domingos.|  
|**sunday_pager_end_time**|**Int**|O fim do período durante o qual o operador está disponível para receber notificações de pager aos domingos.|  
|**pager_days**|**tinyint**|Um bitmask (**1** = domingo, **64** = sábado) de dias da semana indicando quando o operador está disponível para receber notificações por pager.|  
|**netsend_address**|**nvarchar(100)**|Endereço de operador para notificações pop-up de rede.|  
|**last_netsend_date**|**Int**|Data em que o operador foi notificado pela última vez por pop-up de rede.|  
|**last_netsend_time**|**Int**|Hora em que o operador foi notificado pela última vez por pop-up de rede.|  
|**category_name**|**sysname**|Nome da categoria de operador ao qual esse operador pertence.|  
  
## <a name="remarks"></a>Remarks  
 **sp_help_operator** deve ser executado a partir de **msdb** banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir relata informações sobre o operador `François Ajenstat`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_operator  
    @operator_name = N'François Ajenstat' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_update_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
