---
title: "Remover envio de log (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "envio de logs [SQL Server], removendo"
  - "removendo envio de log"
  - "excluindo o envio de log"
ms.assetid: 859373db-c744-4a4b-8479-45163f61e8cb
caps.latest.revision: 18
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 18
---
# Remover envio de log (SQL Server)
  Este tópico descreve como remover o envio de logs no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para remover envio de log, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Os procedimentos armazenados de envio de logs exigem a associação à função de servidor fixa **sysadmin**.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Para remover envio de logs  
  
1.  Conecte à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é no momento o servidor primário para envio de logs e expanda essa instância.  
  
2.  Expanda **Bancos de Dados**, clique com o botão direito do mouse no banco de dados primário de envio de logs e clique em **Propriedades**.  
  
3.  Em **Selecionar uma página**, clique em **Envio do Log de Transações**.  
  
4.  Desmarque a caixa de seleção **Habilite isto como banco de dados primário em uma configuração de envio de logs** .  
  
5.  Clique em **OK** para remover o envio de logs deste banco de dados primário.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para remover envio de log  
  
1.  No servidor primário de envio de logs, execute [sp_delete_log_shipping_primary_secondary](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql.md) para excluir as informações sobre o banco de dados secundário do servidor primário.  
  
2.  No servidor secundário de envio de logs, execute [sp_delete_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md) para excluir o banco de dados secundário.  
  
    > [!NOTE]  
    >  Se não houver outro banco de dados secundário com a mesma ID secundária, **sp_delete_log_shipping_secondary_primary** será invocado de **sp_delete_log_shipping_secondary_database** e excluirá a entrada da ID secundária e os trabalhos de cópia e restauração.  
  
3.  No servidor primário de envio de logs, execute **sp_delete_log_shipping_primary_database** para excluir informações sobre a configuração de envio do log no servidor primário. Isso também exclui a tarefa de backup.  
  
4.  No servidor primário para envio de logs, desabilite o trabalho de backup. Para obter mais informações, consulte [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md).  
  
5.  No servidor secundário para envio de logs, desabilite os trabalhos de cópia e restauração.  
  
6.  Como opção, se você já não estiver usando o banco de dados secundário para envio de logs, poderá excluí-lo do servidor secundário.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Atualizando o envio de logs para o SQL Server 2016 &#40;Transact-SQL&#41;](../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Configurar o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)  
  
-   [Adicionar um banco de dados secundário a uma configuração de envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [Remover um banco de dados secundário de uma configuração de envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/remove-a-secondary-database-from-a-log-shipping-configuration-sql-server.md)  
  
-   [Monitorar o envio de logs &#40;Transact-SQL&#41;](../../database-engine/log-shipping/monitor-log-shipping-transact-sql.md)  
  
-   [Executar failover para um secundário de envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
-   [Desabilitar ou habilitar um trabalho](../../ssms/agent/disable-or-enable-a-job.md)  
  
## Consulte também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Tabelas de envio de log e procedimentos armazenados](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  