---
title: sp_add_log_shipping_secondary_primary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_secondary_primary_TSQL
- sp_add_log_shipping_secondary_primary
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_secondary_primary
ms.assetid: bfbbbee2-c255-4a59-a963-47d6e980a8e2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1768b25ccb4f0e4ad2e75f3d667123d082dd4237
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85879781"
---
# <a name="sp_add_log_shipping_secondary_primary-transact-sql"></a>sp_add_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Configura as informações primárias, adiciona links de monitor local e remoto e cria trabalhos de cópia e restauração no servidor secundário para o banco de dados primário especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_add_log_shipping_secondary_primary  
 [ @primary_server = ] 'primary_server',   
[ @primary_database = ] 'primary_database',  
[ @backup_source_directory = ] 'backup_source_directory' ,   
[ @backup_destination_directory = ] 'backup_destination_directory'  
[ @copy_job_name = ] 'copy_job_name'  
[ @restore_job_name = ] 'restore_job_name'  
[, [ @file_retention_period = ] 'file_retention_period']  
[, [ @monitor_server = ] 'monitor_server']  
[, [ @monitor_server_security_mode = ] 'monitor_server_security_mode']  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @copy_job_id = ] 'copy_job_id' OUTPUT ]  
[, [ @restore_job_id = ] 'restore_job_id' OUTPUT ]  
[, [ @secondary_id = ] 'secondary_id' OUTPUT]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @primary_server = ] 'primary_server'`O nome da instância primária do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] na configuração de envio de logs. *primary_server* é **sysname** e não pode ser nulo.  
  
`[ @primary_database = ] 'primary_database'`É o nome do banco de dados no servidor primário. *primary_database* é **sysname**, sem padrão.  
  
`[ @backup_source_directory = ] 'backup_source_directory'`O diretório em que os arquivos de backup de log de transações do servidor primário são armazenados. *backup_source_directory* é **nvarchar (500)** e não pode ser NULL.  
  
`[ @backup_destination_directory = ] 'backup_destination_directory'`O diretório no servidor secundário para onde os arquivos de backup são copiados. *backup_destination_directory* é **nvarchar (500)** e não pode ser NULL.  
  
`[ @copy_job_name = ] 'copy_job_name'`O nome a ser usado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalho do agente que está sendo criado para copiar backups de log de transações para o servidor secundário. *copy_job_name* é **sysname** e não pode ser nulo.  
  
`[ @restore_job_name = ] 'restore_job_name'`É o nome do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalho do agente no servidor secundário que restaura os backups para o banco de dados secundário. *restore_job_name* é **sysname** e não pode ser nulo.  
  
`[ @file_retention_period = ] 'file_retention_period'`O período de tempo, em minutos, que um arquivo de backup é mantido no servidor secundário no caminho especificado pelo @backup_destination_directory parâmetro antes de ser excluído. *history_retention_period* é **int**, com um padrão de NULL. Se nenhum valor for especificado, será usado o valor 14.420.  
  
`[ @monitor_server = ] 'monitor_server'`É o nome do servidor monitor. *Monitor_server* é **sysname**, sem padrão, e não pode ser nulo.  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'`O modo de segurança usado para se conectar ao servidor monitor.  
  
 1 = Autenticação do Windows.  
  
 0 = Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *monitor_server_security_mode* é **bit** e não pode ser nulo.  
  
`[ @monitor_server_login = ] 'monitor_server_login'`É o nome de usuário da conta usada para acessar o servidor monitor.  
  
`[ @monitor_server_password = ] 'monitor_server_password'`É a senha da conta usada para acessar o servidor monitor.  
  
`[ @copy_job_id = ] 'copy_job_id' OUTPUT`A ID associada ao trabalho de cópia no servidor secundário. *copy_job_id* é **uniqueidentifier** e não pode ser NULL.  
  
`[ @restore_job_id = ] 'restore_job_id' OUTPUT`A ID associada ao trabalho de restauração no servidor secundário. *restore_job_id* é **uniqueidentifier** e não pode ser NULL.  
  
`[ @secondary_id = ] 'secondary_id' OUTPUT`A ID do servidor secundário na configuração de envio de logs. *secondary_id* é **uniqueidentifier** e não pode ser NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_add_log_shipping_secondary_primary** deve ser executado do banco de dados **mestre** no servidor secundário. Esse procedimento armazenado faz o seguinte:  
  
1.  Gera uma ID secundária para o servidor primário especificado e o banco de dados primário.  
  
2.  Faz o seguinte:  

    1.  Adiciona uma entrada para a ID secundária em **log_shipping_secondary** usando os argumentos fornecidos.  
  
    2.  Cria um trabalho de cópia para a ID secundária que é desabilitada.  
  
    3.  Define a ID do trabalho de cópia na entrada de **log_shipping_secondary** para a ID de trabalho do trabalho de cópia.  
  
    4.  Cria um trabalho de restauração para a ID secundária que é desabilitada.  
  
    5.  Defina a ID do trabalho de restauração na entrada **log_shipping_secondary** para a ID do trabalho de restauração.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo ilustra o uso do procedimento armazenado **sp_add_log_shipping_secondary_primary** para configurar informações para o banco de dados primário [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] no servidor secundário.  
  
```  
EXEC master.dbo.sp_add_log_shipping_secondary_primary   
@primary_server = N'TRIBECA'   
,@primary_database = N'AdventureWorks'   
,@backup_source_directory = N'\\tribeca\LogShipping'   
,@backup_destination_directory = N''   
,@copy_job_name = N''   
,@restore_job_name = N''   
,@file_retention_period = 1440   
,@monitor_server = N'ROCKAWAY'   
,@monitor_server_security_mode = 1   
,@copy_job_id = @LS_Secondary__CopyJobId OUTPUT   
,@restore_job_id = @LS_Secondary__RestoreJobId OUTPUT   
,@secondary_id = @LS_Secondary__SecondaryId OUTPUT ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
