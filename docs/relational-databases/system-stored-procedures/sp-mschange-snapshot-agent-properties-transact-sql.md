---
title: sp_MSchange_snapshot_agent_properties (T-SQL)
description: Descreve o sp_MSchange_snapshot_agent_properties procedimento armazenado usado para alterar as propriedades do Agente de Instantâneo usado para Replicação do SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_snapshot_agent_properties_TSQL
- sp_MSchange_snapshot_agent_properties
helpviewer_keywords:
- sp_MSchange_snapshot_agent_properties
ms.assetid: 7947a788-3fd7-469f-84db-b03ba89a153c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6c5c3c2573465072de0d1f0a7c08d47df5d387b6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75321793"
---
# <a name="sp_mschange_snapshot_agent_properties-transact-sql"></a>sp_MSchange_snapshot_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de um trabalho agente de instantâneo executado em um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] distribuidor de versão ou posterior. Esse procedimento armazenado é usado para alterar propriedades quando o Publicador é executado em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_MSchange_snapshot_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @frequency_type= ] frequency_type  
        , [ @frequency_interval= ] frequency_interval  
        , [ @frequency_subday= ] frequency_subday  
        , [ @frequency_subday_interval= ] frequency_subday_interval  
        , [ @frequency_relative_interval= ] frequency_relative_interval  
        , [ @frequency_recurrence_factor= ] frequency_recurrence_factor  
        , [ @active_start_date= ] active_start_date  
        , [ @active_end_date= ] active_end_date  
        , [ @active_start_time_of_day= ] active_start_time_of_day  
        , [ @active_end_time_of_day= ] active_end_time_of_day  
        , [ @snapshot_job_name = ] 'snapshot_agent_name'  
        , [ @publisher_security_mode = ] publisher_security_mode  
        , [ @publisher_login = ] 'publisher_login'  
        , [ @publisher_password = ] 'publisher_password'   
        , [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
        , [ @publisher_type = ] 'publisher_type'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`É o nome do Publicador. o *Publicador* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados de publicação. *publisher_db* é **sysname**, sem padrão.  
  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @frequency_type = ] frequency_type`É a frequência com a qual o Agente de Instantâneo é executado. *frequency_type* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Sob demanda|  
|**4**|Diário|  
|**8**|Semanal|  
|**10**|Mensal|  
|**20,00**|Mensalmente, relativo ao intervalo de frequência|  
|**40**|Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent inicia|  
  
`[ @frequency_interval = ] frequency_interval`É o valor a ser aplicado à frequência definida por *frequency_type*. *frequency_interval* é **int**, sem padrão.  
  
`[ @frequency_subday = ] frequency_subday`É as unidades para *freq_subday_interval*. *frequency_subday* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4**|Minuto|  
|**8**|Hora|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`É o intervalo para *frequency_subday*. *frequency_subday_interval* é **int**, sem padrão.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`É a data em que o Agente de Instantâneo é executado. *frequency_relative_interval* é **int**, sem padrão.  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`É o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor* é **int**, sem padrão.  
  
`[ @active_start_date = ] active_start_date`É a data em que o Agente de Instantâneo é agendado pela primeira vez, formatado como AAAAMMDD. *active_start_date* é **int**, sem padrão.  
  
`[ @active_end_date = ] active_end_date`É a data em que a Agente de Instantâneo para de ser agendada, formatada como AAAAMMDD. *active_end_date* é **int**, sem padrão.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`É a hora do dia em que o Agente de Instantâneo é agendado pela primeira vez, formatado como HHMMSS. *active_start_time_of_day* é **int**, sem padrão.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`É a hora do dia em que a Agente de Instantâneo para de ser agendada, formatada como HHMMSS. *active_end_time_of_day* é **int**, sem padrão.  
  
`[ @snapshot_job_name = ] 'snapshot_agent_name'`É o nome de um nome de trabalho de Agente de Instantâneo existente se um trabalho existente estiver sendo usado. *snapshot_agent_name* é **nvarchar (100)**, sem padrão.  
  
`[ @publisher_security_mode = ] publisher_security_mode`É o modo de segurança usado pelo agente ao se conectar ao Publicador. *publisher_security_mode* é **int**, sem padrão. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a autenticação e **1** especifica a autenticação do Windows. Um valor de **0** deve ser especificado para não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'`É o logon usado ao conectar-se ao Publicador. *publisher_login* é **sysname**, sem padrão. *publisher_login* deve ser especificado quando *publisher_security_mode* é **0**. Se *publisher_login* for NULL e Publisher *_ * * security_mode* for **1**, a conta do Windows especificada em *job_login* será usada durante a conexão com o Publicador.  
  
`[ @publisher_password = ] 'publisher_password'`É a senha usada ao conectar-se ao Publicador. *publisher_password* é **nvarchar (524)**, sem padrão.  
  
> [!IMPORTANT]  
>  Não armazene informações de autenticação em arquivos de script. Para ajudar a melhorar a segurança, recomendamos que você forneça nomes de login e senhas em tempo de execução.  
  
`[ @job_login = ] 'job_login'`É o logon da conta do Windows na qual o agente é executado. *job_login* é **nvarchar (257)**, sem padrão. Essa conta do Windows sempre é usada para conexões de agente com o Distribuidor. Você deve fornecer esse parâmetro ao criar um novo trabalho do Agente de Instantâneo. *Isso não pode ser alterado para um não* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Publicador.*  
  
`[ @job_password = ] 'job_password'`É a senha para a conta do Windows na qual o agente é executado. *job_password* é **sysname**, sem padrão. Você deve fornecer esse parâmetro ao criar um novo trabalho do Agente de Instantâneo.  
  
> [!IMPORTANT]  
>  Não armazene informações de autenticação em arquivos de script. Para ajudar a melhorar a segurança, recomendamos que você forneça nomes de login e senhas em tempo de execução.  
  
`[ @publisher_type = ] 'publisher_type'`Especifica o tipo de Publicador quando o Publicador não estiver em execução [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]em uma instância do. *publisher_type* é **sysname**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**MSSQLSERVER**|Especifica um Editor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|Especifica um Publicador Oracle padrão.|  
|**ORACLE GATEWAY**|Especifica um Editor Oracle Gateway.|  
  
 Para obter mais informações sobre as diferenças entre um Publicador Oracle e um Publicador de gateway da Oracle, consulte [visão geral da publicação Oracle](../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_MSchange_snapshot_agent_properties** é usado na replicação de instantâneos, na replicação transacional e na replicação de mesclagem.  
  
 Você deve especificar todos os parâmetros ao executar **sp_MSchange_snapshot_agent_properties**. Execute [sp_helppublication_snapshot](../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md) para retornar as propriedades atuais do trabalho de agente de instantâneo.  
  
 Quando o Publicador é executado em uma [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] instância do ou versão posterior, você deve usar [sp_changepublication_snapshot](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md) para alterar as propriedades de um trabalho de agente de instantâneo.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** no distribuidor podem executar **sp_MSchange_snapshot_agent_properties**.  
  
## <a name="see-also"></a>Consulte Também  
 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
  
