---
description: sp_change_log_shipping_secondary_database (Transact-SQL)
title: sp_change_log_shipping_secondary_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_database
- sp_change_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_database
ms.assetid: 3ebcf2f1-980f-4543-a84b-fbaeea54eeac
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5fc10c705564c88fe157860d00a61fa5ea682cc0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486260"
---
# <a name="sp_change_log_shipping_secondary_database-transact-sql"></a>sp_change_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Altera as configurações do banco de dados secundário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_change_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database',  
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
`[ @restore_delay = ] 'restore_delay'` A quantidade de tempo, em minutos, que o servidor secundário aguarda antes de restaurar um determinado arquivo de backup. *restore_delay* é **int** e não pode ser NULL. O valor padrão é 0.  
  
`[ @restore_all = ] 'restore_all'` Se definido como 1, o servidor secundário restaura todos os backups de log de transações disponíveis quando o trabalho de restauração é executado. Caso contrário, ele parará após a restauração de um arquivo. *restore_all* é **bit** e não pode ser nulo.  
  
`[ @restore_mode = ] 'restore_mode'` O modo de restauração do banco de dados secundário.  
  
 0 = restaure o log NORECOVERY.  
  
 1 = restaure o log de restauração com STANDBY.  
  
 *Restore* é **bit** e não pode ser nulo.  
  
`[ @disconnect_users = ] 'disconnect_users'` Se definido como 1, os usuários serão desconectados do banco de dados secundário quando uma operação de restauração for executada. Padrão = 0. *disconnect_users* é **bit** e não pode ser nulo.  
  
`[ @block_size = ] 'block_size'` O tamanho, em bytes, que é usado como o tamanho do bloco para o dispositivo de backup. *block_size* é **int** com um valor padrão de-1.  
  
`[ @buffer_count = ] 'buffer_count'` O número total de buffers usados pela operação de backup ou restauração. *buffer_count* é **int** com um valor padrão de-1.  
  
`[ @max_transfer_size = ] 'max_transfer_size'` O tamanho, em bytes, da solicitação de entrada ou saída máxima que é emitida pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o dispositivo de backup. *max_transfersize* é **int** e pode ser NULL.  
  
`[ @restore_threshold = ] 'restore_threshold'` O número de minutos permitido para decorrer entre as operações de restauração antes de um alerta ser gerado. *restore_threshold* é **int** e não pode ser NULL.  
  
`[ @threshold_alert = ] 'threshold_alert'` É o alerta a ser gerado quando o limite de restauração é excedido. *threshold_alert* é **int**, com um padrão de 14420.  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'` Especifica se um alerta será gerado quando *restore_threshold*for excedido. 1 = habilitado; 0 = desabilitado. *threshold_alert_enabled* é **bit** e não pode ser nulo.  
  
`[ @history_retention_period = ] 'history_retention_period'` É o período em minutos em que o histórico será retido. *history_retention_period* é **int**. Um valor de 1440 será usado se nenhum for especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_change_log_shipping_secondary_database** deve ser executado do banco de dados **mestre** no servidor secundário. Esse procedimento armazenado faz o seguinte:  
  
1.  Altera as configurações na **log_shipping_secondary_database** registros conforme necessário.  
  
2.  Altera o registro de monitor local em **log_shipping_monitor_secondary** no servidor secundário usando argumentos fornecidos, se necessário.  

## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo ilustra o uso de **sp_change_log_shipping_secondary_database** para atualizar parâmetros de banco de dados secundário para o banco de dados **LogShipAdventureWorks**.  
  
```  
EXEC master.dbo.sp_change_log_shipping_secondary_database   
 @secondary_database =  'LogShipAdventureWorks'  
,  @restore_delay = 0  
,  @restore_all = 1  
,  @restore_mode = 0  
,  @disconnect_users = 0  
,  @threshold_alert = 14420  
,  @threshold_alert_enabled = 1  
,  @history_retention_period = 14420;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
