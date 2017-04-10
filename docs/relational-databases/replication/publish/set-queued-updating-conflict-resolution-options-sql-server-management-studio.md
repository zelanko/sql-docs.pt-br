---
title: "Definir op&#231;&#245;es de resolu&#231;&#227;o de conflito de atualiza&#231;&#227;o na fila (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "resolução de conflitos [replicação do SQL Server], assinaturas de atualização enfileiradas"
  - "assinaturas de atualização em fila [replicação SQL Server]"
ms.assetid: bb6b6c71-42c7-421a-a0fa-d5594d27e35d
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Definir op&#231;&#245;es de resolu&#231;&#227;o de conflito de atualiza&#231;&#227;o na fila (SQL Server Management Studio)
  Definir as opções de resolução para publicações que suporte enfileirado assinaturas de atualização em conflito o **Opções de assinatura** página o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### Para definir opções de resolução de conflito de atualização na fila  
  
1.  No **Opções de assinatura** página o **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione um dos seguintes valores para o **política de resolução de conflito** opção:  
  
    -   **Mantenha a alteração do Publicador.**  
  
    -   **Mantenha a alteração do Assinante.**  
  
    -   **Reinicialize a assinatura.**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## Consulte também  
 [Enable Updating Subscriptions for Transactional Publications](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)   
 [Detecção e resolução de conflitos de atualização em fila](../../../relational-databases/replication/transactional/queued-updating-conflict-detection-and-resolution.md)  
  
  