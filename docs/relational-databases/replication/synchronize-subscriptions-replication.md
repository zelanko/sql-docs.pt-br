---
title: Sincronizar assinaturas (Replicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ed208c81fe7b3459f22e013117ed1f7cf51ec314
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47796554"
---
# <a name="synchronize-subscriptions-replication"></a>Sincronizar assinaturas (Replicação)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  As assinaturas são sincronizadas por agentes de replicação. O Distribution Agent sincroniza assinaturas para publicações transacionais e de instantâneo e o Merge Agent sincroniza assinaturas para publicações de mesclagem. Você pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], procedimentos armazenados de replicação e RMO (Replication Management Objects) para sincronizar assinaturas e controlar o comportamento de sincronização. Os tópicos a seguir descrevem como sincronizar assinaturas e especificar opções de sincronização.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Criar e aplicar o instantâneo inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [Criar um instantâneo para uma publicação de mesclagem com filtros parametrizados](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [Habilitar a inicialização com um backup para publicações transacionais &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/enable-initialization-with-backup-for-transactional-publications.md)  
  
-   [Inicializar uma assinatura transacional de um backup &#40;Programação de Transact-SQL de Replicação&#41;](../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md)  
  
-   [Inicializar uma assinatura manualmente](../../relational-databases/replication/initialize-a-subscription-manually.md)  
  
-   [Sincronizar uma assinatura pull](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [Sincronizar uma assinatura push](../../relational-databases/replication/synchronize-a-push-subscription.md)  
  
-   [Reinicializar uma assinatura](../../relational-databases/replication/reinitialize-a-subscription.md)  
  
-   [Executar scripts antes e depois de um instantâneo ser aplicado &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   [Executar scripts durante a sincronização &#40;Programação Transact-SQL de Replicação&#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [Exibir e resolver conflitos de dados em publicações de mesclagem &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   [Exibir conflitos de dados em publicações transacionais &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
-   [Sincronizar uma assinatura usando o Gerenciador de Sincronização do Windows &#40;Gerenciador de Sincronização do Windows&#41;](../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)  
  
-   [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [Depurar um manipulador de lógica de negócios &#40;Programação de Replicação&#41;](../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)  
  
-   [Controlar o comportamento de gatilhos e restrições durante a sincronização &#40;Programação de Transact-SQL de Replicação&#41;](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)  
  
-   [Implementar um resolvedor de conflitos personalizado para um artigo de mesclagem](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Sincronizar dados](../../relational-databases/replication/synchronize-data.md)  
  
  
