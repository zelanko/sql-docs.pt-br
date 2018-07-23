---
title: Como usar renomeação e refatoração para fazer alterações em seus objetos de banco de dados | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.dbrefactoring.previewdialog
- sql.data.tools.editor.howto.refactoring
- sql.data.tools.dbrefactoring.renamedialog
- sql.data.tools.dbrefactoring.moveschemadialog
- sql.data.tools.dbrefactoring.renameserverdatabasedialog
ms.assetid: f35520e6-8e6e-47b1-87a3-22c0cf2cabdb
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4ba39da9c13a1a2051f249942de86b18963eade8
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39083358"
---
# <a name="how-to-use-rename-and-refactoring-to-make-changes-to-your-database-objects"></a>Como: Usar renomeação e refatoração para fazer alterações em seus objetos de banco de dados
O menu contextual Refatorar no Editor de Transact\-SQL permite renomear ou mover um objeto para um esquema diferente e permite uma visualização de todas as áreas afetadas antes de confirmar a alteração. Você também pode usar o menu Refatorar para qualificar completamente todas as referências a objetos de banco de dados ou expandir os caracteres curinga nas instruções `SELECT` em seu projeto de banco de dados.  
  
> [!NOTE]  
> Os procedimentos a seguir utilizam entidades criadas em procedimentos anteriores nas seções [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md) e [Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-rename-a-type"></a>Para renomear um tipo  
  
1.  Clique com o botão direito do mouse na tabela **Produtos** (Products.sql) no **Gerenciador de Soluções** e selecione **Exibir Código** para abrir o script no Editor de Transact\-SQL.  
  
2.  Clique com o botão direito do mouse em `[Products]` no script, selecione **Refatorar** e **Renomear**.  
  
3.  No campo **Novo Nome**, altere-o para **Produto**. Deixe a opção **Visualizar Alterações** marcada e clique em **OK**.  
  
4.  Na próxima tela, você poderá visualizar uma lista de scripts que serão afetados por esta operação de renomeação. Especificamente, serão realçados todos os locais que se referem a `Products`. Isto é bem semelhante à tarefa de Localizar todas as referências no procedimento anterior. Clique em qualquer coisa no painel superior e exiba a alteração real nos scripts (realçada em verde) no painel inferior.  
  
5.  Clique em **Aplicar**.  
  
6.  Para arquivos de script que já estão abertos no Designer de Tabela ou no Editor de Transact\-SQL, observe que o Editor Transact\-SQL realçou os locais onde as alterações ocorreram com uma barra verde à esquerda.  
  
7.  Observe a adição de **TradeDev.refactorlog** no **Gerenciador de Soluções**. Clique duas vezes para abri-lo. Contém uma representação XML de todas as alterações nesta sessão.  
  
8.  Pressione F5 para criar e implantar o projeto no banco de dados local.  
  
9. Clique com o botão direito do mouse no banco de dados **TradeDev** em **Local** no **Pesquisador de Objetos do SQL Server** e selecione **Atualizar**.  
  
10. Expanda **Tabelas** e observe que a tabela **Produtos** foi renomeada.  
  
11. Clique com o botão direito do mouse em **Produto** e selecione **Exibir Dados**. Observe que os dados existentes são mantidos intatos independentemente da operação de renomeação.  
  
### <a name="to-expand-wildcards"></a>Para expandir curingas  
  
1.  Expanda o nó **Funções** no **Gerenciador de Soluções** e clique duas vezes em **GetProductsBySupplier.sql**.  
  
2.  Coloque o cursor no asterisco nesta linha e clique com o botão direito do mouse. Selecione **Refatorar** e **Expandir Curingas**.  
  
    ```  
    SELECT * from Product p  
    ```  
  
3.  Na caixa de diálogo **Visualizar Alterações**, clique na opção `SELECT * from Product p` no painel superior para realçá-la.  
  
4.  No painel **Visualizar Alterações** abaixo, observe que `*` foi expandido para o seguinte no script.  
  
    ```  
    [Id], [Name], [ShelfLife], [SupplierId], [CustomerId]  
    ```  
  
5.  Clique no botão **Aplicar**.  Observe a linha que contém alterações produzidas pela operação de expansão é realçada novamente com uma barra verde na esquerda.  
  
### <a name="to-fully-qualify-database-object-names"></a>Para qualificar totalmente nomes de objeto de banco de dados  
  
1.  Verifique se **GetProductsBySupplier.sql** ainda está aberto no Editor Transact\-SQL.  
  
2.  Coloque o cursor no `Product` nesta linha e clique com o botão direito do mouse. Selecione **Refatorar** e **Nomes Totalmente Qualificados**.  
  
    ```  
    SELECT [Id], [Name], [ShelfLife], [SupplierId], [CustomerId] from Product p  
    ```  
  
3.  Clique no botão **Aplicar** na caixa de diálogo **Visualizar Alterações**.  Observe que todas as referências de objeto foram atualizadas para incluir o nome do esquema do objeto e, se o objeto tiver um pai, o nome do pai.  
  
    ```  
    SELECT [p].[Id], [p].[Name], [p].[ShelfLife], [p].[SupplierId], [p].[CustomerId] from [dbo].[Product] p  
    ```  
  
### <a name="to-move-schema"></a>Para mover o esquema  
  
1.  Clique com o botão direito do mouse no objeto que você deseja mover. Selecione **Refatorar** e **Mover Esquema**.  
  
2.  Na lista **Novo Esquema**, clique no nome do esquema para o qual você deseja mover o objeto. Clique em OK.  
  
    Se você tiver marcado a caixa **Visualizar alterações**, a caixa de diálogo **Visualizar Alterações** será exibida. Caso contrário, o nome do objeto será atualizado e o objeto será movido para o novo esquema.  
  
