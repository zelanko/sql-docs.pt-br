---
title: Dicas e truques ao usar o SSMS
description: Saiba como comentar código e remover a marca de comentário dele, recuar texto, filtrar objetos, acessar logs de erros e localizar nomes de instância do SQL Server com o SQL Server Management Studio.
ms.topic: tutorial
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
author: MashaMSFT
ms.author: mathoma
ms.reviewer: sstein
helpviewer_keywords:
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
- Find SQL Server Instance
- find instance name
- find sql server instance name
ms.custom: seo-lt-2019
ms.date: 03/13/2018
ms.openlocfilehash: 2147baf038b99140bf21ab72695f779c0fe69faf
ms.sourcegitcommit: 6c2232c4d2c1ce5710296ce97b909f5ed9787f66
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84462340"
---
# <a name="tips-and-tricks-for-using-sql-server-management-studio-ssms"></a>Dicas e truques para usar o SSMS (SQL Server Management Studio)

Este artigo apresenta algumas dicas e truques para usar o SSMS (SQL Server Management Studio). Este artigo mostra como: 

> [!div class="checklist"]
> * Comentar/remover marca de comentário do seu texto T-SQL (Transact-SQL)
> * Recuar o texto
> * Filtrar objetos no Pesquisador de Objetos
> * Acessar seu log de erros do SQL Server
> * Localize o nome da sua instância do SQL Server

## <a name="prerequisites"></a>Pré-requisitos

Para testar as etapas deste artigo, você precisará do SQL Server Management Studio, acesso a um SQL Server e um banco de dados do AdventureWorks. 

* Instale o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
* Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
* Baixe um [banco de dados de exemplo do AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). Para saber como restaurar um banco de dados no SSMS, consulte [Restaurando um banco de dados](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 

## <a name="commentuncomment-your-t-sql-code"></a>Comentar/remover marca de comentário do seu código T-SQL

Você pode comentar e remover a marca de comentário do seu texto usando o botão **Comentário** na barra de ferramentas. Texto que é comentado não é executado.

1. Abra o SQL Server Management Studio.

2. Conecte-se ao seu SQL Server.

3. Abra uma janela de Nova Consulta.

4. Cole o código T-SQL a seguir na janela de texto.

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

5. Realce a parte **Alterar Banco de Dados** do texto e, em seguida, selecione o botão **Comentário** na barra de ferramentas: 

    ![O botão Comentário](media/ssms-tricks/comment.png)
6. Selecione **Executar** para executar a parte cuja marca de comentário foi removida do texto. 

7. Realce tudo, exceto pelo comando **Alterar Banco de Dados**, e, em seguida, selecione o botão **Comentário**:

    ![Comentar tudo](media/ssms-tricks/commenteverything.png)

    > [!NOTE]
    > O atalho de teclado para comentar texto é **CTRL + K, CTRL + C**.

8. Realce a parte **Alterar Banco de Dados** do texto e, em seguida, selecione o botão **Remover marca de comentário** para remover a marca de comentário:

    ![Remover marca de comentário do texto](media/ssms-tricks/uncomment.png)

    > [!NOTE]
    > O atalho de teclado para remover marca de comentário do texto é **CTRL + K, CTRL + U**.

9. Selecione **Executar** para executar a parte cuja marca de comentário foi removida do texto.

## <a name="indent-your-text"></a>Recuar o texto

Você pode usar os botões de recuo na barra de ferramentas para aumentar ou diminuir o recuo do texto.

1. Abra uma janela de Nova Consulta.

2. Cole o código T-SQL a seguir na janela de texto:

    ```sql
    USE master
      GO

      --Drop the database if it already exists
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

3. Realce a parte **Alterar Banco de Dados** do texto e, em seguida, selecione o botão **Aumentar Recuo** na barra de ferramentas para mover este texto para frente:

    ![Aumentar o recuo](media/ssms-tricks/increaseindent.png)

4. Realce a parte **Alterar Banco de Dados** do texto novamente e, em seguida, selecione **Diminuir Recuo** para mover esse texto para trás.

    ![Diminuir o recuo](media/ssms-tricks/decreaseindent.png)

## <a name="filter-objects-in-object-explorer"></a>Filtrar objetos no Pesquisador de Objetos

Em bancos de dados que têm muitos objetos, é possível usar a filtragem para pesquisar exibições, tabelas específicas, etc. Esta seção descreve como filtrar tabelas, mas você pode usar as etapas a seguir em qualquer outro nó no Pesquisador de Objetos:

1. Conecte-se ao seu SQL Server.

2. Expanda **Bancos de Dados** > **AdventureWorks** > **Tabelas**. Todas as tabelas no banco de dados são exibidas.

3. Clique com o botão direito do mouse em **Tabelas** e, em seguida, selecione **Filtro** > **Configurações de Filtro**:

    ![Configurações de filtro](media/ssms-tricks/filtersettings.png)

4. Na janela **Configurações de Filtro**, você pode modificar algumas das configurações de filtro a seguir:
    * Filtrar por nome: 

      ![Filtrar por nome](media/ssms-tricks/filterbyname.png)

    * Filtrar por esquema: 

      ![Filtrar por esquema](media/ssms-tricks/filterbyschema.png)

5. Para limpar o filtro, clique com o botão direito do mouse em **Tabelas** e, em seguida, selecione **Remover Filtro**.

    ![Remover filtro](media/ssms-tricks/removefilter.png)

## <a name="access-your-sql-server-error-log"></a>Acessar seu log de erros do SQL Server

O log de erros é um arquivo que contém detalhes sobre o que ocorre na sua instância do SQL Server. Você pode procurar e consultar o log de erros no SSMS. O log de erros é um arquivo .log localizado no disco.

### <a name="open-the-error-log-in-ssms"></a>Abra o log de erros no SSMS

1. Conecte-se ao seu SQL Server.  

2. Expanda **Gerenciamento** > **Logs do SQL Server**. 

3. Clique com o botão direito do mouse no log de erros **Atual** e, em seguida, selecione **Exibir Log do SQL Server**:

    ![Exibir o log de erros no SSMS](media/ssms-tricks/viewerrorloginssms.png)

### <a name="query-the-error-log-in-ssms"></a>Consulte o log de erros no SSMS

1. Conecte-se ao seu SQL Server.

2. Abra uma janela de Nova Consulta.

3. Cole o código T-SQL a seguir na janela de consulta:

     ```sql
       sp_readerrorlog 0,1,'Server process ID'
      ```

4. Modifique o texto entre aspas simples para o texto que você deseja pesquisar.

5. Execute a consulta e examine os resultados:

    ![Consulte o log de erros](media/ssms-tricks/queryerrorlog.png)

### <a name="find-the-error-log-location-if-youre-connected-to-sql-server"></a>Localize o local do log de erros se você estiver conectado ao SQL Server

1. Conecte-se ao seu SQL Server.

2. Abra uma janela de Nova Consulta.

3. Cole o código T-SQL a seguir na janela de consulta e, em seguida, selecione **Executar**:

     ```sql
        SELECT SERVERPROPERTY('ErrorLogFileName') AS 'Error log file location'  
      ```

4. Os resultados mostram o local do log de erros no sistema de arquivos: 

    ![Localizar o log de erros por consulta](media/ssms-tricks/finderrorlogquery.png)

### <a name="find-the-error-log-location-if-you-cant-connect-to-sql-server"></a>Localize o local do log de erros se você não conseguir se conectar ao SQL Server

O caminho para o log de erros do SQL Server pode variar dependendo das suas definições de configuração. O caminho para o local do log de erros pode ser encontrado nos parâmetros de inicialização no SQL Server Configuration Manager. Siga as etapas abaixo para localizar o parâmetro de inicialização relevante que identifica o local do seu log de erros do SQL Server. *O caminho pode variar do caminho indicado abaixo*.

1. Abra o SQL Server Configuration Manager.

2. Expanda **Serviços**.

3. Clique com o botão direito do mouse na sua instância do SQL Server e, em seguida, selecione **Propriedades**:

    ![Propriedades do servidor do Configuration Manager](media/ssms-tricks/serverproperties.PNG)

4. Selecione a guia **Parâmetros de Inicialização**.

5. Na área **Parâmetros Existentes**, o caminho após o "-e" é a localização do log de erros: 

    ![Log de erros](media/ssms-tricks/errorlog.png)

    Há vários arquivos errorlog.* neste local. O nome do arquivo que termina com *.log é o arquivo de log de erros atual. Nomes de arquivo que terminam com números são arquivos de log anteriores. Um novo log é criado sempre que o SQL Server é reiniciado.

6. Abra o arquivo errorlog.log no Bloco de Notas. 

## <a name="find-sql-server-instance-name"></a><a name="determine-sql-server-name"></a>Localizar o nome da instância do SQL Server

Você tem algumas opções para localizar o nome do SQL Server antes e depois de se conectar ao SQL Server.  

### <a name="before-you-connect-to-sql-server"></a>Antes de você se conectar ao SQL Server

1. Siga as etapas para localizar o [Log de erros do SQL Server em disco](#find-the-error-log-location-if-you-cant-connect-to-sql-server). O caminho pode ser diferente do caminho na imagem abaixo.

2. Abra o arquivo errorlog.log no Bloco de Notas.

3. Pesquise o texto *O nome do servidor é*.

    Tudo o que está listado entre aspas simples é o nome da instância do SQL Server à qual você vai se conectar:

    ![Localize o nome do servidor no log de erros](media/ssms-tricks/servernameinlog.png)

    O formato do nome é HOSTNAME\INSTANCENAME. Se você visualiza somente o nome do host, a instância padrão está instalada e o nome da instância é MSSQLSERVER. Quando você se conecta a uma instância padrão, o nome do host é tudo o que você precisa inserir para conectar-se ao SQL Server.  

### <a name="when-youre-connected-to-sql-server"></a>Quando você está conectado ao SQL Server

Quando você está conectado ao SQL Server, pode encontrar o nome do servidor em três locais: 

1. O nome do servidor é listado no Pesquisador de Objetos:

    ![Nome da instância do SQL Server no Pesquisador de Objetos](media/ssms-tricks/nameinobjectexplorer.png)
2. O nome do servidor é listado na janela Consulta:

    ![Nome da instância do SQL Server na janela de Consulta](media/ssms-tricks/nameinquerywindow.png)
3. O nome do servidor é listado em **Propriedades**.
    * No menu **Exibir**, selecione **Janela Propriedades**:

      ![Nome da instância do SQL Server na janela Propriedades](media/ssms-tricks/nameinproperties.png)

### <a name="if-youre-connected-to-an-alias-or-availability-group-listener"></a>Se você estiver conectado a um alias ou ouvinte do Grupo de Disponibilidade

Se você estiver conectado a um alias ou a um ouvinte do Grupo de Disponibilidade, essa informação será exibida no Pesquisador de Objetos e em Propriedades. Nesse caso, o nome do SQL Server pode não estar imediatamente aparente e deverá ser consultado:

1. Conecte-se ao seu SQL Server.

2. Abra uma janela de Nova Consulta.

3. Cole o código T-SQL a seguir na janela:

      ```sql
       select @@Servername
     ```

4. Veja os resultados da consulta para identificar o nome da instância do SQL Server à qual você está conectado: 

    ![Consulte o nome do SQL Server](media/ssms-tricks/queryservername.png)

## <a name="next-steps"></a>Próximas etapas

O melhor modo de se familiarizar com o SSMS é praticando. Estes artigos com *tutoriais* e *instruções* ajudam nos diversos recursos disponíveis no SSMS.  Estes artigos ensinam a administrar os componentes do SSMS e a encontrar os recursos que você usa com regularidade.

* [Conectar-se e consultar uma instância](connect-query-sql-server.md)
* [Script](scripting-ssms.md)
* [Usando modelos no SSMS](../template/templates-ssms.md)
* [Configuração do SSMS](ssms-configuration.md)
