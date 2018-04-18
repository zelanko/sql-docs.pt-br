---
title: sp_changesubscriber_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_changesubscriber_schedule
- sp_changesubscriber_schedule_TSQL
helpviewer_keywords:
- sp_changesubscriber_schedule
ms.assetid: ff84e8e2-d496-482c-b23e-38a6626596e6
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9aa99834cda2085a60df8f148b457da52b33b6bf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spchangesubscriberschedule-transact-sql"></a>sp_changesubscriber_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera o agendamento do Distribution Agent ou Merge Agent para um assinante. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changesubscriber_schedule [ @subscriber = ] 'subscriber', [ @agent_type = ] type  
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday = ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@subscriber=**] **'***assinante***'**  
 É o nome do Assinante. *assinante* é **sysname**. O nome do Assinante deve ser exclusivo no banco de dados, não deve existir e não deve ser NULL.  
  
 [  **@agent_type=**] *tipo*  
 É o tipo de agente. *tipo* é **smallint**, com um padrão de **0**. **0** indica um Distribution Agent. **1** indica um Merge Agent.  
  
 [  **@frequency_type=**] *frequency_type*  
 É a frequência de agendamento da tarefa de distribuição. *frequency_type* é **int**, com um padrão de **64**. Há 10 colunas agendadas.  
  
 [  **@frequency_interval=**] *frequency_interval*  
 O valor aplicado à frequência definida *frequency_type*. *frequency_interval* é **int**, com um padrão de **1**.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 É a data da tarefa de distribuição. *frequency_relative_interval* é **int**, com um padrão de **1**.  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 É o fator de recorrência usado por *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão de **0**.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 É a frequência, em minutos, de reagendamento durante o período definido. *frequency_subday* é **int**, com um padrão de **4**.  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 É o intervalo de *frequency_subday*. *frequency_subday_interval* é **int**, com um padrão de **5**.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 É a hora do dia do primeiro agendamento da tarefa de distribuição. *active_start_time_of_day* é **int**, com um padrão de **0**.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 É a hora do dia do último agendamento da tarefa de distribuição. *active_end_time_of_day* é **int**, com um padrão de **235959**, que significa 11:59:59 P.M. em um relógio de 24 horas.  
  
 [  **@active_start_date=**] *active_start_date*  
 É a data do primeiro agendamento da tarefa de distribuição, formatada como AAAAMMDD. *active_start_date* é **int**, com um padrão de **0**.  
  
 [  **@active_end_date=**] *active_end_date*  
 É a data do último agendamento da tarefa de distribuição, formatada como AAAAMMDD. *active_end_date* é **int**, com um padrão de **99991231**, que significa 31 de dezembro de 9999.  
  
 [ **@publisher**=] **'***publicador***'**  
 Especifica um não[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *publicador* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *publicador* não deve ser usado ao alterar as propriedades de artigo em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_changesubscriber_schedule** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa **sp_changesubscriber_schedule**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addsubscriber_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-schedule-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
