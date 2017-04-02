---
title: "Li&#231;&#227;o 3: Sincronizando a assinatura com a publica&#231;&#227;o de mesclagem | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "replicação [SQL Server], tutoriais"
ms.assetid: 49008384-2c55-4080-a890-9bceb40e4d6d
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# Li&#231;&#227;o 3: Sincronizando a assinatura com a publica&#231;&#227;o de mesclagem
Nesta lição, você iniciará o Merge Agent para inicializar a assinatura, usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você também usa este procedimento para sincronizar-se com o Publicador. Esta lição exige que você tenha concluído a lição anterior, [Lição 2: Criando uma assinatura na publicação de mesclagem](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-merge-publication.md).  
  
### Para iniciar a sincronização e inicializar a assinatura  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó de servidor, e em seguida, expanda a pasta **Replicação** .  
  
2.  Na pasta **Assinaturas Locais**, clique com o botão direito do mouse na assinatura no banco de dados **SalesOrdersReplica** e clique em **Exibir Status da Sincronização**.  
  
3.  Clique em **Iniciar** para inicializar a assinatura.  
  
## Próximas etapas  
Você executou com sucesso o Merge Agente para iniciar a sincronização e inicializar a assinatura. Você também pode inserir, atualizar ou excluir dados nas tabelas **SalesOrderHeader** ou **SalesOrderDetail** no Publicador ou Assinante, repita esse procedimento quando a conectividade da rede estiver disponível para sincronizar dados entre o Publicador e o Assinante e, em seguida, consulte as tabelas **SalesOrderHeader** ou **SalesOrderDetail** no outro servidor para visualizar as alterações replicadas.  
  
Isso completa o tutorial Replicando Dados com Clientes Móveis. Para um tutorial semelhante que use replicação transacional, consulte [Tutorial: Replicating Data Between Continuously Connected Servers](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md).  
  
## Consulte também  
[Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[Sincronizar dados](../../relational-databases/replication/synchronize-data.md)  
[Sincronizar uma assinatura pull](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
  
  
