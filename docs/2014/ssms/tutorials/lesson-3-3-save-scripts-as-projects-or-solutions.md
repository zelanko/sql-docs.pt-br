---
title: Salvar scripts como projetos ou soluções | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 72dfd37f-dbe7-4d1d-bda6-7eb54c7922d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9dc290b0cc833b46b11d0db0df42301be098a1ba
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286542"
---
# <a name="save-scripts-as-projects-or-solutions"></a>Salvar scripts como projetos ou soluções
  Desenvolvedores familiarizados com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio darão as boas-vindas ao Gerenciador de Soluções no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Os scripts que dão suporte a seu negócio podem ser agrupados em projetos de script e os projetos de script podem ser administrados juntos, como uma solução. Quando os scripts são colocados em projetos de script e soluções, eles podem ser abertos em conjunto, como um grupo, ou salvos em conjunto em um produto de controle de código-fonte, como o Visual SourceSafe. Projetos de script incluem as informações de conexão dos scripts para serem executados corretamente, e podem incluir arquivos diferentes (não script), como um arquivo de texto de suporte.  
  
 O procedimento a seguir cria um script curto que consulta o banco de dados do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , colocado em um projeto de script ou em uma solução.  
  
## <a name="using-script-projects-and-solutions"></a>Utilizando projetos de script e soluções  
  
#### <a name="to-create-a-script-project-and-solution"></a>Para criar um projeto de script e uma solução  
  
1.  Abra o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e faça a conexão com um servidor usando o Pesquisador de Objetos.  
  
2.  No menu **Arquivo** , aponte para **Novo**e clique em **Projeto**. A caixa de diálogo **Novo Projeto** será aberta.  
  
3.  Na caixa de texto **Nome** , digite **StatusCheck**, clique em **Scripts do SQL Server** em **Modelos**e clique em **OK** para abrir uma nova solução e projeto de script.  
  
4.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Conexões**e clique em **Nova Conexão**. A caixa de diálogo **Conectar ao Servidor** é exibida.  
  
5.  Na caixa de listagem **Nome do servidor** , digite o nome de seu servidor.  
  
6.  Clique em **Opções**e clique na guia **Propriedades da Conexão** .  
  
7.  Na caixa **Conectar ao banco de dados** , procure o servidor, selecione o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e clique em **Conectar**. As informações de conexão, incluindo o banco de dados, são adicionadas ao projeto.  
  
8.  Se a janela Propriedades não for exibida, clique na nova conexão no Gerenciador de Soluções e pressione F4. As propriedades da conexão são exibidas e mostram informações sobre a conexão, incluindo o **Banco de Dados Inicial** como [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
9. No Gerenciador de Soluções, clique com o botão direito do mouse na conexão e clique em **Nova Consulta**. Uma nova consulta chamada **SQLQuery1.sql** é criada, conectada ao banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] em seu servidor e adicionada ao projeto de script.  
  
10. No Editor de Consultas, digite a seguinte consulta para determinar quantos pedidos possuem datas de vencimento anteriores às datas de início dos pedidos. (Você pode copiar e colar o código da janela Tutorial.)  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT COUNT(WorkOrderID)  
    FROM Production.WorkOrder  
    WHERE DueDate < StartDate;  
  
    ```  
  
    > [!NOTE]  
    >  Se você precisar de mais espaço para inserir sua consulta, pressione SHIFT+ALT+ENTER, para alternar para o modo de tela inteira.  
  
11. No Gerenciador de Soluções, clique com o botão direito do mouse em **SQLQuery1**e clique em **Renomear**. Digite **Check Workorders****.sql** como o novo nome da consulta e pressione ENTER.  
  
12. Para salvar a solução e o projeto de script, no menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Resumo: Soluções e Projetos de Script](lesson-3-4-summary-solutions-and-script-projects.md)  
  
  
