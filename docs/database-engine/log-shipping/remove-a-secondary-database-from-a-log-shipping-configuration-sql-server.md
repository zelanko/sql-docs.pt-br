---
title: "Remover um banco de dados secundário de uma configuração de envio de logs (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting secondary databases
- secondary databases [SQL Server], in log shipping
- removing secondary databases
- secondary data files [SQL Server], removing
- log shipping [SQL Server], secondary databases
ms.assetid: ebe368a4-ca1c-45d0-9a71-3ddbd5b26a8e
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9c0ced4d63693c2d299556a28796e55fccbcc2b5
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="remove-a-secondary-database-from-a-log-shipping-configuration-sql-server"></a>Remova um banco de dados secundário de uma configuração de envio de logs (SQL Server)
  Este tópico descreve como remover um banco de dados secundário de envio de logs no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para remover um banco de dados secundário de envio de logs, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Os procedimentos armazenados de envio de logs exigem a associação à função de servidor fixa **sysadmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-remove-a-log-shipping-secondary-database"></a>Para remover um banco de dados secundário de envio de logs  
  
1.  Conecte à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é no momento o servidor primário para envio de logs e expanda essa instância.  
  
2.  Expanda **Bancos de Dados**, clique com o botão direito do mouse no banco de dados primário de envio de logs e clique em **Propriedades**.  
  
3.  Em **Selecionar uma página**, clique em **Envio do Log de Transações**.  
  
4.  Em **Instâncias e banco de dados do servidor secundário**, clique no banco de dados que você deseja remover.  
  
5.  Clique em **Remover**.  
  
6.  Clique em **OK** para atualizar a configuração.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-remove-a-secondary-database"></a>Para remover um banco de dados secundário  
  
1.  No servidor primário, execute [sp_delete_log_shipping_primary_secondary](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql.md) para excluir as informações sobre o banco de dados secundário do servidor primário.  
  
2.  No servidor secundário, execute [sp_delete_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md) para excluir o banco de dados secundário.  
  
    > [!NOTE]  
    >  Se não houver outro banco de dados secundário com a mesma ID secundária, **sp_delete_log_shipping_secondary_primary** será invocado de **sp_delete_log_shipping_secondary_database** e excluirá a entrada da ID secundária e os trabalhos de cópia e restauração.  
  
3.  No servidor secundário, desabilite os trabalhos de cópia e restauração. Para obter mais informações, consulte [Disable or Enable a Job](http://msdn.microsoft.com/library/5041261f-0c32-4d4a-8bee-59a6c16200dd).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Atualizando o envio de logs para o SQL Server 2016 &#40;Transact-SQL&#41;](../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Configurar o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)  
  
-   [Adicionar um banco de dados secundário a uma configuração de envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [Remover envio de log &#40;SQL Server&#41;](../../database-engine/log-shipping/remove-log-shipping-sql-server.md)  
  
-   [Exibir o relatório de envio de logs &#40;SQL Server Management Studio&#41;](../../database-engine/log-shipping/view-the-log-shipping-report-sql-server-management-studio.md)  
  
-   [Monitorar o envio de logs &#40;Transact-SQL&#41;](../../database-engine/log-shipping/monitor-log-shipping-transact-sql.md)  
  
-   [Executar failover para um secundário de envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Tabelas de envio de log e procedimentos armazenados](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  
