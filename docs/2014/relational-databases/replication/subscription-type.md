---
title: Tipo de assinatura | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.subscriptiontype.f1
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3bec01b8de34c7b7273b4599a986cb3064d52298
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37281032"
---
# <a name="subscription-type"></a>Tipo de Assinatura
  A replicação de mesclagem oferece dois tipos de assinatura: servidor e cliente (referenciado em versões anteriores do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como global e local, respectivamente). Os Assinantes com uma assinatura de servidor podem:  
  
-   Republicar dados para outros Assinantes.  
  
-   Servir como parceiros de sincronização alternativos.  
  
-   Resolver conflitos de acordo com uma prioridade definida.  
  
 A maioria dos Assinantes não requer essa funcionalidade e usa uma assinatura de cliente. Assinaturas de cliente ainda permitem detecção e resolução de conflitos, mas não é atribuída uma prioridade aos Assinantes: o primeiro Assinante a enviar uma alteração ao Publicador ganha todos os conflitos que possam surgir daquela alteração.  
  
> [!NOTE]  
>  O tipo da assinatura não pode ser alterado depois que ela é criada.  
  
## <a name="options"></a>Opções  
 **Propriedades da assinatura**  
 Para cada Assinante, selecione **Cliente** ou **Servidor** na caixa de listagem suspensa na coluna **Tipo de Assinatura** . Para Assinantes com assinaturas de servidor, insira um número entre 0 e 99.99 na coluna **Prioridade para a Resolução de Conflitos** (quanto mais alto for o número, mais alta será a prioridade para o Assinante).  
  
## <a name="see-also"></a>Consulte também  
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [Assinar publicações](subscribe-to-publications.md)  
  
  
