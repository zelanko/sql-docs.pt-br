---
title: Aplicativo sqllogship | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: sqllogship
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- sqllogship
ms.assetid: 8ae70041-f3d9-46e4-8fa8-31088572a9f8
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ec4a757306f0e63e2e85b70526a211667a70f6e6
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="sqllogship-application"></a>Aplicativo sqllogship
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]O **sqllogship** aplicativo executa um backup, cópia, ou operação de restauração e tarefas de limpeza associadas para uma configuração de envio de log. A operação é realizada em uma instância específica do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para um banco de dados específico.  
  
 ![Ícone de link do tópico](../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") para as convenções de sintaxe, consulte [referência de utilitários de Prompt de comando &#40; mecanismo de banco de dados &#41;](../tools/command-prompt-utility-reference-database-engine.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqllogship -server instance_name { -backup primary_id | -copy secondary_id | -restore secondary_id } [ –verboselevel level ] [ –logintimeout timeout_value ] [ -querytimeout timeout_value ]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-server** *instance_name*  
 Especifica a instância da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] onde a operação será executada. A instância do servidor a especificar depende da operação de envio de logs que está sendo especificada. Para **-backup**, *instance_name* deve ser o nome do servidor primário em uma configuração de envio de logs. Para **-copy** ou **-restore**, *instance_name* deve ser o nome de um servidor secundário em uma configuração de envio de logs.  
  
 **-backup** *primary_id*  
 Realiza uma operação de backup do banco de dados primário cuja ID primária é especificada por *primary_id*. É possível obter esta ID selecionando-a na tabela do sistema [log_shipping_primary_databases](../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md) ou usando o procedimento armazenado [sp_help_log_shipping_primary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md) .  
  
 A operação de backup cria o backup de log no diretório de backup. O aplicativo **sqllogship** limpa os arquivos de backup antigos, com base no período de retenção dos arquivos. Em seguida, o aplicativo registra o histórico da operação de backup no servidor primário e o servidor monitor. Por fim, o aplicativo executa [sp_cleanup_log_shipping_history](../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md), que limpa as informações do histórico antigo, com base no período de retenção.  
  
 **-copy** *secondary_id*  
 Executa uma operação para copiar os backups de um servidor secundário especificado do banco de dados secundário, ou bancos de dados, cuja ID secundária é especificada por *secondary_id*. É possível obter esta ID selecionando-a na tabela do sistema [log_shipping_secondary](../relational-databases/system-tables/log-shipping-secondary-transact-sql.md) ou usando o procedimento armazenado [sp_help_log_shipping_secondary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md) .  
  
 A operação copia os arquivos de backup do diretório de backup para o diretório de destino. O aplicativo **sqllogship** registra o histórico da operação de cópia no servidor secundário e no servidor do monitor.  
  
 **-restore** *secondary_id*  
 Realiza uma operação de restauração no servidor secundário especificado do banco de dados, ou bancos de dados secundários, cuja ID secundária é especificada por *secondary_id*. É possível obter esta ID usando o procedimento armazenado **sp_help_log_shipping_secondary_database** .  
  
 Qualquer arquivo de backup no diretório de destino criado após o ponto de restauração mais recente é restaurado no banco de dados ou bancos de dados secundários. O aplicativo **sqllogship** limpa os arquivos de backup antigos, com base no período de retenção dos arquivos. Em seguida, o aplicativo registra o histórico da operação de backup no servidor primário e o servidor monitor. Por fim, o aplicativo executa **sp_cleanup_log_shipping_history**, que limpa as informações do histórico antigo, com base no período de retenção.  
  
 **–verboselevel** *level*  
 Especifica o nível das mensagens adicionadas ao histórico do envio de logs. *level* é um dos seguintes inteiros:  
  
|level|Description|  
|-----------|-----------------|  
|0|Não emite nenhuma mensagem de rastreamento ou de depuração.|  
|1|Emite mensagens para tratamento de erros.|  
|2|Emite mensagens para tratamento de erros e avisos.|  
|**3**|Emite mensagens informativas, avisos e mensagens de tratamento de erros. Este é o valor padrão.|  
|4|Emite todas as mensagens de depuração e de rastreamento.|  
  
 **–logintimeout** *timeout_value*  
 Especifica o tempo designado para tentar efetuar o login à instância do servidor antes da tentativa expirar. O padrão é 15 segundos. *timeout_value* é **int *.*  
  
 **-querytimeout** *timeout_value*  
 Especifica o tempo designado para iniciar a operação especificada antes da tentativa expirar. O padrão é sem período de expiração. *timeout_value* é **int *.*  
  
## <a name="remarks"></a>Remarks  
 Recomendamos a utilização das opções de backup, copiar e restaurar para realizar as tarefas de backup, copiar e restaurar quando for possível. Para iniciar esses trabalhos em uma operação em lote ou em outro aplicativo, chame o procedimento armazenado [sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md) .  
  
 O histórico do envio de logs criado por **sqllogship** é intercalado com o histórico criado pelos trabalhos de backup, cópia e restauração do envio de logs. Se você pretende usar **sqllogship** repetidamente para realizar as operações de backup, cópia ou restauração de uma configuração de envio de logs, considere desabilitar o(s) trabalho(s) de envio de logs correspondente(s). Para obter mais informações, consulte [Disable or Enable a Job](http://msdn.microsoft.com/library/5041261f-0c32-4d4a-8bee-59a6c16200dd).  
  
 O aplicativo **sqllogship** , SqlLogShip.exe, é instalado no diretório x:\Arquivos de Programas\Microsoft SQL Server\130\Tools\Binn.  
  
## <a name="permissions"></a>Permissões  
 **sqllogship** usa a Autenticação do Windows. A conta Autenticação do Windows onde o comando é executado requer acesso ao diretório e às permissões [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] do Windows O requisito depende de qual opção é especificada pelo comando **sqllogship** : **-backup**, **-copy**ou **-restore** .  
  
|Opção|Acesso ao diretório|Permissões|  
|------------|----------------------|-----------------|  
|**-backup**|Requer o acesso leitura/gravação ao diretório de backup.|Requer as mesmas permissões da instrução BACKUP. Para obter mais informações, veja [BACKUP &#40;Transact-SQL&#41;](../t-sql/statements/backup-transact-sql.md).|  
|**-copy**|Requer o acesso leitura ao diretório de backup e o acesso gravação ao diretório copiar|Exige as mesmas permissões do procedimento armazenado [sp_help_log_shipping_secondary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md) .|  
|**-restore**|Requer o acesso leitura/gravação ao diretório copiar.|Requer as mesmas permissões da instrução RESTORE. Para obter mais informações, veja [RESTORE &#40;Transact-SQL&#41;](../t-sql/statements/restore-statements-transact-sql.md).|  
  
> [!NOTE]  
>  Para encontrar os caminhos dos diretórios de backup e cópia, execute o procedimento armazenado **sp_help_log_shipping_secondary_database** ou exiba a tabela **log_shipping_secondary** no **msdb**. Os caminhos dos diretórios de backup e de destino estão nas colunas **backup_source_directory** e **backup_destination_directory** , respectivamente.  
  
## <a name="see-also"></a>Consulte também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [log_shipping_primary_databases &#40;Transact-SQL&#41;](../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)   
 [log_shipping_secondary &#40;Transact-SQL&#41;](../relational-databases/system-tables/log-shipping-secondary-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_help_log_shipping_primary_database &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [sp_start_job &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)  
  
  
