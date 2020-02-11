---
title: sp_help_log_shipping_monitor_secondary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_monitor_secondary
- sp_help_log_shipping_monitor_secondary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_monitor_secondary
ms.assetid: 3ac091ea-c9a8-4c05-a0b6-1ccf4e001339
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b1acf456bda88eeee0493d3f9d7ccc063a5bda50
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68001010"
---
# <a name="sp_help_log_shipping_monitor_secondary-transact-sql"></a>sp_help_log_shipping_monitor_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações relativas a um banco de dados secundário das tabelas de monitor.  
  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_log_shipping_monitor_secondary  
[ @secondary_server = ] 'secondary_server',  
[ @secondary_database = ] 'secondary_database'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @secondary_server = ] 'secondary_server'`É o nome do servidor secundário. *secondary_server* é **sysname**, sem padrão.  
  
`[ @secondary_database = ] 'secondary_database'`É o nome do banco de dados secundário. *secondary_database* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Coluna|DESCRIÇÃO|  
|------------|-----------------|  
|**secondary_server**|O nome da instância secundária do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] na configuração de envio de logs.|  
|**secondary_database**|Nome do banco de dados secundário na configuração de envio de logs.|  
|**secondary_id**|ID de servidor secundário na configuração de envio de logs.|  
|**primary_server**|Nome da instância primária do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] na configuração de envio de logs.|  
|**primary_database**|O nome do banco de dados primário na configuração de envio de log.|  
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
  
## <a name="remarks"></a>Comentários  
 **sp_help_log_shipping_monitor_secondary** deve ser executado do banco de dados **mestre** no servidor monitor.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar esse procedimento.  
  
## <a name="see-also"></a>Confira também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
