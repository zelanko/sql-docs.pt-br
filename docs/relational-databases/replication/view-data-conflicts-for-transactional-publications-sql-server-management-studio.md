---
title: 'Exibir conflitos de dados (transacional): SSMS'
description: Exibir conflitos de dados na replicação transacional com o SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
- viewing conflict information
ms.assetid: 9977dd75-b0de-4376-9c13-86d80567d8aa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f95994ac6c663020074c5ef3971c1e0a895b3a10
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127778"
---
# <a name="view-data-conflicts-for-transactional-publications-sql-server-management-studio"></a>Exibir conflitos de dados para publicações transacionais (SQL Server Management Studio)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  É possível exibir conflitos para replicação transacional ponto a ponto e replicação transacional com assinaturas de atualização enfileiradas no Visualizador de Conflitos de Replicação [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter informações sobre como os conflitos são detectados e resolvidos, consulte [Detecção de conflitos em replicação ponto a ponto](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md) e [Definir opções de resolução de conflitos em atualização na fila &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md).  
  
 A disponibilidade de dados de conflito depende do tipo de replicação e do período de retenção de conflito:  
  
-   Para replicação ponto a ponto, por padrão, o Distribution Agent falha ao detectar um conflito. Um erro de conflito é registrado no log de erros, mas nenhum dado de conflito é registrado na tabela de conflito; assim, não está disponível para exibição. Se o Distribution Agent tiver permissão para continuar, um conflito será registrado localmente em cada nó onde ele for detectado. Para obter mais informações, consulte “Controlando conflitos” em [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
-   Para assinatura de atualização enfileirada, dados estão disponíveis para cada conflito. Conflitos de dados estão disponíveis no Visualizador de Conflitos de Replicação pelo período de tempo especificado para o período de retenção de conflito, com um padrão de 14 dias. Para definir o período de retenção de conflito, execute qualquer uma das seguintes opções:  
  
    -   Especificar um valor de retenção para o parâmetro @conflict_retention de [sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md).  
  
    -   Especificar o valor de **'conflict_retention'** para o parâmetro @property e um valor de retenção para o parâmetro @value de [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md).  
  
### <a name="to-view-conflicts"></a>Para exibir conflitos  
  
1.  Conecte-se ao servidor adequado em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e, então, expanda o nó do servidor.  
  
    -   Para replicação ponto a ponto, esse é o nó no qual o conflito aconteceu.  
  
    -   Para assinaturas de atualização em fila, esse é o Publicador.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com o botão direito do mouse na publicação para a qual você quer exibir conflitos e então clique em **Exibir Conflitos**.  
  
4.  Na caixa de diálogo **Selecionar Tabela de Conflito** , selecione um banco de dados, publicação e tabela para os quais quer exibir conflitos.  
  
5.  No Visualizador de Conflitos de Replicação, é possível:  
  
    -   Filtrar linhas com os botões à direita da grade superior.  
  
    -   Selecionar uma linha na grade superior para exibir informações sobre aquela linha na grade inferior.  
  
    -   Selecione uma ou mais linhas na grade superior e, então, clique em **Remover** para remover as linhas da tabela de metadados de conflito.  
  
    -   Clique no botão propriedades ( **...** ) para exibir mais informações sobre uma coluna envolvida em um conflito.  
  
    -   Selecione **Registrar os detalhes deste conflito** para registrar dados de conflito em um arquivo. Para especificar um local para o arquivo, aponte para o menu **Exibir** e então clique em **Opções**. Insira um valor ou clique no botão procurar ( **...** ) e então navegue até o arquivo apropriado. Clique em **OK** para fechar a caixa de diálogo **Opções** .  
  
6.  Feche o Visualizador de Conflitos de Replicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Queued Updating Conflict Detection and Resolution](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
