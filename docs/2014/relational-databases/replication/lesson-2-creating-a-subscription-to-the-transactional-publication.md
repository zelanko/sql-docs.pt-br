---
title: 'Lição 2: Criando uma assinatura na publicação transacional | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 5995b7d2-7c06-46f5-b96c-2bee879bcda2
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: d3e8b5f0be58d9153fbe4d0ffd0287ea753fcc5e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721080"
---
# <a name="lesson-2-creating-a-subscription-to-the-transactional-publication"></a>Lição 2: Criando uma assinatura na publicação transacional
  Nessa lição, você criará uma assinatura usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Esta lição exige que você tenha concluído a lição anterior, [Lição 1: Publicando dados usando a replicação transacional](lesson-1-publishing-data-using-transactional-replication.md).  
  
### <a name="to-create-the-subscription"></a>Para criar a assinatura  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó do servidor e expanda a pasta **replicação** .  
  
2.  Na pasta **Publicações Locais** , clique com o botão direito do mouse na publicação **AdvWorksProductTrans** e clique em **Novas Assinaturas**.  
  
     O Assistente para Nova Assinatura é iniciado.  
  
3.  Na página Publicação, selecione **AdvWorksProductTrans**e clique em **Avançar**.  
  
4.  Na página Local do Distribution Agent, selecione **Executar todos os agentes no Distribuidor**e clique em **Avançar**.  
  
5.  Na página Assinantes, se o nome da instância do Assinante não estiver exibido, clique em **Adicionar Assinante**, clique em **Adicionar Assinante de SQL Server**, digite o nome da instância do Assinante na caixa de diálogo **Conectar ao Servidor** e em seguida clique em **Conectar**.  
  
6.  Na página assinantes, selecione o nome da instância do servidor do assinante e selecione ** \<novo banco de dados>** em **banco de dados de assinatura**.  
  
7.  Na caixa de diálogo **Novo Banco de Dados** , digite **ProductReplica** na caixa **Nome do Banco de Dados** , clique em **OK**e clique em **Avançar**.  
  
8.  Na caixa de diálogo **agente de distribuição segurança** , clique no botão de reticências (**...**) \<, digite _Machine_Name>_ **\ repl_distribution** na caixa **conta de processo** , digite a senha dessa conta, clique em **OK**e em **Avançar**.  
  
9. Clique em **Concluir** para aceitar os valores padrão nas páginas remanescentes e concluir o assistente.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>Definindo permissões de banco de dados no Assinante  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]; expanda **Databases**, **ProductReplica**e **Security**; clique com o botão direito do mouse em **Usuários**e selecione **Novo Usuário**.  
  
2.  Na página **Geral** , na lista **Tipo de usuário** , selecione **Usuário do Windows**.  
  
3.  Selecione a caixa **nome de usuário** e clique no botão de reticências (...), na caixa **Inserir o nome do objeto a ser selecionado** , digite <Machine_Name>**\ Repl_distribution**, clique em **verificar nomes**e clique em **OK**.  
  
4.  Na página **Associação** , na área **Associação à função do banco de dados** , selecione **db_owner**e clique em **OK** para criar o usuário.  
  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>Para exibir o status da sincronização da assinatura  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó do servidor e expanda a pasta **replicação** .  
  
2.  Na pasta **Assinaturas Locais** , expanda a publicação **AdvWorksProductTrans** , clique com o botão direito do mouse na assinatura no banco de dados **ProductReplica** e clique em **Exibir Status da Sincronização**.  
  
     O status atual da sincronização da assinatura é exibido.  
  
3.  Se a assinatura não for visível sob **AdvWorksProductTrans**, pressione F5 para atualizar a lista.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você criou com êxito uma assinatura para publicação transacional. Como o Distribution Agent dessa assinatura executa continuamente, a assinatura é inicializada quando ela é criada. Em seguida, você usará os tokens de rastreamento para verificar se as alterações estão sendo replicadas para o Assinante e para determinar a latência. Consulte [Lesson 3: Validating the Subscription and Measuring Latency](lesson-3-validating-the-subscription-and-measuring-latency.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Inicializar uma assinatura com um instantâneo](initialize-a-subscription-with-a-snapshot.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [Assinar publicações](subscribe-to-publications.md)  
  
  
