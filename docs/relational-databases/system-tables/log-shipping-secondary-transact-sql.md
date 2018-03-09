---
title: log_shipping_secondary (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- log_shipping_secondary
- log_shipping_secondary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_secondary system table
ms.assetid: 69723419-4544-49c6-a517-adb30ffa5741
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f66609b64ef7066fe7edf1ca8459d68cda597f9d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="logshippingsecondary-transact-sql"></a>log_shipping_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Armazena um registro por ID secundária. Essa tabela é armazenada no **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**secondary_id**|**uniqueidentifier**|ID de servidor secundário na configuração de envio de logs.|  
|**primary_server**|**sysname**|O nome da instância primária do Mecanismo de Banco de Dados do SQL Server em uma configuração de envio de log.|  
|**primary_database**|**sysname**|O nome do banco de dados primário na configuração de envio de log.|  
|**backup_source_directory**|**nvarchar(500)**|O diretório onde os arquivos de backup de log de transações do servidor primário são armazenados.|  
|**backup_destination_directory**|**nvarchar(500)**|O diretório no servidor secundário onde arquivos de backup são copiados.|  
|**file_retention_period**|**Int**|A quantidade de tempo, em minutos, que um arquivo de backup é mantido no servidor secundário antes de ser excluído.|  
|**copy_job_id**|**uniqueidentifier**|A ID associada ao trabalho de cópia no servidor secundário.|  
|**restore_job_id**|**uniqueidentifier**|A ID associada ao trabalho de restauração no servidor secundário.|  
|**monitor_server**|**sysname**|O nome da instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que está sendo usado como um servidor monitor na configuração de envio de logs.|  
|**monitor_server_security_mode**|**bit**|O modo de segurança usado para conexão ao servidor monitor.<br /><br /> 1 = Autenticação do Windows.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.|  
|**last_copied_file**|**nvarchar(500)**|O nome do último arquivo de backup copiado para o servidor secundário.|  
|**last_copied_date**|**datetime**|A hora e a data da última operação de cópia para o servidor secundário.|  
  
## <a name="remarks"></a>Remarks  
 Vários bancos de dados secundários no mesmo servidor secundário para um determinado banco de dados primário compartilham algumas das configurações de **log_shipping_secondary** tabela. Se uma configuração compartilhada for alterada para um deles, a configuração será alterada para todos eles.  
  
## <a name="see-also"></a>Consulte também  
 [Sobre o envio de logs &#40; SQL Server &#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [sp_change_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [System Tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
