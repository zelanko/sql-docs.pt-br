---
title: Assinaturas atualizáveis | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.updatablesubscriptions.f1
ms.assetid: 8e9a13a0-6b24-47c6-9d83-3cbaf08f673d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 00d51c24583231f28ec15dd86c1848ba95c345d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63255385"
---
# <a name="updatable-subscriptions"></a>Assinaturas Atualizáveis
  Com a replicação transacional, os dados replicados devem ser tratados como somente leitura; no entanto, podem ser modificados em um Assinante do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando assinaturas atualizáveis. Se for necessário modificar dados no Assinante, escolha um das opções a seguir, dependendo de seus requisitos.  
  
|Tipo de assinatura atualizável|Requisitos|  
|---------------------------------|------------------|  
|Atualização imediata|O Publicador e o Assinante devem estar conectados para atualizar dados no Assinante.|  
|Atualização enfileirada|O Publicador e o Assinante não precisam estar conectados para atualizar dados no Assinante. As atualizações podem ser feitas offline e, depois, sincronizadas entre o Publicador e o Assinante.|  
  
## <a name="options"></a>Opções  
 **Replicar alterações do Assinante**  
 Marque a caixa de seleção na coluna **Replicar** para cada Assinante que possa fazer atualizações. Para esses assinantes que podem fazer atualizações, selecione a opção apropriada na caixa de listagem suspensa, na coluna **Confirmar no Publicador** :  
  
-   Selecione **Confirmar as alterações simultaneamente** para uma assinatura de atualização imediata.  
  
-   Selecione **Enfileirar alterações e confirmar quando possível** para uma assinatura de atualização em fila.  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma assinatura pull](create-a-pull-subscription.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [Assinar publicações](subscribe-to-publications.md)   
 [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
