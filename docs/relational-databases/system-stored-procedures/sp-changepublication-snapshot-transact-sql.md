---
title: sp_changepublication_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changepublication_snapshot_TSQL
- sp_changepublication_snapshot
helpviewer_keywords:
- sp_changepublication_snapshot
ms.assetid: 518a4618-3592-4edc-8425-cbc33cdff891
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8d7252f0335e2fc83c5b8e5e27f5e41535fdc7bc
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68762260"
---
# <a name="sp_changepublication_snapshot-transact-sql"></a>sp_changepublication_snapshot (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Propriedades de alteração do Agente de Instantâneo para a publicação especificada. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!IMPORTANT]  
>  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changepublication_snapshot [ @publication= ] 'publication'  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @snapshot_job_name = ] 'snapshot_agent_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @frequency_type = ] frequency_type`É a frequência com a qual agendar o agente. *frequency_type* é **int**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Sob Demanda|  
|**4**|Diariamente|  
|**8**|Semanalmente|  
|**16**|Mensalmente|  
|**32**|Relativo ao mês|  
|**64**|Iniciar automaticamente|  
|**128**|Recorrente|  
|NULL (padrão)||  
  
`[ @frequency_interval = ] frequency_interval`Especifica os dias em que o agente é executado. *frequency_interval* é **int**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Domingo|  
|**2**|Segunda-feira|  
|**3**|Terça-feira|  
|**4**|Quarta-feira|  
|**5**|Quinta-feira|  
|**6**|Sexta-feira|  
|**7**|Sábado|  
|**8**|Day|  
|**9**|Dias da semana|  
|**10**|Dias de fim de semana|  
|NULL (padrão)||  
  
`[ @frequency_subday = ] frequency_subday`É as unidades para *freq_subday_interval*. *frequency_subday* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4**|Minuto|  
|**8**|Hora|  
|NULL (padrão)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`É o intervalo para *frequency_subday*. *frequency_subday_interval* é **int**, com um padrão de NULL.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`É a data em que o Agente de Instantâneo é executado. *frequency_relative_interval* é **int**, com um padrão de NULL.  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`É o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão de NULL.  
  
`[ @active_start_date = ] active_start_date`É a data em que o Agente de Instantâneo é agendado pela primeira vez, formatado como AAAAMMDD. *active_start_date* é **int**, com um padrão de NULL.  
  
`[ @active_end_date = ] active_end_date`É a data em que a Agente de Instantâneo para de ser agendada, formatada como AAAAMMDD. *active_end_date* é **int**, com um padrão de NULL.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`É a hora do dia em que o Agente de Instantâneo é agendado pela primeira vez, formatado como HHMMSS. *active_start_time_of_day* é **int**, com um padrão de NULL.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`É a hora do dia em que a Agente de Instantâneo para de ser agendada, formatada como HHMMSS. *active_end_time_of_day* é **int**, com um padrão de NULL.  
  
`[ @snapshot_job_name = ] 'snapshot_agent_name'`É o nome de um nome de trabalho de Agente de Instantâneo existente se um trabalho existente estiver sendo usado. *snapshot_agent_name* é **nvarchar (100)** com um valor padrão de NULL.  
  
`[ @publisher_security_mode = ] publisher_security_mode`É o modo de segurança usado pelo agente ao se conectar ao Publicador. *publisher_security_mode* é **smallint**, com um padrão de NULL. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a autenticação e **1** especifica a autenticação do Windows. Um valor de **0** deve ser especificado para não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'`É o logon usado ao conectar-se ao Publicador. *publisher_login* é **sysname**, com um padrão de NULL. *publisher_login* deve ser especificado quando *publisher_security_mode* é **0**. Se *publisher_login* for nulo e *publisher_security_mode* for **1**, a conta do Windows especificada em *job_login* será usada durante a conexão com o Publicador.  
  
`[ @publisher_password = ] 'publisher_password'`É a senha usada ao conectar-se ao Publicador. *publisher_password* é **sysname**, com um padrão de NULL.  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte. Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
`[ @job_login = ] 'job_login'`É o logon da conta do Windows na qual o agente é executado. *job_login* é **nvarchar (257)** , com um padrão de NULL. Essa conta do Windows sempre é usada para conexões de agente com o Distribuidor. Você deve fornecer esse parâmetro ao criar um novo trabalho do Agente de Instantâneo. Isso não pode ser alterado para um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador.  
  
`[ @job_password = ] 'job_password'`É a senha para a conta do Windows na qual o agente é executado. *job_password* é **sysname**, com um padrão de NULL. Você deve fornecer esse parâmetro ao criar um novo trabalho do Agente de Instantâneo.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o Publicador é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o Publicador não deve ser usado ao criar um agente de instantâneo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changepublication_snapshot** é usado na replicação de instantâneo, na replicação transacional e na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **db_owner** podem executar **sp_changepublication_snapshot**.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Alterar propriedades da publicação e do artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
