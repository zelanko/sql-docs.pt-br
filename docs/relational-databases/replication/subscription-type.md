---
title: Tipo de assinatura | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.subscriptiontype.f1
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: fc7416a12971d29c495293213e3f7c0180954dd7
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39545256"
---
# <a name="subscription-type"></a>Tipo de Assinatura
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
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
  
## <a name="see-also"></a>Consulte Também  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
