---
title: "Tutorial: Usar o editor do Transact-SQL Studio de operações do SQL (visualização) para criar objetos de banco de dados | Microsoft Docs"
description: "Este tutorial demonstra os principais recursos no Studio de operações do SQL (visualização) que simplificam o uso de T-SQL."
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b2754a998963be5a25d00aa58dcb9b4105bb8f37
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>Tutorial: Usar o editor do Transact-SQL para criar objetos de banco de dados-[!INCLUDE[name-sos](../includes/name-sos-short.md)]

Criando e executando consultas, procedimentos armazenados, scripts, etc. são as tarefas principais de profissionais de banco de dados. Este tutorial demonstra os principais recursos do editor T-SQL para criar objetos de banco de dados.

Neste tutorial, você aprenderá a usar [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] para:
> [!div class="checklist"]
> * Objetos de banco de dados de pesquisa
> * Editar dados da tabela 
> * Usar trechos de código a escrita de T-SQL
> * Detalhes do objeto de banco de dados de exibição usando *inspecionar definição* e *ir para definição*


## <a name="prerequisites"></a>Prerequisites

Este tutorial requer o SQL Server ou banco de dados do SQL Azure *TutorialDB*. Para criar o *TutorialDB* banco de dados, conclua um dos tutoriais a seguir:

- [Conectar e consultar usando o SQL Server[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectar e consultar usando o banco de dados SQL[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>Localizar um objeto de banco de dados rapidamente e executar uma tarefa comum

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]Fornece um widget de pesquisa para localizar rapidamente os objetos de banco de dados. A lista de resultados fornece um menu de contexto para tarefas comuns relevantes para o objeto selecionado, como *editar dados* para uma tabela.

1. Abra a barra lateral de servidores (**Ctrl + G**), expanda **bancos de dados**e selecione **TutorialDB**. 

1. Abra o *TutorialDB painel* selecionando **gerenciar** no menu de contexto.

   ![menu de contexto - gerenciar](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. Localize o *clientes* tabela digitando *cus* no widget de pesquisa.
1. Clique com botão direito **dbo. Os clientes** e selecione **editar dados**.

   ![widget de pesquisa rápida](./media/tutorial-sql-editor/quick-search-widget.png)

1. Editar o **Email** coluna na primeira linha, tipo  *orlando0@adventure-works.com* e pressione **Enter** para salvar a alteração.

   ![Editar dados](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-a-stored-procedure"></a>Usar trechos de código do T-SQL para criar um procedimento armazenado

### <a name="use-snippets-in-includename-sos-shortincludesname-sos-shortmd"></a>Usar trechos de código[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]

1. Abra um novo editor de consulta pressionando **Ctrl + N**.

2. Tipo **sql** no editor, seta para baixo **sqlCreateStoredProcedure**e pressione a *guia* tecla para carregar o novo trecho de código do procedimento armazenado.

   ![lista de trecho de código](./media/tutorial-sql-editor/snippet-list.png)

3. Tipo *getCustomer* e todos os *StoredProcedureName* entradas de alteração para *getCustomer*. 

   ![Trecho de código](./media/tutorial-sql-editor/snippet.png)

4. Substitua o restante do procedimento armazenado com o T-SQL a seguir:

    ```sql
    -- Create a new stored procedure called 'getCustomer' in schema 'dbo'
    -- Drop the stored procedure if it already exists
    IF EXISTS (
    SELECT *
    FROM INFORMATION_SCHEMA.ROUTINES
    WHERE SPECIFIC_SCHEMA = N'dbo'
    AND SPECIFIC_NAME = N'getCustomer'
    )
    DROP PROCEDURE dbo.getCustomer
    GO
    -- Create the stored procedure in the specified schema
    CREATE PROCEDURE dbo.getCustomer
    @ID int
    -- add more stored procedure parameters here
    AS
    -- body of the stored procedure
    SELECT  c.CustomerID, 
    c.Name, 
    c.Location, 
    c.Email
    FROM dbo.Customers c
    WHERE c.CustomerID = @ID
    FOR JSON PATH

    GO
    -- example to execute the stored procedure we just created
    EXECUTE dbo.getCustomer 1
    GO
    ```
    
5. Para criar o procedimento armazenado e dê a ele uma execução de teste, pressione **F5**.

## <a name="use-peek-definition-and-go-to-definition"></a>Definição de pico de uso e ir para definição 

1. Abra um novo editor pressionando **Ctrl + N**. 

2. Digite e selecione **sqlCreateStoredProcedure** da lista de sugestões de trecho de código. Digite **setCustomer** para **StoredProcedureName** e **dbo** para **SchemaName**

3. Substitua o @param linhas com a seguinte definição de parâmetro:

   ```sql
       @json_val nvarchar(max)
   ```

4. Substitua o corpo do procedimento armazenado com o seguinte:
   ```sql
   -- body of the stored procedure
   INSERT INTO dbo.Customers
   ```

5. Clique com botão direito **dbo. Os clientes** e selecione **inspecionar definição**.

   ![janela Inspecionar definição](./media/tutorial-sql-editor/peek-definition.png)

6. Use a definição de tabela para concluir a seguinte instrução de inserção:

   ```sql
   INSERT INTO dbo.Customers (CustomerID, Name, Location, Email)
       SELECT CustomerID, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerID int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
   ```
7. A instrução final deve ser:

   ```sql
   -- Create a new stored procedure called 'setCustomer' in schema 'dbo'
   -- Drop the stored procedure if it already exists
   IF EXISTS (
   SELECT *
       FROM INFORMATION_SCHEMA.ROUTINES
       WHERE SPECIFIC_SCHEMA = N'dbo'
       AND SPECIFIC_NAME = N'setCustomer'
   )
   DROP PROCEDURE dbo.setCustomer
   GO
   -- Create the stored procedure in the specified schema
   CREATE PROCEDURE dbo.setCustomer
       @json_val nvarchar(max) 
   AS
       -- body of the stored procedure
       INSERT INTO dbo.Customers (CustomerID, Name, Location, Email)
       SELECT CustomerID, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerID int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
       )
   GO
   ```

8. Para executar o script, pressione **F5**.

## <a name="use-save-query-results-as-json-to-test-our-stored-procedure"></a>Use salvar resultados da consulta como JSON para testar nosso procedimento armazenado

1. **Selecionar 1000 linhas SUPERIORES** do *dbo. Os clientes* tabela.

2. Selecione a primeira linha no modo de exibição de resultados e clique **Salvar como JSON**.  
3. Clique em **salvar**, e ele é aberto da linha realçada em formato JSON.

   ![Salvar como JSON](./media/tutorial-sql-editor/save-as-json.png)

4. Selecione os dados JSON e copiá-lo.

5. Abra uma nova consulta para *TutorialDB* e conclua o seguinte script de teste usando os dados JSON como um modelo da etapa anterior. Modifique os valores para *CustomerID*, *nome*, *local*, e *Email*.

   ```sql
   -- example to execute the stored procedure we just created
   declare @json nvarchar(max) =
   N'[
       {
           "CustomerID": 5,
           "Name": "Lucy",
           "Location": "Canada",
           "Email": "lucy0@adventure-works.com"
       }
   ]'

   EXECUTE dbo.setCustomer @json_val = @json
   GO

   EXECUTE dbo.getCustomer @ID = 5
   ```

7. Execute o script pressionando **F5**. O script insere um novo cliente e retorna as novas informações do cliente no formato JSON. Clique no resultado para abrir uma exibição formatada.

   ![Resultado do teste](./media/tutorial-sql-editor/test-result.png)

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como:
> [!div class="checklist"]
> * Objetos de esquema de pesquisa rápida
> * Editar dados da tabela 
> * Escrevendo o script T-SQL usando trechos de código
> * Saiba mais sobre os detalhes do objeto de banco de dados usando a definição de inspecionar e ir para definição


Para saber como habilitar o **cinco consultas mais lentas** insight de exemplo, conclua o seguinte tutorial:

> [!div class="nextstepaction"]
> [Habilitar o widget de informações de exemplo de consultas lentas](tutorial-qds-sql-server.md)
