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
manager: craigg
ms.openlocfilehash: 5af98bd479738785c341b2618561eaab3f43b5d1
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67586015"
---
# <a name="spchangelogshippingsecondarydatabase-transact-sql"></a>sp_change_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as configurações do banco de dados secundário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @restore_delay = ] 'restore_delay'` A quantidade de tempo, em minutos, em que o servidor secundário espera antes de restaurar um determinado arquivo de backup. *restore_delay* está **int** e não pode ser NULL. O valor padrão é 0.  
  
`[ @restore_all = ] 'restore_all'` Se definido como 1, o servidor secundário restaura todos os backups de log de transações disponíveis quando o trabalho de restauração é executada. Caso contrário, ele será interrompido depois de um arquivo foi restaurado. *restore_all* está **bit** e não pode ser NULL.  
  
`[ @restore_mode = ] 'restore_mode'` O modo de restauração de banco de dados secundário.  
  
 0 = restaure o log NORECOVERY.  
  
 1 = restaure o log de restauração com STANDBY.  
  
 *Restaure* está **bit** e não pode ser NULL.  
  
`[ @disconnect_users = ] 'disconnect_users'` Se definido como 1, os usuários estiver desconectado do banco de dados secundário quando uma operação de restauração é executada. Padrão = 0. *disconnect_users* está **bit** e não pode ser NULL.  
  
`[ @block_size = ] 'block_size'` O tamanho, em bytes, que é usado como o tamanho do bloco para o dispositivo de backup. *block_size* está **int** com um valor padrão de -1.  
  
`[ @buffer_count = ] 'buffer_count'` O número total de buffers usados pela operação de backup ou restauração. *buffer_count* está **int** com um valor padrão de -1.  
  
`[ @max_transfer_size = ] 'max_transfer_size'` O tamanho, em bytes, da entrada máximo ou solicitação de saída que é emitida por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o dispositivo de backup. *max_transfersize* está **int** e pode ser NULL.  
  
`[ @restore_threshold = ] 'restore_threshold'` O número de minutos permitidos a decorrer entre operações de restauração antes que um alerta seja gerado. *restore_threshold* está **int** e não pode ser NULL.  
  
`[ @threshold_alert = ] 'threshold_alert'` É o alerta a ser emitido quando o limite de restauração é excedido. *alerta de limite* está **int**, com um padrão de 14.420.  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'` Especifica se um alerta será gerado quando *restore_threshold*for excedido. 1 = habilitado; 0 = desabilitado. *threshold_alert_enabled* está **bit** e não pode ser NULL.  
  
`[ @history_retention_period = ] 'history_retention_period'` É o período de tempo em minutos no qual o histórico será retido. *history_retention_period* está **int**. Um valor de 1440 será usado se nenhum for especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentários  
 **sp_change_log_shipping_secondary_database** deve ser executado a partir de **mestre** banco de dados no servidor secundário. Esse procedimento armazenado faz o seguinte:  
  
1.  Altera as configurações na **log_shipping_secondary_database** registra conforme necessário.  
  
2.  Altera o registro de monitor local na **log_shipping_monitor_secondary** no servidor secundário usando os argumentos fornecidos, se necessário.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa pode executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo ilustra o uso **sp_change_log_shipping_secondary_database** para atualizar os parâmetros de banco de dados secundário para o banco de dados **LogShipAdventureWorks**.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
