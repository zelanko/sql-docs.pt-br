---
title: Especificar o tipo e a prioridade de resolução de conflitos (mesclagem)
description: Saiba como especificar o tipo e a política de resolução de conflitos usados por uma assinatura de mesclagem do SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], merge subscription resolvers
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a988935a1d0a614f1b7b336cc95ed82ce2a36214
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75321731"
---
# <a name="specify-a-merge-subscription-type-and-conflict-resolution-priority"></a>Especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflitos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifique um tipo de assinatura de mesclagem e prioridade de resolução de conflito na página **Tipo da Assinatura** do Assistente para Novas Assinaturas. Para mais informações sobre como usar esse assistente, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) e [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
 O tipo de assinatura não pode ser modificado após a assinatura ser criada, mas a prioridade pode ser modificada para o tipo de assinatura do servidor na caixa de diálogo **Propriedades da Assinatura – \<Publisher>: \<PublicationDatabase>** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) e [View and Modify Pull Subscription Properties](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
### <a name="to-specify-a-merge-subscription-type-and-conflict-resolution-priority"></a>Para especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflito  
  
1.  Na página **Tipo da Assinatura** do Assistente para Novas Assinaturas, selecione **Cliente** ou **Servidor** para a opção **Tipo da Assinatura** .  
  
2.  Se você selecionar um tipo de assinatura no **Servidor**, digite também um valor (0.00 até 99.99) para a opção **Prioridade para a Resolução de Conflitos** .  
  
### <a name="to-modify-the-conflict-resolution-priority"></a>Para modificar a prioridade para a resolução de conflitos  
  
1.  Em **Propriedades da Assinatura – \<Publisher>: \<PublicationDatabase>** no Publicador, digite um valor (0,00 a 99,99) para a opção **Prioridade**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Detecção e resolução de conflito de replicação de mesclagem avançada](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
