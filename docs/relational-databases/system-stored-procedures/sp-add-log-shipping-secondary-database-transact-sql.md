---
title: sp_add_log_shipping_secondary_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_secondary_database
- sp_add_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_secondary_database
ms.assetid: d29e1c24-3a3c-47a4-a726-4584afa6038a
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 70abdc5cb67beeb779af3722d3b5e7f91b923e21
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33239776"
---
# <a name="spaddlogshippingsecondarydatabase-transact-sql"></a>sp_add_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Configura um banco de dados secundário para o envio de logs.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@secondary_database** =] '*secondary_database*'  
 É o nome do banco de dados secundário. *secondary_database* é **sysname**, sem padrão.  
  
 [ **@primary_server** =] '*primary_server*'  
 O nome da instância primária do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] na configuração de envio de logs. *primary_server* é **sysname** e não pode ser NULL.  
  
 [ **@primary_database** =] '*primary_database*'  
 É o nome do banco de dados do servidor primário. *primary_database* é **sysname**, sem padrão.  
  
 [ **@restore_delay** =] '*restore_delay*'  
 A quantidade de tempo, em minutos, que o servidor secundário espera antes de restaurar um determinado arquivo de backup. *restore_delay* é **int** e não pode ser NULL. O valor padrão é 0.  
  
 [ **@restore_all** =] '*restore_all*'  
 Se definido como 1, o servidor secundário restaura todos os backups de log de transações disponíveis quando o trabalho de restauração é executado. Caso contrário, ele será interrompido depois que um arquivo for restaurado. *restore_all* é **bit** e não pode ser NULL.  
  
 [ **@restore_mode** =] '*restore_mode*'  
 O modo de restauração do banco de dados secundário.  
  
 0 = Log de restauração com NORECOVERY.  
  
 1 = restaure o log de restauração com STANDBY.  
  
 *Restaurar* é **bit** e não pode ser NULL.  
  
 [ **@disconnect_users** =] '*disconnect_users*'  
 Se definido como 1, os usuários são desconectados do banco de dados secundário quando uma operação de restauração é executada. Padrão = 0. *Desconectar* usuários é **bit** e não pode ser NULL.  
  
 [ **@block_size** =] '*block_size*'  
 Tamanho, em bytes, usado como tamanho de bloco para o dispositivo de backup. *block_size* é **int** com um valor padrão de -1.  
  
 [ **@buffer_count** =] '*buffer_count*'  
 Número total de buffers usado pela operação de backup ou restauração. *buffer_count* é **int** com um valor padrão de -1.  
  
 [ **@max_transfer_size** =] '*max_transfer_size*'  
 O tamanho, em bytes, da solicitação máxima de entrada ou de saída emitida por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o dispositivo de backup. *max_transfersize* é **int** e pode ser NULL.  
  
 [ **@restore_threshold** =] '*restore_threshold*'  
 Número de minutos permitidos a decorrer entre operações de restauração antes que um alerta seja gerado. *restore_threshold* é **int** e não pode ser NULL.  
  
 [ **@threshold_alert** =] '*threshold_alert*'  
 É o alerta a ser gerado quando o limite do backup for excedido. *threshold_alert* é **int**, com um padrão de 14.420.  
  
 [ **@threshold_alert_enabled** =] '*threshold_alert_enabled*'  
 Especifica se um alerta é gerado quando *backup_threshold* for excedido. O valor de um (1), padrão, significa que o alerta é emitido. *threshold_alert_enabled* é **bit**.  
  
 [ **@history_retention_period** =] '*history_retention_period*'  
 É o período em minutos no qual o histórico é retido. *history_retention_period* é **int**, com um padrão NULL. O valor 14420 será usado se nenhum valor for especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 **sp_add_log_shipping_secondary_database** deve ser executado a partir de **mestre** banco de dados no servidor secundário. Esse procedimento armazenado faz o seguinte:  
  
1.  **sp_add_log_shipping_secondary_primary** deve ser chamado antes deste procedimento armazenado para inicializar as informações de banco de dados no servidor secundário de envio de logs primário.  
  
2.  Adiciona uma entrada para o banco de dados secundário em **log_shipping_secondary_databases** usando os argumentos fornecidos.  
  
3.  Adiciona um registro de monitor local em **log_shipping_monitor_secondary** no servidor secundário usando os argumentos fornecidos.  
  
4.  Se o servidor monitor for diferente do servidor secundário, adiciona um registro de monitor em **log_shipping_monitor_secondary** no monitor de servidor usando os argumentos fornecidos.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função fixa de servidor pode executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo ilustra o uso de **sp_add_log_shipping_secondary_database** procedimento armazenado para adicionar o banco de dados **LogShipAdventureWorks** como um banco de dados secundário em uma configuração de envio de logs com o banco de dados primário [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] que reside no servidor primário TRIBECA.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Sobre o envio de logs & #40; SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
