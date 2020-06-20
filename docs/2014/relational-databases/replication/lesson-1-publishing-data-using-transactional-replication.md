---
title: 'Lição 1: Publicando dados que usam a replicação transacional | Microsoft Docs'
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 9c55aa3c-4664-41fc-943f-e817c31aad5e
author: rothja
ms.author: jroth
ms.openlocfilehash: ff715b51a7fa84a462d1439e78627d648e20472d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065958"
---
# <a name="lesson-1-publishing-data-using-transactional-replication"></a>Lição 1: publicando dados que usam replicação transacional
   Nesta lição, você aprenderá a criar uma publicação transacional usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para publicar um subconjunto filtrado da tabela **Produto** no banco de dados de exemplo do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Você também adicionará o logon do SQL Server usado pelo Distribution Agent à PAL (lista de acesso à publicação). Antes de iniciar este tutorial, você deverá ter completado o tutorial anterior, [Preparando o servidor para replicação](tutorial-preparing-the-server-for-replication.md).  
  
### <a name="to-create-a-publication-and-define-articles"></a>Para criar uma publicação e definir artigos  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó de servidor.  
  
2.  Expanda a pasta **Replicação** , clique com o botão direito do mouse na pasta **Publicações Locais** e clique em **Nova Publicação**.  
  
     O Assistente de Configuração de Publicação é inicializado.  
  
3.  Na página Banco de Dados de Publicação, selecione [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]e clique em **Avançar**.  
  
4.  Na página Tipo de Publicação, selecione **Publicação transacional**e clique em **Avançar**.  
  
5.  Na página Artigos, expanda o nó **Tabelas** , selecione a caixa de seleção **Produto** , expanda **Produto** e desmarque as caixas de seleção **ListPrice** e **StandardCost** . Clique em **Próximo**.  
  
6.  Na página Filtrar Linhas da Tabela, clique em **Adicionar**.  
  
7.  Na caixa de diálogo **Adicionar Filtro** , clique na coluna **SafetyStockLevel** , clique na seta para a direita para adicionar a coluna à cláusula WHERE da instrução de Filtro da consulta de filtro e modifique a cláusula WHERE da seguinte maneira:  
  
    ```  
    WHERE [SafetyStockLevel] < 500  
    ```  
  
8.  Clique em **OK** e em **Avançar**.  
  
9. Marque a caixa de seleção **Criar um instantâneo imediatamente e mantê-lo disponível para inicializar assinaturas** e clique em **Avançar**.  
  
10. Na página Segurança do Agente, desmarque a caixa de seleção **Usar as configurações de segurança do Agente de Instantâneo** .  
  
11. Clique em **configurações de segurança** para a agente de instantâneo, digite \<_Machine_Name> _**\ repl_snapshot** na caixa **conta de processo** , forneça a senha dessa conta e clique em **OK**.  
  
12. Repita a etapa anterior para configurar repl_logreader como a conta de processo do Agente de Leitor de Log e clique em **Concluir**.  
  
13. Na página Concluir o Assistente, digite **AdvWorksProductTrans** na caixa **Nome da publicação** e clique em **Concluir**.  
  
14. Depois que a publicação for criada, clique em **Fechar** para concluir o assistente.  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>Para exibir o status de geração do instantâneo  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , expanda o nó do servidor e expanda a pasta **replicação** .  
  
2.  Na pasta **Publicações Locais** , clique com o botão direito do mouse em **AdvWorksProductTrans**e clique em **Exibir Status do Agente de Instantâneo**.  
  
3.  O status atual do trabalho do Snapshot Agent para a publicação é exibido. Verifique se o trabalho de instantâneo teve êxito antes de continuar à próxima lição.  
  
### <a name="to-add-the-distribution-agent-login-to-the-pal"></a>Para adicionar o logon Distribution Agent à PAL  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , expanda o nó do servidor e expanda a pasta **replicação** .  
  
2.  Na pasta **Publicações Locais** , clique com o botão direito do mouse em **AdvWorksProductTrans**e clique em **Propriedades**.  
  
     A caixa de diálogo **Propriedades da Publicação** é exibida.  
  
3.  Selecione a página **Lista de Acesso à Publicação** e clique em **Adicionar**.  
  
4.  Na caixa de diálogo **Adicionar Acesso à Publicação**, selecione _<Machine_Name>_**\repl_distribution** e clique em **OK**. Clique em **OK**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você criou a publicação transacional com êxito. A seguir, você assinará essa publicação. Consulte [Lição 2: Criando uma assinatura na publicação transacional](lesson-2-creating-a-subscription-to-the-transactional-publication.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Filtrar dados publicados](publish/filter-published-data.md)   
 [Definir um artigo](publish/define-an-article.md)   
 [Criar e aplicar o instantâneo](create-and-apply-the-snapshot.md)  
  
  
