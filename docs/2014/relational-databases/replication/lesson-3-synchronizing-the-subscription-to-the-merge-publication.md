---
title: 'Lição 3: Sincronizando a assinatura com a publicação de mesclagem | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 49008384-2c55-4080-a890-9bceb40e4d6d
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 847b833d793d3b572b44bcb77903c534300109b7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721003"
---
# <a name="lesson-3-synchronizing-the-subscription-to-the-merge-publication"></a>Lição 3: Sincronizando a assinatura com a publicação de mesclagem
  Nesta lição, você iniciará o Merge Agent para inicializar a assinatura, usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você também usa este procedimento para sincronizar-se com o Publicador. Esta lição exige que você tenha concluído a lição anterior, [lição 2: Criando uma assinatura para a publicação de mesclagem](lesson-2-creating-a-subscription-to-the-merge-publication.md).  
  
### <a name="to-start-synchronization-and-initialize-the-subscription"></a>Para iniciar a sincronização e inicializar a assinatura  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó de servidor, e em seguida, expanda a pasta **Replicação** .  
  
2.  Na pasta **Assinaturas Locais** , clique com o botão direito do mouse na assinatura no banco de dados **SalesOrdersReplica** e clique em **Exibir Status da Sincronização**.  
  
3.  Clique em **Iniciar** para inicializar a assinatura.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você executou com sucesso o Merge Agente para iniciar a sincronização e inicializar a assinatura. Você também pode inserir, atualizar ou excluir dados nas tabelas **SalesOrderHeader** ou **SalesOrderDetail** no Publicador ou Assinante, repita esse procedimento quando a conectividade da rede estiver disponível para sincronizar dados entre o Publicador e o Assinante e, em seguida, consulte as tabelas **SalesOrderHeader** ou **SalesOrderDetail** no outro servidor para visualizar as alterações replicadas.  
  
 Isso completa o tutorial Replicando Dados com Clientes Móveis. Para obter um tutorial semelhante que usa replicação transacional, consulte [Tutorial: Replicando dados entre continuamente servidores conectados](tutorial-replicating-data-between-continuously-connected-servers.md).  
  
## <a name="see-also"></a>Consulte também  
 [Inicializar uma assinatura com um instantâneo](initialize-a-subscription-with-a-snapshot.md)   
 [Sincronizar dados](synchronize-data.md)   
 [Sincronizar uma assinatura pull](synchronize-a-pull-subscription.md)  
  
  
