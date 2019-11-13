---
title: sp_addsubscriber (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsubscriber
- sp_addsubscriber_TSQL
helpviewer_keywords:
- sp_addsubscriber
ms.assetid: b8a584ea-2a26-4936-965b-b84f026e39c0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 278af2ca1bd6abdb84cdf2371628c6b95662e46e
ms.sourcegitcommit: eae9efe2a2d3758685e85039ffb8fa698aa47f9b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73962410"
---
# <a name="sp_addsubscriber-transact-sql"></a>sp_addsubscriber (Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Adiciona um novo Assinante a um Publicador, permitindo que ele receba publicações. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação, para publicações transacionais e de instantâneo; e para publicações de mesclagem que usam um Distribuidor remoto esse procedimento armazenado é executado no Distribuidor.  
  
> [!IMPORTANT]  
>  Esse procedimento armazenado foi preterido. Não é mais necessário que você registre explicitamente um Assinante no Publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @subscriber = ] 'subscriber'` é o nome do servidor a ser adicionado como um assinante válido para as publicações neste servidor. o *assinante* é **sysname**, sem padrão.  
  
`[ @type = ] type` é o tipo de assinante. o *tipo* é **tinyint**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0** (padrão)|Assinante do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**1**|Servidor de fontes de dados ODBC|  
|**2**|Banco de dados [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet|  
|**3**|Provedor OLE DB|  
  
`[ @login = ] 'login'` é a ID de logon para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. *login* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada por assinatura durante a execução de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
`[ @password = ] 'password'` é a senha para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. a *senha* é **nvarchar (524)** , com um padrão de NULL.  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada por assinatura durante a execução de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
`[ @commit_batch_size = ] commit_batch_size` esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts.  
  
> [!NOTE]  
>  Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
`[ @status_batch_size = ] status_batch_size` esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts.  
  
> [!NOTE]  
>  Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
`[ @flush_frequency = ] flush_frequency` esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts.  
  
> [!NOTE]  
>  Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
`[ @frequency_type = ] frequency_type` é a frequência com a qual agendar o agente de replicação. *frequency_type* é **int**e pode ser um desses valores.  
  
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
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada por assinatura durante a execução de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
`[ @frequency_interval = ] frequency_interval` é o valor aplicado à frequência definida por *frequency_type*. *frequency_interval* é **int**, com um padrão de 1.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada por assinatura durante a execução de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` é a data do agente de replicação. Esse parâmetro é usado quando *frequency_type* é definido como **32** (relativo mensal). *frequency_relative_interval* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1** (padrão)|First|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Last|  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada por assinatura durante a execução de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` é o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão de **0**.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada por assinatura durante a execução de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
`[ @frequency_subday = ] frequency_subday` é a frequência de reagendar durante o período definido. *frequency_subday* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4** (padrão)|Minuto|  
|**8**|Hora|  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada por assinatura durante a execução de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` é o intervalo para *frequency_subday*. *frequency_subday_interval* é **int**, com um padrão de **5**.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada por assinatura durante a execução de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` é a hora do dia em que o agente de replicação é agendado pela primeira vez, formatado como HHMMSS. *active_start_time_of_day* é **int**, com um padrão de **0**.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada por assinatura durante a execução de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` é a hora do dia em que o agente de replicação para de ser agendado, formatado como HHMMSS. *active_end_time_of_day*é **int**, com um padrão de 235959, o que significa 11:59:59 P.M. medida em um relógio de 24 horas.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada por assinatura durante a execução de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
`[ @active_start_date = ] active_start_date` é a data em que o agente de replicação é agendado pela primeira vez, formatado como AAAAMMDD. *active_start_date* é **int**, com um padrão de 0.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada por assinatura durante a execução de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
`[ @active_end_date = ] active_end_date` é a data em que o agente de replicação para de ser agendado, formatado como AAAAMMDD. *active_end_date* é **int**, com um padrão de 99991231, o que significa 31 de dezembro de 9999.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada por assinatura durante a execução de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
`[ @description = ] 'description'` é uma descrição de texto do Assinante. a *Descrição* é **nvarchar (255)** , com um padrão de NULL.  
  
`[ @security_mode = ] security_mode` é o modo de segurança implementado. *security_mode* é **int**, com um padrão de 1. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. **1** especifica a autenticação do Windows.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e é mantido para compatibilidade com versões anteriores de scripts. A propriedade agora é especificada por assinatura durante a execução de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Quando um valor é especificado, ele é usado como padrão na criação de assinaturas neste Assinante e uma mensagem de aviso é retornada.  
  
`[ @encrypted_password = ] encrypted_password` esse parâmetro foi preterido e é fornecido somente para fins de compatibilidade com versões anteriores *encrypted_password* a qualquer valor, mas **0** resultará em um erro.  
  
`[ @publisher = ] 'publisher'` especifica um Publicador que não é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser usado ao publicar de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_addsubscriber** é usado na replicação de instantâneos, na replicação transacional e na replicação de mesclagem.  
  
 **sp_addsubscriber** não é necessário quando o assinante só terá assinaturas anônimas para publicações de mesclagem.  
  
 **sp_addsubscriber** grava na tabela [MSsubscriber_info](../../relational-databases/system-tables/mssubscriber-info-transact-sql.md) no banco de dados de **distribuição** .  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_addsubscriber**.  
  
## <a name="see-also"></a>Consulte também  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [sp_changesubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)  
  
  
