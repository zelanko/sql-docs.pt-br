---
title: Adicionar o envio de logs secundário
description: Descreve como adicionar um banco de dados secundário a uma configuração de envio de logs.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- adding secondary databases
- secondary databases [SQL Server], in log shipping
- secondary data files [SQL Server], adding
- log shipping [SQL Server], secondary databases
ms.assetid: b02eba13-f8e6-4684-b7e4-75ea038ea473
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 66a194a26529834a3d77229a21b7556b03da635e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74822154"
---
# <a name="add-a-secondary-database-to-a-log-shipping-configuration-sql-server"></a>Adicionar um banco de dados secundário a uma configuração de envio de logs (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como adicionar um banco de dados secundário a uma configuração de envio de logs existente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Os procedimentos armazenados de envio de logs exigem a associação à função de servidor fixa **sysadmin** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-add-a-log-shipping-secondary-database"></a>Para adicionar um banco de dados secundário de envio de logs  
  
1.  Clique com o botão direito do mouse no banco de dados que deve ser usado como banco de dados primário na configuração de envio de logs e clique em **Propriedades**.  
  
2.  Em **Selecionar uma página**, clique em **Envio do Log de Transações**.  
  
3.  Em **Instâncias e bancos de dados do servidor secundário**, clique em **Adicionar**.  
  
4.  Clique em **Conectar** e conecte-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que deseja usar como servidor secundário.  
  
5.  Na caixa **Banco de dados secundário** , escolha um banco de dados da lista ou digite o nome do banco de dados que você quer criar.  
  
6.  Na guia **Inicializar banco de dados secundário** , escolha a opção que deseja usar para inicializar o banco de dados secundário.  
  
7.  Na **Guia Copiar Arquivos**, na caixa **Pasta de destino para arquivos copiados** , digite o caminho da pasta para a qual os backups de log de transações devem ser copiados. Essa pasta fica, frequentemente, alocada no servidor secundário.  
  
8.  Observe a agenda de cópias listada na caixa **Agenda** em **Copiar trabalho**. Caso queira personalizar a agenda para sua instalação, clique em **Agenda** e, em seguida, ajuste a Agenda do agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , conforme necessário. Essa agenda deve aproximar-se da agenda de backup.  
  
9. Na guia **Restaurar** em **Estado de banco de dados ao restaurar backups**, escolha a opção **Nenhum modo de recuperação** ou **Modo de espera** .  
  
10. Caso tenha escolhido a opção **Modo de espera** , escolha se deseja desconectar os usuários do banco de dados secundário enquanto a operação de restauração está em andamento.  
  
11. Caso queira adiar o processo de restauração no servidor secundário, escolha um tempo de atraso em **Atrasar restauração de backups pelo menos**.  
  
12. Escolha um limite de alerta em **Alertar se nenhuma restauração ocorrer em**.  
  
13. Observe a agenda de restauração listada na caixa **Agenda** em **Restaurar trabalho**. Caso queira personalizar a agenda para sua instalação, clique em **Agenda** e, em seguida, ajuste a Agenda do agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , conforme necessário. Essa agenda deve aproximar-se da agenda de backup.  
  
14. Clique em **OK**.  
  
15. Clique em **OK** na caixa de diálogo Propriedades do Banco de Dados para iniciar o processo de configuração.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-add-a-log-shipping-secondary-database"></a>Para adicionar um banco de dados secundário de envio de logs  
  
1.  No servidor secundário, execute [sp_add_log_shipping_secondary_primary](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-primary-transact-sql.md) fornecendo os detalhes do servidor primário e banco de dados. Esse procedimento armazenado retorna a ID secundária e as ID de tarefa de cópia e restauração.  
  
2.  No servidor secundário, execute [sp_add_jobschedule](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md) para definir o agendamento das tarefas de cópia e restauração.  
  
3.  No servidor secundário, execute [sp_add_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md) para adicionar o banco de dados secundário.  
  
4.  No servidor primário, execute [sp_add_log_shipping_primary_secondary](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-secondary-transact-sql.md) para adicionar as informações necessárias sobre o novo banco de dados secundário ao servidor primário.  
  
5.  No servidor secundário, habilite as tarefas de cópia e restauração. Para obter mais informações, consulte [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Atualizando o envio de logs para o SQL Server 2016 &#40;Transact-SQL&#41;](../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Configurar o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)  
  
-   [Remover um banco de dados secundário de uma configuração de envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/remove-a-secondary-database-from-a-log-shipping-configuration-sql-server.md)  
  
-   [Remover envio de log &#40;SQL Server&#41;](../../database-engine/log-shipping/remove-log-shipping-sql-server.md)  
  
-   [Exibir o relatório de envio de logs &#40;SQL Server Management Studio&#41;](../../database-engine/log-shipping/view-the-log-shipping-report-sql-server-management-studio.md)  
  
-   [Monitorar o envio de logs &#40;Transact-SQL&#41;](../../database-engine/log-shipping/monitor-log-shipping-transact-sql.md)  
  
-   [Executar failover para um secundário de envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Tabelas de envio de log e procedimentos armazenados](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  
