---
title: Configurar o envio de logs (SQL Server) | Microsoft Docs
description: Saiba como configurar o envio de logs usando o SQL Server Management Studio ou o Transact-SQL no SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], enabling
- log shipping [SQL Server], configuring
ms.assetid: c42aa04a-4945-4417-b4c7-50589d727e9c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b9735e45e834f60cff3a9d7fa25360b8935ed9b9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85696263"
---
# <a name="configure-log-shipping-sql-server"></a>Configurar o envio de logs (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como configurar o envio de logs no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!NOTE]  
>  O [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e versões posteriores dão suporte à compactação de backup. Ao criar uma configuração de envio de logs, é possível controlar o comportamento de compactação de backup dos backups de log. Para obter mais informações, veja [Compactação de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para configurar o envio de logs, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   O banco de dados primário deve usar o modelo de recuperação completa ou bulk-logged; se o banco de dados for alterado para o modelo de recuperação simples, o envio de logs deixará de funcionar.  
  
-   Antes de configurar o envio de logs, é necessário criar um compartilhamento para disponibilizar os backups de log de transações no servidor secundário. Esse é um compartilhamento do diretório onde os backups de log de transação serão gerados. Por exemplo, se você fez backup dos logs de transação no diretório c:\data\tlogs\\, será possível criar o compartilhamento \\\\*primaryserver*\tlogs desse diretório.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Os procedimentos armazenados de envio de logs exigem a associação à função de servidor fixa **sysadmin** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-log-shipping"></a>Para configurar o envio de logs  
  
1.  Clique com o botão direito do mouse no banco de dados que deve ser usado como banco de dados primário na configuração de envio de logs e, em seguida, clique em **Propriedades**.  
  
2.  Em **Selecionar uma página**, clique em **Envio do Log de Transações**.  
  
3.  Selecione a caixa de seleção **Habilitar como banco de dados primário em uma configuração de envio de logs** .  
  
4.  Em **Backup de log de transações**, clique em **Configurações de backup**.  
  
5.  Na caixa **Caminho de rede para a pasta de backup** , digite o caminho de rede para o compartilhamento criado para a pasta de backup de log de transações.  
  
6.  **Se a pasta de backup estiver localizada no servidor primário, digite um caminho local na caixa da pasta de backup**. (Se a pasta de backup não estiver localizada no servidor primário, deixe essa caixa em branco.)  
  
    > [!IMPORTANT]  
    >  Se a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor primário estiver sendo executada na conta Sistema Local, será necessário criar a pasta de backup no servidor primário e especificar um caminho local para a pasta.  
  
7.  Configure os parâmetros **Excluir arquivos com mais de** e **Alertar se nenhum backup ocorrer em** .  
  
8.  Observe a agenda de backup listada na caixa **Agenda** em **Trabalho de backup**. Se quiser personalizar a agenda para sua instalação, clique em **Agenda** e, em seguida, ajuste a Agenda do agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , conforme necessário.  
  
9. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dá suporte à [compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md). Ao criar uma configuração de envio de logs, é possível controlar o comportamento de compactação de backup dos backups de log escolhendo uma das opções a seguir: **Usar a configuração de servidor padrão**, **Compactar backup** ou **Não compactar o backup**. Para obter mais informações, consulte [Log Shipping Transaction Log Backup Settings](../../relational-databases/databases/log-shipping-transaction-log-backup-settings.md).  
  
10. Clique em **OK**.  
  
11. Em **Instâncias e bancos de dados do servidor secundário**, clique em **Adicionar**.  
  
12. Clique em **Conectar** e conecte-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que deseja usar como servidor secundário.  
  
13. Na caixa **Banco de Dados Secundário** , escolha um banco de dados da lista ou digite o nome do banco de dados que deve ser criado.  
  
14. Na guia **Inicializar banco de dados secundário** , escolha a opção que deseja usar para inicializar o banco de dados secundário.  
  
    > [!NOTE]  
    >  Se você optar para que o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] inicialize o banco de dados secundário por meio de um backup de banco de dados, os arquivos de dados e de log do banco de dados secundário serão colocados no mesmo local que os arquivos de dados e de log do banco de dados **mestre** . É provável que esse local seja diferente do local dos arquivos de dados e de log do banco de dados primário.  
  
15. Na guia **Copiar Arquivos** , na caixa **Pasta de destino dos arquivos copiados** , digite o caminho da pasta onde os backups de log de transações devem ser copiados. Essa pasta fica, frequentemente, alocada no servidor secundário.  
  
16. Observe a agenda de cópias listada na caixa **Agenda** em **Copiar trabalho**. Caso queira personalizar a agenda para sua instalação, clique em **Agenda** e, em seguida, ajuste a Agenda do agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , conforme necessário. Essa agenda deve aproximar-se da agenda de backup.  
  
17. Na guia **Restaurar** em **Estado de banco de dados ao restaurar backups**, escolha a opção **Nenhum modo de recuperação** ou **Modo de espera** .  
    > [!IMPORTANT]  
    > **Modo de espera** é apenas uma opção quando a versão do servidor primário e secundário são as mesmas. Quando a versão principal do servidor secundário for maior do que a do primário, apenas **Nenhum modo de recuperação** será permitido
  
18. Caso tenha escolhido a opção **Modo de espera** , escolha se deseja desconectar os usuários do banco de dados secundário enquanto a operação de restauração está em andamento.  
  
19. Caso queira adiar o processo de restauração no servidor secundário, escolha um tempo de atraso em **Atrasar restauração de backups pelo menos**.  
  
20. Escolha um limite de alerta em **Alertar se nenhuma restauração ocorrer em**.  
  
21. Observe a agenda de restauração listada na caixa **Agenda** em **Restaurar trabalho**. Caso queira personalizar a agenda para sua instalação, clique em **Agenda** e, em seguida, ajuste a Agenda do agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , conforme necessário. Essa agenda deve aproximar-se da agenda de backup.  
  
22. Clique em **OK**.  
  
23. Em **Instância do servidor monitor**, selecione a caixa de seleção **Usar uma instância de servidor monitor** e, em seguida, clique em **Configurações**.  
  
    > [!IMPORTANT]  
    >  Para monitorar essa configuração de envio de logs é necessário adicionar o servidor monitor neste momento. Para adicionar o servidor monitor posteriormente, é necessário remover essa configuração de envio de logs e, em seguida, substituí-la pela configuração nova que inclui um servidor monitor.  
  
24. Clique em **Conectar** e conecte-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que deseja usar como servidor monitor.  
  
25. Em **Conexões de monitor**, escolha o método de conexão para ser usado pelo backup, copie e restaure os trabalhos para fazer a conexão com o servidor monitor.  
  
26. Em **Retenção de histórico**, escolha o período de tempo em que o registro deve ser retido no histórico de envio de logs.  
  
27. Clique em **OK**.  
  
28. Na caixa de diálogo **Propriedades do Banco de Dados** , clique em **OK** para iniciar o processo de configuração.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-log-shipping"></a>Para configurar o envio de logs  
  
1.  Inicialize o banco de dados secundário, restaurando um backup completo do banco de dados primário no servidor secundário.  
  
2.  No servidor primário, execute [sp_add_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md) para adicionar um banco de dados primário. O procedimento armazenado retorna o ID do trabalho de backup e o ID primário.  
  
3.  No servidor primário, execute [sp_add_jobschedule](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md) para adicionar um agendamento ao trabalho de backup.  
  
4.  No servidor monitor, execute [sp_add_log_shipping_alert_job](../../relational-databases/system-stored-procedures/sp-add-log-shipping-alert-job-transact-sql.md) para adicionar o trabalho de alerta.  
  
5.  No servidor primário, habilite o trabalho de backup.  
  
6.  No servidor secundário, execute [sp_add_log_shipping_secondary_primary](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-primary-transact-sql.md) fornecendo os detalhes do servidor primário e banco de dados. Esse procedimento armazenado retorna a ID secundária e as ID de tarefa de cópia e restauração.  
  
7.  No servidor secundário, execute [sp_add_jobschedule](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md) para definir o agendamento das tarefas de cópia e restauração.  
  
8.  No servidor secundário, execute [sp_add_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md) para adicionar o banco de dados secundário.  
  
9. No servidor primário, execute [sp_add_log_shipping_primary_secondary](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-secondary-transact-sql.md) para adicionar as informações necessárias sobre o novo banco de dados secundário ao servidor primário.  
  
10. No servidor secundário, habilite as tarefas de cópia e restauração. Para obter mais informações, consulte [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Atualizando o envio de logs para o SQL Server 2016 &#40;Transact-SQL&#41;](../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Adicionar um banco de dados secundário a uma configuração de envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [Remover um banco de dados secundário de uma configuração de envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/remove-a-secondary-database-from-a-log-shipping-configuration-sql-server.md)  
  
-   [Remover envio de log &#40;SQL Server&#41;](../../database-engine/log-shipping/remove-log-shipping-sql-server.md)  
  
-   [Exibir o relatório de envio de logs &#40;SQL Server Management Studio&#41;](../../database-engine/log-shipping/view-the-log-shipping-report-sql-server-management-studio.md)  
  
-   [Monitorar o envio de logs &#40;Transact-SQL&#41;](../../database-engine/log-shipping/monitor-log-shipping-transact-sql.md)  
  
-   [Executar failover para um secundário de envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Tabelas de envio de log e procedimentos armazenados](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  
