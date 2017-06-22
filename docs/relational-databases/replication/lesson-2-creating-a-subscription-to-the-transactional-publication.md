---
title: "Lição 2: Criando uma assinatura na publicação transacional | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 5995b7d2-7c06-46f5-b96c-2bee879bcda2
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2065387bdf7d23b372f70058c509855e0b0f0792
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-2-creating-a-subscription-to-the-transactional-publication"></a>Lição 2: Criando uma assinatura na publicação transacional
Nessa lição, você criará uma assinatura usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Esta lição exige que você tenha concluído a lição anterior, [Lição 1: Publicando dados usando a replicação transacional](../../relational-databases/replication/lesson-1-publishing-data-using-transactional-replication.md).  
  
### <a name="to-create-the-subscription"></a>Para criar a assinatura  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó do servidor e depois expanda a pasta **Replicação** .  
  
2.  Na pasta **Publicações Locais** , clique com o botão direito do mouse na publicação **AdvWorksProductTrans** e clique em **Novas Assinaturas**.  
  
    O Assistente para Nova Assinatura é iniciado.  
  
3.  Na página Publicação, selecione **AdvWorksProductTrans**e clique em **Avançar**.  
  
4.  Na página Local do Distribution Agent, selecione **Executar todos os agentes no Distribuidor**e clique em **Avançar**.  
  
5.  Na página Assinantes, se o nome da instância do Assinante não estiver exibido, clique em **Adicionar Assinante**, clique em **Adicionar Assinante de SQL Server**, digite o nome da instância do Assinante na caixa de diálogo **Conectar ao Servidor** e em seguida clique em **Conectar**.  
  
6.  Na página Assinantes, selecione o nome da instância do servidor do Assinante e selecione **<New Database>** em **Banco de Dados de Assinatura**.  
  
7.  Na caixa de diálogo **Novo Banco de Dados** , digite **ProductReplica** na caixa **Nome do Banco de Dados** , clique em **OK**e clique em **Avançar**.  
  
8.  Na caixa de diálogo **Segurança do Agente de Distribuição**, clique no botão de reticências (**…**), insira \<*Machine_Name>***\repl_distribution** na caixa **Conta de processo** e insira a senha dessa conta. Em seguida, clique em **OK** e em **Avançar**.  
  
9. Clique em **Concluir** para aceitar os valores padrão nas páginas remanescentes e concluir o assistente.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>Definindo permissões de banco de dados no Assinante  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]; expanda **Databases**, **ProductReplica**e **Security**; clique com o botão direito do mouse em **Usuários**e selecione **Novo Usuário**.  
  
2.  Na página **Geral** , na lista **Tipo de usuário** , selecione **Usuário do Windows**.  
  
3.  Selecione a caixa **Nome de usuário** e clique no botão de reticências (...). Na caixa **Inserir o nome do objeto a ser selecionado**, insira <Machine_Name>**\repl_distribution**, clique em **Verificar nomes** e em **OK**.  
  
4.  Na página **Associação**, na área **Associação à função do banco de dados**, selecione **db_owner** e clique em **OK** para criar o usuário.  
  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>Para exibir o status da sincronização da assinatura  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó do servidor e depois expanda a pasta **Replicação** .  
  
2.  Na pasta **Assinaturas Locais** , expanda a publicação **AdvWorksProductTrans** , clique com o botão direito do mouse na assinatura no banco de dados **ProductReplica** e clique em **Exibir Status da Sincronização**.  
  
    O status atual da sincronização da assinatura é exibido.  
  
3.  Se a assinatura não for visível sob **AdvWorksProductTrans**, pressione F5 para atualizar a lista.  
  
## <a name="next-steps"></a>Próximas etapas  
Você criou com êxito uma assinatura para publicação transacional. Como o Distribution Agent dessa assinatura executa continuamente, a assinatura é inicializada quando ela é criada. Em seguida, você usará os tokens de rastreamento para verificar se as alterações estão sendo replicadas para o Assinante e para determinar a latência. Consulte [Lesson 3: Validating the Subscription and Measuring Latency](../../relational-databases/replication/lesson-3-validating-the-subscription-and-measuring-latency.md).  
  
## <a name="see-also"></a>Consulte também  
[Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)  
[Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  

