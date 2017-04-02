---
title: "Validade e desativa&#231;&#227;o de assinatura | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Distribuidores [replicação do SQL Server], período de retenção da distribuição"
  - "assinaturas [replicação do SQL Server], expiração"
  - "publicações [replicação do SQL Server], períodos de retenção da distribuição"
  - "expiração [replicação do SQL Server]"
  - "períodos de retenção [replicação do SQL Server]"
  - "períodos de retenção da publicação"
  - "período de retenção da distribuição"
  - "assinaturas push [replicação do SQL Server], desativação"
  - "desativando assinaturas"
ms.assetid: 4d03f5ab-e721-4f56-aebc-60f6a56c1e07
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# Validade e desativa&#231;&#227;o de assinatura
  As assinaturas podem ser desativadas ou podem expirar se não forem sincronizadas dentro de um especificado *período de retenção*. A ação que ocorre depende do tipo de replicação e do período de retenção excedido.  
  
 Para definir os períodos de retenção, consulte [definir o período de validade para assinaturas](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md), [definir o período de retenção de distribuição para publicações transacionais e 40; SQL Server Management Studio e 41;](../../relational-databases/replication/set distribution retention period for transactional publications.md), e [Configurar publicação e distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
## Replicação transacional  
 Replicação transacional usa o período de retenção máximo da distribuição (o **@max_distretention** parâmetro [sp_adddistributiondb & #40. Transact-SQL & 41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)) e o período de retenção da publicação (o **@retention** parâmetro [sp_addpublication & #40. Transact-SQL & 41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)):  
  
-   Se uma assinatura não for sincronizada dentro do período de retenção máximo da distribuição (padrão de 72 horas) e houver alterações no banco de dados de distribuição que não foram entregues ao assinante, a assinatura será marcada como desativada pelo **Limpeza da distribuição** trabalho executado no distribuidor. A assinatura deverá ser reinicializada.  
  
-   Se uma assinatura não for sincronizada dentro do período de retenção da publicação (padrão de 336 horas), a assinatura expirará e removida o **assinatura expirada limpeza** trabalho executado no Editor. A assinatura deverá ser criada novamente e ser sincronizada.  
  
     Se uma assinatura push expirar, ela é completamente removida, mas não as assinaturas pull. Você deve limpar as assinaturas pull no Assinante. Para obter mais informações, consulte [Excluir uma assinatura Pull](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
## Replicação de mesclagem  
 Replicação de mesclagem usa o período de retenção da publicação (o **@retention** e **@retention_period_unit** parâmetros de [sp_addmergepublication & #40. Transact-SQL & 41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)). Quando uma assinatura expira, ela deverá ser reiniciada, pois os metadados da assinatura serão removidos. As assinaturas que não forem reinicializadas serão descartadas **assinatura expirada limpeza** trabalho executado no Editor. Por padrão, este trabalho é executado diariamente, ele remove todas as assinaturas push que não sincronizaram por um período duas vezes maior do período de retenção da publicação. Por exemplo:  
  
-   Se a publicação tiver um período de retenção de 14 dias, uma assinatura poderá expirar se não sincronizar dentro de 14 dias.  
  
     Se o publicador estiver executando [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou uma versão posterior e o agente para a assinatura [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou uma versão posterior, uma assinatura expira apenas se houve alterações nos dados na partição de assinatura. Por exemplo, se um Assinante receber dados de cliente apenas de clientes na Alemanha. Se o período de retenção for definido em 14 dias, a assinatura expirará no 14º dia somente se ocorreram mudanças nos dados do cliente alemão nos últimos 14 dias.  
  
-   Do 14º dia até 27 dias após a última sincronização, a assinatura poderá ser reinicializada.  
  
-   28 dias após a última sincronização, a assinatura será descartada **assinatura expirada limpeza** trabalho. Se uma assinatura push expirar, ela é completamente removida, mas não as assinaturas pull. Você deve limpar as assinaturas pull no Assinante. Para obter mais informações, consulte [Excluir uma assinatura Pull](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
### Considerações para definir o período de retenção da publicação para as publicações de mesclagem  
 Lembre-se das considerações a seguir ao definir o período de retenção para publicações de mesclagem:  
  
-   O período de retenção para publicações de mesclagem tem um período de tolerância de 24 horas para incluir os Assinantes em fusos horários diferentes. Por exemplo, se você definir um período de retenção de um dia, o período de retenção real será de 48 horas.  
  
-   A limpeza dos metadados da replicação de mesclagem depende do período de retenção da publicação:  
  
    -   A replicação não poderá limpar os metadados na publicação e nos bancos de dados de assinatura antes de o período de retenção ser atingido. Cuidado ao especificar um valor alto para o período de retenção, pois poderá impactar negativamente o desempenho da replicação. Recomendamos que use uma definição mais baixa se puder prevenir com certeza que todos os Assinantes sincronizarão normalmente dentro daquele período de tempo.  
  
    -   É possível especificar que as assinaturas nunca expirem (um valor de 0 para **@retention**), mas é altamente recomendável que você não use esse valor, porque os metadados não podem ser limpos.  
  
-   O período de retenção para qualquer republicador deve ser definido com um valor igual ou inferior ao período de retenção definido no Publicador original. Você também deve usar os mesmos valores de retenção da publicação para todos os Publicadores e seus parceiros de sincronização alternativos. O uso de valores diferentes pode levar a uma não convergência. Se precisar alterar o valor de retenção da publicação, reinicialize o Assinante para evitar a não convergência de dados.  
  
-   Se, após a limpeza, o período de retenção da publicação aumentar e uma assinatura tentar a mesclagem com o Publicador (que já excluiu os metadados), a assinatura não expirará devido ao aumento no valor da retenção. Porém, o Publicador não tem metadados suficientes para baixar as mudanças para o Assinante, o que resulta em uma não convergência.  
  
## Consulte também  
 [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Administração do agente de replicação](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  