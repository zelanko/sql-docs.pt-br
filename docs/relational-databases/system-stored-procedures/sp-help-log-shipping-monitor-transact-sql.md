---
title: sp_help_log_shipping_monitor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_monitor_TSQL
- sp_help_log_shipping_monitor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_monitor
ms.assetid: a4e96c45-6dcd-471a-a494-b5c619459855
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b8a1029c6423c90fc131ce2a5326ec69781308f6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelplogshippingmonitor-transact-sql"></a>sp_help_log_shipping_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna um conjunto de resultados contendo informações de status e outras informações para bancos de dados primários e secundário registrados, em um primário, secundário ou servidor monitor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_log_shipping_monitor  
```  
  
## <a name="arguments"></a>Argumentos  
 Nenhuma.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**status**|**bit**|Status coletivo de agentes para banco de dados de envio de logs:<br /><br /> **0** = falhas íntegras e não-agente.<br /><br /> **1** = outros.|  
|**is_primary**|**bit**|Indica se essa linha é para um banco de dados primário:<br /><br /> **1** = a linha é para um banco de dados primário.<br /><br /> **0** = a linha é um banco de dados secundário.|  
|**server**|**sysname**|Nome do servidor primário ou secundário em que esse banco de dados reside.|  
|**database_name**|**sysname**|Nome do banco de dados.|  
|**time_since_last_backup**|**Int**|Período, em minutos, desde o último backup de log.<br /><br /> NULL = As informações não estão disponíveis ou não são relevantes.|  
|**last_backup_file**|**nvarchar(500)**|Nome do último arquivo de backup de log com êxito.<br /><br /> NULL = As informações não estão disponíveis ou não são relevantes.|  
|**backup_threshold**|**Int**|O período de tempo, em minutos, depois do último backup antes que um erro de alerta de limite seja gerado. **backup_threshold** é **int**, com um padrão de **60 minutos**.<br /><br /> NULL = As informações não estão disponíveis ou não são relevantes.<br /><br /> Esse valor pode ser alterado usando [sp_add_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md).|  
|**is_backup_alert_enabled**|**bit**|Especifica se um alerta será gerado quando **backup_threshold** for excedido. O valor de um (**1**), o padrão, significa que o alerta será gerado.<br /><br /> NULL = As informações não estão disponíveis ou não são relevantes.<br /><br /> Esse valor pode ser alterado usando [sp_add_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md).|  
|**time_since_last_copy**|**Int**|Período, em minutos, desde que o último backup de log foi copiado.<br /><br /> NULL = As informações não estão disponíveis ou não são relevantes.|  
|**last_copied_file**|**nvarchar(500)**|Nome do último arquivo de backup de log copiado com êxito.<br /><br /> NULL = As informações não estão disponíveis ou não são relevantes.|  
|**time_since_last_restore**|**Int**|Período, em minutos, desde que o último backup de log foi restaurado.<br /><br /> NULL = As informações não estão disponíveis ou não são relevantes.|  
|**last_restored_file**|**nvarchar(500).**|Nome do último arquivo de backup de log restaurado com êxito.<br /><br /> NULL = As informações não estão disponíveis ou não são relevantes.|  
|**last_restored_latency**|**Int**|Período, em minutos, desde a criação do último backup para restaurar o backup.<br /><br /> NULL = As informações não estão disponíveis ou não são relevantes.|  
|**restore_threshold**|**Int**|Número de minutos permitidos a decorrer entre operações de restauração antes que um alerta seja gerado. **restore_threshold** não pode ser NULL.|  
|**is_restore_alert_enabled**|**bit**|Especifica se um alerta é gerado quando **restore_threshold** for excedido. O valor de um (**1**), o padrão, significa que o alerta é gerado.<br /><br /> NULL = As informações não estão disponíveis ou não são relevantes.<br /><br /> Para definir o limite de restauração, use [sp_add_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md).|  
  
## <a name="remarks"></a>Remarks  
 **sp_help_log_shipping_monitor** deve ser executado a partir de **mestre** banco de dados no servidor monitor.  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="see-also"></a>Consulte também  
 [Sobre o envio de logs & #40; SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
