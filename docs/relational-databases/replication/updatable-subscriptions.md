---
title: Assinaturas atualizáveis | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.updatablesubscriptions.f1
ms.assetid: 8e9a13a0-6b24-47c6-9d83-3cbaf08f673d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d89c8a18804722a3d7727b56833c2513ec994518
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67895255"
---
# <a name="updatable-subscriptions"></a>Assinaturas Atualizáveis
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Com a replicação transacional, os dados replicados devem ser tratados como somente leitura; no entanto, você pode modificá-los em um Assinante do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando assinaturas atualizáveis. Se for necessário modificar dados no Assinante, escolha um das opções a seguir, dependendo de seus requisitos.  
  
|Tipo de assinatura atualizável|Requisitos|  
|---------------------------------|------------------|  
|Atualização imediata|O Publicador e o Assinante devem estar conectados para atualizar dados no Assinante.|  
|Atualização enfileirada|O Publicador e o Assinante não precisam estar conectados para atualizar dados no Assinante. As atualizações podem ser feitas offline e, depois, sincronizadas entre o Publicador e o Assinante.|  
  
## <a name="options"></a>Opções  
 **Replicar alterações do Assinante**  
 Marque a caixa de seleção na coluna **Replicar** para cada Assinante que possa fazer atualizações. Para esses assinantes que podem fazer atualizações, selecione a opção apropriada na caixa de listagem suspensa, na coluna **Confirmar no Publicador** :  
  
-   Selecione **Confirmar as alterações simultaneamente** para uma assinatura de atualização imediata.  
  
-   Selecione **Enfileirar alterações e confirmar quando possível** para uma assinatura de atualização em fila.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
