---
title: "Especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflitos | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], merge subscription resolvers
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 642a4b5a78f92264f483c2ab6677ddf25ad86fda
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="specify-a-merge-subscription-type-and-conflict-resolution-priority"></a>Especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflitos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifique um tipo de assinatura de mesclagem e prioridade de resolução de conflito na página **Tipo da Assinatura** do Assistente para Novas Assinaturas. Para mais informações sobre como usar esse assistente, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) e [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
 O tipo de assinatura não pode ser modificado após a assinatura ser criada, mas a prioridade pode ser modificada para o tipo de assinatura do servidor na caixa de diálogo **Propriedades da Assinatura – \<Publisher>: \<PublicationDatabase>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) e [View and Modify Pull Subscription Properties](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
### <a name="to-specify-a-merge-subscription-type-and-conflict-resolution-priority"></a>Para especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflito  
  
1.  Na página **Tipo da Assinatura** do Assistente para Novas Assinaturas, selecione **Cliente** ou **Servidor** para a opção **Tipo da Assinatura** .  
  
2.  Se você selecionar um tipo de assinatura no **Servidor**, digite também um valor (0.00 até 99.99) para a opção **Prioridade para a Resolução de Conflitos** .  
  
### <a name="to-modify-the-conflict-resolution-priority"></a>Para modificar a prioridade para a resolução de conflitos  
  
1.  Em **Propriedades da Assinatura – \<Publisher>: \<PublicationDatabase>** no Publicador, digite um valor (0,00 a 99,99) para a opção **Prioridade**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
