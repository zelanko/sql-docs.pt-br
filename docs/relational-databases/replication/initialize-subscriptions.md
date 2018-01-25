---
title: Inicializar assinaturas | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newsubwizard.initializesubscriptions.f1
ms.assetid: 7b170e4e-470d-4828-a9ed-7435b0b03514
caps.latest.revision: "24"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 11573e80fe10775fd567d4ef11eb3e139421ab2f
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="initialize-subscriptions"></a>Inicializar Assinaturas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Os Assinantes devem ser inicializados antes que possam começar a receber dados replicados. Um conjunto de dados inicial não é requerido, mas o Assinante deve ter pelo menos o esquema para cada objeto replicado e todas as tabelas de metadados e procedimentos requeridos pela replicação.  
  
## <a name="options"></a>Opções  
 **Propriedades da assinatura**  
 Marque a caixa de seleção na coluna **Inicializar** para cada Assinante que requer um conjunto de dados inicial. Se a caixa de seleção for desmarcada, somente os metadados de replicação e procedimentos serão inicializados. Para mais informações sobre a inicialização de uma assinatura sem um instantâneo, consulte [Inicializar uma assinatura transacional sem um instantâneo](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 Selecione **Imediatamente** na caixa de listagem suspensa na coluna **Inicializar Quando** para que o Agente de Mesclagem ou Agente de Distribuição transfira os arquivos de instantâneo para o Assinante depois que o assistente for concluído. Selecione **Na primeira sincronização** para que o agente transfira os arquivos da próxima vez em que for agendado para executar. A opção **Imediatamente** não está disponível para assinaturas pull no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. O Agente de Mesclagem e Agente de Distribuição não executam em instâncias do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]; portanto a assinatura deve ser reiniciada por outro método.  
  
> [!NOTE]  
>  O assistente pode solicitar uma conexão com o Distribuidor para iniciar o trabalho apropriado para o Agente de Distribuição ou Agente de Mesclagem.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Inicializar uma assinatura](../../relational-databases/replication/initialize-a-subscription.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
