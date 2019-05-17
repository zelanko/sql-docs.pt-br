---
title: 'Como fazer: Criar novos objetos de banco de dados usando consultas | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: ac983ac7-f9c4-495d-8a99-e1ba370fb271
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 383992f5e1fc9891fb570dec168d1648913f4254
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65098163"
---
# <a name="how-to-create-new-database-objects-using-queries"></a>Como fazer: Criar objetos de banco de dados usando consultas
Se você preferir usar scripts para criar ou editar modos de exibição, procedimentos armazenados, funções, gatilhos ou tipos definidos pelo usuário, poderá usar o Editor Transact\-SQL. O Editor Transact\-SQL dá suporte a IntelliSense e a outra linguagem. Para saber mais, confira [Usar o Editor Transact-SQL para editar e executar scripts](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md).  
  
O Editor Transact\-SQL é invocado quando você usa o menu contextual **Exibir Código** para abrir uma entidade de banco de dados em um banco de dados conectado ou em um projeto. Ele também é aberto automaticamente quando você usa o menu contextual **Nova Consulta** no Pesquisador de Objetos do SQL Server ou adiciona um novo objeto de script a um projeto de banco de dados. Se você não estiver conectado a um banco de dados, mas quiser executar uma consulta nele, também poderá usar a caixa de diálogo **Nova Conexão de Consulta** selecionando o menu **Editor Transact-SQL** no menu **SQL** para se conectar a um banco de dados e iniciar o Editor Transact\-SQL.  
  
> [!WARNING]  
> Os procedimentos a seguir usam entidades criadas em procedimentos anteriores na seção [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md).  
  
### <a name="to-create-a-new-table-using-a-transact-sql-query"></a>Para criar uma nova tabela usando uma consulta Transact\-SQL  
  
1.  Clique com o botão direito do mouse no nó do banco de dados **Trade** e selecione **Nova Consulta**.  
  
2.  No painel de script, cole este código:  
  
    ```  
  
    CREATE TABLE [dbo].[Fruits] (  
        [Id]         INT NOT NULL,  
        [Perishable] BIT DEFAULT ((1)) NULL,  
        PRIMARY KEY CLUSTERED ([Id] ASC),  
        FOREIGN KEY ([Id]) REFERENCES [dbo].[Products] ([Id])   
    );  
    ```  
  
3.  Clique no botão **Executar Consulta** na barra de ferramentas do Editor Transact\-SQL para executar a consulta.  
  
4.  Clique com o botão direito no banco de dados **Trade** no **Pesquisador de Objetos do SQL Server** e selecione **Atualizar**. Observe que a nova tabela **Fruits** foi adicionada ao banco de dados.  
  
### <a name="to-create-a-new-function"></a>Para criar um novo campo  
  
1.  Substitua o código no Editor Transact\-SQL atual pelos dados a seguir:  
  
    ```  
  
    CREATE FUNCTION [dbo].GetProductsBySupplier  
    (  
    @SupplierId int  
    )  
    RETURNS @returntable TABLE   
    (  
    [Id] int NOT NULL,   
    [Name] NVARCHAR (128) NOT NULL,  
    [Shelflife] INT NOT NULL,  
    [SupplierId] INT NOT NULL,  
    [CustomerId] INT NOT NULL  
    )  
    AS  
    BEGIN  
    INSERT @returntable  
    SELECT *  from Products p  
    where p.SupplierId = @SupplierId  
    RETURN   
    END  
    ```  
  
    Esta função retornará todas as linhas na tabela `Products` em que `SupplierId` é igual ao parâmetro especificado. Clique no botão **Executar Consulta** na barra de ferramentas do Editor Transact\-SQL para executar a consulta.  
  
2.  No Pesquisador de Objetos do SQL Server, no nó **Comércio**, expanda os nós **Programação** e **Funções**. Você pode localizar a nova função que acabou de criar em **Funções com Valor de Tabela**.  
  
### <a name="to-create-a-new-view"></a>Para criar uma nova exibição  
  
1.  Substitua o código no Editor Transact\-SQL atual pelos dados a seguir. Em seguida, clique no botão **Executar Consulta** acima do editor para executar a consulta.  
  
    ```  
    CREATE VIEW [dbo].PerishableFruits   
    AS SELECT p.Id, p.Name FROM dbo.Products p  
    join dbo.Fruits f on f.Id = p.Id  
    where f.Perishable = 1  
    ```  
  
2.  No Pesquisador de Objetos do SQL Server, no nó **Trade**, expanda o nó **Exibição** para localizar a nova exibição que você acabou de criar.  
  
## <a name="see-also"></a>Consulte Também  
[Gerenciar tabelas, relações e corrigir erros](../ssdt/manage-tables-relationships-and-fix-errors.md)  
[Usar o Editor Transact-SQL para editar e executar scripts](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)  
  
