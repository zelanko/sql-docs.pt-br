---
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
ms.openlocfilehash: d0bd62fe3462441d4eab9d3d89bce20cf1144131
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909561"
---
# <a name="sp_change_log_shipping_secondary_database-transact-sql"></a>sp_change_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as configurações do banco de dados secundário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @restore_delay = ] 'restore_delay'` o período de tempo, em minutos, que o servidor secundário aguarda antes de restaurar um determinado arquivo de backup. *restore_delay* é **int** e não pode ser nulo. O valor padrão é 0.  
  
`[ @restore_all = ] 'restore_all'` se definido como 1, o servidor secundário restaura todos os backups de log de transações disponíveis quando o trabalho de restauração é executado. Caso contrário, ele parará após a restauração de um arquivo. *restore_all* é **bit** e não pode ser nulo.  
  
`[ @restore_mode = ] 'restore_mode'` o modo de restauração para o banco de dados secundário.  
  
 0 = restaure o log NORECOVERY.  
  
 1 = restaure o log de restauração com STANDBY.  
  
 *Restore* é **bit** e não pode ser nulo.  
  
`[ @disconnect_users = ] 'disconnect_users'` se definido como 1, os usuários serão desconectados do banco de dados secundário quando uma operação de restauração for executada. Padrão = 0. *disconnect_users* é **bit** e não pode ser nulo.  
  
`[ @block_size = ] 'block_size'` o tamanho, em bytes, que é usado como o tamanho do bloco para o dispositivo de backup. *block_size* é **int** com um valor padrão de-1.  
  
`[ @buffer_count = ] 'buffer_count'` o número total de buffers usados pela operação de backup ou restauração. *buffer_count* é **int** com um valor padrão de-1.  
  
`[ @max_transfer_size = ] 'max_transfer_size'` o tamanho, em bytes, da solicitação máxima de entrada ou saída emitida pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o dispositivo de backup. *max_transfersize* é **int** e pode ser NULL.  
  
`[ @restore_threshold = ] 'restore_threshold'` o número de minutos permitido para decorrer entre as operações de restauração antes de um alerta ser gerado. *restore_threshold* é **int** e não pode ser nulo.  
  
`[ @threshold_alert = ] 'threshold_alert'` é o alerta a ser gerado quando o limite de restauração é excedido. *threshold_alert* é **int**, com um padrão de 14420.  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'` especifica se um alerta será gerado quando *restore_threshold*for excedido. 1 = habilitado; 0 = desabilitado. *threshold_alert_enabled* é **bit** e não pode ser nulo.  
  
`[ @history_retention_period = ] 'history_retention_period'` é o período em minutos em que o histórico será retido. *history_retention_period* é **int**. Um valor de 1440 será usado se nenhum for especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Remarks  
 **sp_change_log_shipping_secondary_database** deve ser executado a partir do banco de dados **mestre** no servidor secundário. Esse procedimento armazenado faz o seguinte:  
  
1.  Altera as configurações nos registros **log_shipping_secondary_database** , conforme necessário.  
  
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
  
  
