---
title: "Propriedades da Assinatura - Publicador | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.subproperties.publisher.f1"
helpviewer_keywords: 
  - "caixa de diálogo Propriedades da Assinatura"
ms.assetid: d4b2bc8b-0431-4331-8305-8992c96d0d34
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Propriedades da Assinatura - Publicador
  O **Propriedades de assinatura** caixa de diálogo no Editor permite exibir e definir propriedades para inscrições de envio. Você também pode exibir algumas propriedades para assinaturas pull, mas o **Propriedades de assinaturas** caixa de diálogo no assinante exibe propriedades adicionais e permite a modificação de propriedades.  
  
 Cada propriedade no **Propriedades de assinatura** caixa de diálogo inclui uma descrição. Clique em uma propriedade para ver sua descrição exibida na parte inferior da caixa de diálogo. Esse tópico fornece informações adicionais sobre várias propriedades, muitas das quais são exibidas no Publicador somente para assinaturas push. As propriedades são agrupadas nas categorias seguintes:  
  
-   Propriedades que se aplicam a todas as assinaturas.  
  
-   Propriedades que se aplicam a assinaturas transacionais.  
  
-   Propriedades que se aplicam a assinaturas de mesclagem.  
  
 Se uma opção for exibida como somente leitura, só poderá ser definida quando a assinatura for criada. Se você quiser definir opções que não estão disponíveis no Assistente para Nova Assinatura, crie a assinatura com procedimentos armazenados. Para obter mais informações, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) e [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
## Opções para todas as assinaturas  
 **Segurança**  
 Clique o **conta de processo do agente** linha e, em seguida, clique no botão Propriedades (**...**) para alterar a conta na qual o Distribution Agent ou do Merge Agent é executado no distribuidor. Para alterar a conta sob a qual o Distribution Agent ou do Merge Agent faz conexões com o assinante, clique **conexão do assinante**, e, em seguida, clique no botão Propriedades (**...**).  
  
 Para obter mais informações sobre as permissões necessárias para cada agente, consulte [modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## Opções para assinaturas transacionais  
 **Evitar loop de transação**  
 Determina se o Distribution Agent envia transações originadas no Assinante de volta para o Assinante: Essa opção é usada para replicação transacional bidirecional. Para obter mais informações, consulte [replicação transacional bidirecional](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md).  
  
 **Assinatura atualizável**  
 Determina se as alterações do Assinante serão replicadas de volta no Publicador. As alterações podem ser replicadas usando atualização enfileirada ou imediata. A opção **método de atualização do assinante** determina qual método usar. Para obter mais informações, consulte [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
## Opções para assinaturas de mesclagem  
 **Definição de partição (HOST_NAME)**  
 Para uma publicação que usa filtros com parâmetros, a replicação de mesclagem avalia uma das duas funções de sistema (ou ambas, se as referências de filtro ambas as funções) durante a sincronização para determinar os dados que um assinante deve receber: **suser_sname ()** ou **HOST_NAME ()**. Por padrão, **HOST_NAME ()** retorna o nome do computador no qual o Merge Agent está em execução, mas você pode substituir esse valor no novo Assistente de assinatura. Para obter mais informações sobre filtros parametrizados e substituindo **HOST_NAME ()**, consulte [filtros de linha com parâmetros](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 **Tipo de assinatura** e **prioridade**  
 Exibe se a assinatura é uma assinatura de cliente ou servidor (isso não pode ser alterado depois que a assinatura tiver sido criada). Assinaturas de Servidor podem republicar dados para outros Assinantes e podem ter atribuição de prioridade para resolução de conflito.  
  
 Se você selecionou um tipo de assinatura de servidor no Assistente para Nova Assinatura, o Assinante receberá uma prioridade que será usada durante resolução de conflito.  
  
 **Resolver conflitos interativamente**  
 Determina se o Resolver Interativo deve usar a interface do usuário para resolver conflitos durante a sincronização de mesclagem. Isso requer um valor de **Habilitar** para **Gerenciador de sincronização do Windows Use**. Para obter mais informações, confira [Interactive Conflict Resolution](../../relational-databases/replication/merge/interactive-conflict-resolution.md).  
  
## Consulte também  
 [Exibir e modificar propriedades de assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  