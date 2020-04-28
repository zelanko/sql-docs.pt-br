---
title: sp_changesubscriber_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriber_schedule
- sp_changesubscriber_schedule_TSQL
helpviewer_keywords:
- sp_changesubscriber_schedule
ms.assetid: ff84e8e2-d496-482c-b23e-38a6626596e6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 22ecb1601108562607d1fdc550daaa945fe72910
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68770730"
---
# <a name="sp_changesubscriber_schedule-transact-sql"></a>sp_changesubscriber_schedule (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Altera o agendamento do Distribution Agent ou Merge Agent para um assinante. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @subscriber = ] 'subscriber'`É o nome do Assinante. *assinante* é **sysname**. O nome do Assinante deve ser exclusivo no banco de dados, não deve existir e não deve ser NULL.  
  
`[ @agent_type = ] type`É o tipo de agente. o *tipo* é **smallint**, com um padrão de **0**. **0** indica um agente de distribuição. **1** indica um agente de mesclagem.  
  
`[ @frequency_type = ] frequency_type`É a frequência com a qual agendar a tarefa de distribuição. *frequency_type* é **int**, com um padrão de **64**. Há 10 colunas agendadas.  
  
`[ @frequency_interval = ] frequency_interval`É o valor aplicado à frequência definida por *frequency_type*. *frequency_interval* é **int**, com um padrão de **1**.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`É a data da tarefa de distribuição. *frequency_relative_interval* é **int**, com um padrão de **1**.  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`É o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão de **0**.  
  
`[ @frequency_subday = ] frequency_subday`É a frequência, em minutos, para reagendar durante o período definido. *frequency_subday* é **int**, com um padrão de **4**.  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`É o intervalo para *frequency_subday*. *frequency_subday_interval* é **int**, com um padrão de **5**.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`É a hora do dia em que a tarefa de distribuição é agendada pela primeira vez. *active_start_time_of_day* é **int**, com um padrão de **0**.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`É a hora do dia em que a tarefa de distribuição para de ser agendada. *active_end_time_of_day* é **int**, com um padrão de **235959**, o que significa 11:59:59 P.M. em um relógio de 24 horas.  
  
`[ @active_start_date = ] active_start_date`É a data em que a tarefa de distribuição é agendada pela primeira vez, formatada como AAAAMMDD. *active_start_date* é **int**, com um padrão de **0**.  
  
`[ @active_end_date = ] active_end_date`É a data em que a tarefa de distribuição para de ser agendada, formatada como AAAAMMDD. *active_end_date* é **int**, com um padrão de **99991231**, o que significa 31 de dezembro de 9999.  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser usado ao alterar as propriedades [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do artigo em um Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changesubscriber_schedule** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_changesubscriber_schedule**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addsubscriber_schedule](../../relational-databases/system-stored-procedures/sp-addsubscriber-schedule-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
