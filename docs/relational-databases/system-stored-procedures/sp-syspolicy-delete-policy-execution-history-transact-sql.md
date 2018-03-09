---
title: sp_syspolicy_delete_policy_execution_history (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- sp_syspolicy_delete_policy_execution_history
- sp_syspolicy_delete_policy_execution_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_delete_policy_execution_history
ms.assetid: fe651af9-267e-45ec-b4e7-4b0698fb1be3
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c505a71c0906e46719f92959c61858af5cacec8a
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="spsyspolicydeletepolicyexecutionhistory-transact-sql"></a>sp_syspolicy_delete_policy_execution_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exclui o histórico de execução de políticas no Gerenciamento Baseado em Políticas. Você pode usar este procedimento armazenado para excluir o histórico de execução de uma política específica ou de todas as políticas e excluir o histórico de execução antes de uma data específica.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syspolicy_delete_policy_execution_history [ @policy_id = ] policy_id ]  
    [ , [ @oldest_date = ] 'oldest_date' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@policy_id=** ] *policy_id*  
 É o identificador da política cujo histórico de execução você deseja excluir. *policy_id* é **int**e é necessário. Pode ser NULL.  
  
 [ **@oldest_date=** ] **'***oldest_date***'**  
 É a data mais antiga para a qual você deseja manter o histórico de execução de política. Qualquer histórico de execução anterior a essa data será excluído. *oldest_date* é **datetime**e é necessário. Pode ser NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 Você deve executar sp_syspolicy_delete_policy_execution_history no contexto do banco de dados de sistema msdb.  
  
 Para obter valores *policy_id*, e para exibir as datas de histórico de execução, você pode usar a consulta a seguir:  
  
```  
SELECT a.name AS N'policy_name', b.policy_id, b.start_date, b.end_date  
FROM msdb.dbo.syspolicy_policies AS a   
INNER JOIN msdb.dbo.syspolicy_policy_execution_history AS b  
ON a.policy_id = b.policy_id  
```  
  
 O comportamento a seguir será aplicado se você especificar NULL para obter um ou ambos valores:  
  
-   Para excluir todo o histórico de execução política, especifique NULL para *policy_id* e *oldest_date*.  
  
-   Para excluir todo o histórico de execução política para uma política específica, especifique um identificador de política para *policy_id*, e especifique NULL como *oldest_date*.  
  
-   Para excluir o histórico de execução de todas as políticas antes de uma data específica, especifique NULL para *policy_id*e especifique uma data para *oldest_date*.  
  
 Para arquivar o histórico de execução de política, você pode abrir o log Histórico de Política no Pesquisador de Objetos e exportar o histórico de execução para um arquivo. Para acessar o log de histórico de política, expanda **gerenciamento**, clique com botão direito **gerenciamento de política de**e, em seguida, clique em **Exibir histórico**.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de banco de dados fixa PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Possível elevação de credenciais: os usuários na função PolicyAdministratorRole podem criar gatilhos de servidor e agendar execuções de políticas que possam afetar a operação da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por exemplo, os usuários da função PolicyAdministratorRole podem criar uma política que impeça a criação da maioria dos objetos no [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Devido a essa possível elevação de credenciais, a função PolicyAdministratorRole deve ser concedida somente a usuários que sejam confiáveis com controle da configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte exclui o histórico de execução de política anterior a uma data específica de uma política com ID 7.  
  
```  
EXEC msdb.dbo.sp_syspolicy_delete_policy_execution_history @policy_id = 7  
, @oldest_date = '2009-02-16 16:00:00.000';  
  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento baseado em políticas armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_set_config_history_retention &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-history-retention-transact-sql.md)   
 [sp_syspolicy_purge_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-purge-history-transact-sql.md)  
  
  
