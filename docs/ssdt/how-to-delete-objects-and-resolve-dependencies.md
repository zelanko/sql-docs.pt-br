---
title: 'Como fazer: excluir objetos e resolver dependências | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- Microsoft.VisualStudio.Data.Tools.Project.HelpKeywords.SqlProjectDropDatabaseConfirmationDialog
- sql.data.tools.dropdatabaseconfirmation.dialog
- sql.data.tools.dropmultipledatabasesconfirmation.dialog
ms.assetid: fb31c2b1-ca4f-4e11-a0b6-5c26430f1c8c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ae25dbc584e564130348507e5aef657823502923
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026615"
---
# <a name="how-to-delete-objects-and-resolve-dependencies"></a>Como fazer: Excluir objetos e resolver dependências
Quando você renomear ou excluir um objeto no **Pesquisador de Objetos do SQL Server**, o SQL Server Data Tools detectará automaticamente todos os seus objetos de dependência e preparará um script ALTER para renomear ou remover a dependência conforme necessário.  
  
> [!WARNING]  
> Os procedimentos a seguir usam entidades criadas em procedimentos anteriores na seção [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md).  
  
### <a name="to-delete-a-database"></a>Para excluir um banco de dados  
  
1.  Clique com botão direito do mouse em um banco de dados no **Pesquisador de Objetos do SQL Server** e selecione **Excluir**.  
  
2.  Aceite todas as configurações padrão na caixa de diálogo **Excluir Banco de Dados** e clique em **OK**.  
  
### <a name="to-rename-a-table"></a>Para renomear uma tabela  
  
1.  Verifique se a tabela `Customer` não está aberta no Designer de Tabela nem no Editor do Transact\-SQL.  
  
2.  Expanda o nó **Tabelas** no **Pesquisador de Objetos do SQL Server**. Clique com o botão direito do mouse na tabela **Cliente** e selecione **Renomear**.  
  
3.  Altere o nome da tabela para **Clientes** e pressione ENTER.  
  
4.  Observe que uma operação de **Atualização de Banco de Dados** é invocada imediatamente para você. O SSDT chamará o procedimento armazenado sp_rename para você para renomear a tabela. Se houver algum objeto dependente, como restrições de chave estrangeira, ele também será atualizado.  
  
    > [!WARNING]  
    > Dependências baseadas em script como referências a uma tabela de uma exibição ou procedimentos armazenados não são atualizados automaticamente pelo SSDT. Depois de renomear, você poderá usar o painel **Lista de Erros** para localizar todas as outras dependências e corrigi-las manualmente.  
  
5.  Aplique a alteração depois das etapas no procedimento anterior [Como atualizar um banco de dados conectado com o Power Buffer](../ssdt/how-to-update-a-connected-database-with-power-buffer.md).  
  
6.  Clique com o botão direito do mouse na tabela **Clientes** no **Pesquisador de Objetos do SQL Server** novamente e selecione **Exibir Dados**. Observe que os dados da tabela estão intatos depois da operação de renomeação.  
  
7.  Clique com o botão direito do mouse na tabela **Produtos** e selecione **Exibir Código**. Observe que a referência de chave estrangeira foi atualizada automaticamente para `REFERENCES [dbo].[Customers] ([Id])` para refletir a mudança de nome.  
  
### <a name="to-delete-a-table"></a>Para excluir uma tabela  
  
1.  Clique com o botão direito do mouse na tabela **Clientes** no **Pesquisador de Objetos do SQL Server** e selecione **Excluir**.  
  
2.  Na caixa de diálogo **Visualizar Atualizações de Banco de Dados**, em **Ação do Usuário**, observe que o SSDT identificou todos os objetos dependentes, nesse caso, uma referência de chave estrangeira que será removida.  
  
3.  Clique em **Atualizar Banco de Dados**.  
  
4.  Clique com o botão direito do mouse na tabela **Produtos** no **Pesquisador de Objetos do SQL Server** e selecione **Exibir Código**. Observe que a referência de chave estrangeira para a tabela `Customers` desapareceu.  
  
    > [!WARNING]  
    > Se você já tiver a tabela **Produtos** aberta no Designer de Tabela ou no Editor de Transact\-SQL quando a operação de exclusão ocorrer, ela não será atualizada automaticamente para mostrar a exclusão da referência de chave estrangeira. Além disso, erros sobre referências não resolvidas poderão ser exibidos na **Lista de Erros**. Para resolver esse problema, feche o Designer de Tabela ou o Editor Transact\-SQL e reabra a tabela Produtos.  
  
