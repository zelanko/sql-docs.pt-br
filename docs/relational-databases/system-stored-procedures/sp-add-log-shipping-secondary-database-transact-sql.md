---
title: sp_add_log_shipping_secondary_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_secondary_database
- sp_add_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_secondary_database
ms.assetid: d29e1c24-3a3c-47a4-a726-4584afa6038a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e26fa9b22578d91636eb554c75a55f184869d529
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68046215"
---
# <a name="sp_add_log_shipping_secondary_database-transact-sql"></a>sp_add_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Configura um banco de dados secundário para o envio de logs.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_add_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database',  
[ @primary_server = ] 'primary_server',   
[ @primary_database = ] 'primary_database',  
[, [ @restore_delay = ] 'restore_delay']  
[, [ @restore_all = ] 'restore_all']  
[, [ @restore_mode = ] 'restore_mode']  
[, [ @disconnect_users = ] 'disconnect_users']  
[, [ @block_size = ] 'block_size']  
[, [ @buffer_count = ] 'buffer_count']  
[, [ @max_transfer_size = ] 'max_transfer_size']  
[, [ @restore_threshold = ] 'restore_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @secondary_database = ] 'secondary_database'`É o nome do banco de dados secundário. *secondary_database* é **sysname**, sem padrão.  
  
`[ @primary_server = ] 'primary_server'`O nome da instância primária do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] na configuração de envio de logs. *primary_server* é **sysname** e não pode ser nulo.  
  
`[ @primary_database = ] 'primary_database'`É o nome do banco de dados no servidor primário. *primary_database* é **sysname**, sem padrão.  
  
`[ @restore_delay = ] 'restore_delay'`A quantidade de tempo, em minutos, que o servidor secundário aguarda antes de restaurar um determinado arquivo de backup. *restore_delay* é **int** e não pode ser NULL. O valor padrão é 0.  
  
`[ @restore_all = ] 'restore_all'`Se definido como 1, o servidor secundário restaura todos os backups de log de transações disponíveis quando o trabalho de restauração é executado. Caso contrário, ele será interrompido depois que um arquivo for restaurado. *restore_all* é **bit** e não pode ser nulo.  
  
`[ @restore_mode = ] 'restore_mode'`O modo de restauração do banco de dados secundário.  
  
 0 = Log de restauração com NORECOVERY.  
  
 1 = restaure o log de restauração com STANDBY.  
  
 *Restore* é **bit** e não pode ser nulo.  
  
`[ @disconnect_users = ] 'disconnect_users'`Se definido como 1, os usuários serão desconectados do banco de dados secundário quando uma operação de restauração for executada. Padrão = 0. a *desconexão* de usuários é **bit** e não pode ser nula.  
  
`[ @block_size = ] 'block_size'`O tamanho, em bytes, que é usado como o tamanho do bloco para o dispositivo de backup. *block_size* é **int** com um valor padrão de-1.  
  
`[ @buffer_count = ] 'buffer_count'`O número total de buffers usados pela operação de backup ou restauração. *buffer_count* é **int** com um valor padrão de-1.  
  
`[ @max_transfer_size = ] 'max_transfer_size'`O tamanho, em bytes, da solicitação de entrada ou saída máxima que é emitida [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pelo para o dispositivo de backup. *max_transfersize* é **int** e pode ser NULL.  
  
`[ @restore_threshold = ] 'restore_threshold'`O número de minutos permitido para decorrer entre as operações de restauração antes de um alerta ser gerado. *restore_threshold* é **int** e não pode ser NULL.  
  
`[ @threshold_alert = ] 'threshold_alert'`O alerta será gerado quando o limite de backup for excedido. *threshold_alert* é **int**, com um padrão de 14.420.  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'`Especifica se um alerta é gerado quando *backup_threshold* é excedido. O valor de um (1), padrão, significa que o alerta é emitido. *threshold_alert_enabled* é **bit**.  
  
`[ @history_retention_period = ] 'history_retention_period'`É o período de tempo em minutos em que o histórico é retido. *history_retention_period* é **int**, com um padrão de NULL. O valor 14420 será usado se nenhum valor for especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_add_log_shipping_secondary_database** deve ser executado do banco de dados **mestre** no servidor secundário. Esse procedimento armazenado faz o seguinte:  
  
1.  **sp_add_log_shipping_secondary_primary** deve ser chamado antes desse procedimento armazenado para inicializar as informações do banco de dados de envio de log primário no servidor secundário.  
  
2.  Adiciona uma entrada para o banco de dados secundário no **log_shipping_secondary_databases** usando os argumentos fornecidos.  
  
3.  Adiciona um registro de monitor local em **log_shipping_monitor_secondary** no servidor secundário usando argumentos fornecidos.  
  
4.  Se o servidor monitor for diferente do servidor secundário, o adicionará um registro de monitor em **log_shipping_monitor_secondary** no servidor monitor usando os argumentos fornecidos.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo ilustra o uso do procedimento armazenado **sp_add_log_shipping_secondary_database** para adicionar o banco de dados **LogShipAdventureWorks** como um banco de dados secundário em uma configuração de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] envio de logs com o banco de dados primário que reside no servidor primário Tribeca.  
  
```  
EXEC master.dbo.sp_add_log_shipping_secondary_database   
@secondary_database = N'LogShipAdventureWorks'   
,@primary_server = N'TRIBECA'   
,@primary_database = N'AdventureWorks2012'   
,@restore_delay = 0   
,@restore_mode = 1   
,@disconnect_users = 0   
,@restore_threshold = 45     
,@threshold_alert_enabled = 0   
,@history_retention_period = 1440 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
