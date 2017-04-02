---
title: "Especificar um tipo de assinatura de mesclagem e prioridade de resolu&#231;&#227;o de conflitos (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "02/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "resolução de conflitos de replicação de mesclagem [replicação do SQL Server], resolvedores de assinatura de mesclagem"
  - "resolução de conflitos [replicação do SQL Server], replicação de mesclagem"
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Especificar um tipo de assinatura de mesclagem e prioridade de resolu&#231;&#227;o de conflitos (SQL Server Management Studio)
  Especifique uma assinatura de mesclagem tipo e conflito de resolução prioridade no **tipo de assinatura** página do Assistente para nova assinatura. Para obter mais informações sobre como usar esse assistente, consulte [criar uma assinatura Pull](../../relational-databases/replication/create-a-pull-subscription.md) e [criar uma assinatura Push](../../relational-databases/replication/create-a-push-subscription.md).  
  
 Tipo de assinatura não pode ser modificado depois que uma assinatura for criada, mas a prioridade pode ser modificada para o tipo de assinatura de servidor no **Propriedades de assinatura - \< publicador>: \< Banco_de_dados_de_publicação>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) e [View and Modify Pull Subscription Properties](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
### Para especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflito  
  
1.  Sobre o **tipo de assinatura** página do Assistente para nova assinatura, selecione **cliente** ou **servidor** para o **tipo de assinatura** opção.  
  
2.  Se você selecionar um tipo de assinatura **Server**, insira também um valor (0.00 até 99.99) para o **prioridade para resolução de conflitos** opção.  
  
### Para modificar a prioridade para a resolução de conflitos  
  
1.  No **Propriedades de assinatura - \< publicador>: \< Banco_de_dados_de_publicação>** no Editor, digite um valor (0.00 até 99.99) para o **prioridade** opção.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Consulte também  
 [Detecção e resolução de conflito de replicação de mesclagem avançada ](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  