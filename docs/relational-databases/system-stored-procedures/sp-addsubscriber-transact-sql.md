---
title: sp_addsubscriber (Transact-SQL) | Microsoft Docs
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
applies_to:
- SQL Server
f1_keywords:
- sp_addsubscriber
- sp_addsubscriber_TSQL
helpviewer_keywords:
- sp_addsubscriber
ms.assetid: b8a584ea-2a26-4936-965b-b84f026e39c0
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: aaccd874d7f559b422f0f4c8ac6d2e9a2baacb83
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spaddsubscriber-transact-sql"></a>sp_addsubscriber (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona um novo Assinante a um Publicador, permitindo que ele receba publicações. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação, para publicações transacionais e de instantâneo; e para publicações de mesclagem que usam um Distribuidor remoto esse procedimento armazenado é executado no Distribuidor.  
  
> [!IMPORTANT]  
>  Esse procedimento armazenado foi preterido. Não é mais necessário que você registre explicitamente um Assinante no Publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addsubscriber [ @subscriber = ] 'subscriber'  
    [ , [ @type = ] type ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @commit_batch_size = ] commit_batch_size ]  
    [ , [ @status_batch_size = ] status_batch_size ]  
    [ , [ @flush_frequency = ] flush_frequency ]  
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
    [ , [ @description = ] 'description' ]  
    [ , [ @security_mode = ] security_mode ]  
    [ , [ @encrypted_password = ] encrypted_password ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@subscriber=**] **'***assinante***'**  
 É o nome do servidor a ser adicionado como um Assinante válido à publicação neste servidor. *assinante* é **sysname**, sem padrão.  
  
 [  **@type=**] *tipo*  
 É o tipo de assinante. *tipo* é **tinyint**, e pode ser um destes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**0** (padrão)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assinante|  
|**1**|Servidor de fontes de dados ODBC|  
|**2**|Banco de dados [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet |  
|**3**|Provedor OLE DB|  
  
 [  **@login=**] **'***login***'**  
 É a ID do logon para a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *login* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada em uma base por assinatura ao executar [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
 [  **@password=**] **'***senha***'**  
 É a senha para a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *senha* é **nvarchar (524)**, com um padrão NULL.  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada em uma base por assinatura ao executar [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
 [  **@commit_batch_size=**] *commit_batch_size*  
 Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts.  
  
> [!NOTE]  
>  Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
 [  **@status_batch_size=**] *status_batch_size*  
 Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts.  
  
> [!NOTE]  
>  Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
 [  **@flush_frequency=**] *flush_frequency*  
 Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts.  
  
> [!NOTE]  
>  Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
 [  **@frequency_type=**] *frequency_type*  
 É a frequência de agendamento do agente de replicação. *frequency_type* é **int**, e pode ser um destes valores.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Sob Demanda|  
|**4**|Diariamente|  
|**8**|Semanalmente|  
|**16**|Mensalmente|  
|**32**|Relativo ao mês|  
|**64** (padrão)|Iniciar automaticamente|  
|**128**|Recorrente|  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada em uma base por assinatura ao executar [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
 [**@frequency_interval=** ] *frequency_interval*  
 O valor aplicado à frequência definida *frequency_type*. *frequency_interval* é **int**, com um padrão de 1.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada em uma base por assinatura ao executar [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 É a data do agente de replicação. Esse parâmetro é usado quando *frequency_type* é definido como **32** (mensal relativo). *frequency_relative_interval* é **int**, e pode ser um destes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**1** (padrão)|First|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Last|  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada em uma base por assinatura ao executar [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 É o fator de recorrência usado por *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão de **0**.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada em uma base por assinatura ao executar [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 É a frequência de reagendamento durante o período definido. *frequency_subday* é **int**, e pode ser um destes valores.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4** (padrão)|Minuto|  
|**8**|Hora|  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada em uma base por assinatura ao executar [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 É o intervalo de *frequency_subday*. *frequency_subday_interval* é **int**, com um padrão de **5**.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada em uma base por assinatura ao executar [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 É a hora do dia do primeiro agendamento do agente de replicação, formatada como HHMMSS. *active_start_time_of_day* é **int**, com um padrão de **0**.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada em uma base por assinatura ao executar [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 É a hora do dia do último agendamento do agente de replicação, formatada como HHMMSS. *active_end_time_of_day*é **int**, com um padrão de 235959, o que significa 11:59:59 P.M. medida em um relógio de 24 horas.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada em uma base por assinatura ao executar [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
 [  **@active_start_date=**] *active_start_date*  
 É a data do primeiro agendamento do agente de replicação, formatada como AAAAMMDD. *active_start_date* é **int**, com um padrão de 0.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada em uma base por assinatura ao executar [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
 [  **@active_end_date=**] *active_end_date*  
 É a data do último agendamento do agente de replicação, formatada como AAAAMMDD. *active_end_date* é **int**, com um padrão de 99991231, que significa 31 de dezembro de 9999.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada em uma base por assinatura ao executar [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
 [  **@description=**] **'***descrição***'**  
 É uma descrição de texto do Assinante. *Descrição* é **nvarchar (255)**, com um padrão NULL.  
  
 [  **@security_mode=**] *security_mode*  
 É o modo de segurança implementado. *security_mode* é **int**, com um padrão de 1. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. **1** Especifica autenticação do Windows.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada em uma base por assinatura ao executar [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
 [  **@encrypted_password=**] *encrypted_password*  
 Esse parâmetro foi preterido e é fornecido para compatibilidade com versões anteriores somente configuração *encrypted_password* para qualquer valor mas **0** resultará em erro.  
  
 [ **@publisher**=] **'***publicador***'**  
 Especifica um Publicador que não é do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publicador* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *publicador* não deve ser usado durante a publicação de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_addsubscriber** é usado em replicação de instantâneo, replicação transacional e replicação de mesclagem.  
  
 **sp_addsubscriber** não é necessário quando o assinante só tiver assinaturas anônimas para publicações de mesclagem.  
  
 **sp_addsubscriber** grava o [MSsubscriber_info](../../relational-databases/system-tables/mssubscriber-info-transact-sql.md) tabela o **distribuição** banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa **sp_addsubscriber**.  
  
## <a name="see-also"></a>Consulte também  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [sp_changesubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)  
  
  
