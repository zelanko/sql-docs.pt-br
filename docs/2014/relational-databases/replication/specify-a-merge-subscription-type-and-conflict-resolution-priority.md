---
title: Especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflitos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], merge subscription resolvers
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0ef72b3c36e1cfc7d59792056e080d1cbf2d5c55
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63156352"
---
# <a name="specify-a-merge-subscription-type-and-conflict-resolution-priority-sql-server-management-studio"></a>Especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflitos (SQL Server Management Studio)
  Especifique um tipo de assinatura de mesclagem e prioridade de resolução de conflito na página **Tipo da Assinatura** do Assistente para Novas Assinaturas. Para mais informações sobre como usar esse assistente, consulte [Create a Pull Subscription](create-a-pull-subscription.md) e [Create a Push Subscription](create-a-push-subscription.md).  
  
 O tipo de assinatura não pode ser modificado após a assinatura ser criada, mas a prioridade pode ser modificada para o tipo de assinatura do servidor na caixa de diálogo **Propriedades da Assinatura – \<Publisher>: \<PublicationDatabase>** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Push Subscription Properties](view-and-modify-push-subscription-properties.md) e [View and Modify Pull Subscription Properties](view-and-modify-pull-subscription-properties.md).  
  
### <a name="to-specify-a-merge-subscription-type-and-conflict-resolution-priority"></a>Para especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflito  
  
1.  Na página **Tipo da Assinatura** do Assistente para Novas Assinaturas, selecione **Cliente** ou **Servidor** para a opção **Tipo da Assinatura** .  
  
2.  Se você selecionar um tipo de assinatura no **Servidor**, digite também um valor (0.00 até 99.99) para a opção **Prioridade para a Resolução de Conflitos** .  
  
### <a name="to-modify-the-conflict-resolution-priority"></a>Para modificar a prioridade para a resolução de conflitos  
  
1.  Em **Propriedades da Assinatura – \<Publisher>: \<PublicationDatabase>** no Publicador, digite um valor (0,00 a 99,99) para a opção **Prioridade**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Detecção e resolução de conflito de replicação de mesclagem avançada](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Assinar publicações](subscribe-to-publications.md)  
  
  
