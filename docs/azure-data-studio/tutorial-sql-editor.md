---
title: Usar o editor de Transact-SQL para criar objetos de banco de dados
description: Siga este tutorial para saber como usar o editor do Transact-SQL para executar tarefas de banco de dados principais, incluindo criação e pesquisa de objetos de banco de dados.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 09/24/2018
ms.openlocfilehash: bd604ea3ad643aa7f70d0be2a1ee7727810b6705
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88745706"
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---azure-data-studio"></a>Tutorial: Usar o editor Transact-SQL para criar objetos de banco de dados – Azure Data Studio

Criar e executar consultas, procedimentos armazenados, scripts etc. são as principais tarefas dos profissionais de banco de dados. Este tutorial demonstra os principais recursos do editor de T-SQL para criar objetos de banco de dados.

Neste tutorial, você aprenderá a usar o [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] para:
> [!div class="checklist"]
> * Pesquisar objetos de banco de dados
> * Editar dados de tabela 
> * Usar snippets para escrever T-SQL rapidamente
> * Exibir detalhes do objeto de banco de dados usando *Inspecionar Definição* e *Ir para Definição*


## <a name="prerequisites"></a>Pré-requisitos

Este tutorial requer o SQL Server ou o *TutorialDB* do Banco de Dados SQL do Azure. Para criar o banco de dados *TutorialDB*, siga um destes guias de início rápido:

- [Conectar e consultar o SQL Server usando [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectar e consultar o Banco de Dados SQL do Azure usando [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>Localizar rapidamente um objeto de banco de dados e executar uma tarefa comum

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] fornece um widget de pesquisa para localizar rapidamente objetos de banco de dados. A lista de resultados fornece um menu de contexto com tarefas comuns relevantes para o objeto selecionado, como *Editar Dados* para uma tabela.

1. Abra a barra lateral SERVIDORES (**Ctrl+G**), expanda **Bancos de dados** e selecione **TutorialDB**. 

1. Abra o *Painel do TutorialDB* clicando com o botão direito do mouse em **TutorialDB** e selecionando **Gerenciar** no menu de contexto:

   ![Menu de contexto – Gerenciar](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. No painel, clique com o botão direito do mouse em **dbo.Customers** (no widget de pesquisa) e selecione **Editar Dados**.
   
   > [!TIP]
   > Para bancos de dados com muitos objetos, use o widget de pesquisa para localizar rapidamente a tabela, exibição etc. que você está buscando.

   ![widget de pesquisa rápida](./media/tutorial-sql-editor/quick-search-widget.png)

1. Edite a coluna **Email** na primeira linha, digite *orlando0\@adventure-works.com* e pressione **Enter** para salvar a alteração.

   ![editar dados](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-stored-procedures"></a>Usar snippets de T-SQL para criar procedimentos armazenados

O Azure Data Studio fornece muitos snippets de T-SQL internos para criar instruções rapidamente.


1. Abra um novo editor de consultas pressionando **Ctrl + N**.

2. Digite **sql** no editor, use a seta para baixo até chegar em **sqlCreateStoredProcedure** e pressione a tecla *Tab* (ou *Enter*) para carregar o snippet de criação de procedimento armazenado.

   ![snippet-list](./media/tutorial-sql-editor/snippet-list.png)

3. O snippet de criação de procedimento armazenado tem dois campos configurados para edição rápida, *StoredProcedureName* e *SchemaName*. Selecione *StoredProcedureName*, clique com o botão direito do mouse e selecione **Alterar Todas as Ocorrências**. Agora, digite *getCustomer* e todas as entradas de *StoredProcedureName* serão alteradas para *getCustomer*.

   ![snippet](./media/tutorial-sql-editor/snippet.png)

5. Altere todas as ocorrências de *SchemaName* para *dbo*. 
6. O snippet contém parâmetros de espaço reservado e texto de corpo que precisam ser atualizados. A instrução *EXECUTE* também contém texto de espaço reservado porque não sabe quantos parâmetros o procedimento terá. Para este tutorial, atualize o snippet de forma que ele se pareça com o código a seguir:

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
    
5. Para criar o procedimento armazenado e fazer uma execução de teste, pressione **F5**.

O procedimento armazenado é criado e o painel **RESULTADOS** exibe o cliente retornado em JSON. Para ver o JSON formatado, clique no registro retornado. 


## <a name="use-peek-definition"></a>Usar Inspecionar Definição 

O Azure Data Studio possibilita exibir a definição de um objeto usando o recurso Espiar Definição. Esta seção cria um segundo procedimento armazenado e usa inspecionar definição para ver quais colunas estão em uma tabela para criar rapidamente o corpo do procedimento armazenado.

1. Abra um novo editor pressionando **Ctrl + N**. 

2. Digite *sql* no editor, use a seta para baixo até chegar em *sqlCreateStoredProcedure* e pressione a tecla *Tab* (ou *Enter*) para carregar o snippet de criação de procedimento armazenado.
3. Digite *setCustomer* para *StoredProcedureName* e *dbo* para *SchemaName*

3. Substitua os espaços reservados @param pela definição de parâmetro a seguir:

   ```sql
   @json_val nvarchar(max)
   ```

4. Substitua o corpo do procedimento armazenado pelo código a seguir:
   ```sql
   INSERT INTO dbo.Customers
   ```

5. Na linha *INSERT* que você acabou de adicionar, clique com o botão direito do mouse em **dbo.Customers** e selecione **Inspecionar Definição**.

   ![inspecionar definição](./media/tutorial-sql-editor/peek-definition.png)

6. A definição da tabela é exibida para que você possa ver rapidamente quais colunas estão nela. Confira a lista de colunas para concluir facilmente as instruções para seu procedimento armazenado. Conclua a criação da instrução INSERT que você adicionou anteriormente para preencher o corpo do procedimento armazenado e feche a janela Inspecionar Definição:

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
7. Exclua (ou comente) o comando *EXECUTE* na parte inferior da consulta.
8. A instrução inteira deve ser semelhante ao seguinte código:

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

8. Para criar o procedimento armazenado *setCustomer*, pressione **F5**.

## <a name="use-save-query-results-as-json-to-test-the-setcustomer-stored-procedure"></a>Use Salvar resultados da consulta como JSON para testar o procedimento armazenado setCustomer

O procedimento armazenado *setCustomer* criado na seção anterior requer que dados JSON sejam passados para o parâmetro *\@json_val*. Esta seção mostra como obter um trecho de JSON formatado corretamente para passar para o parâmetro para que você possa testar o procedimento armazenado.

1. Na barra lateral **SERVIDORES**, clique com o botão direito do mouse na tabela *dbo.Customers* e clique em **Selecionar 1000 Linhas Superiores**.

2. Selecione a primeira linha na visualização dos resultados, certifique-se de que a linha inteira esteja selecionada (clique no número 1 na coluna à extrema esquerda) e selecione **Salvar como JSON**.  
3. Altere a pasta para uma localização da qual você se lembrará para que possa excluir o arquivo posteriormente (por exemplo, a área de trabalho) e clique em **Salvar**. O arquivo formatado em JSON é aberto.

   ![Salvar como JSON](./media/tutorial-sql-editor/save-as-json.png)

4. Selecione os dados JSON no editor e copie-os.
5. Abra um novo editor pressionando **Ctrl + N**.
6. As etapas anteriores mostram como você pode formatar facilmente os dados da forma correta para fazer a chamada para o procedimento *setCustomer*. Você pode ver que o seguinte código usa o mesmo formato JSON com novos detalhes do cliente para que possamos testar o procedimento *setCustomer*. A instrução inclui a sintaxe para declarar o parâmetro e executar os novos procedimentos get e set. Você pode colar os dados copiados da seção anterior e editá-los para que eles fiquem iguais ao exemplo a seguir ou simplesmente colar a instrução a seguir no editor de consultas.

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

7. Execute o script pressionando **F5**. O script insere um novo cliente e retorna as informações do novo cliente no formato JSON. Clique no resultado para abrir uma exibição formatada.

   ![resultado do teste](./media/tutorial-sql-editor/test-result.png)

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu a:
> [!div class="checklist"]
> * Pesquisar rapidamente objetos de esquema
> * Editar dados de tabela 
> * Escrever script de T-SQL usando snippets
> * Conheça mais detalhes sobre o objeto de banco de dados usando Inspecionar Definição e Ir para Definição


Para saber como habilitar o widget das **cinco consultas mais lentas**, conclua o seguinte tutorial:

> [!div class="nextstepaction"]
> [Habilitar o widget de insight de exemplo de consultas lentas](tutorial-qds-sql-server.md)
