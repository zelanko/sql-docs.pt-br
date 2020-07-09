---
title: Tipo de assinatura | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.subscriptiontype.f1
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: c8b31b962fed5f250f2c16c74736a1a2061341fd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729348"
---
# <a name="subscription-type"></a>Tipo de Assinatura
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
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
  
  
