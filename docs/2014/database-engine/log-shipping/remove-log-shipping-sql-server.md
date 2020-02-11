---
title: Remover o envio de logs (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], removing
- removing log shipping
- deleting log shipping
ms.assetid: 859373db-c744-4a4b-8479-45163f61e8cb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 270ca92b723aa67938dc1f56d72425d7e1c98040
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62774990"
---
# <a name="remove-log-shipping-sql-server"></a>Remover envio de log (SQL Server)
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
 Os procedimentos armazenados de envio de logs exigem a associação à função de servidor fixa **sysadmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-remove-log-shipping"></a>Para remover envio de logs  
  
1.  Conecte à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é no momento o servidor primário para envio de logs e expanda essa instância.  
  
2.  Expanda **Bancos de Dados**, clique com o botão direito do mouse no banco de dados primário de envio de logs e clique em **Propriedades**.  
  
3.  Em **Selecionar uma página**, clique em **Envio do Log de Transações**.  
  
4.  Desmarque a caixa de seleção **Habilite isto como banco de dados primário em uma configuração de envio de logs** .  
  
5.  Clique em **OK** para remover o envio de logs deste banco de dados primário.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-remove-log-shipping"></a>Para remover envio de logs  
  
1.  No servidor primário de envio de logs, execute [sp_delete_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql) para excluir as informações sobre o banco de dados secundário do servidor primário.  
  
2.  No servidor secundário de envio de logs, execute [sp_delete_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql) para excluir o banco de dados secundário.  
  
    > [!NOTE]  
    >  Se não houver outro banco de dados secundário com a mesma ID secundária, **sp_delete_log_shipping_secondary_primary** será invocado de **sp_delete_log_shipping_secondary_database** e excluirá a entrada da ID secundária e os trabalhos de cópia e restauração.  
  
3.  No servidor primário de envio de logs, execute **sp_delete_log_shipping_primary_database** para excluir informações sobre a configuração de envio do log no servidor primário. Isso também exclui a tarefa de backup.  
  
4.  No servidor primário para envio de logs, desabilite o trabalho de backup. Para obter mais informações, consulte [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md).  
  
5.  No servidor secundário para envio de logs, desabilite os trabalhos de cópia e restauração.  
  
6.  Como opção, se você já não estiver usando o banco de dados secundário para envio de logs, poderá excluí-lo do servidor secundário.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Atualizar o envio de logs para SQL Server 2014 &#40;Transact-SQL&#41;](upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Configurar o envio de logs &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)  
  
-   [Adicionar um banco de dados secundário a uma configuração de envio de logs &#40;SQL Server&#41;](add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [Remover um banco de dados secundário de uma configuração de envio de logs &#40;SQL Server&#41;](remove-a-secondary-database-from-a-log-shipping-configuration-sql-server.md)  
  
-   [Monitorar o envio de logs &#40;Transact-SQL&#41;](monitor-log-shipping-transact-sql.md)  
  
-   [Executar failover para um secundário de envio de logs &#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
-   [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](about-log-shipping-sql-server.md)   
 [Tabelas de envio de log e procedimentos armazenados](log-shipping-tables-and-stored-procedures.md)  
  
  
