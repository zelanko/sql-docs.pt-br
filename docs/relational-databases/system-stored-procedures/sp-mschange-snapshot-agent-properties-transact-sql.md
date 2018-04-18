---
title: sp_MSchange_snapshot_agent_properties (Transact-SQL) | Microsoft Docs
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
- sp_MSchange_snapshot_agent_properties_TSQL
- sp_MSchange_snapshot_agent_properties
helpviewer_keywords:
- sp_MSchange_snapshot_agent_properties
ms.assetid: 7947a788-3fd7-469f-84db-b03ba89a153c
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b3219fc1832d781e3156ec4a2284c3a8e861db67
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spmschangesnapshotagentproperties-transact-sql"></a>sp_MSchange_snapshot_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de um trabalho do Snapshot Agent que é executado em um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou versão posterior do distribuidor. Esse procedimento armazenado é usado para alterar propriedades quando o publicador é executado em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@publisher** =] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, sem padrão.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 É o nome do banco de dados de publicação. *publisher_db* é **sysname**, sem padrão.  
  
 [  **@publication =** ] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@frequency_type =** ] *frequency_type*  
 É a frequência de execução do Agente de Instantâneo. *frequency_type* é **int**, e pode ser um destes valores.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Sob Demanda|  
|**4**|Diariamente|  
|**8**|Semanalmente|  
|**10**|Mensalmente|  
|**20**|Mensalmente, relativo ao intervalo de frequência|  
|**40**|Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent inicia|  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 É o valor a ser aplicado à frequência definida *frequency_type*. *frequency_interval* é **int**, sem padrão.  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 É a unidade do *freq_subday_interval*. *frequency_subday* é **int**, e pode ser um destes valores.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4**|Minuto|  
|**8**|Hora|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 É o intervalo de *frequency_subday*. *frequency_subday_interval* é **int**, sem padrão.  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 É a data de execução do Agente de Instantâneo. *frequency_relative_interval* é **int**, sem padrão.  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 É o fator de recorrência usado por *frequency_type*. *frequency_recurrence_factor* é **int**, sem padrão.  
  
 [  **@active_start_date =** ] *active_start_date*  
 É a data do primeiro agendamento do Agente de Instantâneo, formatada como AAAAMMDD. *active_start_date* é **int**, sem padrão.  
  
 [  **@active_end_date =** ] *active_end_date*  
 É a data em que o Agente de Instantâneo para de ser agendado, formatada como AAAAMMDD. *active_end_date* é **int**, sem padrão.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 É a hora do dia do primeiro agendamento do Agente de Instantâneo, formatada como HHMMSS. *active_start_time_of_day* é **int**, sem padrão.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 É a hora do dia do último agendamento do Agente de Instantâneo, formatada como HHMMSS. *active_end_time_of_day* é **int**, sem padrão.  
  
 [  **@snapshot_job_name =** ] **'***snapshot_agent_name***'**  
 É o nome de um trabalho existente do Agente de Instantâneo se um trabalho existente estiver sendo usado. *snapshot_agent_name* é **nvarchar (100)**, sem padrão.  
  
 [ **@publisher_security_mode**=] *publisher_security_mode*  
 É o modo de segurança usado pelo agente ao conectar-se ao Publicador. *publisher_security_mode* é **int**, sem padrão. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação, e **1** Especifica autenticação do Windows. Um valor de **0** devem ser especificados para não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [ **@publisher_login**=] **'***publisher_login***'**  
 É o logon usado na conexão com o Publicador. *publisher_login* é **sysname**, sem padrão. *publisher_login* deve ser especificado quando *publisher_security_mode* é **0**. Se *publisher_login* é NULL e o publicador*_ * * security_mode* é **1**, em seguida, a conta do Windows especificada na *job_login* será usado ao conectar-se ao publicador.  
  
 [ **@publisher_password**=] **'***publisher_password***'**  
 É a senha usada ao conectar-se ao Publicador. *publisher_password* é **nvarchar (524)**, sem padrão.  
  
> [!IMPORTANT]  
>  Não armazene informações de autenticação em arquivos de script. Para ajudar a melhorar a segurança, recomendamos que você forneça nomes de login e senhas em tempo de execução.  
  
 [ **@job_login**=] **'***job_login***'**  
 É o logon da conta do Windows na qual o agente é executado. *job_login* é **nvarchar (257)**, sem padrão. Essa conta do Windows sempre é usada para conexões de agente com o Distribuidor. Você deve fornecer esse parâmetro ao criar um novo trabalho do Agente de Instantâneo. *Isso não pode ser alterado para não* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *publicador.*  
  
 [ **@job_password**=] **'***job_password***'**  
 É a senha da conta do Windows na qual o agente é executado. *job_password* é **sysname**, sem padrão. Você deve fornecer esse parâmetro ao criar um novo trabalho do Agente de Instantâneo.  
  
> [!IMPORTANT]  
>  Não armazene informações de autenticação em arquivos de script. Para ajudar a melhorar a segurança, recomendamos que você forneça nomes de login e senhas em tempo de execução.  
  
 [ **@publisher_type**=] **'***publisher_type***'**  
 Especifica o tipo de Publicador quando o Publicador não está sendo executado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publisher_type* é **sysname**, e pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|Especifica um Editor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|Especifica um Publicador Oracle padrão.|  
|**ORACLE GATEWAY**|Especifica um Editor Oracle Gateway.|  
  
 Para obter mais informações sobre as diferenças entre um publicador Oracle e um publicador Oracle Gateway, consulte [visão geral da publicação Oracle](../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_MSchange_snapshot_agent_properties** é usado em replicação de instantâneo, replicação transacional e replicação de mesclagem.  
  
 Você deve especificar todos os parâmetros ao executar **sp_MSchange_snapshot_agent_properties**. Executar [sp_helppublication_snapshot](../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md) para retornar as propriedades atuais do trabalho do Snapshot Agent.  
  
 Quando o publicador é executado em uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou versão posterior, você deve usar [sp_changepublication_snapshot](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md) para alterar as propriedades de um trabalho do agente de instantâneo.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa no distribuidor **sp_MSchange_snapshot_agent_properties**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
  
