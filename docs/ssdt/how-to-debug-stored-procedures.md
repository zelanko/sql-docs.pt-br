---
title: Depurar Procedimentos Armazenados
description: Saiba como usar o depurador de Transact-SQL para depurar interativamente um procedimento armazenado. Veja como exibir a pilha de chamadas SQL, as variáveis locais e os parâmetros.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.EXECUTESTOREDPROCEDURE.DIALOG
ms.assetid: e3c8707f-0f6b-4265-8a5a-81f079330b52
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: fc60da27d0176057fb7340b4db743786efe27017
ms.sourcegitcommit: b860fe41b873977649dca8c1fd5619f294c37a58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2020
ms.locfileid: "85518866"
---
# <a name="how-to-debug-stored-procedures"></a>Como fazer: Depurar Procedimentos Armazenados

O depurador Transact\-SQL permite depurar procedimentos armazenados interativamente exibindo a pilha de chamadas de SQL, variáveis locais e parâmetros para o procedimento armazenado de SQL. Assim como a depuração em outras linguagens de programação, você pode exibir e modificar variáveis e parâmetros locais, exibir variáveis globais, bem como controlar e gerenciar pontos de interrupção enquanto depura seu script Transact\-SQL.  
  
Este exemplo mostra como criar e depurar um procedimento armazenado Transact\-SQL passo a passo.  
  
> [!WARNING]  
> O procedimento a seguir usa entidades criadas em procedimentos nas seções [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md) e [Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-debug-stored-procedures"></a>Para depurar procedimentos armazenados  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito no projeto **TradeDev** e selecione **Adicionar** e **Procedimento Armazenado**. Nomeie esse novo procedimento armazenado **AddProduct** e clique em **Adicionar**.  
  
2.  Cole o código a seguir no procedimento armazenado.  
  
    ```  
    CREATE PROCEDURE [dbo].[AddProduct]  
    @id int,  
    @name nvarchar(128)  
    AS  
    INSERT INTO [dbo].[Product] (Id, Name) VALUES (@id, @name)  
    ```  
  
3.  Pressione F5 para criar e implantar o projeto.  
  
4.  No Pesquisador de Objetos do SQL Server, no nó **Local**, clique com o botão direito do mouse no banco de dados **TradeDev** e selecione **Nova Consulta**.  
  
5.  Cole o código a seguir na janela de consulta.  
  
    ```  
    EXEC [dbo].[AddProduct] 50, N'Contoso';  
    GO  
    ```  
  
6.  Clique na margem da janela esquerda para adicionar um ponto de interrupção à instrução `EXEC`.  
  
7.  Pressione a seta suspensa no botão de seta verde na barra de ferramentas do editor Transact\-SQL e selecione **Executar com Depurador** para executar a consulta com a depuração ativada.  
  
8.  Como alternativa, você pode iniciar a depuração do Pesquisador de Objetos do SQL Server. Clique com o botão direito do mouse no procedimento armazenado **AddProduct** (localizado em **Local** -> **banco de dados TradeDev** -> **Programação** -> **Procedimentos Armazenados**). Selecione **Depurar Procedimento...** . Se o objeto exigir parâmetros, a caixa de diálogo **Depurar Procedimento** será exibida, com uma tabela contendo uma linha para cada parâmetro. Cada linha na tabela contém uma coluna para o nome do parâmetro e uma para o valor desse parâmetro. Insira valores para cada parâmetro e clique em OK.  
  
9. Verifique se a janela **Locais** está aberta. Se não estiver, clique no menu **Depurar**, selecione **Janelas** e **Local**.  
  
10. Pressione F11 para entrar na consulta. Observe que os parâmetros do procedimento armazenado e seus valores respectivos aparecem na janela **Locais**. Como alternativa, passe o mouse sobre o parâmetro `@name` na cláusula `INSERT` e você verá o valor **Contoso** sendo atribuído a ele.  
  
11. Clique em **Contoso** na caixa de texto. Digite **Fabrikam** e pressione ENTER para alterar o valor da variável `name` enquanto depura. Você também pode alterar seu valor na janela **Locais**. Observe que o valor do parâmetro é exibido agora em vermelho, indicando que foi alterado.  
  
12. Pressione F10 para depurar parcialmente o código restante.  
  
13. No Pesquisador de Objetos do SQL Server, atualize o nó do banco de dados **TradeDev** para ver o novo conteúdo na exibição de dados da tabela **Produto**.  
  
14. No Pesquisador de Objetos do SQL Server, no nó **Local**, localize a tabela **Produto** do banco de dados **TradeDev**.  
  
15. Clique com o botão direito na tabela **Produto** e selecione **Exibir Dados**. Observe que a nova linha foi adicionada à tabela.  
  
