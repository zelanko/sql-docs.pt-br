---
Title: 'Tutorial: Additional Tips and Tricks for using SSMS'
description: 'Um tutorial que aborda algumas outras Dicas e Truques para usar o SSMS. '
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
ms.openlocfilehash: 792d6c7fe69a1b8ec77c70d0fbfa6ceaa92d808a
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="tutorial-additional-tips-and-tricks-for-using-ssms"></a>Tutorial: mais dicas e truques para usar o SSMS
Este tutorial fornecerá algumas outras dicas e truques para usar o SQL Server Management Studio. Este artigo ensinará como: 

> [!div class="checklist"]
> * Comentar/remover marca de comentário do texto do T-SQL (Transact-SQL)
> * Recuar o texto
> * Filtrar objetos no Pesquisador de Objetos
> * Acessar o log de erros do SQL Server
> * Encontrar o nome da sua instância do SQL Server

## <a name="prerequisites"></a>Prerequisites
Para concluir este Tutorial, você precisará do SQL Server Management Studio, bem como acesso a um SQL Server e um banco de dados do AdventureWorks. 

- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Baixar [Bancos de dados de exemplo do AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). As instruções para restaurar bancos de dados no SSMS podem ser encontradas aqui: [Restaurando um banco de dados](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 

## <a name="comment--uncomment-your-t-sql-code"></a>Comentar/remover marca de comentário no código T-SQL
Partes do texto podem ser comentadas ou ter a marca de comentário removida delas usando o botão de comentário na barra de ferramentas. Texto comentado não será executado. 

1. Abra o SQL Server Management Studio. 
2. Conecte-se ao SQL Server.
3. Abra uma janela **Nova Consulta**. 
4. Cole o seguinte trecho de código T-SQL na janela de texto: 

  ```sql
    USE master
    GO

    -- Drop the database if it already exists
    IF  EXISTS (
        SELECT name 
            FROM sys.databases 
            WHERE name = N'TutorialDB'
            )

    DROP DATABASE TutorialDB
    GO

    CREATE DATABASE TutorialDB
    GO

    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
 ``` 


5. Selecione a parte do texto de **Alterar Banco de Dados** e clique em **Comentar** na barra de ferramentas: 

    ![Comentário](media/ssms-tricks/comment.png)
6. Clique em **Executar** para executar a parte cuja marca de comentário foi removida do texto. 
7. Selecione tudo o que não for o comando **Alterar Banco de Dados** e clique em **Comentar** na barra de ferramentas:

    ![Comentar tudo](media/ssms-tricks/commenteverything.png)

8. Selecione a parte de **Alterar Banco de Dados** e clique em **Remover marca de comentário** para fazer isso:

    ![Remover marca de comentário](media/ssms-tricks/uncomment.png)
    
9. Clique em **Executar** para executar a parte cuja marca de comentário foi removida do texto. 

## <a name="indent-your-text"></a>Recuar o texto
Os botões de recuo permitem aumentar e diminuir o recuo do texto. 

1. Abra uma janela **Nova Consulta**. 
2. Cole o seguinte trecho de código T-SQL na janela de texto: 

  ```sql
    USE master
    GO

    -- Drop the database if it already exists
    IF  EXISTS (
        SELECT name 
            FROM sys.databases 
            WHERE name = N'TutorialDB'
            )

    DROP DATABASE TutorialDB
    GO

    CREATE DATABASE TutorialDB
    GO

    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
 ``` 
 
3. Selecione a parte **Alterar Banco de Dados** do texto e pressione **Aumentar Recuo** na barra de ferramentas para mover este texto para a frente:

    ![Aumentar Recuo](media/ssms-tricks/increaseindent.png)

4. Selecione a parte do texto **Alterar Banco de Dados** novamente e, dessa vez, clique em **Diminuir Recuo** para mover o texto para trás. 
    ![Diminuir Recuo](media/ssms-tricks/decreaseindent.png)


## <a name="filter-objects-in-object-explorer"></a>Filtrar objetos no Pesquisador de Objetos
Quando um banco de dados tem muitos objetos, pode ser difícil localizar um objeto específico. Para facilitar essa tarefa, é possível filtrar objetos. Esta seção explica como filtrar tabelas, mas as mesmas etapas podem ser aplicadas a qualquer outro nó no **Pesquisador de Objetos**

1. Conecte-se ao SQL Server.
2. Expanda o nó **Bancos de Dados**.
3. Expanda o nó **AdventureWorks** do banco de dados. 
4. Expanda o nó **Tabelas**. 
   - Observe que todas as tabelas que estão presentes no banco de dados são mostradas.
5. Clique com botão direito do mouse no nó **Tabelas** > **Filtro** > **Configurações de Filtro**:

    ![Configurações de Filtro](media/ssms-tricks/filtersettings.png)

6. Na janela Configurações de Filtro, é possível modificar as configurações de filtro. Veja alguns exemplos:
    - Filtrar por nome: ![Filtrar por nome](media/ssms-tricks/filterbyname.png)
    - Filtrar por esquema: ![Filtrar por esquema](media/ssms-tricks/filterbyschema.png)

7. Para limpar o filtro, clique com o botão direito do mouse em **Tabelas** > **Remover Filtro**

    ![Remover Filtro](media/ssms-tricks/removefilter.png)
    


## <a name="access-your-sql-server-error-log"></a>Acessar o log de erros do SQL Server
O log de erros é um arquivo que contém os detalhes sobre as coisas que ocorrem dentro do SQL Server. Ele pode ser pesquisado e consultado no SSMS. Ele também pode ser encontrado como um arquivo .log no disco.

### <a name="open-error-log-within-ssms"></a>Abra o Log de erros no SSMS
1. Conecte-se ao SQL Server.
2. Expanda o nó **Gerenciamento** . 
3. Expanda o nó **Logs do SQL Server**. 
4. Clique com o botão direito do mouse no log de erros **Atual** > **Exibir Log do SQL Server**:

    ![Exibir o Log de erros no SSMS](media/ssms-tricks/viewerrorloginssms.png)

### <a name="query-error-log-within-ssms"></a>Consultar o Log de erros no SSMS
1. Conecte-se ao SQL Server.
2. Abra uma janela **Nova Consulta**.
3. Cole o seguinte trecho de código T-SQL na janela de consulta:

 ```sql
   sp_readerrorlog 0,1,'Server process ID' 
  ``` 
4. Modifique o texto nas aspas simples para o texto desejado.
5. Execute a consulta e examine os resultados:
   
    ![Consultar Log de erros](media/ssms-tricks/queryerrorlog.png)


### <a name="find-error-log-location-if-youre-connected-to-sql"></a>Localizar o local do log de erros se você estiver conectado ao SQL
1. Conecte-se ao SQL Server.
2. Abra uma janela **Nova Consulta**.
3. Cole o seguinte trecho de código T-SQL na janela de consulta e clique em **Executar**:

 ```sql
    SELECT SERVERPROPERTY('ErrorLogFileName') AS 'Error log file location'  
  ``` 

4. Os resultados mostram o local do log de erros no sistema de arquivos: 

    ![Localizar o log de erros por consulta](media/ssms-tricks/finderrorlogquery.png)

### <a name="find-error-log-location-if-you-cannot-connect-to-sql"></a>Localizar o local do log de erros se você não puder se conectar ao SQL
1. Abra o SQL Server Configuration Manager. 
2. Expanda o nó **Serviços**.
3. Clique com o botão direito do mouse na instância do SQL Server > **Propriedades**:

    ![Propriedades de Servidor do Gerenciador de Configurações](media/ssms-tricks/serverproperties.PNG)

4. Selecione a guia **Parâmetros de Inicialização**.
5. Na área **Parâmetros Existentes**, o caminho após o “-e” é a localização do log de erros: 
    
    ![Log de erros](media/ssms-tricks/errorlog.png)
    - Você observará que há vários errorlog.* neste local. Aquele que termina com *.log é o atual. Os que terminam com números são logs anteriores, visto que um novo log é criado sempre que o SQL Server for reiniciado. 
6. Abra esse arquivo no Bloco de Notas. 

## <a name="determine-sql-server-name"></a>Determine o nome do SQL Server...
Há diferentes maneiras de determinar o nome do SQL Server antes e depois de conectar-se a ele.  

### <a name="when-you-dont-know-it"></a>...Quando você não a conhece
1. Siga as etapas para localizar o [Log de erros do SQL Server em disco](#finding-your-error-log-if-you-cannot-connect-to-sql). 
2. Abra o errorlog.log no Bloco de Notas. 
3. Navegue por ele até encontrar o texto em inglês "Server name is" ("O nome do servidor é"):
  - Tudo o que está listado entre as aspas simples é o nome do SQL Server, ou seja, o nome ao qual você se conectará: ![Nome do Servidor no Log de Erros](media/ssms-tricks/servernameinlog.png) O formato do nome é 'HOSTNAME\INSTANCENAME'. Se aparecer apenas o nome do host, a instância padrão estará instalada, e o nome da instância será 'MSSQLSERVER'. Ao conectar-se a uma instância padrão, basta digitar o nome do host para conectar-se ao SQL Server.  

### <a name="once-youre-connected-to-sql"></a>...Quando estiver conectado ao SQL 
Há três locais para identificar a qual SQL Server você está se conectado. 

1. O nome do servidor será listado no **Pesquisador de Objetos**:

    ![Nome da instância no Pesquisador de Objetos](media/ssms-tricks/nameinobjectexplorer.png)
2. O nome do servidor será listado na janela de consulta:

    ![Nome na Janela de Consulta](media/ssms-tricks/nameinquerywindow.png)
3. O nome do servidor também será listado na **janela Propriedades**.
    - Para acessá-lo, abra o Menu **Exibir** > **Janela Propriedades**:

    ![Nome em Propriedades](media/ssms-tricks/nameinproperties.png)

### <a name="if-youre-connected-to-an-alias-or-availability-group-listener"></a>...Se você estiver conectado a um Alias ou Ouvinte do Grupo de Disponibilidade 
Quando você estiver conectado a um alias ou a um ouvinte do Grupo de Disponibilidade, é isso que aparecerá em **Pesquisador de Objetos** e **Propriedades**. Nesse caso, o nome do SQL Server pode não ser aparente e precisa ser consultado. 

1. Conecte-se ao SQL Server.
2. Abra uma janela **Nova Consulta**.
3. Cole o seguinte trecho de código T-SQL na janela: 

  ```sql
   select @@Servername 
 ``` 
4. Exiba os resultados da consulta para identificar o nome do SQL Server ao qual você está conectado: 
    
    ![Consultar Nome do Servidor](media/ssms-tricks/queryservername.png)


