---
title: "Detectar e resolver conflitos de replica&#231;&#227;o de mesclagem | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "resolução de conflitos de replicação de mesclagem [replicação do SQL Server], sobre a resolução do conflito"
  - "resolvedor de conflitos padrão"
  - "resolução de conflito [replicação do SQL Server]"
  - "exibindo conflitos de replicação de mesclagem"
  - "resolvendo conflitos de replicação de mesclagem"
  - "artigos [replicação do SQL Server], resolução de conflitos"
  - "resolução de conflito de replicação de mesclagem [replicação do SQL Server]"
  - "resolução de conflitos [replicação do SQL Server], replicação de mesclagem"
ms.assetid: 0d033c76-e8c9-4e35-ab95-4d335abb18c1
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Detectar e resolver conflitos de replica&#231;&#227;o de mesclagem
  Quando o Publicador e o Assinante estão conectados e ocorre a sincronização, o Agente de Mesclagem detecta se há algum conflito. Se houver conflitos detectados, o Agente de Mesclagem utiliza um resolvedor de conflitos para determinar quais dados serão aceitos e propagados para outros sites.  
  
> [!NOTE]  
>  Embora o Assinante esteja sincronizado com o Publicador, os conflitos ocorrem normalmente entre as atualizações feitas em diferentes Assinantes, em lugar de atualizações feitas no Assinante e no Publicador.  
  
 A replicação de mesclagem oferece uma variedade de métodos para detectar e resolver conflitos. Com relação à maioria dos aplicativos, o método padrão é apropriado.  
  
-   Se um conflito ocorrer entre um Publicador e um Assinante, a alteração do Publicador é mantida e a alteração do Assinante é descartada.  
  
-   Se ocorrer um conflito entre dois Assinantes que usam assinaturas de cliente (tipo padrão para assinaturas pull), a alteração do primeiro Assinante para sincronizar com o Publicador é mantida, e a alteração do segundo Assinante é descartada. Para obter informações sobre a especificação de assinaturas de cliente e servidor, consulte [especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflitos e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/specify a merge subscription type and conflict resolution priority.md).  
  
-   Em caso de conflito entre dois Assinantes que usam assinaturas de servidor (tipo padrão para assinaturas push), a alteração do Assinante com o maior valor da prioridade será mantida, e a alteração do segundo Assinante será descartada. Se os valores de prioridade forem iguais, a alteração do primeiro Assinante a sincronizar com o Publicador será mantida.  
  
 Para obter mais informações sobre a detecção de conflitos e a resolução para replicação de mesclagem, consulte [avançada detecção de conflitos de replicação de mesclagem e resolução de](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
## Consulte também  
 [Opções de artigo para replicação de mesclagem](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [Assinar publicações](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  