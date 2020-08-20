---
description: log_shipping_secondary_databases (Transact-SQL)
title: log_shipping_secondary_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_secondary_databases_TSQL
- log_shipping_secondary_databases
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_secondary_databases system table
ms.assetid: ba2374af-86b8-480c-a10c-51e7c4e3ae23
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cee2eca7d0f75b6a27c17056f70195f3aae14d99
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488849"
---
# <a name="log_shipping_secondary_databases-transact-sql"></a>log_shipping_secondary_databases (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Armazena um registro para o banco de dados secundário em uma configuração de envio de logs. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**secondary_database**|**sysname**|Nome do banco de dados secundário na configuração de envio de logs.|  
|**secondary_id**|**uniqueidentifier**|ID de servidor secundário na configuração de envio de logs.|  
|**restore_delay**|**int**|Período, em minutos, em que o servidor secundário aguardará para restaurar um determinado arquivo de backup. O padrão é 0 minuto.|  
|**restore_all**|**bit**|Se definido como 1, o servidor secundário restaurará todos os backups de log de transações disponíveis quando o trabalho de restauração for executado. Caso contrário, ele parará após a restauração de um arquivo.|  
|**restore_mode**|**bit**|O modo de restauração do banco de dados secundário.<br /><br /> 0 = Log de restauração com NORECOVERY.<br /><br /> 1 = Log de restauração com STANDBY.|  
|**disconnect_users**|**bit**|Se definido como 1, os usuários serão desconectados do banco de dados secundário quando uma operação de restauração for executada. O padrão = 0.|  
|**block_size**|**int**|Tamanho, em bytes, usado como tamanho de bloco para o dispositivo de backup.|  
|**buffer_count**|**int**|Número total de buffers usado pela operação de backup ou restauração.|  
|**max_transfer_size**|**int**|O tamanho, em bytes, da solicitação máxima de entrada ou de saída emitida por [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o dispositivo de backup.|  
|**last_restored_file**|**nvarchar (500)**|Nome do último arquivo de backup restaurado no banco de dados secundário.|  
|**last_restored_date**|**datetime**|Hora e data da última operação de restauração no banco de dados secundário.|  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [&#41;&#40;Transact-SQL de sp_add_log_shipping_secondary_database ](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_log_shipping_secondary_database ](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [log_shipping_secondary &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-secondary-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
