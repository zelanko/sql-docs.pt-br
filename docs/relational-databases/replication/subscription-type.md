---
title: "Tipo de Assinatura | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.subscriptiontype.f1"
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Tipo de Assinatura
  Replicação de mesclagem oferece dois tipos de assinatura: servidor e cliente (referenciado em versões anteriores do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como global e local, respectivamente). Os Assinantes com uma assinatura de servidor podem:  
  
-   Republicar dados para outros Assinantes.  
  
-   Servir como parceiros de sincronização alternativos.  
  
-   Resolver conflitos de acordo com uma prioridade definida.  
  
 A maioria dos Assinantes não requer essa funcionalidade e usa uma assinatura de cliente. Assinaturas de cliente ainda permitem detecção e resolução de conflitos, mas não é atribuída uma prioridade aos Assinantes: o primeiro Assinante a enviar uma alteração ao Publicador ganha todos os conflitos que possam surgir daquela alteração.  
  
> [!NOTE]  
>  O tipo da assinatura não pode ser alterado depois que ela é criada.  
  
## Opções  
 **Propriedades da assinatura**  
 Para cada assinante, selecione **cliente** ou **Server** da caixa de listagem suspensa de **tipo de assinatura** coluna. Para assinantes com assinaturas de servidor, insira um número entre 0 e 99,99 no **prioridade para resolução de conflitos** coluna (quanto maior o número, maior a prioridade para o assinante).  
  
## Consulte também  
 [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  