---
title: 'Lição 2: Criando uma assinatura para a publicação de mesclagem | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 06722baa-9065-443e-b1d5-99036cf89074
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 495fb831490a35043b500caea2c835bfd80b6a8c
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54127536"
---
# <a name="lesson-2-creating-a-subscription-to-the-merge-publication"></a>Lição 2: Criando uma assinatura na publicação de mesclagem
  Nesta lição, você criará uma assinatura usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Em seguida, definirá permissões no banco de dados da assinatura e gerará manualmente o instantâneo de dados filtrados para a nova assinatura. Esta lição exige que você tenha concluído a lição anterior, [lição 1: Publicando dados usando a replicação de mesclagem](lesson-1-publishing-data-using-merge-replication.md).  
  
### <a name="to-create-the-subscription"></a>Para criar a assinatura  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó de servidor, expanda a pasta **Replicação** , clique com o botão direito do mouse na pasta **Assinaturas Locais** e clique em **Novas Assinaturas**.  
  
     O Assistente para Nova Assinatura é iniciado.  
  
2.  Na página **Publicação** , clique em **Encontrar Publicador SQL Server** na lista **Publicador** .  
  
3.  Na caixa de diálogo **Conectar ao Servidor** , insira o nome da instância do Publicador na caixa **Nome do servidor** e clique em **Conectar**.  
  
4.  Clique em **AdvWorksSalesOrdersMerge**e em **Avançar**.  
  
5.  Na página Local do Agente de Mesclagem, clique em **Executar cada agente em seu Assinante**e em **Avançar**.  
  
6.  Na página assinantes, selecione o nome da instância do servidor assinante e, em **banco de dados de assinatura**, selecione  **\<novo banco de dados >** na lista.  
  
7.  Na caixa de diálogo **Novo Banco de Dados** , insira **SalesOrdersReplica** na caixa **Nome do banco de dados** , clique em **OK**e em **Avançar**.  
  
8.  Na página segurança do Merge Agent, clique no botão de reticências (**...** ) botão, digite \< _Machine_Name >_**\repl_merge** no **conta de processo** caixa, forneça a senha para essa conta, clique em **Okey**, clique em **próxima**e, em seguida, clique em **próxima** novamente.  
  
9. Na página Inicializar Assinaturas, selecione **Na primeira sincronização** na lista **Inicializar Quando** , clique em **Avançar**e em **Avançar** novamente.  
  
10. Na página valores de HOST_NAME, insira um valor de `adventure-works\pamela0` no **valor de HOST_NAME** caixa e, em seguida, clique em **concluir**.  
  
11. Clique em **Concluir** novamente. Após a criação da assinatura, clique em **Fechar**.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>Definindo permissões de banco de dados no Assinante  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Bancos de Dados**, **SalesOrdersReplica**e **Segurança**, clique com o botão direito do mouse em **Usuários**e selecione **Novo Usuário**.  
  
2.  No **gerais** , insira \< _Machine_Name >_**\repl_merge** no **nome de usuário** , clique no botão reticências ( **...** ), clique em **navegue**, selecione \< _Machine_Name >_**\repl_merge**, clique em **Okey**, clique em **verificar nomes**e, em seguida, clique em **Okey**.  
  
3.  Em **Associação à função do banco de dados**, selecione **db_owner**e clique em **OK** para criar o usuário.  
  
### <a name="to-create-the-filtered-data-snapshot-for-the-subscription"></a>Para criar o instantâneo de dados filtrados para a assinatura  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o nó do servidor e depois expanda a pasta **Replicação** .  
  
2.  Na pasta **Publicações Locais** , clique com o botão direito do mouse na publicação **AdvWorksSalesOrdersMerge** e clique em **Propriedades**.  
  
     A caixa de diálogo **Propriedades da Publicação** é exibida.  
  
3.  Selecione a página **Partições de Dados** e clique em **Adicionar**.  
  
4.  No **Adicionar partição de dados** caixa de diálogo, digite `adventure-works\pamela0` no **valor de HOST_NAME** caixa e, em seguida, clique em **Okey**.  
  
5.  Selecione a partição recém-adicionada, clique em **Gerar os instantâneos selecionados agora**e em **OK**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você criou com êxito uma assinatura para a publicação mesclada e gerou o instantâneo filtrado para a partição de dados da nova assinatura, de modo que ele esteja disponível no momento da inicialização das assinaturas. Em seguida, conceda direitos ao Merge Agent no banco de dados de assinatura e execute o Merge Agent para iniciar a sincronização e iniciar a assinatura. Consulte [lição 3: Sincronizando a assinatura com a publicação de mesclagem](lesson-3-synchronizing-the-subscription-to-the-merge-publication.md).  
  
## <a name="see-also"></a>Consulte também  
 [Subscribe to Publications](subscribe-to-publications.md)   
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
