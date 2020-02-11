---
title: Tabelas de envio de logs e procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- secondary servers [SQL Server]
- monitor servers [SQL Server]
- log shipping [SQL Server], system tables
- log shipping [SQL Server], stored procedures
- primary servers [SQL Server]
ms.assetid: 03420810-4c38-4c0c-adf0-913eb044c50a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d88e0826617b63638c720f176da84a85d68a7e18
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62774490"
---
# <a name="log-shipping-tables-and-stored-procedures"></a>Log Shipping Tables and Stored Procedures
  Este tópico descreve tudo das tabelas e procedimentos armazenados associados a uma configuração de envio de logs. Todas as tabelas de envio de logs são armazenadas em **msdb** em cada servidor. As tabelas seguintes descrevem quais tabelas e procedimentos armazenados são usados em quais servidores em uma configuração de envio de logs.  
  
## <a name="primary-server-tables"></a>Tabelas de servidor primário  
  
|Tabela|DESCRIÇÃO|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](/sql/relational-databases/system-tables/log-shipping-monitor-alert-transact-sql)|Armazena ID de trabalho de alerta. Esta tabela só será usada no servidor primário se um servidor monitor remoto não tiver sido configurado.|  
|[log_shipping_monitor_error_detail](/sql/relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql)|Armazena detalhe de erro para trabalhos de envio de logs associados a este servidor primário.|  
|[log_shipping_monitor_history_detail](/sql/relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql)|Armazena detalhes de história para trabalhos de envio de logs associados a este servidor primário.|  
|[log_shipping_monitor_primary](/sql/relational-databases/system-tables/log-shipping-monitor-primary-transact-sql)|Armazena um registro de monitor para este banco de dados primário.|  
|[log_shipping_primary_databases](/sql/relational-databases/system-tables/log-shipping-primary-databases-transact-sql)|Contém informações de configuração para bancos de dados primários em um determinado servidor. Armazena uma linha por banco de dados primário.|  
|[log_shipping_primary_secondaries](/sql/relational-databases/system-tables/log-shipping-primary-secondaries-transact-sql)|Mapeia bancos de dados primários para bancos de dados secundários.|  
  
## <a name="primary-server-stored-procedures"></a>Procedimentos armazenados em servidor primário  
  
|Procedimento armazenado|DESCRIÇÃO|  
|----------------------|-----------------|  
|[sp_add_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql)|Instala o banco de dados primário para uma configuração de envio de log, incluindo o trabalho de backup, registro de monitor local e registro de monitor remoto.|  
|[sp_add_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-secondary-transact-sql)|Adiciona um nome de banco de dados secundário a um banco de dados primário existente.|  
|[sp_change_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql)|Altera configurações de banco de dados primárias, inclusive registro de monitor local e remoto.|  
|[sp_cleanup_log_shipping_history](/sql/relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql)|Limpa histórico localmente e no monitor baseado em período de retenção.|  
|[sp_delete_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql)|Remove o envio de logs do banco de dados primário inclusive o trabalho posterior como também o histórico local e remoto.|  
|[sp_delete_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql)|Remove um nome de banco de dados secundário de um banco de dados primário.|  
|[sp_help_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql)|Recupera configurações do banco de dados primário e exibe os valores das tabelas **log_shipping_primary_databases** e **log_shipping_monitor_primary** .|  
|[sp_help_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-secondary-transact-sql)|Recupera nomes de banco de dados secundários para um banco de dados primário.|  
|[sp_refresh_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql)|Atualiza o monitor com as últimas informações sobre o agente de envio do logs especificado.|  
  
## <a name="secondary-server-tables"></a>Tabelas de servidor secundário  
  
|Tabela|DESCRIÇÃO|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](/sql/relational-databases/system-tables/log-shipping-monitor-alert-transact-sql)|Armazena ID de trabalho de alerta. Essa tabela só será usada no servidor secundário se um servidor monitor remoto não tiver sido configurado.|  
|[log_shipping_monitor_error_detail](/sql/relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql)|Armazena detalhe de erro para trabalhos de envio de logs associados a este servidor secundário.|  
|[log_shipping_monitor_history_detail](/sql/relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql)|Armazena detalhes de histórico para trabalhos de envio de logs associados a este servidor secundário.|  
|[log_shipping_monitor_secondary](/sql/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql)|Armazena um registro de monitor por banco de dados secundário associado a este servidor secundário.|  
|[log_shipping_secondary](/sql/relational-databases/system-tables/log-shipping-secondary-transact-sql)|Contém informações de configuração para os bancos de dados secundários em um determinado servidor. Armazena uma linha por ID secundário.|  
|[log_shipping_secondary_databases](/sql/relational-databases/system-tables/log-shipping-secondary-databases-transact-sql)|Armazena informações de configuração para um determinado banco de dados secundário. Armazena uma linha por banco de dados secundário.|  
  
> [!NOTE]  
>  Os bancos de dados secundários no mesmo servidor secundário para um determinado banco de dados primário compartilham as configurações na tabela **log_shipping_secondary** . Se uma configuração compartilhada for alterada para um banco de dados secundário, a configuração será alterada para todos eles.  
  
## <a name="secondary-server-stored-procedures"></a>Procedimentos armazenados em servidor secundário  
  
|Procedimento armazenado|DESCRIÇÃO|  
|----------------------|-----------------|  
|[sp_add_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql)|Define um banco de dados secundário para envio de logs.|  
|[sp_add_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-primary-transact-sql)|Configura as informações primárias, adiciona links de monitor local e remoto e cria trabalhos de cópia e restauração no servidor secundário para o banco de dados primário especificado.|  
|[sp_change_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql)|Altera configurações de banco de dados secundários inclusive registros de monitor local e remoto.|  
|[sp_change_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-primary-transact-sql)|Altera configurações de banco de dados secundários como fonte e diretório de destino e período de retenção de arquivo.|  
|[sp_cleanup_log_shipping_history](/sql/relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql)|Limpa histórico localmente e no monitor baseado em período de retenção.|  
|[sp_delete_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql)|Remove um banco de dados secundário e o histórico local e histórico remoto.|  
|[sp_delete_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-primary-transact-sql)|Remove as informações sobre o servidor primário especificado do servidor secundário.|  
|[sp_help_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql)|Recupera configurações de bancos de dados primários e exibe os valores das tabelas **log_shipping_secondary**, **log_shipping_secondary_databases**e **log_shipping_monitor_secondary** .|  
|[sp_help_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-primary-transact-sql)|Esse procedimento armazenado recupera a configurações de um banco de dados primário específico no servidor secundário.|  
|[sp_refresh_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql)|Atualiza o monitor com as últimas informações sobre o agente de envio do logs especificado.|  
  
## <a name="monitor-server-tables"></a>Tabelas de Servidor Monitor  
  
|Tabela|DESCRIÇÃO|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](/sql/relational-databases/system-tables/log-shipping-monitor-alert-transact-sql)|Armazena ID de trabalho de alerta.|  
|[log_shipping_monitor_error_detail](/sql/relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql)|Armazena detalhes de erros para trabalhos de envio de logs.|  
|[log_shipping_monitor_history_detail](/sql/relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql)|Armazena detalhe de histórico para trabalhos de envio de logs.|  
|[log_shipping_monitor_primary](/sql/relational-databases/system-tables/log-shipping-monitor-primary-transact-sql)|Armazena um registro de monitor por banco de dados primário associado a este servidor monitor.|  
|[log_shipping_monitor_secondary](/sql/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql)|Armazena um registro de monitor por banco de dados secundário associado a este servidor monitor.|  
  
## <a name="monitor-server-stored-procedures"></a>Procedimentos armazenados em Servidor Monitor  
  
|Procedimento armazenado|DESCRIÇÃO|  
|----------------------|-----------------|  
|[sp_add_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-alert-job-transact-sql)|Criará um trabalho de alerta de envio de logs se já não foi criado um.|  
|[sp_delete_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-alert-job-transact-sql)|Removerá um trabalho de alerta de envio de logs se não houver nenhum banco de dados primário associado.|  
|[sp_help_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-alert-job-transact-sql)|Retorna a ID de trabalho do trabalho de alerta.|  
|[sp_help_log_shipping_monitor_primary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql)|Retorna registros de monitor para o banco de dados primário especificado da tabela **log_shipping_monitor_primary** .|  
|[sp_help_log_shipping_monitor_secondary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql)|Retorna registros de monitor para o banco de dados secundário especificado da tabela **log_shipping_monitor_secondary** .|  
  
  
