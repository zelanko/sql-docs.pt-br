---
title: "Inicializar Assinaturas | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.initializesubscriptions.f1"
ms.assetid: 7b170e4e-470d-4828-a9ed-7435b0b03514
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Inicializar Assinaturas
  Os Assinantes devem ser inicializados antes que possam começar a receber dados replicados. Um conjunto de dados inicial não é requerido, mas o Assinante deve ter pelo menos o esquema para cada objeto replicado e todas as tabelas de metadados e procedimentos requeridos pela replicação.  
  
## Opções  
 **Propriedades da assinatura**  
 Marque a caixa de seleção no **inicializar** coluna para cada assinante que requer um conjunto de dados inicial. Se a caixa de seleção for desmarcada, somente os metadados de replicação e procedimentos serão inicializados. Para obter mais informações sobre como inicializar uma assinatura sem um instantâneo, consulte [inicializar um transacional assinatura sem um instantâneo](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 Selecione **imediatamente** da caixa de listagem suspensa de **inicializar quando** coluna para que o Merge Agent ou Distribution Agent transfira arquivos para o assinante de instantâneo depois que o assistente for concluído. Selecione **Na primeira sincronização** para que o agente transfira os arquivos da próxima vez em que for agendado para executar. A opção **Imediatamente** não está disponível para assinaturas pull no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. O Agente de Mesclagem e Agente de Distribuição não executam em instâncias do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]; portanto a assinatura deve ser reiniciada por outro método.  
  
> [!NOTE]  
>  O assistente pode solicitar uma conexão com o Distribuidor para iniciar o trabalho apropriado para o Agente de Distribuição ou Agente de Mesclagem.  
  
## Consulte também  
 [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Inicializar uma assinatura](../../relational-databases/replication/initialize-a-subscription.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  