---
title: "Envio de logs e replicação (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- replication [SQL Server], log shipping and
- log shipping [SQL Server], replication and
ms.assetid: 132bebfd-0206-4d23-829a-b38e5ed17bc9
caps.latest.revision: "30"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: fc7c67f47d535a639f1862cc1bc8be92855f6567
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="log-shipping-and-replication-sql-server"></a>Replicação e envio de logs (SQL Server)
  O envio de logs envolve duas cópias de um único banco de dados que, normalmente, residem em computadores diferentes. Em determinado momento, apenas uma cópia do banco de dados está atualmente disponível aos clientes. Essa cópia é conhecida como o banco de dados primário. As atualizações feitas pelos clientes no banco de dados primário são propagadas por meio do envio de logs para a outra cópia do banco de dados, conhecida como banco de dados secundário. O envio de logs envolve a aplicação de um log de transações de todas as inserções, atualizações ou exclusões feitas no banco de dados primário para o banco de dados secundário.  
  
 O envio de logs pode ser usado em combinação com a replicação, com o seguinte comportamento:  
  
-   A replicação não continua depois de um failover de envio de logs. Se ocorrer um failover, os agentes de replicação não conectarão ao secundário, portanto, as transações não serão replicadas para os Assinantes. Se ocorrer um failback para o primário, a replicação será retomada. Todas as transações que o envio de logs copia do secundário para o primário são replicadas para os Assinantes.  
  
-   Se o primário for permanentemente perdido, o secundário poderá ser renomeado para que a replicação possa continuar. O restante deste tópico descreve os requisitos e procedimentos para manipular este caso. O exemplo fornecido é o banco de dados de publicação, que é o banco de dados mais comum de envio de logs, porém, também pode ser aplicado em um processo semelhante para bancos de dados de assinatura e distribuição.  
  
 Para obter informações sobre como recuperar bancos de dados envolvidos em replicação sem nenhuma necessidade de reconfigurar a replicação, consulte [Fazer backup e restaurar bancos de dados replicados](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md).  
  
> [!NOTE]  
>  É recomendável usar espelhamento de banco de dados, em vez de envio de logs, para dar mais disponibilidade ao banco de dados de publicação. Para obter mais informações, consulte [Espelhamento e replicação de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
## <a name="requirements-and-procedures-for-replicating-from-the-secondary-if-the-primary-is-lost"></a>Requisitos e procedimentos para replicação do secundário caso o primário seja perdido  
 Lembre-se dos requisitos e considerações a seguir:  
  
-   Se o primário contiver mais de um banco de dados de publicação, envie os logs de todos os bancos de dados de publicação ao mesmo secundário.  
  
-   O caminho de instalação da instância do servidor secundário deve ser igual ao do primário. Os locais do banco de dados do usuário no servidor secundário devem ser iguais aos do primário.  
  
-   Faça o backup da chave mestra de serviço no primário. Essa chave será restaurada no secundário. Para obter mais informações, consulte [BACKUP SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-service-master-key-transact-sql.md).  
  
-   O envio de logs não oferece garantia contra a perda de dados. Uma falha no banco de dados primário pode resultar na perda de dados para os quais ainda não foi feito o backup ou para backups perdidos durante a falha.  
  
### <a name="log-shipping-with-transactional-replication"></a>Envio de logs com replicação transacional  
 Para replicação transacional, o comportamento do envio de logs depende da opção **sincronizar com backup** . Essa opção pode ser definida no banco de dados de publicação e no banco de dados de distribuição; no envio de logs para o Publicador, apenas a configuração no banco de dados de publicação é relevante.  
  
 Definir essa opção no banco de dados de publicação assegura que as transações não serão entregues ao banco de dados de distribuição até ser realizado o backup do banco de dados de publicação. O último backup do banco de dados de publicação poderá então ser restaurado no servidor secundário sem qualquer possibilidade do banco de dados de distribuição possuir transações que o banco de dados de publicação restaurado não possua. Essa opção garante que se ocorrer failover do Publicador para o servidor secundário, será mantida a consistência entre o Publicador, o Distribuidor e os Assinantes. A latência e a taxa de transferência serão afetadas porque as transações não poderão ser entregues ao banco de dados de distribuição até que tenha sido feito backup no Publicador. É recomendável definir essa opção no banco de dados de publicação caso o seu aplicativo possa tolerar essa latência. Se a opção **sincronizar com backup** ainda não estiver definida, os Assinantes poderão receber alterações que não estão mais incluídas no banco de dados recuperado no servidor secundário. Para obter mais informações, consulte [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
 **Para configurar a replicação transacional e o envio de logs com a opção sincronizar com backup**  
  
1.  Se a opção sincronizar com backup não estiver definida no banco de dados de publicação, execute `sp_replicationdboption '<publicationdatabasename>', 'sync with backup', 'true'`. Para obter mais informações, consulte [sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md).  
  
2.  Configure o envio de logs para o banco de dados de publicação. Para obter mais informações, consulte [Configurar o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md).  
  
3.  Se ocorrer falha no Publicador, restaure o último log do banco de dados no servidor secundário por meio da opção KEEP_REPLICATION do RESTORE LOG. Isso retém todas as configurações de replicação do banco de dados. Para obter mais informações, consulte [Failover para um envio de logs secundário&#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md) e [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
4.  Restaure o banco de dados **msdb** e os bancos de dados **mestres** do primário no secundário. Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md). Se o primário também era um Distribuidor, restaure o banco de dados de distribuição do primário no secundário.  
  
     Esses bancos de dados devem ser consistentes com o banco de dados de publicação no primário em termos de configuração de replicação e definições.  
  
5.  No servidor secundário, renomeie o computador e, em seguida, renomeie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que corresponda ao nome do servidor primário. Para obter informações sobre como renomear um computador, consulte a documentação do Windows. Para obter informações sobre como renomear o servidor, consulte [Renomear um computador que hospeda uma instância autônoma do SQL Server](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md) e [Renomear uma instância do cluster de failover do SQL Server](../../sql-server/failover-clusters/install/rename-a-sql-server-failover-cluster-instance.md).  
  
6.  No servidor secundário, restaure a chave mestra de serviço da qual foi feito o backup do primário. Para obter mais informações, consulte [RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-service-master-key-transact-sql.md).  
  
 **Para configurar a replicação transacional e envio de logs sem a opção sincronizar com backup**  
  
1.  Configure o envio de logs para o banco de dados de publicação. Para obter mais informações, consulte [Configurar o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md).  
  
2.  Se ocorrer falha no Publicador, restaure o último log do banco de dados no servidor secundário por meio da opção KEEP_REPLICATION do RESTORE LOG. Isso retém todas as configurações de replicação do banco de dados. Para obter mais informações, consulte [Failover para um envio de logs secundário&#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md) e [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
3.  Restaure o banco de dados **msdb** e os bancos de dados **mestres** do primário no secundário. Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md). Se o primário também era um Distribuidor, restaure o banco de dados de distribuição do primário no secundário.  
  
     Esses bancos de dados devem ser consistentes com o banco de dados de publicação no primário em termos de configuração de replicação e definições.  
  
4.  No servidor secundário, renomeie o computador e, em seguida, renomeie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que corresponda ao nome do servidor primário. Para obter informações sobre como renomear um computador, consulte a documentação do Windows. Para obter informações sobre como renomear o servidor, consulte [Renomear um computador que hospeda uma instância autônoma do SQL Server](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md) e [Renomear uma instância do cluster de failover do SQL Server](../../sql-server/failover-clusters/install/rename-a-sql-server-failover-cluster-instance.md).  
  
     Você poderá receber uma mensagem de erro do Log Reader Agent informando que o banco de dados de publicação e o banco de dados de distribuição não estão sincronizados.  
  
5.  No servidor secundário, restaure a chave mestra de serviço da qual foi feito o backup do primário. Para obter mais informações, consulte [RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-service-master-key-transact-sql.md).  
  
6.  Execute **sp_replrestart**. Esse procedimento armazenado pode ser usado para forçar o Log Reader Agent a ignorar todas as transações replicadas anteriormente no log do banco de dados de publicação. As transações aplicadas depois da conclusão do procedimento armazenado serão processadas pelo Log Reader Agent. Para obter mais informações, consulte [sp_replrestart &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md).  
  
7.  Reinicie o Log Reader Agent depois que o procedimento armazenado for executado com êxito. Para obter mais informações, consulte [Iniciar e interromper um agente de replicação &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
8.  As transações que já foram distribuídas ao Assinante podem ser aplicadas no Publicador. Para garantir que o Agente de Distribuição não tenha uma falha com um erro ao tentar aplicar novamente essas transações a um Assinante, especifique o perfil do agente intitulado **Continuar em caso de erros de consistência de dados**.  
  
### <a name="log-shipping-with-merge-replication"></a>Envio de logs com replicação de mesclagem  
 Siga as etapas do procedimento a seguir para configurar a replicação de mesclagem e envio de logs.  
  
 **Para configurar a replicação de mesclagem e envio de logs**  
  
1.  Configure o envio de logs para o banco de dados de publicação. Para obter mais informações, consulte [Configurar o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md).  
  
2.  Se ocorrer falha no Publicador, no servidor secundário, renomeie o computador e, em seguida, renomeie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que corresponda ao nome do servidor primário. Para obter informações sobre como renomear um computador, consulte a documentação do Windows. Para obter informações sobre como renomear o servidor, consulte [Renomear um computador que hospeda uma instância autônoma do SQL Server](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md) e [Renomear uma instância do cluster de failover do SQL Server](../../sql-server/failover-clusters/install/rename-a-sql-server-failover-cluster-instance.md).  
  
3.  Restaure o último log do banco de dados no servidor secundário por meio da opção KEEP_REPLICATION do RESTORE LOG. Isso retém todas as configurações de replicação do banco de dados. Para obter mais informações, consulte [Failover para um envio de logs secundário&#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md) e [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
4.  Restaure o banco de dados **msdb** e os bancos de dados **mestres** do primário no secundário. Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md). Se o primário também era um Distribuidor, restaure o banco de dados de distribuição do primário no secundário.  
  
     Esses bancos de dados devem ser consistentes com o banco de dados de publicação no primário em termos de configuração de replicação e definições.  
  
5.  No servidor secundário, restaure a chave mestra de serviço da qual foi feito o backup do primário. Para obter mais informações, consulte [RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-service-master-key-transact-sql.md).  
  
6.  Sincronize o banco de dados de publicação com um ou mais bancos de dados de assinatura. Isso permite que você carregue as alterações feitas anteriormente no banco de dados de publicação, mas que não estão representadas no backup restaurado. Os dados que podem ser carregados dependem do modo como uma publicação é filtrada:  
  
    -   Se a publicação não for filtrada, você deverá conseguir atualizar o banco de dados de publicação com uma sincronização com o Assinante mais atualizado.  
  
    -   Se a publicação for filtrada, talvez você possa atualizar o banco de dados de publicação. Considere uma tabela particionada, de modo que cada assinatura receba os dados de clientes somente de uma região: norte, leste, sul e oeste. Se existir pelo menos um Assinante para cada partição de dados, a sincronização com um Assinante para cada partição deverá atualizar o banco de dados de publicação. Entretanto, se por exemplo, os dados da partição oeste, não foram replicados para nenhum Assinante, então esses dados no Publicador não poderão ser atualizados. Nesse caso, é recomendável reinicializar todas as assinaturas de forma que os dados no Publicador e nos Assinantes convirjam. Para obter mais informações, consulte [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md).  
  
     Se você sincronizar com um Assinante que está executando uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior à [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], a assinatura não poderá ser anônima; ela deverá ser a assinatura de um cliente ou de um servidor (referenciadas como assinaturas locais e assinaturas globais nas versões anteriores). Para obter mais informações, consulte [Sincronizar dados](../../relational-databases/replication/synchronize-data.md).  
  
## <a name="see-also"></a>Consulte também  
 [Recursos e tarefas de replicação](../../relational-databases/replication/replication-features-and-tasks.md)   
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Espelhamento e replicação de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)  
  
  
