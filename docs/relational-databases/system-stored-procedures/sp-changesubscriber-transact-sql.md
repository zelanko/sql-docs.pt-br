---
title: sp_changesubscriber (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_changesubscriber
- sp_changesubscriber_TSQL
helpviewer_keywords:
- sp_changesubscriber
ms.assetid: d453c451-e957-490f-b968-5e03aeddaf10
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 799a2a8b398d3ff6eff13a83a3cc60af90421cc4
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43019827"
---
# <a name="spchangesubscriber-transact-sql"></a>sp_changesubscriber (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as opções para um Assinante. Qualquer tarefa de distribuição para os Assinantes deste Publicador será atualizada. Esse procedimento armazenado grava os **MSsubscriber_info** tabela no banco de dados de distribuição. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@subscriber=**] **'***assinante***'**  
 É o nome do Assinante no qual alterar as opções. *assinante* está **sysname**, sem padrão.  
  
 [  **@type=**] *tipo*  
 É o tipo de Assinante. *tipo de* está **tinyint**, com um padrão NULL. **0** indica uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinante. **1** Especifica um não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou em outro servidor de origem de dados ODBC assinante.  
  
 [  **@login=**] **'***logon***'**  
 É a ID do logon de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *login* é **sysname**, com um padrão de NULL.  
  
 [  **@password=**] **'***senha***'**  
 É a senha de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *senha* está **sysname**, com um padrão de **%**. **%** indica que nenhuma alteração para a propriedade de senha.  
  
 [  **@commit_batch_size=**] *commit_batch_size*  
 Com suporte somente para compatibilidade com versões anteriores.  
  
 [  **@status_batch_size=**] *status_batch_size*  
 Com suporte somente para compatibilidade com versões anteriores.  
  
 [  **@flush_frequency=**] *flush_frequency*  
 Com suporte somente para compatibilidade com versões anteriores.  
  
 [  **@frequency_type=**] *frequency_type*  
 É a frequência de agendamento da tarefa de distribuição. *frequency_type* está **int**, e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Sob Demanda|  
|**4**|Diariamente|  
|**8**|Semanalmente|  
|**16**|Mensalmente|  
|**32**|Relativo ao mês|  
|**64**|Iniciar automaticamente|  
|**128**|Recorrente|  
  
 [  **@frequency_interval=**] *frequency_interval*  
 É o intervalo de *frequency_type*. *frequency_interval* está **int**, com um padrão NULL.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 É a data da tarefa de distribuição. Esse parâmetro é usado quando *frequency_type* é definido como **32** (mensal relativo). *frequency_relative_interval* está **int**, e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**1**|First|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Last|  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 É a frequência com que a tarefa de distribuição deve ser repetido durante o definido *frequency_type*. *frequency_recurrence_factor* está **int**, com um padrão NULL.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 É a frequência de reagendamento durante o período definido. *frequency_subday* está **int**, e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4**|Minuto|  
|**8**|Hora|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 É o intervalo de *frequence_subday*. *frequency_subday_interval* está **int**, com um padrão NULL.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 É a hora do dia do primeiro agendamento da tarefa de distribuição, formatada como HHMMSS. *active_start_time_of_day* está **int**, com um padrão NULL.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 É a hora do dia do último agendamento da tarefa de distribuição, formatada como HHMMSS. *active_end_time_of_day*está **int**, com um padrão NULL.  
  
 [  **@active_start_date=**] *active_start_date*  
 É a data do primeiro agendamento da tarefa de distribuição, formatada como AAAAMMDD. *active_start_date* está **int**, com um padrão NULL.  
  
 [  **@active_end_date=**] *active_end_date*  
 É a data do último agendamento da tarefa de distribuição, formatada como AAAAMMDD. *active_end_date*está **int**, com um padrão NULL.  
  
 [  **@description=**] **'***descrição***'**  
 É uma descrição de texto opcional. *Descrição* está **nvarchar (255)**, com um padrão NULL.  
  
 [  **@security_mode=**] *security_mode*  
 É o modo de segurança implementado. *security_mode* está **int**, e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticação|  
|**1**|Autenticação do Windows|  
  
 [ **@publisher**=] **'***publisher***'**  
 Especifica um Publicador que não é do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Publisher* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *Publisher* não deve ser usado ao alterar as propriedades do artigo em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_changesubscriber** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** pode executar a função de servidor fixa **sp_changesubscriber**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
