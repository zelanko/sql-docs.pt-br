---
title: Configurar um cliente de ciência de dados para o desenvolvimento de R no SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.openlocfilehash: 489d4c3b008aa31c8f36f8018dfb3ea8358963e3
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2018
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>Configurar um cliente de ciência de dados para o desenvolvimento de R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Depois de configurar uma instância de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para suportar o aprendizado de máquina, você deve configurar um ambiente de desenvolvimento é capaz de se conectar ao servidor para implantação e execução remota.

Este artigo descreve alguns cenários comuns do cliente, incluindo a configuração do Visual Studio Community edition gratuito para executar código R no SQL Server.

## <a name="install-r-libraries-on-the-client"></a>Instalar bibliotecas de R no cliente

O ambiente de cliente deve incluir o Microsoft R Open, bem como os pacotes RevoScaleR adicionais que dão suporte à execução distribuída do R no SQL Server. Distribuições padrão do R não tem os pacotes que dão suporte a contextos de computação remota ou execução paralela de tarefas de R.

Para obter essas bibliotecas, instale qualquer um dos seguintes:
  
+ [Cliente do Microsoft R](http://aka.ms/rclient/download)

+ Microsoft R Server (for SQL Server 2016)

    - Para instalar o programa de instalação do SQL Server, consulte [instalar o SQL Server 2016 R Server (autônomo)](../install/sql-r-standalone-windows-install.md)

    - Para usar o instalador separado baseado no Windows, consulte [instalar Machine Learning Server para Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)

+ Máquina de aprendizagem do servidor (SQL Server 2017)

    - Para instalar o programa de instalação do SQL Server, consulte [instalar 2017 Machine Learning servidor do SQL Server (autônomo)](../install/sql-machine-learning-standalone-windows-install.md)

    - Para usar o instalador separado baseado no Windows, consulte [instalar o R Server 9.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

## <a name="r-tools"></a>Ferramentas de R

Quando você instala o R com o SQL Server, você obtém as mesmas ferramentas de R que são instaladas com qualquer **base** instalação do R, como RGui, Rterm e assim por diante. Portanto, tecnicamente, você tem todas as ferramentas que você precisa para desenvolver e testar o código de R.

As seguintes ferramentas de R padrão são incluídas em um *base instalação* do R e, portanto, são instalados por padrão.

+ **O RTerm**: um terminal de linha de comando para execução de scripts de R

+ **RGui.exe**: um editor interativo simples de R. Os argumentos de linha de comando são os mesmos para RGui.exe e RTerm.

+ **RScript**: uma ferramenta de linha de comando para executar scripts R no modo de lote.

Para localizar essas ferramentas, determine a biblioteca de R instalado quando você configurar o SQL Server ou a recurso de aprendizado de máquina autônomo. Por exemplo, em uma instalação padrão, as ferramentas de R estão localizadas nessas pastas:

+ SQL Server 2016 R Services: `~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`
+ Microsoft R Server autônomo: `~\Program Files\Microsoft R\R_SERVER\bin\x64`
+ SQL Server 2017 aprendizado de máquina serviços: `~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`
+ Server (autônomo) de aprendizado de máquina: `~\Program Files\Microsoft\ML Server\R_SERVER\bin\x64`

Se você precisar de ajuda com as ferramentas de R, basta abrir **RGui**, clique em **ajuda**e selecione uma das opções

## <a name="microsoft-r-client"></a>Cliente do Microsoft R

O cliente do Microsoft R é um download gratuito que permite o acesso aos pacotes RevoScaleR para uso de desenvolvimento. Instalando o cliente do R, você pode criar soluções de R que podem ser executadas em todos os contextos de computação com suporte, incluindo a análise do SQL Server no banco de dados e computação distribuída de R no Hadoop, Spark ou Linux usando o servidor de aprendizado de máquina.

Se você já tiver instalado um ambiente de desenvolvimento R diferente, como RStudio, certifique-se reconfigurar o ambiente para usar as bibliotecas e executáveis fornecidos pelo cliente do Microsoft R. Ao fazer isso, você pode usar todos os recursos do pacote RevoScaleR, embora o desempenho será limitado.

Para obter mais informações, consulte [o que é cliente do Microsoft R?](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

## <a name="install-a-development-environment"></a>Instalar um ambiente de desenvolvimento

Se você ainda não tiver um ambiente de desenvolvimento R preferencial, é recomendável que um destes procedimentos:

+ Ferramentas de R para o Visual Studio

    Funciona com o Visual Studio 2015.

    Para obter informações de instalação, consulte [como instalar as ferramentas de R para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation).
 
    Para configurar RTVS para usar bibliotecas de cliente do Microsoft R, consulte [sobre o cliente do Microsoft R](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

+ Visual Studio 2017

    Até mesmo a edição Community gratuita inclui a carga de trabalho de ciência de dados, que instala os modelos de projeto para R, Python e F #.

    Baixar o Visual Studio de [este site](https://www.visualstudio.com/vs/). 

+ RStudio

    Se você preferir usar o RStudio, algumas etapas adicionais serão necessárias para usar as bibliotecas de RevoScaleR:

    - Instale o cliente do Microsoft R para obter os pacotes necessários e bibliotecas.
    - Atualize o caminho de R para usar o tempo de execução do Microsoft R.

    Para obter mais informações, consulte [cliente R - configurar seu IDE](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client#step-2-configure-your-ide).

## <a name="configure-your-ide"></a>Configurar seu IDE

+ Ferramentas de R para o Visual Studio

    Consulte [este site](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r) para obter alguns exemplos de como criar e depurar R projetos usando ferramentas de R para Visual Studio. 

+ Visual Studio 2017

    Se você instalar o cliente do Microsoft R ou R Server **antes de** instalar o Visual Studio, as bibliotecas de R Server são detectadas automaticamente e usadas para o caminho de biblioteca. Se você não tiver instalado as bibliotecas de RevoScaleR, do **ferramentas R** menu, selecione **instalar o cliente de R**.

## <a name="run-r-in-sql-server"></a>Executar R no SQL Server

Este exemplo usa o Visual Studio 2017 Community Edition, com a carga de trabalho de ciência de dados instalada.

1. Do **arquivo** menu, selecione **novo** e, em seguida, selecione **projeto**.

2. -Mão painel contém uma lista de modelos pré-instalado. Clique em **R**e selecione **R projeto**. No **nome** , digite `dbtest` e clique em **Okey**.

3. O Visual Studio cria uma nova pasta de projeto e um arquivo de script padrão, `Script.R`. 

4. Tipo `.libPaths()` na primeira linha do script de arquivo e, em seguida, pressione CTRL + ENTER.

5. O caminho da biblioteca R atual deve ser exibido no **R interativo** janela. 

6. Clique o **ferramentas R** menu e selecione **Windows** para ver uma lista das outras janelas específicas de R que você pode exibir em seu espaço de trabalho.
 
    + Exibir a Ajuda pressionando CTRL + 3 em pacotes na biblioteca atual.
    + Consulte as variáveis de R no **Explorer variável**, pressionando CTRL + 8.

7. Criar uma cadeia de caracteres de conexão a uma instância do SQL Server e usar a cadeia de caracteres de conexão no construtor RxInSqlServer para criar um objeto de fonte de dados do SQL Server. 

    ```r
    connStr <- "Driver=SQL Server;Server=MyServer;Database=MyTestDB;Uid=;Pwd="
    sqlShareDir <- paste("C:\\AllShare\\", Sys.getenv("USERNAME"), sep = "")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    cc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    sampleDataQuery <- "SELECT TOP 100 * from [dbo].[MyTestTable]"
    inDataSource <- RxSqlServerData(sqlQuery = sampleDataQuery, connectionString = connStr, rowsPerRead = 500)
    ```

    > [!TIP]
    > Para executar um lote, selecione as linhas que você deseja executar e pressione CTRL + ENTER.

8. Definir o contexto de computação para o servidor e, em seguida, executar um código de R simples nos dados.

    ```r
    rxSetComputeContext(cc)
    rxGetVarInfo(data = inDataSource)
    ```

    Os resultados são retornados no **R interativo** janela.
    
    Se você quiser assegurar-se de que o código está sendo executado na instância do SQL Server, você pode usar o criador de perfil para criar um rastreamento.