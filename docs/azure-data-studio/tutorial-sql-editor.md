---
title: 'Tutorial: Usar o editor Transact-SQL para criar objetos de banco de dados'
titleSuffix: Azure Data Studio
description: Este tutorial demonstra os principais recursos no estúdio de dados do Azure que simplificam o trabalho com o T-SQL.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: b4778d54fe3853f2560159a83dae42c4fd8e55e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959019"
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>Tutorial: Use o editor Transact-SQL para criar objetos de banco de dados- [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Criando e executando consultas, procedimentos armazenados, scripts, etc. são as tarefas principais de profissionais de banco de dados. Este tutorial demonstra os principais recursos no editor T-SQL para criar objetos de banco de dados.

Neste tutorial, você aprenderá a usar [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] para:
> [!div class="checklist"]
> * Objetos de banco de dados de pesquisa
> * Editar dados da tabela 
> * Usar trechos de gravar rapidamente o T-SQL
> * Exibir detalhes de objeto de banco de dados usando *inspecionar definição* e *ir para definição*


## <a name="prerequisites"></a>Prerequisites

Este tutorial requer o SQL Server ou banco de dados SQL *TutorialDB*. Para criar o *TutorialDB* banco de dados, conclua um dos seguintes inícios rápidos:

- [Conectar e consultar usando SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectar e consultar usando o banco de dados SQL [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>Localizar um objeto de banco de dados rapidamente e executar uma tarefa comum

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] Fornece um widget de pesquisa para localizar rapidamente os objetos de banco de dados. Lista de resultados fornece um menu de contexto para tarefas comuns de relevantes para o objeto selecionado, como *editar dados* para uma tabela.

1. Abra a barra lateral de servidores (**Ctrl + G**), expanda **bancos de dados**e selecione **TutorialDB**. 

1. Abra o *TutorialDB Dashboard* clicando com o **TutorialDB** e selecionando **gerenciar** no menu de contexto:

   ![menu de contexto - gerenciar](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. No painel, clique com botão direito **dbo. Os clientes** (no widget de pesquisa) e selecione **editar dados**.
   
   > [!TIP]
   > Para bancos de dados com muitos objetos, use o widget de pesquisa para localizar rapidamente a tabela, exibição, etc. que você está procurando.

   ![widget de pesquisa rápida](./media/tutorial-sql-editor/quick-search-widget.png)

1. Editar o **E-mail** coluna na primeira linha, digite *orlando0@adventure-works.com* e pressione **Enter** para salvar a alteração.

   ![Editar dados](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-stored-procedures"></a>Usar trechos de código T-SQL para criar procedimentos armazenados

[!INCLUDE[name-sos](../includes/name-sos-short.md)] fornece muitos trechos de código internos do T-SQL para rapidamente criar instruções.


1. Abra um novo editor de consulta pressionando **Ctrl + N**.

2. Tipo de **sql** no editor, seta para baixo até **sqlCreateStoredProcedure**e pressione a *guia* chave (ou *Enter*) para carregar o criar armazenado trecho de código do procedimento.

   ![lista de trechos](./media/tutorial-sql-editor/snippet-list.png)

3. O trecho de código do procedimento armazenado criar tem dois campos configurados para edição rápida, *StoredProcedureName* e *SchemaName*. Selecione *StoredProcedureName*, mouse e selecione **alteração de todas as ocorrências**. Agora, digite *getCustomer* e todos os *StoredProcedureName* entradas de alteração para *getCustomer*.

   ![Trecho de código](./media/tutorial-sql-editor/snippet.png)

5. Alterar todas as ocorrências de *SchemaName* à *dbo*. 
6. O trecho de código contém parâmetros de espaço reservado e o corpo do texto que precisa ser atualizado. O *EXECUTE* instrução também contém o texto do espaço reservado porque não sabe quantos parâmetros terá o procedimento. Para este tutorial o trecho de código de atualização então, ele se parece com o código a seguir:

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
    SELECT  c.CustomerId, 
    c.Name, 
    c.Location, 
    c.Email
    FROM dbo.Customers c
    WHERE c.CustomerId = @ID
    FOR JSON PATH

    GO
    -- example to execute the stored procedure we just created
    EXECUTE dbo.getCustomer 1
    GO
    ```
    
5. Para criar o procedimento armazenado e dê a ele uma execução de teste, pressione **F5**.

O procedimento armazenado foi criado e o **resultados** painel exibe o cliente retornado em JSON. Para ver o JSON formatado, clique no registro retornado. 


## <a name="use-peek-definition"></a>Usar inspecionar definição 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] fornece a capacidade de exibir uma definição de objetos usando o recurso de definição de espiada. Esta seção cria um segundo procedimento armazenado e usa a definição de inspeção para ver quais colunas são em uma tabela para criar rapidamente o corpo do procedimento armazenado.

1. Abra um novo editor pressionando **Ctrl + N**. 

2. Tipo de *sql* no editor, seta para baixo até *sqlCreateStoredProcedure*e pressione a *guia* chave (ou *Enter*) para carregar o criar armazenado trecho de código do procedimento.
3. Digite *setCustomer* para *StoredProcedureName* e *dbo* para *SchemaName*

3. Substitua o @param espaços reservados com a seguinte definição de parâmetro:

   ```sql
   @json_val nvarchar(max)
   ```

4. Substitua o corpo do procedimento armazenado com o código a seguir:
   ```sql
   INSERT INTO dbo.Customers
   ```

5. No *inserir* recém-adicionada, clique com botão direito da linha você **dbo. Os clientes** e selecione **inspecionar definição**.

   ![Inspecionar definição](./media/tutorial-sql-editor/peek-definition.png)

6. A definição da tabela é exibida para que você possa ver rapidamente quais colunas são na tabela. Consulte a lista de colunas para concluir facilmente as instruções para o procedimento armazenado. Concluir a criação da instrução INSERT que você adicionou anteriormente para concluir o corpo do procedimento armazenado e fechar uma janela Inspecionar definição:

   ```sql
   INSERT INTO dbo.Customers (CustomerId, Name, Location, Email)
       SELECT CustomerId, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerId int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
    )
   ```
7. Excluir (ou comente) a *EXECUTE* comando na parte inferior da consulta.
8. A instrução inteira deve parecer com o código a seguir:

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
       INSERT INTO dbo.Customers (CustomerId, Name, Location, Email)
       SELECT CustomerId, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerId int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
       )
   GO
   ```

8. Para criar o *setCustomer* procedimento armazenado, pressione **F5**.

## <a name="use-save-query-results-as-json-to-test-the-setcustomer-stored-procedure"></a>Use salvar os resultados da consulta como JSON para testar o procedimento armazenado de setCustomer

O *setCustomer* procedimento armazenado criado na seção anterior requer JSON dados passados para o *@json_val* parâmetro. Esta seção mostra como obter um pouco corretamente formatado de JSON para passar para o parâmetro para que você possa testar o procedimento armazenado.

1. No **servidores** barra lateral com o botão direito do *dbo. Os clientes* tabela e clique em **selecionar 1000 linhas SUPERIORES**.

2. Selecione a primeira linha na exibição dos resultados, verifique se toda a linha está selecionada (clique no número 1 na coluna mais à esquerda) e selecione **Salvar como JSON**.  
3. Alterar a pasta para um local que você vai se lembrar para que você pode excluir o arquivo mais tarde (para a área de trabalho de exemplo) e clique em **salvar**. O JSON formatado arquivo é aberto.

   ![Salvar como JSON](./media/tutorial-sql-editor/save-as-json.png)

4. Selecione os dados JSON no editor e copiá-lo.
5. Abra um novo editor pressionando **Ctrl + N**.
6. As etapas anteriores mostram como você pode obter facilmente os dados formatados corretamente para completar a chamada para o *setCustomer* procedimento. Você pode ver o código a seguir usa o mesmo formato JSON com novos detalhes do cliente para que possamos testar o *setCustomer* procedimento. A instrução inclui a sintaxe para declarar o parâmetro e executar get novo e conjunto de procedimentos. Você pode colar os dados copiados da seção anterior e editá-lo, portanto, é o mesmo que o exemplo a seguir ou simplesmente colar a instrução a seguir no editor de consultas.

   ```sql
   -- example to execute the stored procedure we just created
   declare @json nvarchar(max) =
   N'[
       {
           "CustomerId": 5,
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

   ![resultado do teste](./media/tutorial-sql-editor/test-result.png)

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como:
> [!div class="checklist"]
> * Objetos de esquema de pesquisa rápida
> * Editar dados da tabela 
> * Escrevendo o script T-SQL usando trechos de código
> * Saiba mais sobre os detalhes do objeto de banco de dados usando inspecionar definição e ir para definição


Para saber como habilitar a **cinco consultas mais lentas** widget, conclua o próximo tutorial:

> [!div class="nextstepaction"]
> [Habilitar o widget de insight de exemplo de consultas lentas](tutorial-qds-sql-server.md)
