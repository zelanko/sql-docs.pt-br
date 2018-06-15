---
title: Expiração e desativação de assinatura | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Distributors [SQL Server replication], distribution retention period
- subscriptions [SQL Server replication], expiration
- publications [SQL Server replication], publication retention periods
- expiration [SQL Server replication]
- retention periods [SQL Server replication]
- publication retention periods
- distribution retention period
- subscriptions [SQL Server replication], deactivation
- deactivating subscriptions
ms.assetid: 4d03f5ab-e721-4f56-aebc-60f6a56c1e07
caps.latest.revision: 45
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5135c5773a99804e692d0e46467d5d62dcd0d02c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32963631"
---
# <a name="subscription-expiration-and-deactivation"></a>Validade e desativação de assinatura
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  As assinaturas podem ser desativadas ou podem expirar se não forem sincronizadas dentro de um *período de retenção*especificado. A ação que ocorre depende do tipo de replicação e do período de retenção excedido.  
  
 Para definir os períodos de retenção, consulte [Definir o período de validade para assinaturas](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md), [Definir o período de retenção de distribuição para publicações transacionais &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/set-distribution-retention-period-for-transactional-publications.md) e [Configurar publicação e distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
## <a name="transactional-replication"></a>Replicação transacional  
 A replicação transacional usa o período de retenção máximo da distribuição (o parâmetro **@max_distretention** de [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)) e o período de retenção da publicação (o parâmetro **@retention** do [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)):  
  
-   Se a assinatura não for sincronizada dentro do período de retenção máximo da distribuição (padrão de 72 horas) e houver mudanças no banco de dados de distribuição que não foram entregues ao Assinante, a assinatura será marcada como desativada pelo trabalho de **Limpeza da distribuição** sendo executado no Distribuidor. A assinatura deverá ser reinicializada.  
  
-   Se a assinatura não for sincronizada no período de retenção máximo da publicação (padrão de 336 horas), a assinatura expirará e será descartada pelo trabalho de **Limpeza de assinaturas expiradas** executado no Publicador. A assinatura deverá ser criada novamente e ser sincronizada.  
  
     Se uma assinatura push expirar, ela é completamente removida, mas não as assinaturas pull. Você deve limpar as assinaturas pull no Assinante. Para obter mais informações, consulte [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
## <a name="merge-replication"></a>Replicação de mesclagem  
 A replicação de mesclagem usa o período de retenção da publicação (os parâmetros **@retention** e **@retention_period_unit** do [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)). Quando uma assinatura expira, ela deverá ser reiniciada, pois os metadados da assinatura serão removidos. As assinaturas que não forem reinicializadas serão descartadas pelo trabalho de **Limpeza de assinaturas expiradas** executado no Publicador. Por padrão, este trabalho é executado diariamente, ele remove todas as assinaturas push que não sincronizaram por um período duas vezes maior do período de retenção da publicação. Por exemplo:  
  
-   Se a publicação tiver um período de retenção de 14 dias, uma assinatura poderá expirar se não sincronizar dentro de 14 dias.  
  
     Se o Publicador estiver executando o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou uma versão posterior e o agente para a assinatura pertencer ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou versão posterior, uma assinatura só expirará se ocorrerem mudanças nos dados naquela partição da assinatura. Por exemplo, se um Assinante receber dados de cliente apenas de clientes na Alemanha. Se o período de retenção for definido em 14 dias, a assinatura expirará no 14º dia somente se ocorreram mudanças nos dados do cliente alemão nos últimos 14 dias.  
  
-   Do 14º dia até 27 dias após a última sincronização, a assinatura poderá ser reinicializada.  
  
-   No 28º dia após a última sincronização, a assinatura será descartada pelo trabalho de **Limpeza de assinaturas expiradas** . Se uma assinatura push expirar, ela é completamente removida, mas não as assinaturas pull. Você deve limpar as assinaturas pull no Assinante. Para obter mais informações, consulte [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
### <a name="considerations-for-setting-the-publication-retention-period-for-merge-publications"></a>Considerações para definir o período de retenção da publicação para as publicações de mesclagem  
 Lembre-se das considerações a seguir ao definir o período de retenção para publicações de mesclagem:  
  
-   O período de retenção para publicações de mesclagem tem um período de tolerância de 24 horas para incluir os Assinantes em fusos horários diferentes. Por exemplo, se você definir um período de retenção de um dia, o período de retenção real será de 48 horas.  
  
-   A limpeza dos metadados da replicação de mesclagem depende do período de retenção da publicação:  
  
    -   A replicação não poderá limpar os metadados na publicação e nos bancos de dados de assinatura antes de o período de retenção ser atingido. Cuidado ao especificar um valor alto para o período de retenção, pois poderá impactar negativamente o desempenho da replicação. Recomendamos que use uma definição mais baixa se puder prevenir com certeza que todos os Assinantes sincronizarão normalmente dentro daquele período de tempo.  
  
    -   É possível especificar para que as assinaturas nunca expirem (um valor de 0 para a **@retention**), mas recomendamos não usar este valor, pois os metadados não poderão ser limpos.  
  
-   O período de retenção para qualquer republicador deve ser definido com um valor igual ou inferior ao período de retenção definido no Publicador original. Você também deve usar os mesmos valores de retenção da publicação para todos os Publicadores e seus parceiros de sincronização alternativos. O uso de valores diferentes pode levar a uma não convergência. Se precisar alterar o valor de retenção da publicação, reinicialize o Assinante para evitar a não convergência de dados.  
  
-   Se, após a limpeza, o período de retenção da publicação aumentar e uma assinatura tentar a mesclagem com o Publicador (que já excluiu os metadados), a assinatura não expirará devido ao aumento no valor da retenção. Porém, o Publicador não tem metadados suficientes para baixar as mudanças para o Assinante, o que resulta em uma não convergência.  
  
## <a name="see-also"></a>Consulte Também  
 [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Administração do agente de replicação](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
