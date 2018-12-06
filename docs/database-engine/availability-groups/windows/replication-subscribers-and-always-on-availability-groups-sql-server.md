---
title: Assinantes de replicação e Grupos de Disponibilidade AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover subscribers with AlwaysOn
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 0995f269-0580-43ed-b8bf-02b9ad2d7ee6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 80bc2cd3fab4a81d76bac5623fef8f37d3167289
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52416887"
---
# <a name="replication-subscribers-and-always-on-availability-groups-sql-server"></a>Assinantes de replicação e Grupos de Disponibilidade AlwaysOn (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Quando um grupo de disponibilidade AlwaysOn contendo um banco de dados que é um assinante de replicação executar failover, a assinatura de replicação poderá falhar. Para assinantes transacionais, o agente de distribuição continuará a replicar automaticamente se a assinatura estiver usando o nome do ouvinte do grupo de disponibilidade do assinante. Para mesclar assinantes, um administrador de replicação deve reconfigurar o assinante manualmente, recriando a assinatura.  
  
## <a name="what-is-supported"></a>O que tem suporte  
 A replicação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tem suporte para o failover automático do publicador e de assinantes transacionais. Não há suporte para o failover de um distribuidor em um banco de dados de disponibilidade. Os assinantes de mesclagem podem fazer parte de um grupo de disponibilidade. No entanto, é necessário realizar ações manuais para configurar o novo assinante após um failover. Não é possível combinar Grupos de Disponibilidade com cenários Websync e ssNoVersion Compact.  
  
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
  
  
