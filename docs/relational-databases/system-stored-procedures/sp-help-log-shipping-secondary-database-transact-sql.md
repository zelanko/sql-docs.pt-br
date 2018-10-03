---
title: sp_help_log_shipping_secondary_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_secondary_database
- sp_help_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_secondary_database
ms.assetid: 11ce42ca-d3f1-44c8-9cac-214ca8896b9a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 19bac76afeb56bf196b7f717596777435d813f04
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47846424"
---
# <a name="sphelplogshippingsecondarydatabase-transact-sql"></a>sp_help_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esse procedimento armazenado recupera as configurações de um ou mais bancos de dados secundários.  
  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database' OR  
[ @secondary_id = ] 'secondary_id'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@secondary_database =** ] '*secondary_database*'  
 É o nome do banco de dados secundário. *secondary_database* está **sysname**, sem padrão.  
  
 [  **@secondary_id =** ] '*secondary_id*'  
 ID de servidor secundário na configuração de envio de logs. *secondary_id* está **uniqueidentifier** e não pode ser NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|**secondary_id**|ID de servidor secundário na configuração de envio de logs.|  
|**primary_server**|O nome da instância primária do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] na configuração de envio de logs.|  
|**primary_database**|O nome do banco de dados primário na configuração de envio de log.|  
|**backup_source_directory**|O diretório onde os arquivos de backup de log de transações do servidor primário são armazenados.|  
|**backup_destination_directory**|O diretório no servidor secundário onde arquivos de backup são copiados.|  
|**file_retention_period**|A quantidade de tempo, em minutos, que um arquivo de backup é mantido no servidor secundário antes de ser excluído.|  
|**copy_job_id**|A ID associada ao trabalho de cópia no servidor secundário.|  
|**restore_job_id**|A ID associada ao trabalho de restauração no servidor secundário.|  
|**monitor_server**|O nome da instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usado como servidor monitor na configuração de envio de log.|  
|**monitor_server_security_mode**|O modo de segurança usado para conexão ao servidor monitor.<br /><br /> 1 = Autenticação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.|  
|**secondary_database**|Nome do banco de dados secundário na configuração de envio de logs.|  
|**restore_delay**|A quantidade de tempo, em minutos, que o servidor secundário espera antes de restaurar um determinado arquivo de backup. O padrão é 0 minuto.|  
|**restore_all**|Se definido como 1, o servidor secundário restaura todos os backups de log de transações disponíveis quando o trabalho de restauração é executado. Caso contrário, ele será interrompido depois de um arquivo foi restaurado.|  
|**restore_mode**|O modo de restauração do banco de dados secundário.<br /><br /> 0 = Log de restauração com NORECOVERY.<br /><br /> 1 = Log de restauração com STANDBY.|  
|**disconnect_users**|Se definido como 1, os usuários são desconectados do banco de dados secundário quando uma operação de restauração é executada. Padrão = 0.|  
|**block_size**|Tamanho, em bytes, usado como tamanho de bloco para o dispositivo de backup.|  
|**buffer_count**|Número total de buffers usado pela operação de backup ou restauração.|  
|**max_transfer_size**|O tamanho, em bytes, da solicitação máxima de entrada ou de saída emitida por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o dispositivo de backup.|  
|**restore_threshold**|Número de minutos permitidos a decorrer entre operações de restauração antes que um alerta seja gerado.|  
|**threshold_alert**|Alerta a ser emitido quando o limite da restauração for excedido.|  
|**threshold_alert_enabled**|Determina se os alertas de limite de restauração estão habilitados.<br /><br /> 1 = Habilitado.<br /><br /> 0 = Desabilitado.|  
|**last_copied_file**|O nome do último arquivo de backup copiado para o servidor secundário.|  
|**last_copied_date**|A hora e a data da última operação de cópia para o servidor secundário.|  
|**last_copied_date_utc**|Hora e data da última operação de cópia no servidor secundário, expressa em UTC (Coordinated Universal Time).|  
|**last_restored_file**|Nome do último arquivo de backup restaurado no banco de dados secundário.|  
|**last_restored_date**|Hora e data da última operação de restauração no banco de dados secundário.|  
|**last_restored_date_utc**|Hora e data da última operação de restauração no banco de dados secundário, expressa em UTC (Coordinated Universal Time).|  
|**history_retention_period**|O período em minutos em que os registros de histórico de envio de logs são retidos em um determinado banco de dados secundário antes de serem excluídos.|  
|**last_restored_latency**|Período em minutos decorrido entre o momento de criação do backup de log no primário e o momento em que ele foi restaurado no secundário.<br /><br /> O valor inicial é NULL.|  
  
## <a name="remarks"></a>Comentários  
 Se você incluir a *secondary_database* parâmetro, o conjunto de resultados conterá informações sobre o banco de dados secundário; se você incluir a *secondary_id* parâmetro, o conjunto de resultados conterá informações sobre todos os bancos de dados secundários associados àquela identificação secundária.  
  
 **sp_help_log_shipping_secondary_database** deve ser executado a partir de **mestre** banco de dados no servidor secundário.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa pode executar esse procedimento.  
  
## <a name="see-also"></a>Consulte também  
 [sp_help_log_shipping_secondary_primary &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-primary-transact-sql.md)   
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
