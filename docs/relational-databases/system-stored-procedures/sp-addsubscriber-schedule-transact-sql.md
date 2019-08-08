---
title: sp_addsubscriber_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsubscriber_schedule_TSQL
- sp_addsubscriber_schedule
helpviewer_keywords:
- sp_addsubscriber_schedule
ms.assetid: a6225033-5c3b-452f-ae52-79890a3590ed
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7baa7419620fd25be06a731894432862bfba2b96
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769051"
---
# <a name="sp_addsubscriber_schedule-transact-sql"></a>sp_addsubscriber_schedule (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Adiciona uma agenda para o Distribution Agent e Merge Agent. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addsubscriber_schedule [ @subscriber = ] 'subscriber'  
    [ , [ @agent_type = ] agent_type ]  
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
  
`[ @agent_type = ] agent_type`É o tipo de agente. *agent_type* é **smallint**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0** (padrão)|Agente de Distribuição|  
|**1**|Merge Agent|  
  
`[ @frequency_type = ] frequency_type`É a frequência com a qual agendar a Agente de Distribuição. *frequency_type* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Sob Demanda|  
|**4**|Diariamente|  
|**8**|Semanalmente|  
|**16**|Mensalmente|  
|**32**|Relativo ao mês|  
|**64** (padrão)|Iniciar automaticamente|  
|**128**|Recorrente|  
  
`[ @frequency_interval = ] frequency_interval`É o valor a ser aplicado à frequência definida por *frequency_type*. *frequency_interval* é **int**, com um padrão de **1**.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`É a data da Agente de Distribuição. Esse parâmetro é usado quando *frequency_type* é definido como **32** (relativo mensal). *frequency_relative_interval* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1** (padrão)|First|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Last|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`É o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão de **0**.  
  
`[ @frequency_subday = ] frequency_subday`É a frequência de reagendar durante o período definido. *frequency_subday* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4** (padrão)|Minuto|  
|**8**|Hora|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`É o intervalo para *frequency_subday*. *frequency_subday_interval* é **int**, com um padrão de **5**.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`É a hora do dia em que o Agente de Distribuição é agendado pela primeira vez, formatado como HHMMSS. *active_start_time_of_day* é **int**, com um padrão de **0**.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`É a hora do dia em que a Agente de Distribuição para de ser agendada, formatada como HHMMSS. *active_end_time_of_day*é **int**, com um padrão de 235959, o que significa 11:59:59 P.M. medida em um relógio de 24 horas.  
  
`[ @active_start_date = ] active_start_date`É a data em que o Agente de Distribuição é agendado pela primeira vez, formatado como AAAAMMDD. *active_start_date* é **int**, com um padrão de **0**.  
  
`[ @active_end_date = ] active_end_date`É a data em que a Agente de Distribuição para de ser agendada, formatada como AAAAMMDD. *active_end_date* é **int**, com um padrão de 99991231, que significa 31 de dezembro de 9999.  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o Publicador é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o Publicador não deve ser especificado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addsubscriber_schedule** é usado na replicação de instantâneo, na replicação transacional e na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_addsubscriber_schedule**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_changesubscriber_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-schedule-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
