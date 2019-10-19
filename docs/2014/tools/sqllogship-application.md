---
title: Aplicativo sqllogship | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- sqllogship
ms.assetid: 8ae70041-f3d9-46e4-8fa8-31088572a9f8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 14b9cda05bca998bd113a316692c4c2c2111d091
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "63035049"
---
# <a name="sqllogship-application"></a>Aplicativo sqllogship
  O aplicativo **sqllogship** executa uma operação de backup, cópia ou restauração e tarefas de limpeza associadas para uma configuração de envio de logs. A operação é executada em uma instância específica do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para um banco de dados específico.  
  
 ![Ícone de link do tópico](../../2014/database-engine/media/topic-link.gif "Ícone de link do tópico") Para obter as convenções de sintaxe, consulte [referência &#40;do utilitário&#41;de prompt de comando mecanismo de banco de dados](../tools/command-prompt-utility-reference-database-engine.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqllogship  
-server  
instance_name { -backupprimary_id | -copysecondary_id | -restoresecondary_id } [ -verboselevellevel ] [ -logintimeouttimeout_value ] [ -querytimeouttimeout_value ]  
```  
  
## <a name="arguments"></a>argumentos  
 **-servidor** _instance_name_  
 Especifica a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em que a operação será executada. A instância de servidor a ser especificada depende de qual operação de envio de logs está sendo especificada. Para **-backup**, *instance_name* deve ser o nome do servidor primário em uma configuração de envio de logs. Para **-Copy** ou **-Restore**, *instance_name* deve ser o nome de um servidor secundário em uma configuração de envio de logs.  
  
 **-backup** _primary_id_  
 Executa uma operação de backup para o banco de dados primário cuja ID primária é especificada por *primary_id*. Você pode obter essa ID selecionando-a na tabela do sistema [log_shipping_primary_databases](/sql/relational-databases/system-tables/log-shipping-primary-databases-transact-sql) ou usando o procedimento armazenado [sp_help_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql) .  
  
 A operação de backup cria o backup de log no diretório de backup. O aplicativo **sqllogship** limpa todos os arquivos de backup antigos, com base no período de retenção do arquivo. Em seguida, o aplicativo registra o histórico da operação de backup no servidor primário e no servidor monitor. Por fim, o aplicativo executa o [sp_cleanup_log_shipping_history](/sql/relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql), que limpa as informações do histórico antigo, com base no período de retenção.  
  
 **-copiar** _secondary_id_  
 Executa uma operação de cópia para copiar backups do servidor secundário especificado para o banco de dados secundário, ou bancos de dados, cuja ID secundária é especificada por *secondary_id*. Você pode obter essa ID selecionando-a na tabela do sistema [log_shipping_secondary](/sql/relational-databases/system-tables/log-shipping-secondary-transact-sql) ou usando o procedimento armazenado [sp_help_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql) .  
  
 A operação copia os arquivos de backup do diretório de backup para o diretório de destino. O aplicativo **sqllogship** registra em log o histórico da operação de cópia no servidor secundário e no servidor monitor.  
  
 **-restaurar** _secondary_id_  
 Executa uma operação de restauração no servidor secundário especificado para o banco de dados secundário, ou bancos de dados, cuja ID secundária é especificada por *secondary_id*. Você pode obter essa ID usando o procedimento armazenado **sp_help_log_shipping_secondary_database** .  
  
 Todos os arquivos de backup no diretório de destino que foram criados após o ponto de restauração mais recente são restaurados para o banco de dados secundário ou para os dados. O aplicativo **sqllogship** limpa todos os arquivos de backup antigos, com base no período de retenção do arquivo. Em seguida, o aplicativo registra o histórico da operação de restauração no servidor secundário e no servidor monitor. Por fim, o aplicativo executa o **sp_cleanup_log_shipping_history**, que limpa as informações do histórico antigo, com base no período de retenção.  
  
 **-nível de verboselevel**  
 Especifica o nível de mensagens adicionadas ao histórico de envio de logs. o *nível* é um dos seguintes inteiros:  
  
|Geral|Description|  
|-----------|-----------------|  
|0|Saída sem rastreamento e mensagens de depuração.|  
|uma|Mensagens de tratamento de erros de saída.|  
|2|Avisos de saída e mensagens de tratamento de erros.|  
|**Beta**|Mensagens informativas de saída, avisos e mensagens de tratamento de erros. Este é o valor padrão.|  
|quatro|Saída de todas as mensagens de depuração e rastreamento.|  
  
 **-LoginTimeout** _timeout_value_  
 Especifica a quantidade de tempo alocada para tentar fazer logon na instância do servidor antes da tentativa expirar. O padrão é 15 segundos. *timeout_value* é **int** _._  
  
 **-QueryTimeout** _timeout_value_  
 Especifica a quantidade de tempo alocada para iniciar a operação especificada antes de a tentativa atingir o tempo limite. O padrão é sem período de tempo limite. *timeout_value* é **int** _._  
  
## <a name="remarks"></a>Remarks  
 Recomendamos que você use os trabalhos de backup, cópia e restauração para executar o backup, a cópia e a restauração quando possível. Para iniciar esses trabalhos de uma operação em lote ou outro aplicativo, chame o procedimento armazenado [sp_start_job](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql) .  
  
 O histórico de envio de logs criado pelo **sqllogship** é intercalado com o histórico criado pelos trabalhos de backup, cópia e restauração de envio de logs. Se você planeja usar o **sqllogship** repetidamente para executar operações de backup, cópia ou restauração para uma configuração de envio de logs, considere desabilitar o trabalho ou trabalhos de envio de logs correspondentes. Para obter mais informações, consulte [desabilitar ou habilitar um trabalho](../ssms/agent/disable-or-enable-a-job.md).  
  
 O aplicativo **sqllogship** , sqllogship. exe, é instalado no diretório X:\Arquivos de Programas\microsoft SQL Server\120\Tools\Binn.  
  
## <a name="permissions"></a>Permissões  
 o **sqllogship** usa a autenticação do Windows. A conta de autenticação do Windows em que o comando é executado requer permissões de acesso e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de diretório do Windows. O requisito depende se o comando **sqllogship** especifica a opção **-backup**, **-Copy**ou **-Restore** .  
  
|Option|Acesso ao diretório|Permissões|  
|------------|----------------------|-----------------|  
|**-backup**|Requer acesso de leitura/gravação ao diretório de backup.|Requer as mesmas permissões que a instrução BACKUP. Para obter mais informações, consulte [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).|  
|**-cópia**|Requer acesso de leitura ao diretório de backup e acesso de gravação ao diretório de cópia.|Requer as mesmas permissões que o procedimento armazenado [sp_help_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql) .|  
|**-restaurar**|Requer acesso de leitura/gravação ao diretório de cópia.|Requer as mesmas permissões que a instrução RESTOre. Para obter mais informações, [consulte &#40;Restore Transact&#41;-SQL](/sql/t-sql/statements/restore-statements-transact-sql).|  
  
> [!NOTE]  
>  Para descobrir os caminhos dos diretórios de backup e cópia, você pode executar o procedimento armazenado **sp_help_log_shipping_secondary_database** ou exibir a tabela **log_shipping_secondary** no **msdb**. Os caminhos do diretório de backup e o diretório de destino estão nas colunas **backup_source_directory** e **backup_destination_directory** , respectivamente.  
  
## <a name="see-also"></a>Consulte também  
 [Sobre o envio &#40;de&#41; logs SQL Server](../database-engine/log-shipping/about-log-shipping-sql-server.md)    
 [  &#40;Transact-SQL&#41; log_shipping_primary_databases](/sql/relational-databases/system-tables/log-shipping-primary-databases-transact-sql)  
 [  &#40;Transact-SQL&#41; log_shipping_secondary](/sql/relational-databases/system-tables/log-shipping-secondary-transact-sql)  
 [  &#40;Transact-SQL&#41; sp_cleanup_log_shipping_history](/sql/relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql)  
 [  &#40;Transact-SQL&#41; sp_help_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql)  
 [  &#40;Transact-SQL&#41; sp_help_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql)  
 [Transact &#40;-SQL sp_start_job&#41;](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql)  
  
  
