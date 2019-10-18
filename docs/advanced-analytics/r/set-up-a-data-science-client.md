---
title: Configurar um cliente de ciência de dados para desenvolvimento em R
description: Instale bibliotecas e ferramentas locais do R em uma estação de trabalho de desenvolvimento para conexões remotas a SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7c81a69181d1bc723e622bac9ffeb5ff67fd0280
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "69633631"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>Configurar um cliente de ciência de dados para o desenvolvimento de R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A integração do r está disponível no SQL Server 2016 ou posterior quando você inclui a opção de linguagem R em uma instalação [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) ou [SQL Server serviços de Machine Learning (no banco de dados)](../install/sql-machine-learning-services-windows-install.md) . 

Para desenvolver e implantar soluções de R para SQL Server, instale [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) em sua estação de trabalho de desenvolvimento para obter [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) e outras bibliotecas de R. A biblioteca RevoScaleR, que também é necessária na instância de SQL Server remota, coordena as solicitações de computação entre ambos os sistemas. 

Neste artigo, saiba como configurar uma estação de trabalho de desenvolvimento de cliente R para que você possa interagir com um SQL Server remoto habilitado para aprendizado de máquina e integração de R. Depois de concluir as etapas neste artigo, você terá as mesmas bibliotecas de R que aquelas em SQL Server. Você também saberá como enviar por push cálculos de uma sessão de R local para uma sessão de R remota em SQL Server.

![Componentes cliente-servidor](media/sqlmls-r-client-revo.png "Bibliotecas e sessões de R locais e remotas")

Para validar a instalação, você pode usar a ferramenta interna **RGUI** , conforme descrito neste artigo, ou [vincular as bibliotecas](#install-ide) ao RStudio ou a qualquer outro IDE que você normalmente usa.

> [!Note]
> Uma alternativa para a instalação da biblioteca de cliente é usar um [servidor autônomo](../install/sql-machine-learning-standalone-windows-install.md) como um cliente avançado, que alguns clientes preferem para um cenário mais profundo de trabalho. Um servidor autônomo é totalmente dissociado de SQL Server, mas como ele tem as mesmas bibliotecas de R, você pode usá-lo como um cliente para SQL Server análise no banco de dados. Você também pode usá-lo para trabalho não relacionado ao SQL, incluindo a capacidade de importar e modelar dados de outras plataformas de dados. Se você instalar um servidor autônomo, poderá encontrar o executável do R neste local: `C:\Program Files\Microsoft SQL Server\140\R_SERVER`. Para validar a instalação, [abra um aplicativo de console do r](#R-tools) para executar comandos usando o R. exe nesse local.

## <a name="commonly-used-tools"></a>Ferramentas usadas com frequência

Seja você um desenvolvedor de R novo no SQL ou um desenvolvedor de SQL novo para R e análise no banco de dados, precisará de uma ferramenta de desenvolvimento R e de um editor de consultas T-SQL como o [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) para exercitar todos os recursos do no banco de dados Analytics.

Para cenários de desenvolvimento simples de R, você pode usar o executável RGUI, agrupado na distribuição de R base em MRO e SQL Server. Este artigo explica como usar o RGUI para sessões de R locais e remotas. Para aumentar a produtividade, você deve usar um IDE completo, como o [RStudio ou o Visual Studio](#install-ide).

O SSMS é um download separado, útil para criar e executar procedimentos armazenados em SQL Server, incluindo aqueles que contêm o código R. Quase todos os códigos do R que você escreve em um ambiente de desenvolvimento podem ser inseridos em um procedimento armazenado. Você pode percorrer outros tutoriais para saber mais sobre o [SSMS e o R incorporado](../tutorials/sqldev-in-database-r-for-sql-developers.md).

## <a name="1---install-r-packages"></a>1-instalar pacotes do R

Os pacotes R da Microsoft estão disponíveis em vários produtos e serviços. Em uma estação de trabalho local, é recomendável instalar Microsoft R Client. O r Client fornece [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler), [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), [SQLRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)e outros pacotes de R.

1. [Baixar Microsoft R Client](https://aka.ms/rclient/download).

2. No assistente de instalação, aceite ou altere o caminho de instalação padrão, aceite ou altere a lista de componentes e aceite o Microsoft R Client termos de licença.

  Quando a instalação é concluída, uma tela de boas-vindas apresenta o produto e a documentação.

3. Crie uma variável de ambiente do sistema MKL_CBWR para garantir uma saída consistente em cálculos da Intel Math Kernel Library (MKL).

  + No painel de controle, clique em **sistema e segurança**  > **sistema**  > **Configurações avançadas do sistema**  > **variáveis de ambiente**.
  + Crie uma nova variável de sistema chamada **MKL_CBWR**, com um valor definido como **auto**.

## <a name="2---locate-executables"></a>2-localizar executáveis

Localize e liste o conteúdo da pasta de instalação para confirmar se o R. exe, o RGUI e outros pacotes estão instalados. 

1. No explorador de arquivos, abra a pasta C:\Program Files\Microsoft\R Client\R_SERVER\bin para confirmar o local do R. exe.

2. Abra a subpasta x64 para confirmar **RGUI**. Você usará essa ferramenta na próxima etapa.

3. Abra C:\Program Files\Microsoft\R Client\R_SERVER\library para examinar a lista de pacotes instalados com o R Client, incluindo RevoScaleR, MicrosoftML e outros.


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3-iniciar RGUI

Ao instalar o R com o SQL Server, você obtém as mesmas ferramentas de R que são padrão para qualquer instalação básica do R, como RGui, Rterm e assim por diante. Essas ferramentas são leves, úteis para a verificação de informações de pacote e biblioteca, execução de comandos ou scripts ad hoc ou depuração por meio de tutoriais. Você pode usar essas ferramentas para obter informações de versão do R e confirmar a conectividade.

1. Abra C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 e clique duas vezes em **RGui** para iniciar uma sessão do r com um prompt de comando do r.

  Quando você inicia uma sessão do R de uma pasta do programa da Microsoft, vários pacotes, incluindo RevoScaleR, são carregados automaticamente. 

2. Insira `print(Revo.version)` no prompt de comando para retornar informações de versão do pacote RevoScaleR. Você deve ter a versão 9.2.1 ou 9.3.0 para RevoScaleR.

3. Digite **Search ()** no prompt do R para obter uma lista de pacotes instalados.

   ![Informações de versão ao carregar R](../install/media/rclient-rgui-r-prompt.png "Abrir um prompt do R")


## <a name="4---get-sql-permissions"></a>4-obter permissões do SQL

No R Client, o processamento de R é limitado em dois threads e em dados na memória. Para o processamento escalonável usando vários núcleos e grandes conjuntos de dados, você pode alterar a execução (conhecida como *contexto de computação*) para os conjuntos de dados e poder computacional de uma instância de SQL Server remota. Essa é a abordagem recomendada para a integração do cliente com uma instância de SQL Server de produção, e você precisará de permissões e informações de conexão para fazê-lo funcionar.

Para se conectar a uma instância do SQL Server para executar scripts e carregar dados, você deve ter um logon válido no servidor de banco de dados. Você pode usar um logon do SQL ou uma autenticação integrada do Windows. Geralmente, é recomendável usar a autenticação integrada do Windows, mas usar o logon do SQL é mais simples para alguns cenários, especialmente quando o script contém cadeias de conexão para dados externos.

No mínimo, a conta usada para executar o código deve ter permissão para ler os bancos de dados com os quais você está trabalhando, além da permissão especial executar qualquer SCRIPT externo. A maioria dos desenvolvedores também exige permissões para criar procedimentos armazenados e para gravar dados em tabelas que contêm dados de treinamento ou dados pontuados. 

Peça ao administrador do banco de dados para [configurar as seguintes permissões para sua conta](../security/user-permission.md), no banco de dados em que você usa o R:

+ **Execute qualquer script externo** para executar o script R no servidor.
+ privilégios **db_datareader** para executar as consultas usadas para treinar o modelo.
+ **db_datawriter** para escrever dados de treinamento ou dados pontuados.
+ **db_owner** para criar objetos, como procedimentos armazenados, tabelas, funções. 
  Você também precisa do **db_owner** para criar bancos de dados de exemplo e de teste. 

Se o seu código exigir pacotes que não estão instalados por padrão com SQL Server, organize com o administrador de banco de dados para que os pacotes sejam instalados com a instância do. SQL Server é um ambiente seguro e há restrições sobre onde os pacotes podem ser instalados. Para obter mais informações, consulte [instalar novos pacotes R no SQL Server](install-additional-r-packages-on-sql-server.md).

## <a name="5---test-connections"></a>5-testar conexões

 Como uma etapa de verificação, use **RGUI** e RevoScaleR para confirmar a conectividade com o servidor remoto. SQL Server deve ser habilitado para [conexões remotas](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server) e você deve ter permissões, incluindo um logon de usuário e um banco de dados para se conectar. 

As etapas a seguir pressupõem o banco de dados de demonstração, o [NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md)e a autenticação do Windows.

1. Abra **RGUI** na estação de trabalho cliente. Por exemplo, acesse `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` e clique duas vezes em **RGui. exe** para iniciá-lo.

2. RevoScaleR carrega automaticamente. Confirme se o RevoScaleR está funcionando executando este comando: `print(Revo.version)`

3. Insira o script de demonstração que é executado no servidor remoto. Você deve modificar o script de exemplo a seguir para incluir um nome válido para uma instância de SQL Server remota. Essa sessão começa como uma sessão local, mas a função **rxSummary** é executada na instância de SQL Server remota.

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

  **Da**

  Esse script se conecta a um banco de dados no servidor remoto, fornece uma consulta, cria um contexto de computação `cc` instrução para a execução remota de código e, em seguida, fornece a função RevoScaleR **rxSummary** para retornar um resumo estatístico dos resultados da consulta.

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

4. Obter e definir o contexto de computação. Depois que você definir um contexto de computação, ele permanecerá em vigor durante a sessão. Se você não tiver certeza se a computação é local ou remota, execute o comando a seguir para descobrir. Os resultados que especificam uma cadeia de conexão indicam um contexto de computação remota.

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

5. Retornar informações sobre variáveis na fonte de dados, incluindo nome e tipo.

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

  A captura de tela a seguir mostra a saída de gráfico de entrada e dispersão.

   ![Gráfico de dispersão em RGUI](media/rclient-setup-scatterplot.png "Gráfico de dispersão em dados de demonstração de táxi de NYC")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6-ferramentas de link para R. exe

Para projetos de desenvolvimento contínuos e sérios, você deve instalar um IDE (ambiente de desenvolvimento integrado). As ferramentas de SQL Server e as ferramentas de R internas não são equipadas para um desenvolvimento de R pesado. Depois de trabalhar com código, você pode implantá-lo como um procedimento armazenado para execução em SQL Server.

Aponte o IDE para as bibliotecas do R local: R base, RevoScaleR e assim por diante. A execução de cargas de trabalho em um SQL Server remoto ocorre durante a execução do script, quando o script invoca um contexto de computação remota no SQL Server, acessando dados e operações nesse servidor.

### <a name="rstudio"></a>RStudio

Ao usar o [RStudio](https://www.rstudio.com/), você pode configurar o ambiente para usar as bibliotecas e os executáveis do R que correspondem àqueles em um SQL Server remoto.

1. Verifique as versões do pacote R instaladas em SQL Server. Para obter mais informações, consulte [obter informações de pacote do R](../package-management/r-package-information.md).

1. Instale Microsoft R Client ou uma das opções de servidor autônomo para adicionar RevoScaleR e outros pacotes de R, incluindo a distribuição de R base usada por sua instância de SQL Server. Escolha uma versão no mesmo nível ou inferior (pacotes são compatíveis com versões anteriores) que fornecem as mesmas versões de pacote que no servidor. Para obter informações sobre a versão, consulte o mapa de versão neste artigo: [atualizar os componentes R e Python](../install/upgrade-r-and-python.md).

1. No RStudio, [atualize seu caminho r](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R) para apontar para o ambiente de r que fornece RevoScaleR, Microsoft R Open e outros pacotes da Microsoft. 

  + Para uma instalação de cliente R, procure C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64
  + Para um servidor autônomo, procure C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library ou C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library

2. Feche e abra RStudio.

Quando você reabre o RStudio, o executável do R do cliente R (ou servidor autônomo) é o mecanismo R padrão.


### <a name="r-tools-for-visual-studio-rtvs"></a>Ferramentas do R para Visual Studio (RTVS)

Se você ainda não tiver um IDE preferencial para R, recomendamos **Ferramentas do R para Visual Studio**.

+ [Baixar Ferramentas do R para Visual Studio (RTVS)](https://visualstudio.microsoft.com/vs/features/rtvs/)
+ [Instruções de instalação](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio) – o RTVS está disponível em várias versões do Visual Studio.
+ [Introdução ao Ferramentas do R para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>Conectar-se a SQL Server do RTVS

Este exemplo usa o Visual Studio 2017 Community Edition, com a carga de trabalho de ciência de dados instalada.

1. No menu **arquivo** , selecione **novo** e **projeto**.

2. O painel esquerdo contém uma lista de modelos pré-instalados. Clique em **r**e selecione **projeto r**. Na caixa **nome** , digite `dbtest` e clique em **OK**. 

  O Visual Studio cria uma nova pasta de projeto e um arquivo de script padrão, `Script.R`. 

3. Digite `.libPaths()` na primeira linha do arquivo de script e pressione CTRL + ENTER.

  O caminho da biblioteca do R atual deve ser exibido na janela de **R interativo** . 

4. Clique no menu **ferramentas de R** e selecione **Windows** para ver uma lista de outras janelas específicas do r que você pode exibir em seu espaço de trabalho.
 
  + Exiba a ajuda nos pacotes na biblioteca atual pressionando CTRL + 3.
  + Consulte variáveis de R na **Gerenciador de variáveis**, pressionando CTRL + 8.

## <a name="next-steps"></a>Próximas etapas

Dois tutoriais diferentes incluem exercícios para que você possa praticar a alternância do contexto de computação de local para uma instância de SQL Server remota.

+ [Tutorial: usar as funções do R RevoScaleR com dados de SQL Server](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [Instruções de ponta a ponta sobre a ciência de dados](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)