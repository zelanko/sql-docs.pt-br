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
ms.openlocfilehash: 0613d9352e7be20de52fb771fb8e28823556304b
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/21/2018
---
# <a name="tutorial-additional-tips-and-tricks-for-using-ssms"></a>Tutorial: mais dicas e truques para usar o SSMS
Este tutorial fornecerá algumas outras dicas e truques para usar o SQL Server Management Studio. Este artigo ensinará como: 

   - Comentar/remover marca de comentário do texto do T-SQL (Transact-SQL)
   - Recuar o texto
   - Filtrar objetos no Pesquisador de Objetos
   - Acessar o log de erros do SQL Server
   - Encontrar o nome da sua instância do SQL Server

## <a name="prerequisites"></a>Prerequisites
Para concluir este Tutorial, você precisará do SQL Server Management Studio, bem como acesso a um SQL Server e um banco de dados do AdventureWorks. 

- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- Baixar [Bancos de dados de exemplo do AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). 
    - As instruções para restaurar bancos de dados no SSMS podem ser encontradas aqui: [Restaurando um banco de dados](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 

## <a name="commenting--uncommenting-your-t-sql"></a>Comentar/remover marca de comentário do seu T-SQL
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
2. Selecione a parte do texto de **Alterar Banco de Dados** e clique em **Comentar** na barra de ferramentas: 

    ![Comentário](media/ssms-tricks/comment.png)
3. Clique em **Executar** para executar a parte cuja marca de comentário foi removida do texto. 
4. Selecione tudo o que não for o comando **Alterar Banco de Dados** e clique em **Comentar** na barra de ferramentas:

    ![Comentar tudo](media/ssms-tricks/commenteverything.png)

5. Selecione a parte de **Alterar Banco de Dados** e clique em **Remover marca de comentário** para fazer isso:

    ![Remover marca de comentário](media/ssms-tricks/uncomment.png)
    
6. Clique em **Executar** para executar a parte cuja marca de comentário foi removida do texto 

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
2. Selecione a parte do texto **Alterar Banco de Dados** e pressione **Aumentar Recuo** na barra de ferramentas para mover este texto para a frente

    ![Aumentar Recuo](media/ssms-tricks/increaseindent.png)

3. Selecione a parte do texto **Alterar Banco de Dados** novamente e, dessa vez, clique em **Diminuir Recuo** para mover o texto para trás. 
    ![Diminuir Recuo](media/ssms-tricks/decreaseindent.png)


## <a name="filtering-objects-in-object-explorer"></a>Filtrando objetos no Pesquisador de Objetos
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
    


## <a name="accessing-your-sql-server-error-log"></a>Acessar o log de erros do SQL Server
O log de erros é um arquivo que contém os detalhes sobre as coisas que ocorrem dentro do SQL Server. Ele pode ser pesquisado e consultado no SSMS. Ele também pode ser encontrado como um arquivo .log no disco.

### <a name="finding-your-error-log-if-you-cannot-connect-to-sql"></a>Localizando o log de erros se não for possível se conectar ao SQL
1. Abra o SQL Server Configuration Manager. 
2. Expanda o nó **Serviços**.
3. Clique com o botão direito do mouse na instância do SQL Server > **Propriedades**:

    ![Propriedades de Servidor do Gerenciador de Configurações](media/ssms-tricks/serverproperties.PNG)

4. Selecione a guia **Parâmetros de Inicialização**.
5. Na área **Parâmetros Existentes**, o caminho após o “-e” é a localização do log de erros: 
    
    ![Log de erros](media/ssms-tricks/errorlog.png)
    - Você observará que há vários errorlog.* neste local. Aquele que termina com *.log é o atual. Os que terminam com números são logs anteriores, visto que um novo log é criado sempre que o SQL Server for reiniciado. 
6. Abra esse arquivo no Bloco de Notas. 

### <a name="finding-your-error-log-if-youre-connected-to-sql"></a>Localizando o log de erros se você não estiver conectado ao SQL
1. Conectar ao SQL Server
2. Abrir uma janela **Nova Consulta** 
3. Cole o seguinte trecho de código T-SQL na janela de consulta e clique em **Executar**:


  ```sql
   SELECT SERVERPROPERTY('ErrorLogFileName') AS 'Error log file location' 
  ```
3. Os resultados mostram o local do log de erros no sistema de arquivos: 

![Localizar o Log de erros por consulta](media/ssms-tricks/finderrorlogquery.png)

### <a name="open-error-log-within-ssms"></a>Abra o Log de erros no SSMS
1. Conecte-se ao SQL Server.
2. Expanda o nó **Gerenciamento** . 
3. Expanda o nó **Logs do SQL Server**. 
4. Clique com o botão direito do mouse no log de erros **Atual** > **Exibir Log do SQL Server**:

    ![Exibir o Log de erros no SSMS](media/ssms-tricks/viewerrorloginssms.png)

### <a name="query-error-log-within-ssms"></a>Consultar o Log de erros no SSMS
1. Conectar-se ao SQL Server
2. Abrir uma janela **Nova Consulta**
3. Cole o seguinte trecho de código T-SQL na janela de consulta:

 ```sql
   sp_readerrorlog 0,1,'Server process ID' 
  ``` 
4. Modifique o texto nas aspas simples para o texto desejado.
5. Execute a consulta e examine os resultados:
   
    ![Consultar Log de erros](media/ssms-tricks/queryerrorlog.png)

## <a name="determine-sql-server-instance-name"></a>Determinar o nome da instância do SQL Server...
Há diferentes maneiras de determinar o nome da sua instância de antes e depois de se conectar ao SQL Server.  

### <a name="when-you-dont-know-it"></a>...Quando você não a conhece
1. Siga as etapas para localizar o [Log de erros do SQL Server em disco.](#finding-your-error-log-if-you-cannot-connect-to-sql) 
2. Abra o errorlog.log no Bloco de Notas. 
3. Navegue por ele até encontrar o texto “Server name is” (“O nome do servidor é”, em inglês)
  - Tudo o que está listado entre as aspas simples é o nome da instância e ao que você vai se conectar ![Nome do servidor no Log de erros](media/ssms-tricks/servernameinlog.png)

### <a name="once-youre-connected"></a>...Quando você estiver conectado
Há três locais para descobrir a qual instância você está conectado. 

1. O nome do servidor será listado no **Pesquisador de Objetos**

    ![Nome da instância no Pesquisador de Objetos](media/ssms-tricks/nameinobjectexplorer.png)
2. O nome do servidor será listado na janela de consulta:

    ![Nome na Janela de Consulta](media/ssms-tricks/nameinquerywindow.png)
3. para obter informações sobre a ferramenta de configuração e recursos adicionais. O nome do servidor também será listado na **janela Propriedades**.
    - Para acessá-lo, abra o Menu **Exibir** > **Janela Propriedades**

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


