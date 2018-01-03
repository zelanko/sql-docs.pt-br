---
title: Instalar pacotes R adicionais no SQL Server | Microsoft Docs
ms.date: 11/15/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 996b69b08973805648da329a328e712d5de45660
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="install-additional-r-packages-on-sql-server"></a>Instalar pacotes R adicionais no SQL Server

Este artigo descreve como instalar novos pacotes de R em uma instância do SQL Server onde o aprendizado de máquina está habilitado.

> [!IMPORTANT]
> O processo para adicionar novos pacotes difere dependendo da versão do SQL Server está executando e as ferramentas que você está usando. 

**Aplica-se a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] e  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]
[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="overview-of-package-installation-process"></a>Visão geral do processo de instalação do pacote

1.  Determinar se há uma versão do Windows do pacote: [obter a versão correta do pacote e o formato](#packageVersion)

2.  Se o servidor não tiver acesso à internet, baixe os binários com antecedência: [arquivos zip de Download](#bkmk_zipPreparation)

    Certifique-se de verificar as dependências do pacote e obter todos os pacotes relacionados que podem ser necessárias durante a instalação. Para preparar uma coleção de pacotes e suas dependências, recomendamos a [miniCRAN pacote](#bkmk_packageDependencies).

    Se você obtiver erros de download ou instalação, tente um site diferente do espelho.

3.  Como você instala o pacote depende se o servidor tem acesso à internet e em sua versão do SQL Server. Os processos recomendados são da seguinte maneira:

    **Instalação do pacote para o SQL Server 2016**
    
    1. O cientista de dados fornece os pacotes necessários para um projeto ou equipe. Use [miniCRAN](create-a-local-package-repository-using-minicran.md) para preparar a coleções de pacotes com suas dependências.

    2. O administrador de banco de dados instala os pacotes para a biblioteca de instância usando ferramentas de R.

    **Instalação do pacote para o SQL Server 2017**

    1. O administrador de banco de dados permite o gerenciamento de pacote na instância e adiciona os usuários às novas funções de gerenciamento de pacote.

    2. O cientista de dados fornece os pacotes necessários para um projeto ou equipe. Use [miniCRAN](create-a-local-package-repository-using-minicran.md) para preparar a coleções de pacotes com suas dependências.

    3. O pacote é carregado para a instância do SQL Server, usando a instrução Criar biblioteca externa.
    
    4. Depois que o pacote foi adicionado à instância, qualquer usuário com as permissões apropriadas pode instalar os pacotes no banco de dados onde os scripts de R são executados, chamando o código R a partir `sp_execute_external_script`.
    
    5. Usuários com permissões apropriadas também podem instalar ou localizar os pacotes de um cliente remoto do R, usando a nova função de RevoScaleR para gerenciamento de pacotes.

## <a name="install-new-packages"></a>Instalar novos pacotes

Esta seção fornece procedimentos detalhados para cenários de instalação do pacote de chaves. Escolha o melhor método, dependendo de:

- A versão do SQL Server que você está usando

- Se você é o único proprietário da instância ou está tentando gerenciar pacotes para várias pessoas usando funções de banco de dados.

- Se você estiver instalando um pacote ou vários pacotes com dependências

**Use o gerenciamento de pacotes do SQL Server**

Se sua instância dá suporte a recursos de gerenciamento de pacote, você pode usar o T-SQL ou ferramentas de R convencionais.

-  Pacote de carregamento um R para o SQL Server onde o gerenciamento de pacote e pacote com base em função de acesso está habilitado. Um usuário instala o pacote usando o T-SQL.

    [Instalar pacotes usando criar biblioteca externa](#bkmk_sqlInstall)

- Use um cliente remoto do R para adicionar novos pacotes para um servidor. Requer o SQL Server de 2017. Gerenciamento de pacotes deve ter sido habilitado no servidor. 

    [Usar o R para instalar os pacotes em um servidor quando o pacote de gerenciamento está habilitado](#bkmk_rAddPackage)

- Prepare uma biblioteca de pacote para uso com a biblioteca externa criar que contém vários pacotes junto com suas dependências.

    [Instalar vários pacotes de um repositório miniCRAN](#bkmk_minicran)

**Usar as ferramentas de R convencionais**

Se você estiver usando uma versão anterior do SQL Server R services, siga estas instruções para instalar pacotes usando ferramentas de R convencionais. Opcionalmente, use miniCRAN para preparar uma coleção de pacotes para a instalação.

-  Instale um pacote R para a biblioteca de instância padrão usando as ferramentas de R. Requer acesso administrativo.

    [Instalar os pacotes na biblioteca de instância usando ferramentas de R](#bkmk_rInstall)

- Crie uma coleção compartilhada de pacotes para oferecer suporte a facilitar a instalação de vários pacotes e suas dependências.

    [Criar um repositório de pacotes usando miniCRAN](create-a-local-package-repository-using-minicran.md)

### <a name="bkmk_sqlInstall"></a>Instalar pacotes usando ferramentas do SQL Server

1. Verifique se o recurso de gerenciamento de biblioteca externa no SQL Server 2017 foi habilitado na instância.

    [Como habilitar ou desabilitar o gerenciamento de pacote](r-package-how-to-enable-or-disable.md)

2. Conecte-se ao servidor usando uma conta que tenha permissões para instalar novos pacotes, usando uma das funções de banco de dados com suporte descritas neste tópico: [gerenciamento de pacotes de R para o SQL Server](r-package-management-for-sql-server-r-services.md)

3.  Copie o arquivo compactado que contém o pacote de R que você deseja instalar em uma pasta no computador do servidor, como o **usuários** ou **documentos** pasta. Você não pode adicionar um pacote de uma unidade de rede ou de uma pasta no computador cliente. Se você tiver usado o miniCRAN para criar um repositório de pacotes, copie o repositório de pacotes em sua totalidade para qualquer pasta local no servidor: ou seja, não em uma unidade de rede.

    Se você não tiver acesso a pastas no servidor, você pode passar o conteúdo do pacote em formato binário. Consulte [criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) para obter um exemplo.

4.  O banco de dados em que você deseja usar o pacote, execute o [criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrução.

    Neste exemplo, vamos supor que a sua conta tem permissão para carregar novos pacotes para o servidor e instalá-los para **compartilhado** escopo no banco de dados.

    A instrução a seguir adiciona a versão de lançamento do [zoo](https://cran.r-project.org/web/packages/zoo/index.html) pacote no contexto do banco de dados atual, de um compartilhamento de arquivos local.

    ```SQL
    CREATE EXTERNAL LIBRARY zoo
    FROM (CONTENT = 'C:\Temp\RPackages\zoo_1.8-0.zip')
    WITH (LANGUAGE = 'R');
    ```

    Se você se conectar usando uma conta que seja um proprietário de banco de dados (membro da função dbo), o pacote é disponibilizado em **compartilhado** escopo: ou seja, ele pode ser instalado por qualquer usuário que seja membro do `rpkgs-users` função.

    Se você carregar o pacote usando uma conta que pode acessar somente **privada** escopo, o pacote pode ser instalado apenas por você.

4.  Para instalar o pacote para a biblioteca padrão R usada pela instância, execute o R `library()` comando dentro do procedimento armazenado sp_execute_external_script.

    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # load the binaries in zoo
    library(zoo)'
    ```

    Se for bem-sucedido, o **mensagens** janela deve relatar uma mensagem, como "pacote 'zoo' descompactados com êxito e verificada MD5 somas." Se um pacote exigido já estiver instalado, o processo de instalação, em seguida, anexa e carrega o pacote desejado.

    > [!NOTE]
    > Se um pacote necessário não estiver disponível, será retornado um erro: "não há nenhum pacote chamado \<required_package\>". 
    > 
    > Para evitar erros, recomendamos que você verifique as dependências do pacote com antecedência, ou use miniCRAN para coletar todos os pacotes necessários em um único arquivo compactado antes de executar `CREATE EXTERNAL LIBRARY`.

### <a name="bkmk_rAddPackage"></a>Usar o R para instalar os pacotes em um servidor quando o pacote de gerenciamento está habilitado

Se você já tiver ativado o gerenciamento de pacotes na instância, você pode instalar novos pacotes de R de um cliente remoto do R, usando funções de RevoScaleR para gerenciamento de pacotes.

1. Antes de começar, certifique-se de que essas condições forem atendidas:

    + Use a versão mais recente do cliente do Microsoft R, que inclui atualizações para RevoScale.
    + Gerenciamento de pacotes foi habilitado na instância e do banco de dados.
    + Você tem permissão para uma das funções de gerenciamento de banco de dados.

2. Lista os pacotes que você deseja instalar em uma variável de cadeia de caracteres.

    ```R
    packageList <- c("e1071")
    ```
    
3. Definir uma cadeia de caracteres de conexão para a instância e banco de dados em que o gerenciamento de pacotes está habilitado e usar a cadeia de conexão para criar um contexto de computação do SQL Server.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

4. Chamar `rxInstallPackages` e passar o contexto de computação e a variável de cadeia de caracteres que contém os nomes de pacote.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    Se os pacotes dependentes forem necessários, eles também serão baixados.
    
    Neste exemplo, porque o proprietário do pacote e o escopo não foi especificado, o pacote é instalado usando as credenciais do usuário que faz a conexão e os pacotes são instalados usando o escopo padrão para esse usuário.

### <a name="bkmk_rInstall"></a>Instalar os pacotes na biblioteca de instância usando ferramentas de R

Você pode usar ferramentas de R para instalar novos pacotes no SQL Server 2016 e 2017 do SQL Server. No entanto, você deve ser um administrador para fazer isso.

1.  Se o servidor não tiver acesso à internet, baixe os pacotes antecipadamente.

    É recomendável que você usar um repositório de pacotes para preparar a coleções de pacotes offline. Para obter mais informações, consulte [criar um repositório de pacote local usando miniCRAN](create-a-local-package-repository-using-minicran.md).

2.  Navegue até a pasta no servidor em que as bibliotecas de R para a instância estão instaladas.

    > [!IMPORTANT] 
    > Certifique-se de instalar os pacotes para a biblioteca padrão que está associada com a instância atual. Nunca instale pacotes em um diretório de usuário. Para obter instruções sobre como localizar a biblioteca padrão, consulte [pacotes R instalados com o SQL Server](installing-and-managing-r-packages.md).

    Para cada instância em que você executa um pacote, instale uma cópia separada do pacote. Pacotes não podem ser compartilhados entre instâncias.

4.  Abra um prompt de comando de R como administrador.

    Por exemplo, se você estiver usando o prompt de comando do Windows, navegue até o diretório onde estão localizados os arquivos RTerm.Exe ou RGui.exe. 

    **Instância padrão**

    2017 do SQL Server:`C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016:`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **Instância nomeada**

    2017 do SQL Server:`C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016:`C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

5.  Execute o comando de R `install.packages` para instalar o pacote.

    A sintaxe depende se você está obtendo o pacote da Internet ou de um arquivo compactado local. 

    **Instalar o pacote usando uma conexão de internet**

    Por exemplo, a instrução a seguir instala o pacote de e1071 populares. Aspas duplas são sempre obrigatórias para o nome do pacote.

    ```R
    install.packages("e1071", lib = lib.SQL)
    ```

    Quando for solicitado para um site de espelhamento, selecione qualquer local que é conveniente para seu local.

    Se o pacote de destino depender de outros pacotes, o instalador de R automaticamente baixa as dependências e as instala para você.

    **Instalar pacote manualmente ou em um computador sem acesso à Internet**

    Se o pacote que você pretende instalar tem dependências, obtenha os pacotes necessários antecipadamente e adicione-os à pasta com outro pacote de arquivos compactados. Consulte o [dicas de instalação](#bkmk_tips) seção para obter ajuda sobre como preparar os pacotes.

    No prompt de comando de R, digite o seguinte comando para especificar o caminho e o nome do pacote para instalação:

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Esse comando extrai um único pacote de R de seu arquivo compactado local, supondo que você salvou a cópia no diretório `C:\Temp\Downloaded packages`e instala o pacote (com suas dependências) na biblioteca R no computador local.

### <a name="bkmk_minicran"></a>Instalar vários pacotes de um repositório miniCRAN

O processo geral de como instalar pacotes de um repositório miniCRAN é semelhante à instalação de um pacote de um único arquivo compactado. No entanto, em vez de carregar um pacote individual no formato compactado, o repositório de miniCRAN contém o pacote de destino, bem como os pacotes necessários relacionados.

1.  Prepare o repositório de miniCRAN e, em seguida, copie o arquivo compactado para uma pasta local no servidor.

2.  Se você estiver usando o T-SQL, um administrador executa a instrução T-SQL `CREATE EXTERNAL LIBRARY` para carregar a coleção de pacote compactado para o banco de dados.

    Por exemplo, a instrução a seguir faz referência a um repositório miniCRAN que contém o pacote de randomForest e suas dependências.

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Downloads\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

3. Para instalar os pacotes para uso com o SQL Server, execute o comando a seguir como parte do código R em um procedimento armazenado.
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # install randomForest and its dependencies
    library(randomForest)'
    ```

    Se for bem-sucedido, o **mensagens** janela deve relatar uma mensagem, como "o pacote 'randomForest' descompactado com êxito e somas de MD5 verificada" e "Concluído encadeados execução".

## <a name="package-installation-tips"></a>Dicas de instalação do pacote

Esta seção fornece dicas variadas e código de exemplo relacionadas à instalação do pacote de R no SQL Server. 

###  <a name="packageVersion"></a>Obter a versão correta do pacote e o formato

Há várias fontes de pacotes R, os mais conhecidos entre eles são CRAN e Bioconductor. O site oficial da linguagem R (<https://www.r-project.org/>) lista vários desses recursos. Muitos pacotes são publicados no GitHub, onde é possível obter o código-fonte. No entanto, você talvez tenha recebido pacotes R desenvolvidos por alguém de sua empresa.

Independentemente da origem, você deve garantir que o pacote que você deseja instalar tem um formato binário para a plataforma Windows. Caso contrário, o pacote baixado não é possível executar no ambiente do SQL Server.

Antes de baixar, você também deve verificar se o pacote é compatível com a versão do R que está em execução no SQL Server.

### <a name="bkmk_zipPreparation"></a>Baixe o pacote como um arquivo compactado

Para instalação em um servidor sem acesso à internet, baixe uma cópia do pacote no formato de um arquivo compactado para instalação offline. Não descompacte o pacote.

Por exemplo, o procedimento a seguir descreve agora para obter a versão correta do [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) pacote da Bioconductor, supondo que o computador tem acesso à internet.

1.  Na lista **Arquivos de Pacote** , localize a versão **Binário do Windows** .

2.  Clique no link para o. Arquivo ZIP e selecione **Salvar destino como**.

3.  Navegue até a pasta local onde os pacotes compactados são armazenados e clique em **salvar**.

Esse processo cria uma cópia local do pacote. Em seguida, você pode instalar o pacote ou copiar o pacote compactado em um servidor que não tenha acesso à internet.

Para obter mais informações sobre o conteúdo do formato de arquivo zip e como criar um pacote R, é recomendável neste tutorial, o que pode ser baixado no formato PDF no site do projeto R: [criação de pacotes de R](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf).

### <a name="bkmk_packageDependencies"></a>Obter as dependências do pacote

Pacotes de R com frequência dependem de vários pacotes, alguns dos quais podem não estar disponíveis na biblioteca R padrão usada pela instância. Ou, às vezes, um pacote exige uma versão diferente de um pacote dependente que já está instalado.

Se você precisar instalar vários pacotes, ou para garantir que todas as pessoas em sua organização obtém o tipo correto de pacote e versão, é recomendável que você usar o pacote de miniCRAN para criar um repositório local que pode ser compartilhado entre vários usuários ou computador. Para obter mais informações, consulte [criar um repositório de pacote local usando miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="permissions"></a>Permissões

Se você for um usuário experiente do R, talvez seja acostumado a instalação de pacotes da linha de comando sem permissões especiais ou sem baixá-los antecipadamente. No entanto, a maioria dos servidores não tem uma conexão de internet. Além disso, acesso a compartilhamentos de arquivos ou armazenamento pode ser restrito.

Esta seção descreve os diferentes níveis de permissões necessárias para instalar pacotes no SQL Server 2016 e 2017 do SQl Server. A instalação pode ser feita usando as ferramentas de R ou SQL Server, mas o processo e as permissões de um pouco diferem.

-   SQL Server 2016

    Nesta versão, somente um administrador no computador pode instalar pacotes para o local desejado. Use ferramentas padrão de R para instalar pacotes, mas você deve executar como administrador e use as ferramentas de R associadas com a instância.

-   SQL Server 2017

    Esta versão fornece novos recursos que permitem que um administrador de banco de dados delegue a instalação do pacote para os usuários. O DBA deve habilitar os recursos de gerenciamento de pacotes em uma base por instância. Depois que esse recurso está habilitado, o DBA pode usar funções de banco de dados para fornecer a capacidade para instalar os pacotes conforme necessário, ou para compartilhar pacotes em uma base por banco de dados de usuários individuais.

    Para obter mais informações, consulte [gerenciamento de pacotes de R para o SQL Server](r-package-management-for-sql-server-r-services.md).


> [!IMPORTANT]
> 
> Usuários experientes do R estão acostumados a instalação de pacotes em uma biblioteca de usuário e, em seguida, referenciar o pacote na pasta como parte da solução R, especificando um caminho de arquivo. No entanto, essa prática não tem suporte no SQL Server. Para obter mais informações e soluções alternativas, consulte [como usar pacotes nas bibliotecas de usuário](packages-installed-in-user-libraries.md).

### <a name="comparing-package-management-methods"></a>Comparação de métodos de gerenciamento de pacote

Esta seção compara os métodos de instalação de pacote disponíveis e lista algumas considerações adicionais e dicas para ajudá-lo a determinar uma estratégia de gerenciamento e instalação do pacote apropriado.

#### <a name="using-sql-server-package-management-features"></a>Usando recursos de gerenciamento de pacotes do SQL Server

Se você habilitar o gerenciamento de pacotes, você pode instalar um pacote para um banco de dados específico. Se você precisar usar um pacote em todos os bancos de dados em que o script R está habilitado, você precisa instalá-lo em cada banco de dados.

No entanto, como o SQL Server gerencia as informações sobre o usuário que tem o direito de usar os pacotes, é mais fácil copiar informações sobre usuários e pacotes entre bancos de dados. Também é fácil recriar um conjunto de pacotes de trabalho para um ou vários usuários ao restaurar um banco de dados ou ao mover entre instâncias.

Usando o T-SQL e os recursos de gerenciamento de pacote no SQL Server 2017 é o método preferencial sempre que você tiver vários usuários de banco de dados instalados ou executados pacotes R.

Este recurso está disponível a partir 2017 do SQL Server.

#### <a name="using-r-tools-to-install-packages-for-the-sql-server-instance"></a>Usando ferramentas de R para instalar os pacotes para a instância do SQL Server

Se você usar esse método, os pacotes instalados para a instância estão disponíveis em qualquer banco de dados. No entanto, como os pacotes são instalados diretamente ao sistema de arquivos, eles devem ser gerenciados fora do SQL Server. Pacotes não podem ser copiados ou restaurados. Além disso, o administrador de banco de dados deve aprender a usar as ferramentas de R.

No entanto, essa solução é o mais simples se você for o único proprietário do banco de dados.

#### <a name="managing-multiple-packages-and-multiple-versions-of-the-same-package"></a>Gerenciamento de vários pacotes e várias versões do mesmo pacote

Se você precisar executar uma instalação offline de pacotes de R, configurando um repositório local usando [miniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/) permite compartilhar pacotes e gerenciar as versões disponíveis para uso pela organização.

#### <a name="establish-a-single-mirror-site-as-standard"></a>Estabelecer um site único espelho como padrão

Para evitar ter que selecionar um local de espelhamento sempre que adicionar um novo pacote, configure seu ambiente de desenvolvimento R para usar sempre o mesmo repositório. Para fazer isso, edite o arquivo de configurações global do R, **. Rprofile**e adicione a seguinte linha:

`options(repos=structure(c(CRAN="<mirror site URL>")))`

Espelhos CRAN atuais são listados na [este site](https://cran.r-project.org/mirrors.html).

Para obter informações detalhadas sobre as preferências e outros arquivos carregados quando o tempo de execução de R é iniciado, execute este comando em um console R:`?Startup`

#### <a name="know-which-library-you-are-using-for-installation"></a>Saber qual biblioteca que você está usando para instalação

Se você modificou anteriormente o ambiente R no computador, antes de instalar qualquer coisa, pausar um momento e certifique-se de que a variável de ambiente R `.libPath` usa apenas um caminho.

Esse caminho deve apontar para a pasta R_SERVICES para a instância. Para obter mais informações, consulte [pacotes R instalados com o SQL Server](installing-and-managing-r-packages.md).

#### <a name="side-by-side-installation-with-r-server"></a>Instalação lado a lado com o servidor de R

Se você tiver instalado o Microsoft Machine Learning Server (autônomo) além de serviços de aprendizado de máquina do SQL Server, o computador deve ter instalações separadas do R para cada, com as duplicatas de todas as bibliotecas e ferramentas de R.

> [!IMPORTANT]
> 
> Pacotes que estão instalados para a biblioteca R_SERVER são usados apenas pelo Microsoft R Server e não podem ser acessados pelo SQL Server.
> 
> Certifique-se de usar o `R_SERVICES` biblioteca ao instalar os pacotes que você deseja usar no SQL Server.
