---
title: sp_change_log_shipping_secondary_database (Transact-SQL) | Microsoft Docs
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
- sp_change_log_shipping_secondary_database
- sp_change_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_database
ms.assetid: 3ebcf2f1-980f-4543-a84b-fbaeea54eeac
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5e4ee6324e92130f3f887fe3a36ecd5469cd9d99
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33239136"
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
 [  **@restore_delay =** ] '*restore_delay*'  
 A quantidade de tempo, em minutos, que o servidor secundário espera antes de restaurar um determinado arquivo de backup. *restore_delay* é **int** e não pode ser NULL. O valor padrão é 0.  
  
 [  **@restore_all =** ] '*restore_all*'  
 Se definido como 1, o servidor secundário restaura todos os backups de log de transações disponíveis quando o trabalho de restauração é executado. Caso contrário, ele será interrompido depois de um arquivo foi restaurado. *restore_all* é **bit** e não pode ser NULL.  
  
 [  **@restore_mode =** ] '*restore_mode*'  
 O modo de restauração do banco de dados secundário.  
  
 0 = restaure o log NORECOVERY.  
  
 1 = restaure o log de restauração com STANDBY.  
  
 *Restaurar* é **bit** e não pode ser NULL.  
  
 [  **@disconnect_users =** ] '*disconnect_users*'  
 Se definido em 1, os usuários são desconectados de um banco de dados secundários quando a operação de restauração é executada. Padrão = 0. *disconnect_users* é **bit** e não pode ser NULL.  
  
 [  **@block_size =** ] '*block_size*'  
 Tamanho, em bytes, usado como tamanho de bloco para o dispositivo de backup. *block_size* é **int** com um valor padrão de -1.  
  
 [  **@buffer_count =** ] '*buffer_count*'  
 Número total de buffers usado pela operação de backup ou restauração. *buffer_count* é **int** com um valor padrão de -1.  
  
 [  **@max_transfer_size =** ] '*max_transfer_size*'  
 O tamanho, em bytes, da solicitação máxima de entrada ou de saída emitida por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o dispositivo de backup. *max_transfersize* é **int** e pode ser NULL.  
  
 [  **@restore_threshold =** ] '*restore_threshold*'  
 Número de minutos permitidos a decorrer entre operações de restauração antes que um alerta seja gerado. *restore_threshold* é **int** e não pode ser NULL.  
  
 [  **@threshold_alert =** ] '*threshold_alert*'  
 É o alerta a ser gerado quando o limite da restauração é excedido. *threshold_alert* é **int**, com um padrão de 14.420.  
  
 [  **@threshold_alert_enabled =** ] '*threshold_alert_enabled*'  
 Especifica se um alerta será gerado quando *restore_threshold*for excedido. 1 = habilitado; 0 = desabilitado. *threshold_alert_enabled* é **bit** e não pode ser NULL.  
  
 [  **@history_retention_period =** ] '*history_retention_period*'  
 É a duração de tempo em minutos na qual o histórico será retido. *history_retention_period* é **int**. Um valor de 1440 será usado se nenhum for especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 **sp_change_log_shipping_secondary_database** deve ser executado a partir de **mestre** banco de dados no servidor secundário. Esse procedimento armazenado faz o seguinte:  
  
1.  Altera as configurações de **log_shipping_secondary_database** registra conforme necessário.  
  
2.  Altera o registro de monitor local em **log_shipping_monitor_secondary** no servidor secundário usando os argumentos fornecidos, se necessário.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função fixa de servidor pode executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo ilustra o uso **sp_change_log_shipping_secondary_database** para atualizar parâmetros de banco de dados secundário para o banco de dados **LogShipAdventureWorks**.  
  
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
 [Sobre o envio de logs & #40; SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
