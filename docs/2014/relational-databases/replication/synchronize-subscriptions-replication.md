---
title: Sincronizar assinaturas (Replicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- synchronization [SQL Server replication], subscriptions
- subscriptions [SQL Server replication], synchronizing
- replication [SQL Server], synchronization
ms.assetid: cbe13120-8dd9-4309-88dd-07a801c68f5f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d82ef2a50da415504c2a7c461e652beb7547d501
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52772008"
---
# <a name="synchronize-subscriptions-replication"></a>Sincronizar assinaturas (Replicação)
  As assinaturas são sincronizadas por agentes de replicação. O Distribution Agent sincroniza assinaturas para publicações transacionais e de instantâneo e o Merge Agent sincroniza assinaturas para publicações de mesclagem. Você pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], procedimentos armazenados de replicação e RMO (Replication Management Objects) para sincronizar assinaturas e controlar o comportamento de sincronização. Os tópicos a seguir descrevem como sincronizar assinaturas e especificar opções de sincronização.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Criar e aplicar o instantâneo inicial](create-and-apply-the-initial-snapshot.md)  
  
-   [Criar um instantâneo para uma publicação de mesclagem com filtros parametrizados](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [Habilitar a inicialização com um backup para publicações transacionais &#40;SQL Server Management Studio&#41;](enable-initialization-with-backup-for-transactional-publications.md)  
  
-   [Inicializar uma assinatura transacional de um backup &#40;Programação de Transact-SQL de Replicação&#41;](initialize-a-transactional-subscription-from-a-backup.md)  
  
-   [Inicializar uma assinatura manualmente](initialize-a-subscription-manually.md)  
  
-   [Sincronizar uma assinatura pull](synchronize-a-pull-subscription.md)  
  
-   [Sincronizar uma assinatura push](synchronize-a-push-subscription.md)  
  
-   [Reinicializar uma assinatura](reinitialize-a-subscription.md)  
  
-   [Executar scripts antes e depois de um instantâneo ser aplicado &#40;SQL Server Management Studio&#41;](execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   [Executar scripts durante a sincronização &#40;Programação Transact-SQL de Replicação&#41;](execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [Exibir e resolver conflitos de dados em publicações de mesclagem &#40;SQL Server Management Studio&#41;](view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   [Exibir conflitos de dados em publicações transacionais &#40;SQL Server Management Studio&#41;](view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
-   [Sincronizar uma assinatura usando o Gerenciador de Sincronização do Windows &#40;Gerenciador de Sincronização do Windows&#41;](synchronize-a-subscription-using-windows-synchronization-manager.md)  
  
-   [Implementar um manipulador de lógica de negócios para um artigo de mesclagem](implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [Depurar um manipulador de lógica de negócios &#40;Programação de Replicação&#41;](debug-a-business-logic-handler-replication-programming.md)  
  
-   [Controlar o comportamento de gatilhos e restrições durante a sincronização &#40;Programação de Transact-SQL de Replicação&#41;](control-behavior-of-triggers-and-constraints-in-synchronization.md)  
  
-   [Implementar um resolvedor de conflitos personalizado para um artigo de mesclagem](implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="see-also"></a>Consulte também  
 [Sincronizar dados](synchronize-data.md)  
  
  
