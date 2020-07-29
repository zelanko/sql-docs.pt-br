---
title: Configurar um cliente de ciência de dados do R
description: Instale bibliotecas e ferramentas locais do R em uma estação de trabalho de desenvolvimento para conexões remotas ao SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/13/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a42d3203455d4273410b9b216c19e7a9d1da4e3a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896386"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>Configurar um cliente de ciência de dados para desenvolvimento em R no SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

A integração do R está disponível no SQL Server 2016 ou posterior quando você inclui a opção de linguagem R em uma instalação do [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) ou dos [Serviços de Machine Learning do SQL Server (no banco de dados)](../install/sql-machine-learning-services-windows-install.md). 

Para desenvolver e implantar soluções de R para SQL Server, instale o [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) em sua estação de trabalho de desenvolvimento para obter o [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) e outras bibliotecas do R. A biblioteca RevoScaleR, que também é necessária na instância do SQL Server remoto, coordena as solicitações de computação entre os dois sistemas. 

Neste artigo, saiba como configurar uma estação de trabalho de desenvolvimento do R Client para que você possa interagir com um SQL Server remoto habilitado para aprendizado de máquina e para integração com o R. Depois de concluir as etapas neste artigo, você terá as mesmas bibliotecas do R que aquelas existentes no SQL Server. Você também saberá como efetuar push de computações de uma sessão local do R para uma sessão remota do R no SQL Server.

![Componentes cliente-servidor](media/sqlmls-r-client-revo.png "Bibliotecas e sessões locais e remotas do R")

Para validar a instalação, você pode usar a ferramenta **RGUI** interna conforme descrito neste artigo ou [vincular as bibliotecas](#install-ide) ao RStudio ou a qualquer outro IDE que você normalmente use.

> [!Note]
> Uma alternativa à instalação da biblioteca de clientes é usar um [servidor autônomo](../install/sql-machine-learning-standalone-windows-install.md) como um cliente avançado, que alguns clientes preferem para trabalho em um cenário mais aprofundado. Um servidor autônomo é totalmente dissociado do SQL Server, mas como ele tem as mesmas bibliotecas do R, você pode usá-lo como um cliente para análise no banco de dados do SQL Server. Você também pode usá-lo para trabalho não relacionado ao SQL, incluindo a capacidade de importar e modelar dados de outras plataformas de dados. Se você instalar um servidor autônomo, poderá encontrar o executável do R nesta localização: `C:\Program Files\Microsoft SQL Server\140\R_SERVER`. Para validar a instalação, [abra um aplicativo de console do R](#R-tools) para executar comandos usando o R.exe nessa localização.

## <a name="commonly-used-tools"></a>Ferramentas usadas com frequência

Seja você um desenvolvedor do R não familiarizado com o SQL ou um desenvolvedor do SQL não familiarizado com o R e a análise no banco de dados, você precisará de uma ferramenta de desenvolvimento em R e de um editor de consultas T-SQL, como o [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), para fazer uso de todas as funcionalidades da análise no banco de dados.

Para cenários de desenvolvimento simples em R, você pode usar o executável RGUI, agrupado na distribuição do R base no MRO e no SQL Server. Este artigo explica como usar o RGUI para sessões de R locais e remotas. Para aumentar a produtividade, você deve usar um IDE completo, como [RStudio ou Visual Studio](#install-ide).

O SSMS é um download separado, útil para criar e executar procedimentos armazenados no SQL Server, incluindo aqueles que contêm código do R. Praticamente qualquer código do R que você escreva em um ambiente de desenvolvimento poderá ser inserido em um procedimento armazenado. Você pode percorrer outros tutoriais para saber mais sobre [SSMS e R inserido](../tutorials/sqldev-in-database-r-for-sql-developers.md).

## <a name="1---install-r-packages"></a>1 – Instalar pacotes do R

Os pacotes do R da Microsoft estão disponíveis em vários produtos e serviços. Em uma estação de trabalho local, é recomendável instalar o Microsoft R Client. O R Client fornece [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler), [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), [SQLRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) e outros pacotes do R.

1. [Baixar o Microsoft R Client](https://aka.ms/rclient/download).

2. No assistente de instalação, aceite ou altere o caminho de instalação padrão, aceite ou altere a lista de componentes e aceite os termos de licença do Microsoft R Client.

   Quando a instalação for concluída, uma tela de boas-vindas apresentará o produto e a documentação.

3. Crie uma a variável de ambiente do sistema MKL_CBWR para garantir a saída consistente dos cálculos da Intel MKL (Math Kernel Library).

   + No Painel de Controle, clique em **Sistema e Segurança** > **Sistema** > **Configurações Avançadas do Sistema** > **Variáveis de Ambiente**.
   + Crie uma variável de sistema chamada **MKL_CBWR**, com um valor definido como **AUTO**.

## <a name="2---locate-executables"></a>2 – Localizar os executáveis

Localize e liste o conteúdo da pasta de instalação para confirmar se o R.exe, o RGUI e outros pacotes estão instalados. 

1. No Explorador de Arquivos, abra a pasta C:\Program Files\Microsoft\R Client\R_SERVER\bin para confirmar a localização do R.exe.

2. Abra a subpasta x64 para confirmar o **RGUI**. Você usará essa ferramenta na próxima etapa.

3. Abra C:\Program Files\Microsoft\R Client\R_SERVER\library para examinar a lista de pacotes instalados com o R Client, incluindo RevoScaleR, MicrosoftML e outros.


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3 – Iniciar RGUI

Ao instalar o R com o SQL Server, você obtém as mesmas ferramentas do R que são padrão para qualquer instalação básica do R, como RGui, Rterm e assim por diante. Essas ferramentas são leves e úteis para verificação de informações de pacote e biblioteca, execução de comandos ou scripts ad hoc ou para passo a passo de tutoriais. Você pode usar essas ferramentas para obter informações de versão do R e confirmar a conectividade.

1. Abra C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 e clique duas vezes em **RGui** para iniciar uma sessão do R com um prompt de comando do R.

   Quando você inicia uma sessão do R de uma pasta do programa da Microsoft, vários pacotes, incluindo o RevoScaleR, são carregados automaticamente. 

2. Insira `print(Revo.version)` no prompt de comando para retornar as informações de versão do pacote RevoScaleR. Você deve ter a versão 9.2.1 ou 9.3.0 para RevoScaleR.

3. Insira **search()** no prompt do R para obter uma lista de pacotes instalados.

   ![Informações de versão ao carregar o R](../install/media/rclient-rgui-r-prompt.png "Abrir um prompt do R")


## <a name="4---get-sql-permissions"></a>4 – Obter Permissões do SQL

No R Client, o processamento do R é limitado em dois threads e em dados na memória. Para o processamento escalonável usando vários núcleos e grandes conjuntos de dados, você pode alterar a execução (chamada de *contexto de computação*) para os conjuntos de dados e a capacidade computacional de uma instância remota do SQL Server. Essa é a abordagem recomendada para a integração do cliente com uma instância de produção do SQL Server e você precisará de permissões e informações de conexão para fazer funcionar.

Para se conectar a uma instância do SQL Server para executar scripts e fazer upload de dados, você deve ter um logon válido no servidor de banco de dados. Você pode usar um logon SQL ou a autenticação integrada do Windows. Geralmente, é recomendável usar a autenticação integrada do Windows, mas usar o logon do SQL é mais simples para alguns cenários, especialmente quando o script contém cadeias de conexão para dados externos.

No mínimo, a conta usada para executar o código deve ter permissão para ler os bancos de dados com os quais você está trabalhando, além da permissão especial EXECUTE ANY EXTERNAL SCRIPT. A maioria dos desenvolvedores também exige permissões para criar procedimentos armazenados e para gravar dados em tabelas que contêm dados de treinamento ou dados pontuados. 

Peça ao administrador de banco de dados para [configurar as permissões a seguir para sua conta](../security/user-permission.md) no banco de dados em que você usa o R:

+ **EXECUTE ANY EXTERNAL SCRIPT** para executar o script do R no servidor.
+ Privilégios de **db_datareader** para executar as consultas usadas para treinar o modelo.
+ **db_datawriter** para gravar dados de treinamento ou dados pontuados.
+ **db_owner** para criar objetos como procedimentos armazenados, tabelas e funções. 
  Você também precisa de **db_owner** para criar bancos de dados de exemplo e de teste. 

Se o código exigir pacotes que não sejam instalados por padrão com o SQL Server, providencie junto ao administrador de banco de dados para que os pacotes sejam instalados com a instância. O SQL Server é um ambiente seguro e há restrições sobre onde os pacotes podem ser instalados. Para saber mais, veja [Instalar novos pacotes do R no SQL Server](../package-management/install-additional-r-packages-on-sql-server.md).

## <a name="5---test-connections"></a>5 – Testar conectividade

Como uma etapa de verificação, use **RGUI** e RevoScaleR para confirmar a conectividade com o servidor remoto. O SQL Server deve estar habilitado para [conexões remotas](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server) e você deve ter permissões, incluindo um logon de usuário e um banco de dados ao qual se conectar. 

As etapas a seguir pressupõem o banco de dados de demonstração, [NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md) e a autenticação do Windows.

1. Abra o **RGUI** na estação de trabalho cliente. Por exemplo, acesse `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` e clique duas vezes em **RGui.exe** para iniciá-lo.

2. O RevoScaleR carrega automaticamente. Confirme se o RevoScaleR está funcionando executando este comando: `print(Revo.version)`

3. Insira o script de demonstração que é executado no servidor remoto. Você deve modificar o script de exemplo a seguir para incluir um nome válido para uma instância remota do SQL Server. Essa sessão começa como uma sessão local, mas a função **rxSummary** é executada na instância remota do SQL Server.

   ```R
   # Define a connection. Replace server with a valid server name.
   connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
  
   # Specify the input data in a SQL query.
   sampleQuery <-"SELECT DISTINCT TOP(100) tip_amount FROM [dbo].nyctaxi_sample ORDER BY tip_amount DESC;"
  
   # Define a remote compute context based on the remote server.
   cc <-RxInSqlServer(connectionString=connStr)

   # Execute the function using the remote compute context.
   rxSummary(formula = ~ ., data = RxSqlServerData(sqlQuery=sampleQuery, connectionString=connStr), computeContext=cc)
   ```

   **Resultados:**

   Esse script se conecta a um banco de dados no servidor remoto, fornece uma consulta, cria uma instrução `cc` de contexto de computação para a execução remota de código e, em seguida, fornece a função **rxSummary** do RevoScaleR para retornar um resumo estatístico dos resultados da consulta.

   ```R
     Call:
   rxSummary(formula = ~., data = RxSqlServerData(sqlQuery = sampleQuery, 
       connectionString = connStr), computeContext = cc)

   Summary Statistics Results for: ~.
   Data: RxSqlServerData(sqlQuery = sampleQuery, connectionString = connStr) (RxSqlServerData Data Source)
   Number of valid observations: 100 
  
   Name       Mean   StdDev   Min Max ValidObs MissingObs
   tip_amount 63.245 31.61087 36  180 100      0     
   ```

4. Definir e obter contexto de computação. Depois que você definir um contexto de computação, ele permanecerá em vigor durante a sessão. Se você não tiver certeza se a computação é local ou remota, execute o comando a seguir para descobrir. Os resultados que especificam uma cadeia de conexão indicam um contexto de computação remota.

   ```R
   # Return the current compute context.
   rxGetComputeContext()

   # Revert to a local compute context.
   rxSetComputeContext("local")
   rxGetComputeContext()

   # Switch back to remote.
   connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
   cc <-RxInSqlServer(connectionString=connStr)
   rxSetComputeContext(cc)
   rxGetComputeContext()
   ```  

5. Retorne informações sobre variáveis na fonte de dados, incluindo nome e tipo.

   ```R
   rxGetVarInfo(data = inDataSource)
   ```
   Os resultados incluem 23 variáveis.


6. Gere um gráfico de dispersão para explorar se há dependências entre duas variáveis. 

   ```R
   # Set the connection string. Substitute a valid server name for the placeholder.
   connStr <- "Driver=SQL Server;Server=<your database name>;Database=NYCTaxi_Sample;Trusted_Connection=true"

   # Specify a query on the nyctaxi_sample table.
   # For variables on each axis, remove nulls. Use a WHERE clause and <> to do this.
   sampleQuery <-"SELECT DISTINCT TOP 100 * from [dbo].[nyctaxi_sample] WHERE fare_amount <> '' AND  tip_amount <> ''"
   cc <-RxInSqlServer(connectionString=connStr)

   # Generate a scatter plot.
   rxLinePlot(fare_amount ~ tip_amount, data = RxSqlServerData(sqlQuery=sampleQuery, connectionString=connStr, computeContext=cc), type="p")
   ```

   A captura de tela a seguir mostra a entrada e a saída de gráfico de dispersão.

   ![Gráfico de dispersão em RGUI](media/rclient-setup-scatterplot.png "Gráfico de dispersão dos dados de demonstração de NYC Taxi")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6 – Ferramentas de vinculação para R.exe

Para projetos de desenvolvimento contínuos e sérios, você deve instalar um IDE (ambiente de desenvolvimento integrado). As ferramentas do SQL Server e as ferramentas do R internas não são equipadas para um desenvolvimento de R pesado. Depois de trabalhar com o código, você pode implantá-lo como um procedimento armazenado para execução em SQL Server.

Aponte o IDE para as bibliotecas do R local: R base, RevoScaleR e assim por diante. A execução de cargas de trabalho em um SQL Server remoto ocorre durante a execução do script, quando o script invoca um contexto de computação remota no SQL Server, acessando dados e operações nesse servidor.

### <a name="rstudio"></a>RStudio

Ao usar o [RStudio](https://www.rstudio.com/), você pode configurar o ambiente para usar as bibliotecas e os executáveis do R que correspondem àqueles em um SQL Server remoto.

1. Verifique as versões do pacote do R instaladas no SQL Server. Para obter mais informações, confira [Obter informações sobre o pacote do R](../package-management/r-package-information.md).

1. Instale o Microsoft R Client ou uma das opções de servidor autônomo para adicionar o RevoScaleR e outros pacotes do R, incluindo a distribuição base do R usada por sua instância do SQL Server. Escolha uma versão no mesmo nível ou inferior (pacotes são compatíveis com versões anteriores) que forneça as mesmas versões de pacote que no servidor. Para obter informações sobre a versão, confira o mapa da versão neste artigo: [Atualizar componentes do R e do Python](../install/upgrade-r-and-python.md).

1. No RStudio, [atualize seu caminho do R](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R) para apontar para o ambiente do R que fornece o RevoScaleR, o Microsoft R Open e outros pacotes da Microsoft. 

   + Para uma instalação do R Client, procure C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64
   + Para um servidor autônomo, procure C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library ou C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library

1. Feche e abra o RStudio.

Quando você reabre o RStudio, o executável R do R Client (ou servidor autônomo) é o mecanismo do R padrão.


### <a name="r-tools-for-visual-studio-rtvs"></a>RTVS (Ferramentas do R para Visual Studio)

Se você ainda não tiver um IDE preferencial para R, recomendamos as **Ferramentas do R para Visual Studio**.

+ [Baixar RTVS (Ferramentas do R para Visual Studio)](https://marketplace.visualstudio.com/items?itemName=MikhailArkhipov007.RTVS2019)
+ [Instruções de instalação](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio) – o RTVS está disponível em várias versões do Visual Studio.
+ [Introdução às Ferramentas do R para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>Conectar ao SQL Server usando o RTVS

Este exemplo usa o Visual Studio 2017 Community Edition, com a carga de trabalho de ciência de dados instalada.

1. No menu **Arquivo**, selecione **Novo** e **Projeto**.

2. O painel esquerdo contém uma lista de modelos pré-instalados. Clique em **R** e selecione **R Project**. Na caixa **Nome**, digite `dbtest` e clique em **OK**. 

   O Visual Studio cria uma pasta de projeto e um arquivo de script padrão, `Script.R`. 

3. Digite `.libPaths()` na primeira linha do arquivo de script e pressione CTRL + ENTER.

   O caminho da biblioteca do R atual deve ser exibido na janela **R Interativo**. 

4. Clique no menu **Ferramentas do R** e selecione **Janelas** para ver uma lista de outras janelas específicas do R que você pode exibir em seu workspace.
 
   + Exiba a ajuda nos pacotes na biblioteca atual pressionando CTRL + 3.
   + Veja as variáveis do R no **Gerenciador de Variáveis**, pressionando CTRL + 8.

## <a name="next-steps"></a>Próximas etapas

Dois tutoriais diferentes incluem exercícios para que você possa praticar a comutação do contexto de computação de uma instância do SQL Server local para uma remota.

+ [Tutorial: Usar funções do R do RevoScaleR com os dados do SQL Server](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [Passo a passo de ponta a ponta sobre a ciência de dados](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
