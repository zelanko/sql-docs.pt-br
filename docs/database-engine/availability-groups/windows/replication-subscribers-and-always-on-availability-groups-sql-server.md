---
title: Assinantes de replicação e grupos de disponibilidade (SQL Server)
description: Saiba o que acontece quando um grupo de disponibilidade Always On contendo um banco de dados que é um assinante de replicação faz failover no SQL Server.
ms.custom: seo-lt-2019
ms.date: 08/08/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover subscribers with AlwaysOn
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 0995f269-0580-43ed-b8bf-02b9ad2d7ee6
author: cawrites
ms.author: chadam
ms.openlocfilehash: e15653aebc8f887aa43a95360cc5090df50605d5
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583934"
---
# <a name="replication-subscribers-and-always-on-availability-groups-sql-server"></a>Assinantes de replicação e Grupos de Disponibilidade AlwaysOn (SQL Server)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  Quando um grupo de disponibilidade AlwaysOn contendo um banco de dados que é um assinante de replicação executar failover, a assinatura de replicação poderá falhar. Para assinantes por push de replicação transacional, o agente de distribuição continuará a replicar automaticamente após um failover se a assinatura tiver sido criada usando o nome do ouvinte do grupo de disponibilidade. Para assinantes por pull de replicação transacional, o agente de distribuição continuará a replicar automaticamente após um failover se a assinatura tiver sido criada usando o nome do ouvinte do grupo de disponibilidade e o servidor original do assinante estiver em execução. Isso ocorre porque os trabalhos de agente de distribuição são criados somente no assinante original (réplica primária do grupo de disponibilidade). Para mesclar assinantes, um administrador de replicação deve reconfigurar o assinante manualmente, recriando a assinatura.  
  
## <a name="what-is-supported"></a>O que tem suporte  
 A replicação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tem suporte para o failover automático do publicador e de assinantes transacionais. Os assinantes de mesclagem podem fazer parte de um grupo de disponibilidade. No entanto, é necessário realizar ações manuais para configurar o novo assinante após um failover. Não é possível combinar Grupos de Disponibilidade com cenários WebSync e SQL Server Compact.  
  
## <a name="how-to-create-transactional-subscription-in-an-always-on-environment"></a>Como criar uma assinatura transacional em um ambiente AlwaysOn  
 Para a replicação transacional, use as seguintes etapas para configurar e fazer o failover de um grupo de disponibilidade do assinante:  
  
1.  Antes de criar a assinatura, adicione o banco de dados do assinante ao grupo de disponibilidade AlwaysOn apropriado.  
  
2.  Adicione o ouvinte do grupo de disponibilidade do assinante como um servidor vinculado para todos os nós do grupo de disponibilidade. Essa etapa garante que todos os parceiros de failover potenciais estejam cientes de e possam se conectar ao ouvinte.  
  
3.  Usando o script da seção abaixo **Criando uma assinatura push de replicação transacional** , crie a assinatura usando o nome do ouvinte de grupo de disponibilidade do assinante. Depois de um failover, o nome do ouvinte sempre permanecerá válido, enquanto que o nome de servidor real do assinante dependerá do nó real que se tornou o novo primário.  
  
    > [!NOTE]  
    >  A assinatura deve ser criada usando um script [!INCLUDE[tsql](../../../includes/tsql-md.md)] e não pode ser criada usando o [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)].  
  
4.  Para criar uma assinatura pull:  
  
    1.  Usando o script de exemplo da seção **Como criar uma assinatura pull de replicação transacional** abaixo, crie a assinatura usando o nome do ouvinte do grupo de disponibilidade do assinante. 
   
    2.  Após o failover, crie o trabalho do agente de distribuição na nova réplica primária usando o procedimento armazenado **sp_addpullsubscription_agent**. 
  
 Ao criar uma assinatura pull com o banco de dados de assinatura, no Grupo de disponibilidade, depois de um failover, é recomendável desabilitar o trabalho do agente de distribuição na réplica primária antiga e habilitar o trabalho na nova réplica primária.  
  
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

## <a name="creating-a-transactional-replication-pull-subscription"></a>Como criar uma assinatura pull de replicação transacional  
  
```  
-- commands to execute at the subscriber, in the subscriber database:  
use [<subscriber database name>]  
EXEC sp_addpullsubscription @publisher= N'<publisher name>',
        @publisher_db= N'<publisher database name>',
        @publication= N'<publication name>',
        @subscription_type = N'pull';
Go

EXEC sp_addpullsubscription_agent 
        @publisher =  N'<publisher name>', 
        @subscriber = N'<availability group listener name>',
        @publisher_db= N'<publisher database name>',
        @publication= N'<publication name>' ;
        @job_login = null, @job_password = null, @subscriber_security_mode = 1;  
GO
```  
  
## <a name="to-resume-the-merge-agents-after-the-availability-group-of-the-subscriber-fails-over"></a>Para retomar os Agentes de Mesclagem após o failover do grupo de disponibilidade do assinante  
 Para a replicação de mesclagem, um administrador de replicação deve reconfigurar o assinante manualmente com as seguintes etapas:  
  
1.  Execute **sp_subscription_cleanup** para remover a assinatura antiga no assinante. Execute esta ação na nova réplica primária (a antiga réplica secundária).  
  
2.  Recrie a assinatura criando uma nova assinatura, começando por um novo instantâneo.  
  
> [!NOTE]  
>  O processo atual é inconveniente para assinantes de replicação de mesclagem; entretanto, o cenário principal para a replicação de mesclagem é de usuários desconectados (áreas de trabalho, laptops, dispositivos de fone) que não usarão grupos de disponibilidade AlwaysOn no assinante.  
  
  
