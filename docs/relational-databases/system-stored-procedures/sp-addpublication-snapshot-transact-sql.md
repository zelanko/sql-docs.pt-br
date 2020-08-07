---
title: sp_addpublication_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpublication_snapshot_TSQL
- sp_addpublication_snapshot
helpviewer_keywords:
- sp_addpublication_snapshot
ms.assetid: 192b6214-df6e-44a3-bdd4-9d933a981619
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d8b5f827126afca81baeafe5f5c35e3d94666fcc
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87865254"
---
# <a name="sp_addpublication_snapshot-transact-sql"></a>sp_addpublication_snapshot (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Cria o Agente de Instantâneo para a publicação especificada. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!IMPORTANT]  
>  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addpublication_snapshot [ @publication= ] 'publication'  
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
  
`[ @frequency_type = ] frequency_type`É a frequência com a qual o Agente de Instantâneo é executado. *frequency_type* é **int**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez.|  
|**4** (padrão)|Diariamente.|  
|**8**|Semanalmente.|  
|**16**|Mensalmente.|  
|**32**|Mensalmente, relativo ao intervalo de frequência.|  
|**64**|Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent inicia.|  
|**128**|Executar quando o computador estiver ocioso|  
  
`[ @frequency_interval = ] frequency_interval`É o valor a ser aplicado à frequência definida por *frequency_type*. *frequency_interval* é **int**e pode ser um dos valores a seguir.  
  
|Valor de frequency_type|Efeito em frequency_interval|  
|------------------------------|-----------------------------------|  
|**1**|*frequency_interval* não é usado.|  
|**4** (padrão)|A cada *frequency_interval* dias, com um padrão de diariamente.|  
|**8**|*frequency_interval* é um ou mais dos itens a seguir (combinados com um operador lógico [&#124; (OR-bit)](../../t-sql/language-elements/bitwise-or-transact-sql.md) ):<br /><br /> **1** = domingo &#124;<br /><br /> **2** = segunda-feira &#124;<br /><br /> **4** = terça-feira &#124;<br /><br /> **8** = quarta-feira &#124;<br /><br /> **16** = quinta &#124;<br /><br /> **32** = sexta-feira &#124;<br /><br /> **64** = sábado|  
|**16**|No *frequency_interval* dia do mês.|  
|**32**|*frequency_interval* é um dos seguintes:<br /><br /> **1** = domingo &#124;<br /><br /> **2** = segunda-feira &#124;<br /><br /> **3** = terça-feira &#124;<br /><br /> **4** = quarta-feira &#124;<br /><br /> **5** = quinta &#124;<br /><br /> **6** = sexta-feira &#124;<br /><br /> **7** = sábado &#124;<br /><br /> **8** = dia &#124;<br /><br /> **9** = dia da semana &#124;<br /><br /> **10** = dia do fim de semana|  
|**64**|*frequency_interval* não é usado.|  
|**128**|*frequency_interval* não é usado.|  
  
`[ @frequency_subday = ] frequency_subday`É a unidade para *freq_subday_interval*. *frequency_subday* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4** (padrão)|Minuto|  
|**8**|Hora|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`É o intervalo para *frequency_subday*. *frequency_subday_interval* é **int**, com um padrão de 5, o que significa a cada 5 minutos.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`É a data em que o Agente de Instantâneo é executado. *frequency_relative_interval* é **int**, com um padrão de 1.  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`É o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor* é **int**, com um padrão de 0.  
  
`[ @active_start_date = ] active_start_date`É a data em que o Agente de Instantâneo é agendado pela primeira vez, formatado como AAAAMMDD. *active_start_date* é **int**, com um padrão de 0.  
  
`[ @active_end_date = ] active_end_date`É a data em que a Agente de Instantâneo para de ser agendada, formatada como AAAAMMDD. *active_end_date* é **int**, com um padrão de 99991231, o que significa 31 de dezembro de 9999.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`É a hora do dia em que o Agente de Instantâneo é agendado pela primeira vez, formatado como HHMMSS. *active_start_time_of_day* é **int**, com um padrão de 0.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`É a hora do dia em que a Agente de Instantâneo para de ser agendada, formatada como HHMMSS. *active_end_time_of_day* é **int**, com um padrão de 235959, o que significa 11:59:59 P.M. medida em um relógio de 24 horas.  
  
`[ @snapshot_job_name = ] 'snapshot_agent_name'`É o nome de um nome de trabalho de Agente de Instantâneo existente se um trabalho existente estiver sendo usado. *snapshot_agent_name* é **nvarchar (100)** com um valor padrão de NULL. Esse parâmetro é para uso interno e não deve ser especificado ao criar uma nova publicação. Se *snapshot_agent_name* for especificado, *job_login* e *job_password* deverão ser nulos.  
  
`[ @publisher_security_mode = ] publisher_security_mode`É o modo de segurança usado pelo agente ao se conectar ao Publicador. *publisher_security_mode* é **smallint**, com um padrão de 1. **0** especifica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação e **1** especifica a autenticação do Windows. Um valor de **0** deve ser especificado para não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'`É o logon usado ao conectar-se ao Publicador. *publisher_login* é **sysname**, com um padrão de NULL. *publisher_login* deve ser especificado quando *publisher_security_mode* é **0**. Se *publisher_login* for nulo e *publisher_security_mode* for **1**, a conta especificada em *job_login* será usada durante a conexão com o Publicador.  
  
`[ @publisher_password = ] 'publisher_password'`É a senha usada ao conectar-se ao Publicador. *publisher_password* é **sysname**, com um padrão de NULL.  
  
> [!IMPORTANT]  
>  Não armazene informações de autenticação em arquivos de script. Para ajudar a melhorar a segurança, recomendamos que você forneça nomes de login e senhas em tempo de execução.  
  
`[ @job_login = ] 'job_login'`É o logon da conta sob a qual o agente é executado. No Azure SQL Instância Gerenciada, use uma conta de SQL Server. *job_login* é **nvarchar (257)**, com um padrão de NULL. Essa conta é sempre usada para conexões de agente com o distribuidor. Você deve fornecer esse parâmetro ao criar um novo trabalho do Agente de Instantâneo.  
  
> [!NOTE]
>  Para não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores, esse deve ser o mesmo logon especificado em [Sp_adddistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md).  
  
`[ @job_password = ] 'job_password'`É a senha para a conta do Windows na qual o agente é executado. *job_password* é **sysname**, sem padrão. Você deve fornecer esse parâmetro ao criar um novo trabalho do Agente de Instantâneo.  
  
> [!IMPORTANT]  
>  Não armazene informações de autenticação em arquivos de script. Para ajudar a melhorar a segurança, recomendamos que você forneça nomes de login e senhas em tempo de execução.  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser usado ao criar um agente de instantâneo em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addpublication_snapshot** é usado na replicação de instantâneos, na replicação transacional e na replicação de mesclagem.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-snapsh_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_addpublication_snapshot**.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Criar e aplicar o instantâneo](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [&#41;&#40;Transact-SQL de sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changepublication_snapshot](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_startpublication_snapshot](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
