---
title: Configurar um cliente de ciência de dados para o desenvolvimento de R – serviços do SQL Server Machine Learning
description: Instale ferramentas e bibliotecas do R locais em uma estação de trabalho de desenvolvimento para conexões remotas ao SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5630bd485936a07c3fb8cf64de483fdb93ead3af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962450"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>Configurar um cliente de ciência de dados para o desenvolvimento de R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Integração do R está disponível no SQL Server 2016 ou posterior ao incluir a opção de linguagem R em um [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) ou [serviços SQL Server 2017 Machine Learning (no banco de dados)](../install/sql-machine-learning-services-windows-install.md) instalação. 

Para desenvolver e implantar soluções de R para SQL Server, instale [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) em sua estação de trabalho de desenvolvimento para obter [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) e outras bibliotecas de R. A biblioteca RevoScaleR, que também é necessário na instância remota do SQL Server, coordena solicitações de computação entre os dois sistemas. 

Neste artigo, saiba como configurar uma estação de trabalho de desenvolvimento de cliente do R para que você pode interagir com um SQL Server remoto habilitado para o aprendizado de máquina e integração do R. Depois de concluir as etapas neste artigo, você terá as mesmas bibliotecas de R, como aqueles no SQL Server. Você também saberá como enviar por push os cálculos de uma sessão de R local a uma sessão remota do R no SQL Server.

![Componentes de cliente-servidor](media/sqlmls-r-client-revo.png "sessões de R Local e remotas e bibliotecas")

Para validar a instalação, é possível usar interno **RGUI** ferramenta conforme descrito neste artigo, ou [vincular as bibliotecas](#install-ide) RStudio ou qualquer outro IDE que você normalmente usa.

> [!Note]
> Uma alternativa para a instalação da biblioteca de cliente está usando um [servidor autônomo](../install/sql-machine-learning-standalone-windows-install.md) como um cliente avançado, que alguns clientes preferem para o trabalho mais profundo do cenário. Um servidor autônomo é totalmente separado do SQL Server, mas porque ele tem as mesmas bibliotecas de R, você pode usá-lo como um cliente para análise do SQL Server no banco de dados. Você também pode usá-lo para o trabalho não relacionados ao SQL, incluindo a capacidade de importar e modelar dados de outras plataformas de dados. Se você instalar um servidor autônomo, você pode encontrar o executável do R neste local: `C:\Program Files\Microsoft SQL Server\140\R_SERVER`. Para validar sua instalação [abrir um aplicativo de console do R](#R-tools) para executar comandos que usam o R.exe nesse local.

## <a name="commonly-used-tools"></a>Ferramentas usadas comumente

Se você for um desenvolvedor de R novidade no SQL ou um desenvolvedor SQL novo para o R e análise no banco de dados, será necessário uma ferramenta de desenvolvimento de R e um editor de consultas T-SQL, como [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) para exercer todos os recursos de análise no banco de dados.

Para cenários de desenvolvimento de R simples, você pode usar o RGUI executável, agrupado na distribuição de R base no MRO e o SQL Server. Este artigo explica como usar o RGUI para sessões de R locais e remotas. Para melhorar a produtividade, você deve usar um IDE completo, como [RStudio ou no Visual Studio](#install-ide).

O SSMS é um download separado, útil para criar e executar procedimentos armazenados no SQL Server, incluindo aqueles que contém o código R. Praticamente qualquer código de R que você escreve em um ambiente de desenvolvimento pode ser inserido em um procedimento armazenado. Você pode percorrer os outros tutoriais para saber mais sobre [SSMS e R incorporado](../tutorials/sqldev-in-database-r-for-sql-developers.md).

## <a name="1---install-r-packages"></a>1 – instalar pacotes R

Pacotes de R da Microsoft estão disponíveis em vários produtos e serviços. Em uma estação de trabalho local, é recomendável instalar o Microsoft R Client. Fornece o R Client [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler), [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), [SQLRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)e outros pacotes de R.

1. [Baixe o Microsoft R Client](https://aka.ms/rclient/download).

2. No Assistente de instalação, aceite ou altere o caminho de instalação padrão, aceite ou altere a lista de componentes e aceitar os termos de licença do Microsoft R Client.

  Quando a instalação for concluída, uma tela de boas-vindas apresenta o produto e a documentação.

3. Crie uma variável de ambiente do sistema MKL_CBWR para garantir que a saída consistente em cálculos da Intel MKL Math Kernel Library ().

  + No painel de controle, clique em **sistema e segurança** > **sistema** > **configurações avançadas do sistema**  >   **Variáveis de ambiente**.
  + Criar uma nova variável de sistema nomeada **MKL_CBWR**, com um valor definido como **automática**.

## <a name="2---locate-executables"></a>2 – localizar executáveis

Localizar e listar o conteúdo da pasta de instalação para confirmar que R.exe, RGUI e outros pacotes são instalados. 

1. No Explorador de arquivos, abra a pasta C:\Program Files\Microsoft\R Client\R_SERVER\bin para confirmar o local do R.exe.

2. Abrir x64 subpasta para confirmar **RGUI**. Você usará essa ferramenta na próxima etapa.

3. Abra C:\Program Files\Microsoft\R Client\R_SERVER\library para examinar a lista de pacotes instalados com o cliente do R, incluindo RevoScaleR, MicrosoftML e outros.


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3 - início RGUI

Quando você instala o R com o SQL Server, você pode obter as mesmas ferramentas de R que são padrão para qualquer instalação básica do R, como RGui, Rterm e assim por diante. Essas ferramentas são leves e útil para verificando informações de pacote e biblioteca, executando comandos ad hoc ou script ou percorrer os tutoriais. Você pode usar essas ferramentas para obter informações de versão do R e confirme a conectividade.

1. Abra C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 e clique duas vezes em **RGui** para iniciar uma sessão de R com um prompt de comando do R.

  Quando você inicia uma sessão de R de uma pasta de programa da Microsoft, vários pacotes, incluindo RevoScaleR, carregar automaticamente. 

2. Insira `print(Revo.version)` no prompt de comando para retornar o RevoScaleR informações de versão do pacote. Você deve ter a versão 9.2.1 ou 9.3.0 para RevoScaleR.

3. Insira **Search ()** no prompt de R para obter uma lista de pacotes instalados.

   ![Informações de versão durante o carregamento R](../install/media/rclient-rgui-r-prompt.png "abra um prompt de R")


## <a name="4---get-sql-permissions"></a>4 – obter permissões do SQL

No cliente do R, o processamento de R é limitado a dois threads e os dados na memória. Para o processamento escalonável usando vários núcleos e grandes conjuntos de dados, você pode alternar a execução (conhecido como *contexto de computação*) para os conjuntos de dados e a potência computacional de uma instância remota do SQL Server. Essa é a abordagem recomendada para a integração de cliente com uma instância do SQL Server de produção, e você precisará de permissões e informações de conexão para fazê-lo funcionar.

Para se conectar a uma instância do SQL Server para executar scripts e carregar dados, você deve ter um logon válido no servidor de banco de dados. Você pode usar um logon SQL ou a autenticação integrada do Windows. Em geral, é recomendável que você usa a autenticação integrada do Windows, mas usando o logon do SQL é mais simples para alguns cenários, especialmente quando o script contém cadeias de caracteres de conexão para dados externos.

No mínimo, a conta usada para executar o código deve ter permissão para ler os bancos de dados você está trabalhando, além de permissão especial executar qualquer SCRIPT externo. A maioria dos desenvolvedores também exigem permissões para criar procedimentos armazenados e para gravar dados em tabelas que contêm dados de treinamento ou pontuação de dados. 

Peça ao administrador de banco de dados para [configure as seguintes permissões para sua conta](../security/user-permission.md), no banco de dados em que você usar o r:

+ **EXECUTE ANY EXTERNAL SCRIPT** para executar o script do R no servidor.
+ **db_datareader** privilégios para executar as consultas usadas para treinar o modelo.
+ **db_datawriter** para gravar dados de treinamento ou dados de pontuação.
+ **db_owner** para criar objetos, como procedimentos armazenados, tabelas, funções. 
  Você também precisa **db_owner** criar bancos de dados de exemplo e teste. 

Se seu código exigir pacotes que não são instalados por padrão com o SQL Server, organize-se com o administrador de banco de dados para ter os pacotes instalados com a instância. SQL Server é um ambiente seguro e há restrições sobre onde os pacotes podem ser instalados. Para obter mais informações, consulte [instalar novos pacotes de R no SQL Server](install-additional-r-packages-on-sql-server.md).

## <a name="5---test-connections"></a>5 - testar conexões

 Como uma etapa de verificação, use **RGUI** e RevoScaleR para confirmar a conectividade ao servidor remoto. SQL Server deve estar habilitado para [conexões remotas](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server) e você deve ter permissões, incluindo um logon de usuário e se conectar a um banco de dados. 

As etapas a seguir pressupõem o banco de dados de demonstração [NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md)e a autenticação do Windows.

1. Abra **RGUI** na estação de trabalho cliente. Por exemplo, acesse `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` e clique duas vezes **RGui.exe** para iniciá-lo.

2. RevoScaleR carrega automaticamente. Confirme que revoscaler está funcionando executando este comando: `print(Revo.version)`

3. Insira o script de demonstração que é executado no servidor remoto. Você deve modificar o script de exemplo a seguir para incluir um nome válido para uma instância remota do SQL Server. Esta sessão começa como uma sessão local, mas o **rxSummary** função é executada na instância remota do SQL Server.

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

  Esse script se conecta a um banco de dados no servidor remoto, fornece uma consulta, cria um contexto de computação `cc` instrução para execução remota de código, em seguida, fornece a função RevoScaleR **rxSummary** para retornar uma estatística Resumo dos resultados da consulta.

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

4. Obter e definir o contexto de computação. Depois de definir um contexto de computação, ele permanecerá em vigor para a duração da sessão. Se você não tiver certeza se a computação é local ou remoto, execute o comando a seguir para descobrir. Os resultados que especificam uma cadeia de caracteres de conexão indicam um contexto de computação remota.

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

5. Retorne informações sobre as variáveis na fonte de dados, incluindo o nome e tipo.

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

  Captura de tela a seguir mostra a saída de plotagem de dispersão e de entrada.

   ![Gráfico de dispersão em RGUI](media/rclient-setup-scatterplot.png "gráfico de dispersão nos dados de demonstração de táxi de NYC")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6 - ferramentas de link para R.exe

Para projetos de desenvolvimento sério e sustentado, você deve instalar um ambiente de desenvolvimento integrado (IDE). Ferramentas do SQL Server e as ferramentas do R internos não estão preparadas para o desenvolvimento de R pesado. Uma vez que o código de trabalho, você pode implantá-lo como um procedimento armazenado para execução no SQL Server.

Aponte seu IDE para as bibliotecas do R locais: base R, RevoScaleR e assim por diante. Executar cargas de trabalho em um servidor SQL remoto ocorre durante a execução do script, quando seu script invoca um contexto de computação remota no SQL Server, acesso a dados e operações nesse servidor.

### <a name="rstudio"></a>RStudio

Ao usar [RStudio](https://www.rstudio.com/), você pode configurar o ambiente para usar as bibliotecas do R e executáveis que correspondem às em um servidor SQL remoto.

1. Verifique as versões do pacote de R instaladas no SQL Server. Para obter mais informações, consulte [informações do pacote de R Obtenha](../package-management/installed-package-information.md).

1. Instale o Microsoft R Client ou uma das opções de servidor autônomo para adicionar o RevoScaleR e outros pacotes de R, incluindo a distribuição de R base usada pela instância do SQL Server. Escolha uma versão ao mesmo nível ou abaixo (pacotes são compatíveis com versões anteriores) que fornece as mesmas versões de pacote que no servidor. Para obter informações de versão, consulte a versão mapear neste artigo: [Atualizar os componentes de R e Python](../install/upgrade-r-and-python.md).

1. No RStudio, [atualize o caminho de R](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R) para apontar para o ambiente de R fornecendo RevoScaleR, Microsoft R Open e outros pacotes da Microsoft. 

  + Para uma instalação de cliente do R, procure C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64
  + Para um servidor autônomo, procure C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library ou C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library

2. Feche e, em seguida, abra o RStudio.

Quando você reabrir o RStudio, o executável do cliente do R (ou servidor autônomo) do R é o mecanismo padrão R.


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

## <a name="next-steps"></a>Próximas etapas

Dois tutoriais diferentes incluem exercícios, de modo que você pode praticar alternar o contexto de computação do local para uma instância remota do SQL Server.

+ [Tutorial: Usar funções RevoScaleR R com dados do SQL Server](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [Passo a passo de ponta a ponta sobre a ciência de dados](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)