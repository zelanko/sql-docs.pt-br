---
title: Configurar um cliente de ciência de dados para o desenvolvimento de R no SQL Server | Microsoft Docs
description: Instale ferramentas e bibliotecas do R locais em uma estação de trabalho de desenvolvimento para conexões remotas ao SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 309a78a2195f55a3ec39604b0c2bd385bb06a271
ms.sourcegitcommit: 9d0ff4f3e40db48fc01788684d34719065d159b6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/12/2018
ms.locfileid: "44724310"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>Configurar um cliente de ciência de dados para o desenvolvimento de R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Depois de configurar uma instância de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para suportar o aprendizado de máquina, você deve configurar um ambiente de desenvolvimento de R que é capaz de se conectar ao servidor para implantação e execução remota.

### <a name="evaluation-and-independent-development"></a>Desenvolvimento independente e avaliação
 
Se você tiver a edição de desenvolvedor e o plano para trabalhar localmente em um script R que você planeja mover para o SQL Server, você poderá pular para [instalar um IDE](#install-ide) e apontar a ferramenta para bibliotecas do R locais usadas pelo SQL Server.

> [!Tip]
> Para obter uma demonstração e vídeo passo a passo, consulte [executar R e Python remotamente no SQL Server de qualquer IDE ou de blocos de anotações do Jupyter](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/) ou isso [vídeo do YouTube](https://youtu.be/D5erljpJDjE).

## <a name="1---install-r-packages"></a>1 – instalar pacotes R

Funcionalidade de R em produtos da Microsoft está em várias camadas. Ele começa com a distribuição de R de base de código-fonte aberto da Microsoft, mas é então estendido com pacotes de produtos específicos, tais como [RevoScaleR](revoscaler-overview.md), que permitem contextos de computação remota e a execução paralela de tarefas de R.

Operações coordenadas entre um cliente e o servidor remoto exigem que os dois sistemas tendo os mesmos pacotes. Para obter o conjunto completo de bibliotecas em uma estação de trabalho do cliente, instale um dos pacotes de software na tabela a seguir. 

| Provedor de biblioteca | Uso  |
|------------------|--------------------------------|
| [Cliente do Microsoft R](http://aka.ms/rclient/download) |  Este download gratuito fornece RevoScaleR, MicrosoftML e outros pacotes de R, mas está limitado a dois threads e os dados na memória. No entanto, você pode ainda criar soluções de R que inicie localmente e mudar de execução (conhecido como *contexto de computação*) para acessar dados e a potência computacional de uma instância remota do SQL Server. Essa é a abordagem recomendada para a integração de cliente com uma instância do SQL Server de produção. Para obter mais informações sobre essa ferramenta, consulte [o que é o Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client).|
| Servidores autônomos | Sob **recursos compartilhados**, instalação do SQL Server inclui opções de instalação de servidor autônomo para o aprendizado de máquina do SQL Server 2016 R Services e SQL Server 2017. Esses são servidores completos, totalmente separados do SQL Server, com a capacidade de se conectar e consumir dados de várias plataformas de dados. Mas você poderia potencialmente usar o software em uma capacidade do cliente para acessar a instância do mecanismo de banco de dados do SQL Server executando tarefas de R e Python. [Servidor de aprendizado de máquina do SQL Server 2017 (autônomo)](../install/sql-machine-learning-standalone-windows-install.md) tem as mesmas bibliotecas como uma instância de aprendizado de máquina do SQL Server 2017. [SQL Server 2016 R Server (autônomo)](../install/sql-r-standalone-windows-install.md) tem as mesmas bibliotecas como o SQL Server 2016 R Services. |


<a name="r-tool"></a>
 
## <a name="2---open-an-r-prompt"></a>2 - abrir um prompt de R

Quando você instala o R com o SQL Server, você pode obter as mesmas ferramentas de R que são padrão para qualquer instalação básica do R, como RGui, Rterm e assim por diante. Essas ferramentas são leves e útil para verificando informações de pacote e biblioteca, executando comandos ad hoc ou script ou percorrer os tutoriais. Você pode usar essas ferramentas para obter informações de versão do R e confirme a conectividade.

Para usar a versão do R instalada com o SQL Server ou cliente do R, abra um prompt de R da pasta de programa do SQL Server ou cliente do R. As etapas a seguir são para o R Client e RGui.exe.

1. Para o R Client, vá para `~\Program Files\Microsoft\R Client\R_SERVER\bin\x64`.
2. Clique duas vezes em **RGui.exe** para iniciar uma sessão de R com um prompt de comando do R.

Quando você inicia uma sessão de R de uma pasta de programa da Microsoft, vários pacotes, incluindo RevoScaleR, carregar automaticamente. Insira **Search ()** no prompt do R para confirmação.

   ![Informações de versão durante o carregamento R](../install/media/rclient-rgui-r-prompt.png "abra um prompt de R")

### <a name="tool-list-and-location"></a>Local e a lista de ferramentas

| Ferramenta | Description | 
|------|-------------|
| **RTerm**: | Um terminal de linha de comando para executar scripts R | 
| **RGui.exe** | Um editor interativo simples para R. Os argumentos de linha de comando são as mesmas para RGui.exe e RTerm. |
| **RScript** | Uma ferramenta de linha de comando para executar scripts do R no modo de lote. |

Ferramentas estão localizadas em **bin** pasta para R base instalada do SQL Server ou cliente do R. Os caminhos a seguir são os locais válidos para as ferramentas, dependendo de qual versão do produto e o recurso que você instalou:

| Produto da Microsoft | Local da ferramenta de R |
|-------------------|-----------------|
| Cliente do Microsoft R | `~\Program Files\Microsoft\R Client\R_SERVER\bin\x64` |
| Servidor de Learning (R) máquina da Microsoft | `~\Program Files\Microsoft\R_SERVER\bin\x64`
| SQL Server 2016 R Services | `~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`|
| Servidor do SQL Server 2016 R autônomo | `~\Program Files\Microsoft SQL Server\130\R_SERVER\bin\x64` 
| (R) serviços de aprendizado de máquina do SQL Server 2017 | `~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`|
| Servidor autônomo do SQL Server 2017 Machine Learning (R) | `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` |

## <a name="3---permissions"></a>3 - permissões

Para se conectar a uma instância do SQL Server para executar scripts e carregar dados, você deve ter um logon válido no servidor de banco de dados. Você pode usar um logon SQL ou a autenticação integrada do Windows. Em geral, é recomendável que você usa a autenticação integrada do Windows, mas usar o logon do SQL é mais simples para alguns cenários.

No mínimo, a conta usada para executar o código deve ter permissão para ler os bancos de dados você está trabalhando, além de permissão especial executar qualquer SCRIPT externo. A maioria dos desenvolvedores também exigem permissões para criar novos objetos na forma de procedimentos armazenados que contém o script e gravar dados em tabelas que contêm dados de treinamento ou pontuados dados. 

Peça ao administrador de banco de dados para configurar as seguintes permissões para a conta, no banco de dados em que você usar o r:

+ **EXECUTE ANY EXTERNAL SCRIPT** executar R no servidor.
+ **db_datareader** privilégios para executar as consultas usadas para treinar o modelo.
+ **db_datawriter** para gravar dados de treinamento ou dados de pontuação.
+ **db_owner** para criar objetos, como procedimentos armazenados, tabelas, funções. 
  Você também precisa **db_owner** criar bancos de dados de exemplo e teste. 

Se seu código exigir pacotes que não são instalados por padrão com o SQL Server, organize-se com o administrador de banco de dados para ter os pacotes instalados com a instância. SQL Server é um ambiente seguro e há restrições sobre onde os pacotes podem ser instalados. Instalação de ad hoc de pacotes como parte do seu código não é recomendável, mesmo se você tiver direitos. Além disso, sempre considere as implicações de segurança antes de instalar novos pacotes na biblioteca do servidor.

> [!Tip]
> Se você estiver familiarizado com o SQL Server e trabalhar em um ambiente de desenvolvimento local, você pode percorrer este tutorial para saber mais sobre logons e permissões de configuração: [aprofundamento no RevoScaleR](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

## <a name="4---test-connections"></a>4 - testar conexões

SQL Server deve estar habilitado para [conexões remotas](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md) e você deve ter permissões, incluindo um logon de usuário e se conectar a um banco de dados. As etapas a seguir pressupõem o banco de dados de demonstração [NYCTaxi_Sample](../tutorials/sqldev-download-the-sample-data.md) e autenticação do Windows.

 Como uma etapa de verificação, use uma ferramenta interna e o RevoScaleR para confirmar a conectividade ao servidor remoto.

1. Comece [abrindo uma ferramenta de R](#r-tool) na estação de trabalho cliente. RevoScaleR carrega automaticamente. Por exemplo, acesse `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` e clique duas vezes **RGui.exe** para iniciá-lo.

2. Confirme o que revoscaler está funcionando executando este comando, que retorna um resumo estatístico em um conjunto de dados de demonstração. Verifique se que você fornecer um nome de servidor válido para a instância do mecanismo de banco de dados do SQL Server.

```r
connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
testQuery <-"SELECT DISTINCT TOP(100) tip_amount FROM [dbo].nyctaxi_sample ORDER BY tip_amount DESC;"
cc <-RxInSqlServer(connectionString=connStr)
rxSummary(formula = ~ ., data = RxSqlServerData(sqlQuery=testQuery, connectionString=connStr), computeContext=cc)
```
Esse script se conecta a um banco de dados no servidor remoto, fornece uma consulta, cria um contexto de computação `cc` instrução para execução remota de código, em seguida, fornece a função RevoScaleR **rxSummary** para retornar uma estatística Resumo dos resultados da consulta.

<a name="install-ide"></a>

## <a name="5---install-an-ide"></a>5 - instalar um IDE

Para projetos de desenvolvimento sério e sustentado, você deve instalar um ambiente de desenvolvimento integrado (IDE). Ferramentas do SQL Server e as ferramentas do R internos não estão preparadas para o desenvolvimento de R pesado. Uma vez que o código de trabalho, você pode implantá-lo como um procedimento armazenado para execução no SQL Server.

Você deve apontar o seu IDE para as bibliotecas do R locais: base R, RevoScaleR e assim por diante. Executar cargas de trabalho em um servidor SQL remoto ocorre durante a execução do script, quando seu script invoca um contexto de computação remota no SQL Server, acesso a dados e operações nesse servidor.

### <a name="rstudio"></a>RStudio

Ao usar [RStudio](https://www.rstudio.com/), você pode configurar o ambiente para usar as bibliotecas do R e executáveis que correspondem às em um servidor SQL remoto.

1. Verifique as versões do pacote de R instaladas no SQL Server. Para obter mais informações, consulte [informações do pacote de R Obtenha](determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location).

1. Instale o Microsoft R Client ou uma das opções de servidor autônomo para adicionar o RevoScaleR e outros pacotes de R, incluindo a distribuição de R base usada pela instância do SQL Server. Escolha uma versão ao mesmo nível ou abaixo (pacotes são compatíveis com versões anteriores) que fornece as mesmas versões de pacote como os do servidor. Para obter informações de versão, consulte a versão mapear neste artigo: [componentes atualizar R e Python](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

1. No RStudio, [atualize o caminho de R](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R) para apontar para o ambiente de R fornecendo RevoScaleR, Microsoft R Open e outros pacotes da Microsoft. Dependendo de como você adquiriu o RevoScaleR e outras bibliotecas, é provavelmente um dos seguintes caminhos:

  + C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library
  + C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library
  + C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64

### <a name="r-tools-for-visual-studio-rtvs"></a>Ferramentas do R para Visual Studio (RTVS)

Se você ainda não tiver um IDE preferencial para R, recomendamos **ferramentas do R para Visual Studio**.

+ [Baixar R Tools para Visual Studio (RTVS)](https://visualstudio.microsoft.com/vs/features/rtvs/)
+ [Instruções de instalação](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio) -RTVS está disponível em várias versões do Visual Studio.
+ [Introdução às ferramentas do R para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>Conectar-se ao SQL Server das RTVS

Este exemplo usa o Visual Studio 2017 Community Edition, com a carga de trabalho de ciência de dados instalada.

1. Dos **arquivo** menu, selecione **New** e, em seguida, selecione **projeto**.

2. O painel esquerdo contém uma lista de modelos pré-instalados. Clique em **R**e selecione **projeto R**. No **nome** , digite `dbtest` e clique em **Okey**. 

  O Visual Studio cria uma nova pasta de projeto e um arquivo de script padrão, `Script.R`. 

3. Tipo `.libPaths()` na primeira linha do script do arquivo e, em seguida, pressione CTRL + ENTER.

  O caminho da biblioteca R atual deve ser exibido na **R interativo** janela. 

4. Clique o **ferramentas do R** menu e selecione **Windows** para ver uma lista das outras janelas específicas de R que você pode exibir em seu espaço de trabalho.
 
    + Exibir a Ajuda em pacotes na biblioteca atual, pressionando CTRL + 3.
    + Consulte as variáveis do R na **Gerenciador de variáveis**, pressionando CTRL + 8.

5. Criar uma cadeia de conexão para uma instância do SQL Server e usar a cadeia de caracteres de conexão no construtor RxInSqlServer para criar um objeto de fonte de dados do SQL Server. 

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

6. Definir o contexto de computação com o servidor e, em seguida, execute um código de R simples nos dados.

    ```r
    rxSetComputeContext(cc)
    rxGetVarInfo(data = inDataSource)
    ```

    Os resultados são retornados na **R interativo** janela.
    
    Se você quiser garantir que você mesmo que o código está sendo executado na instância do SQL Server, você pode usar o Profiler para criar um rastreamento.

## <a name="next-steps"></a>Próximas etapas

Dois tutoriais diferentes incluem exercícios, de modo que você pode praticar alternar o contexto de computação do local para uma instância remota do SQL Server.

+ [Tutorial: Funções de usam RevoScaleR R com dados do SQL Server](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [Passo a passo de ponta a ponta sobre a ciência de dados](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)