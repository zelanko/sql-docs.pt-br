---
title: log_shipping_primary_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_primary_databases
- log_shipping_primary_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_primary_databases system table
ms.assetid: 56888756-a798-42be-9b5e-0f9aa05a2cc6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9c1dfefbc309e9ccc0f170461795c00a117247e2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72304990"
---
# <a name="log_shipping_primary_databases-transact-sql"></a>log_shipping_primary_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Armazena um registro para o banco de dados primário em uma configuração de envio de logs. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|A ID do banco de dados primário para a configuração de envio de log.|  
|**primary_database**|**sysname**|O nome do banco de dados primário na configuração de envio de log.|  
|**backup_directory**|**nvarchar (500)**|O diretório onde os arquivos de backup de log de transações do servidor primário são armazenados.|  
|**backup_share**|**nvarchar (500)**|A rede ou o caminho UNC para o diretório de backup.|  
|**backup_retention_period**|**int**|A quantidade de tempo, em minutos, que um arquivo de backup log é retido no diretório de backups antes de ser excluído.|  
|**backup_job_id**|**uniqueidentifier**|A ID de trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent associada ao trabalho de backup no servidor primário.|  
|**monitor_server**|**sysname**|O nome da instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usado como servidor monitor na configuração de envio de log.|  
|**monitor_server_security_mode**|**bit**|O modo de segurança usado para conexão ao servidor monitor.<br /><br /> 1 = Autenticação do Windows.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.|  
|**last_backup_file**|**nvarchar (500)**|O caminho absoluto de backup de log de transações mais recente.|  
|**last_backup_date**|**datetime**|A hora e a data da última operação de backup de log.|  
|**user_specified_monitor**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **sp_help_log_shipping_primary_database** e **sp_help_log_shipping_secondary_primary** Use essa coluna para controlar a exibição das configurações do monitor [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]no.<br /><br /> 0 = ao invocar um desses dois procedimentos armazenados, o usuário não especificou um valor explícito para o ** \@parâmetro monitor_server** .<br /><br /> 1 = Um valor explícito foi especificado pelo usuário.|  
|**backup_compression**|**tinyint**|Indica se a configuração de envio de logs substitui o comportamento da compactação de backup no nível do servidor.<br /><br /> 0 = Desabilitado. Os backups de log nunca são compactados, independentemente das configurações de compactação de backup configuradas pelo servidor.<br /><br /> 1 = Habilitado. Os backups de log são sempre compactados, independentemente das configurações de compactação de backup configuradas pelo servidor.<br /><br /> 2 = usa a configuração de servidor para a [exibição ou configurar a opção de configuração de servidor padrão de compactação de backup](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) Server-Configuration Option. Esse é o valor padrão.<br /><br /> Há suporte para a compactação de backup somente na edição Enterprise do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [&#41;&#40;Transact-SQL de sp_add_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [Tabelas do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
