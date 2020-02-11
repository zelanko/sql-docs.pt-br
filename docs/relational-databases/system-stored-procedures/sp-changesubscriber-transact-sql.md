---
title: sp_changesubscriber (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriber
- sp_changesubscriber_TSQL
helpviewer_keywords:
- sp_changesubscriber
ms.assetid: d453c451-e957-490f-b968-5e03aeddaf10
author: stevestein
ms.author: sstein
ms.openlocfilehash: 42b56712e8b441184d55bf12ce16dbcb55930374
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68762777"
---
# <a name="sp_changesubscriber-transact-sql"></a>sp_changesubscriber (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Altera as opções para um Assinante. Qualquer tarefa de distribuição para os Assinantes deste Publicador será atualizada. Esse procedimento armazenado grava na tabela de **MSsubscriber_info** no banco de dados de distribuição. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changesubscriber [ @subscriber= ] 'subscriber'  
    [ , [ @type= ] type ]  
    [ , [ @login= ] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @commit_batch_size= ] commit_batch_size ]  
    [ , [ @status_batch_size= ] status_batch_size ]  
    [ , [ @flush_frequency= ] flush_frequency ]  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @security_mode= ] security_mode ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @subscriber = ] 'subscriber'`É o nome do Assinante no qual as opções serão alteradas. o *assinante* é **sysname**, sem padrão.  
  
`[ @type = ] type`É o tipo de assinante. o *tipo* é **tinyint**, com um padrão de NULL. **0** indica um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinante. **1** especifica um assinante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de servidor de fonte de dados ODBC não ou outro.  
  
`[ @login = ] 'login'`É a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID de logon de autenticação. *logon* é **sysname**, com um padrão de NULL.  
  
`[ @password = ] 'password'`É a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] senha de autenticação. a *senha* é **sysname**, com um padrão **%** de. **%** indica que não há nenhuma alteração na propriedade password.  
  
`[ @commit_batch_size = ] commit_batch_size`Com suporte apenas para compatibilidade com versões anteriores.  
  
`[ @status_batch_size = ] status_batch_size`Com suporte apenas para compatibilidade com versões anteriores.  
  
`[ @flush_frequency = ] flush_frequency`Com suporte apenas para compatibilidade com versões anteriores.  
  
`[ @frequency_type = ] frequency_type`É a frequência com a qual agendar a tarefa de distribuição. *frequency_type* é **int**e pode ser um desses valores.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Sob demanda|  
|**quatro**|Diário|  
|**8**|Semanalmente|  
|**16**|Mensal|  
|**32**|Relativo ao mês|  
|**64**|Iniciar automaticamente|  
|**128**|Recorrente|  
  
`[ @frequency_interval = ] frequency_interval`É o intervalo para *frequency_type*. *frequency_interval* é **int**, com um padrão de NULL.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`É a data da tarefa de distribuição. Esse parâmetro é usado quando *frequency_type* é definido como **32** (relativo mensal). *frequency_relative_interval* é **int**e pode ser um desses valores.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**1**|Primeiro|  
|**2**|Segundo|  
|**quatro**|Terceiro|  
|**8**|Quarto|  
|**16**|Último|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`É a frequência com que a tarefa de distribuição deve ocorrer durante o *frequency_type*definido. *frequency_recurrence_factor* é **int**, com um padrão de NULL.  
  
`[ @frequency_subday = ] frequency_subday`É a frequência de reagendar durante o período definido. *frequency_subday* é **int**e pode ser um desses valores.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**quatro**|Minuto|  
|**8**|Hora|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`É o intervalo para *frequence_subday*. *frequency_subday_interval* é **int**, com um padrão de NULL.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`É a hora do dia em que a tarefa de distribuição é agendada pela primeira vez, formatada como HHMMSS. *active_start_time_of_day* é **int**, com um padrão de NULL.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`É a hora do dia em que a tarefa de distribuição para de ser agendada, formatada como HHMMSS. *active_end_time_of_day*é **int**, com um padrão de NULL.  
  
`[ @active_start_date = ] active_start_date`É a data em que a tarefa de distribuição é agendada pela primeira vez, formatada como AAAAMMDD. *active_start_date* é **int**, com um padrão de NULL.  
  
`[ @active_end_date = ] active_end_date`É a data em que a tarefa de distribuição para de ser agendada, formatada como AAAAMMDD. *active_end_date*é **int**, com um padrão de NULL.  
  
`[ @description = ] 'description'`É uma descrição de texto opcional. a *Descrição* é **nvarchar (255)**, com um padrão de NULL.  
  
`[ @security_mode = ] security_mode`É o modo de segurança implementado. *security_mode* é **int**e pode ser um desses valores.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticação|  
|**1**|Autenticação do Windows|  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser usado ao alterar as propriedades [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do artigo em um Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changesubscriber** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_changesubscriber**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addsubscriber](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropsubscriber](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpdistributiondb](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpserver](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
