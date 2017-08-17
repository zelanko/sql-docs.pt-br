---
title: "Trocar funções entre servidores de envio de logs primários e secundários (SQL Server) | Microsoft Docs"
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
- log shipping [SQL Server], role changes
- secondary data files [SQL Server], roles changed between
- primary databases [SQL Server]
- initial role changes [SQL Server]
- log shipping [SQL Server], failover
- failover [SQL Server], log shipping
ms.assetid: 2d7cc40a-47e8-4419-9b2b-7c69f700e806
caps.latest.revision: 20
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 47e98a220a3480a854be76dbae16e98c0c17d180
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="change-roles-between-primary-and-secondary-log-shipping-servers-sql-server"></a>Alterar funções entre servidores de envio de log primários e secundários (SQL Server)
  Depois de fazer failover em uma configuração de log de envio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um servidor secundário, você pode configurar seu banco de dados secundário para agir como um banco de dados primário. Então, você poderá trocar os bancos de dados primários e secundários como necessário.  
  
## <a name="performing-the-initial-role-change"></a>Executando a alteração inicial de função  
 Na primeira vez que você fizer failover no banco de dados secundário e torná-lo seu novo banco de dados primário, há uma série de etapas que deverão ser seguidas. Depois de seguir essas etapas iniciais, você poderá alterar as funções facilmente entre o banco de dados primário e o banco de dados secundário.  
  
1.  Faça failover manualmente do banco de dados primário para um banco de dados secundário. Certifique-se de ter feito backup do log de transações ativas em seu servidor primário com NORECOVERY. Para obter mais informações, consulte [Executar failover para um secundário de envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md).  
  
2.  Desabilite o trabalho de backup de envio de logs no servidor primário original e os trabalhos de cópia e restauração no servidor secundário original.  
  
3.  Em seu banco de dados secundário (o banco de dados que você quer que seja o novo primário), configure o envio do log usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Configurar o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md). Inclua as seguintes etapas:  
  
    1.  Use o mesmo compartilhamento usado para criar o servidor primário original para criar os backups.  
  
    2.  Quando adicionar o banco de dados secundário, na caixa de diálogo **Configurações do Banco de Dados Secundário** , digite o nome do banco de dados primário original na caixa **Banco de dados secundário** .  
  
    3.  Na caixa de diálogo **Configurações do Banco de Dados Secundário** , selecione **Não, o banco de dados secundário é inicializado**.  
  
4.  Se o monitoramento de envio de logs tiver sido habilitado em sua configuração de envio de logs antiga, reconfigure o monitoramento de envio de logs para monitorar a nova configuração de envio de logs.  Execute os seguintes comandos, substituindo *database_name* pelo nome de seu banco de dados:  
  
    1.  **No novo servidor primário**  
  
         Execute as seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
        ```  
        -- Statement to execute on the new primary server  
        USE msdb  
        GO  
        EXEC master.dbo.sp_change_log_shipping_secondary_database @secondary_database = N'database_name', @threshold_alert_enabled = 0;  
        GO  
        ```  
  
    2.  **No novo servidor secundário:**  
  
         Execute as seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
        ```  
        -- Statement to execute on the new secondary server  
        USE msdb  
        GO  
        EXEC master.dbo.sp_change_log_shipping_primary_database @database=N'database_name', @threshold_alert_enabled = 0;  
        GO  
        ```  
  
## <a name="swapping-roles"></a>Alterando as funções  
 Depois de ter concluído as etapas acima para a mudança inicial de funções, você poderá alterar as funções entre o banco de dados primário e o banco de dados secundário seguindo as etapas nesta seção. Para executar uma mudança de função, siga estas etapas gerais:  
  
1.  Coloque o banco de dados secundário online, fazendo backup do log de transações no servidor primário com NORECOVERY.  
  
2.  Desabilite o trabalho de backup de envio de logs no servidor primário original e os trabalhos de cópia e restauração no servidor secundário original.  
  
3.  Habilite o trabalho de backup de envio de logs no servidor secundário (o novo servidor primário) e os trabalhos de cópia e restauração no servidor primário (o novo servidor secundário).  
  
> [!IMPORTANT]  
>  Ao alterar um banco de dados secundário para um banco de dados primário, para oferecer uma experiência consistente aos usuários e aplicativos, você poderá ter de recriar alguns ou todos os metadados do banco de dados, como logons e trabalhos, na nova instância de servidor primário. Para obter mais informações, consulte [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Executar failover para um secundário de envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
-   [Gerenciamento de logons e trabalhos após a troca de funções &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de envio de log e procedimentos armazenados](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  
