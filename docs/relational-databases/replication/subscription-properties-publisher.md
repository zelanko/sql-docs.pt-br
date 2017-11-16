---
title: "Propriedades da Assinatura – Publicador | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newsubwizard.subproperties.publisher.f1
helpviewer_keywords: Subscription Properties dialog box
ms.assetid: d4b2bc8b-0431-4331-8305-8992c96d0d34
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5e23aa71ea138af1689a60a44f00424a4158906c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="subscription-properties---publisher"></a>Propriedades da Assinatura - Publicador
  A caixa de diálogo **Propriedades da Assinatura** no Publicador permite exibir e definir propriedades para assinaturas push. Você também pode exibir algumas propriedades de assinaturas pull, mas a caixa de diálogo **Propriedades da Assinatura** no Assinante exibe propriedades adicionais e permite que elas sejam modificadas.  
  
 Cada propriedade na caixa de diálogo **Propriedades da Assinatura** inclui uma descrição. Clique em uma propriedade para ver sua descrição exibida na parte inferior da caixa de diálogo. Esse tópico fornece informações adicionais sobre várias propriedades, muitas das quais são exibidas no Publicador somente para assinaturas push. As propriedades são agrupadas nas categorias seguintes:  
  
-   Propriedades que se aplicam a todas as assinaturas.  
  
-   Propriedades que se aplicam a assinaturas transacionais.  
  
-   Propriedades que se aplicam a assinaturas de mesclagem.  
  
 Se uma opção for exibida como somente leitura, só poderá ser definida quando a assinatura for criada. Se você quiser definir opções que não estão disponíveis no Assistente para Nova Assinatura, crie a assinatura com procedimentos armazenados. Para obter mais informações, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) e [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
## <a name="options-for-all-subscriptions"></a>Opções para todas as assinaturas  
 **Segurança**  
 Clique na linha **Conta de processo de agente** e, depois, clique no botão de propriedades (**...**) para alterar a conta na qual o Distribution Agent ou Merge Agent são executados no Distribuidor. Para alterar a conta na qual o Distribution Agent ou Merge Agent fazem conexões com o Assinante, clique em **Conexão do Assinante**e, depois, clique no botão de propriedades (**...**).  
  
 Para obter mais informações sobre as permissões exigidas para cada agente, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## <a name="options-for-transactional-subscriptions"></a>Opções para assinaturas transacionais  
 **Evitar loop de transação**  
 Determina se o Distribution Agent envia transações originadas no Assinante de volta para o Assinante: Essa opção é usada para replicação transacional bidirecional. Para obter mais informações, consulte [Bidirectional Transactional Replication](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md).  
  
 **Assinatura atualizável**  
 Determina se as alterações do Assinante serão replicadas de volta no Publicador. As alterações podem ser replicadas usando atualização enfileirada ou imediata. A opção **Método de atualização do assinante** determina qual método usar. Para obter mais informações, consulte [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
## <a name="options-for-merge-subscriptions"></a>Opções para assinaturas de mesclagem  
 **Definição de partição (HOST_NAME)**  
 Para uma publicação que usa filtros com parâmetros, a replicação de mesclagem avalia uma das duas funções de sistema (ou ambas, se as referências de filtro funcionam) durante a sincronização para determinar a data em que um Assinante deve receber: **SUSER_SNAME()** ou **HOST_NAME()**. Por padrão, **HOST_NAME()** retorna o nome do computador no qual o Merge Agent está sendo executado, mas esse valor pode ser substituído no Assistente para Nova Assinatura. Para obter mais informações sobre filtros com parâmetros e substituição de **HOST_NAME ()**, consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 **Tipo de assinatura** e **Prioridade**  
 Exibe se a assinatura é uma assinatura de cliente ou servidor (isso não pode ser alterado depois que a assinatura tiver sido criada). Assinaturas de Servidor podem republicar dados para outros Assinantes e podem ter atribuição de prioridade para resolução de conflito.  
  
 Se você selecionou um tipo de assinatura de servidor no Assistente para Nova Assinatura, o Assinante receberá uma prioridade que será usada durante resolução de conflito.  
  
 **Resolver conflitos interativamente**  
 Determina se o Resolver Interativo deve usar a interface do usuário para resolver conflitos durante a sincronização de mesclagem. Isso requer um valor de **Habilitar** para **Usar Gerenciador de Sincronização do Windows**. Para obter mais informações, confira [Interactive Conflict Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar propriedades de assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Exibir e modificar propriedades de assinatura push](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Assinar Publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
