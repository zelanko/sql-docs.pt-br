---
title: 'Lição 3: Sincronizando a assinatura com a publicação de mesclagem | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 49008384-2c55-4080-a890-9bceb40e4d6d
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 79b8774de74316a4595d7ebd028b9f2e853882bd
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/10/2018
---
# <a name="lesson-3-synchronizing-the-subscription-to-the-merge-publication"></a>Lição 3: Sincronizando a assinatura com a publicação de mesclagem
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Nesta lição, você iniciará o Merge Agent para inicializar a assinatura, usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você também usa este procedimento para sincronizar-se com o Publicador. Esta lição exige que você tenha concluído a lição anterior, [Lição 2: Criando uma assinatura na publicação de mesclagem](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-merge-publication.md).  
  
### <a name="to-start-synchronization-and-initialize-the-subscription"></a>Para iniciar a sincronização e inicializar a assinatura  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó de servidor, e em seguida, expanda a pasta **Replicação** .  
  
2.  Na pasta **Assinaturas Locais** , clique com o botão direito do mouse na assinatura no banco de dados **SalesOrdersReplica** e clique em **Exibir Status da Sincronização**.  
  
3.  Clique em **Iniciar** para inicializar a assinatura.  
  
## <a name="next-steps"></a>Next Steps  
Você executou com sucesso o Merge Agente para iniciar a sincronização e inicializar a assinatura. Você também pode inserir, atualizar ou excluir dados nas tabelas **SalesOrderHeader** ou **SalesOrderDetail** no Publicador ou Assinante, repita esse procedimento quando a conectividade da rede estiver disponível para sincronizar dados entre o Publicador e o Assinante e, em seguida, consulte as tabelas **SalesOrderHeader** ou **SalesOrderDetail** no outro servidor para visualizar as alterações replicadas.  
  
Isso completa o tutorial Replicando Dados com Clientes Móveis. Para um tutorial semelhante que use replicação transacional, consulte [Tutorial: Replicating Data Between Continuously Connected Servers](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md).  
  
## <a name="see-also"></a>Consulte Também  
[Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[Sincronizar dados](../../relational-databases/replication/synchronize-data.md)  
[Sincronizar uma assinatura pull](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
  
  
