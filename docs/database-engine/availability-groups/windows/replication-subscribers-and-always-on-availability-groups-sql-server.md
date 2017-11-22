---
title: "Assinantes de replicação e Grupos de Disponibilidade AlwaysOn (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- failover subscribers with AlwaysOn
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 0995f269-0580-43ed-b8bf-02b9ad2d7ee6
caps.latest.revision: "19"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 275b71fed45df9fee3ba4e87e780e9311b7d3157
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="replication-subscribers-and-always-on-availability-groups-sql-server"></a>Assinantes de replicação e Grupos de Disponibilidade AlwaysOn (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Quando um grupo de disponibilidade AlwaysOn contendo um banco de dados que é um assinante de replicação executar failover, a assinatura de replicação poderá falhar. Para assinantes transacionais, o agente de distribuição continuará a replicar automaticamente se a assinatura estiver usando o nome do ouvinte do grupo de disponibilidade do assinante. Para mesclar assinantes, um administrador de replicação deve reconfigurar o assinante manualmente, recriando a assinatura.  
  
## <a name="what-is-supported"></a>O que tem suporte  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece suporte ao failover automático do publicador, ao failover automático dos assinantes transacionais e ao failover manual dos assinantes de mesclagem. Não há suporte para o failover de um distribuidor em um banco de dados de disponibilidade. O AlwaysOn não pode ser combinado com cenários Websync e ssNoVersion Compact.  
  
 **Failover de uma assinatura pull de mesclagem**  
  
 Uma assinatura pull apresenta falha após o failover do grupo de disponibilidade porque o agente de pull não pode localizar os trabalhos armazenados no banco de dados **msdb** da instância de servidor que hospeda a réplica primária, que não está disponível porque a instância do servidor apresentou falha.  
  
 **Failover de uma assinatura push de mesclagem**  
  
 Uma assinatura push apresenta falha após o failover do grupo de disponibilidade porque o agente de push não pode mais se conectar ao banco de dados de assinatura original no assinante original.  
  
## <a name="how-to-create-transactional-subscription-in-an-always-on-environment"></a>Como criar uma assinatura transacional em um ambiente AlwaysOn  
 Para a replicação transacional, use as seguintes etapas para configurar e fazer o failover de um grupo de disponibilidade do assinante:  
  
1.  Antes de criar a assinatura, adicione o banco de dados do assinante ao grupo de disponibilidade AlwaysOn apropriado.  
  
2.  Adicione o ouvinte do grupo de disponibilidade do assinante como um servidor vinculado para todos os nós do grupo de disponibilidade. Essa etapa garante que todos os parceiros de failover potenciais estejam cientes de e possam se conectar ao ouvinte.  
  
3.  Usando o script da seção abaixo **Criando uma assinatura push de replicação transacional** , crie a assinatura usando o nome do ouvinte de grupo de disponibilidade do assinante. Depois de um failover, o nome do ouvinte sempre permanecerá válido, enquanto que o nome de servidor real do assinante dependerá do nó real que se tornou o novo primário.  
  
    > [!NOTE]  
    >  A assinatura deve ser criada usando um script [!INCLUDE[tsql](../../../includes/tsql-md.md)] e não pode ser criada usando o [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)].  
  
4.  Se estiver criando uma assinatura pull:  
  
    1.  No [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], no nó primário do assinante, abra a árvore do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent.  
  
    2.  Identifique o trabalho do **Agente de Distribuição de Pull** e edite o trabalho.  
  
    3.  Na etapa de trabalho **Executar Agente** , verifique os parâmetros `-Publisher` e `-Distributor` . Verifique se esses parâmetros contêm os nomes diretos do servidor e a instância corretos do servidor do publicador e do distribuidor.  
  
    4.  Altere o parâmetro `-Subscriber` para o nome do ouvinte do grupo de disponibilidade do assinante.  
  
 Quando você cria sua assinatura seguindo essas etapas, não precisa fazer nada após um failover.  
  
## <a name="creating-a-transactional-replication-push-subscription"></a>Criando uma assinatura push de replicação transacional  
  
```  
-- commands to execute at the publisher, in the publisher database:  
use [<publisher database name>]  
EXEC sp_addsubscription @publication = N'<publication name>',   
       @subscriber = N'<availability group listener name>',   
       @destination_db = N'<subscriber database name>',   
       @subscription_type = N'Push',   
       @sync_type = N'automatic', @article = N'all', @update_mode = N'read only', @subscriber_type = 0;  
GO  
  
EXEC sp_addpushsubscription_agent @publication = N'<publication name>',   
       @subscriber = N'<availability group listener name>',   
       @subscriber_db = N'<subscriber database name>',   
       @job_login = null, @job_password = null, @subscriber_security_mode = 1;  
GO  
```  
  
## <a name="to-resume-the-merge-agents-after-the-availability-group-of-the-subscriber-fails-over"></a>Para retomar os Agentes de Mesclagem após o failover do grupo de disponibilidade do assinante  
 Para a replicação de mesclagem, um administrador de replicação deve reconfigurar o assinante manualmente com as seguintes etapas:  
  
1.  Execute **sp_subscription_cleanup** para remover a assinatura antiga no assinante. Execute esta ação na nova réplica primária (a antiga réplica secundária).  
  
2.  Recrie a assinatura criando uma nova assinatura, começando por um novo instantâneo.  
  
> [!NOTE]  
>  O processo atual é inconveniente para assinantes de replicação de mesclagem; entretanto, o cenário principal para a replicação de mesclagem é de usuários desconectados (áreas de trabalho, laptops, dispositivos de fone) que não usarão grupos de disponibilidade AlwaysOn no assinante.  
  
  
