---
title: Instalar pacotes R adicionais no SQL Server | Microsoft Docs
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 530745918dfd4808694b401be55e40bac00f3cce
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="install-additional-r-packages-on-sql-server"></a>Instalar pacotes R adicionais no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como instalar novos pacotes de R em uma instância do SQL Server onde o aprendizado de máquina está habilitado.

**Aplica-se a:** 
+ [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]  [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]
+ [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="prerequisites"></a>Prerequisites

+ Determinar se há uma versão do Windows do pacote: [obter a versão correta do pacote e o formato](#packageVersion)

+ Se o servidor não tiver acesso à internet, você deve baixar os binários do Windows com antecedência: [arquivos zip de Download](#bkmk_zipPreparation)

+ Identificar as dependências do pacote. 

    - Se o servidor tem acesso à internet, você não precisa se preocupar com dependências. todos os pacotes necessários podem ser instalados automaticamente.

    - Se o servidor não **não** tem acesso à internet, você deve identificar todas as dependências e baixar os pacotes necessários com antecedência, em formato compactado. Uma maneira fácil de fazer isso é usar [miniCRAN](create-a-local-package-repository-using-minicran.md) para preparar uma coleção de pacotes com todas as dependências. Esse repositório, em seguida, pode ser copiado para o computador do servidor.

+ Verificar a compatibilidade de pacote. O pacote deve ser compatível com a versão do R que está em execução no SQL Server.

    Além disso, verifique se o pacote (ou todos os pacotes que ele requer) contém recursos que seriam bloqueados pelo SQL Server ou pela política. Por exemplo, determinados pacotes são uma opção de baixo para um ambiente protegido do SQL Server. Esses pacotes podem incluir pacotes que acessam a rede, que usam o Java ou outras estruturas não geralmente usadas em um ambiente do SQL Server, ou pacotes que exigem acesso de sistema de arquivos com privilégios elevados.

+ Permissões

    É necessário o acesso administrativo ao computador que executa o SQL Server.

    Além disso, para executar no SQL Server, os pacotes devem ser instalados na biblioteca padrão que está associada com a instância atual. Para obter instruções sobre como localizar a biblioteca padrão, consulte [pacotes R instalados com o SQL Server](installing-and-managing-r-packages.md).
    
    Se você for um usuário experiente do R, talvez seja acostumado a instalação de pacotes da linha de comando sem permissões especiais ou sem baixá-los antecipadamente. No entanto, esse método não funciona no SQL Server. Em muitos casos do SQL Server computadores não têm uma conexão de internet. Além disso, acesso aos arquivos do servidor ou armazenamento externo pode ser restringido. Pacotes instalados em uma biblioteca de usuário não podem ser acessados por runnign de trabalhos de R no SQL Server. 

    Se você não tem acesso administrativo ao computador do SQL Server, localize um administrador de banco de dados para ajudar com a instalação do pacote.

+ Para cada instância em que você precisa usar o pacote, execute a instalação separadamente.

     Pacotes não podem ser compartilhados entre instâncias. Você pode usar a mesma fonte de arquivo compactado para instalar o pacote ao separar instâncias, mas uma cópia separada do pacote é adicionada à biblioteca de cada instância.

## <a name="install-packages"></a>Instalar pacotes

Esta seção fornece as etapas de instalação do pacote para os seguintes cenários:

+ [Instalar novos pacotes em um servidor com acesso à Internet](#bkmk_rInstall)
+ [Executar uma instalação offline de pacotes em um servidor com **sem** acesso à internet](#bkmk_offlineInstall)
+ [Instalar os pacotes em um contexto de computação do SQL Server usando o RevoScaleR](#bkmk_rAddPackage)
+ [Instalar pacotes usando a instrução Criar biblioteca externa](#bkmk_createlibrary) (2017 somente do SQL Server; outras restrições que se aplicam)

### <a name="bkmk_rInstall"></a>Instalação online usando ferramentas de R

Você pode usar ferramentas padrão de R para instalar novos pacotes em uma instância do SQL Server 2016 ou 2017 do SQL Server. No entanto, você deve ser um administrador para fazer isso.

1.  Navegue até a pasta no servidor em que as bibliotecas de R para a instância estão instaladas.

    > [!IMPORTANT] 
    > Certifique-se de instalar os pacotes para a biblioteca padrão que está associada com a instância atual. Nunca instale pacotes em um diretório de usuário.

    Se você não tiver as permissões necessárias, contate o administrador de banco de dados e fornecer uma lista dos pacotes que você precisa.

2.  Abra um prompt de comando de R como administrador.

    Por exemplo, se você estiver usando o prompt de comando do Windows, navegue até o diretório onde estão localizados RTerm.Exe ou RGui.exe. 

    **Instância padrão**

    SQL Server 2017: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **Instância nomeada**

    SQL Server 2017: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

    Se você tiver usado a associação para atualizar a componentes de aprendizado de máquina, o caminho pode ter alterado. Sempre verifique o caminho da instância antes de instalar novos pacotes. 

3.  Execute o comando de R `install.packages` para instalar o pacote. Por exemplo, a instrução a seguir instala o pacote de e1071 populares. 

    ```R
    install.packages("e1071", lib = lib.SQL)
    ```

    Aspas duplas são necessárias para o nome do pacote.

4. Quando for solicitado para um site de espelhamento, selecione qualquer local que é conveniente para seu local.

5. Se o pacote de destino depender de outros pacotes, o instalador de R automaticamente baixa as dependências e as instala para você.

> [!IMPORTANT]
> Para cada instância em que você precisa usar o pacote, execute a instalação separadamente. Pacotes não podem ser compartilhados entre instâncias.

### <a name = "bkmk_offlineInstall"></a>Instalação offline usando ferramentas de R 

Se o pacote que você pretende instalar tem dependências, preparar **todos os** necessário pacotes antecipadamente.  Consulte o [dicas de instalação](#bkmk_tips) seção para obter ajuda sobre como preparar os pacotes.

> [!IMPORTANT]
>  Sempre que você instala pacotes em um servidor que tem sem acesso à internet, é essencial que você analisar dependências completas com antecedência e certifique-se de que você baixou todos os pacotes necessários **antes de** iniciando a instalação. É recomendável [miniCRAN](https://mran.microsoft.com/package/miniCRAN) para esse processo. Este pacote de R usa uma lista de pacotes que você deseja instalar, analisa as dependências e obtém todos os arquivos compactados para você. miniCRAN, em seguida, cria um único repositório que você pode copiar para o computador do servidor.
> 
> Para obter detalhes, consulte [criar um repositório de pacote local usando miniCRAN](create-a-local-package-repository-using-minicran.md)

1. Copie o pacote ou o repositório em formato compactado para um compartilhamento local ou em outro local que o servidor possa acessar.

2.  Localize a pasta no servidor em que as bibliotecas de R para a instância são instaladas.

    Por exemplo, se você estiver usando o prompt de comando do Windows, navegue até o diretório onde estão localizados RTerm.Exe ou RGui.exe.

    **Instância padrão**

    SQL Server 2017: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **Instância nomeada**

    SQL Server 2017: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

3. Abra um prompt de comando de R como administrador.

4.  Execute o comando de R `install.packages` e especifique o pacote ou o nome do repositório e o local dos arquivos compactados.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Esse comando extrai o pacote R `mynewpackage` de seu arquivo compactado local, supondo que você salvou a cópia no diretório `C:\Temp\Downloaded packages`e instala o pacote no computador local. Se o pacote tiver quaisquer dependências, o instalador verifica se os pacotes existentes na biblioteca. Se você tiver criado um repositório que inclui as dependências, o instalador instala os pacotes de requireed também.

    Se os pacotes necessários não estão presentes na biblioteca de instância e não podem ser encontrados em arquivos compactados, a instalação do pacote de destino falha.

### <a name="bkmk_rAddPackage"></a>Instalar pacotes de R em um servidor de um cliente remoto do R

Em versões recentes do [R Server ou servidor de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server), RevoScaleR inclui funções que oferece suporte à instalação de novos pacotes de R em um contexto de computação do SQL Server. 

1. Antes de começar, certifique-se de que essas condições forem atendidas:

    + O cliente tem RevoScale 9.0.1 ou posterior.
    + Uma versão equivalente da RevoScaleR foi instalada na instância do SQL Server.
    + O [recurso de pacote de gerenciamento](..\r\r-package-how-to-enable-or-disable.md) foi habilitado na instância.
    + Você é um membro de uma função de banco de dados que permite que você instale os pacotes em um compartilhado ou no contexto de prvate, na instância especificada e ddatabase.

2. Em uma linha de comando de R, definir uma cadeia de caracteres de conexão para a instância e banco de dados e usar a cadeia de conexão com o [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) construtor para criar um contexto de computação do SQL Server.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. Crie uma lista dos pacotes que você deseja instalar e salvá-la em uma variável de cadeia de caracteres.

    ```R
    packageList <- c("e1071", "mice")
    ```

4. Chamar [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) e passar o contexto de computação e a variável de cadeia de caracteres que contém os nomes de pacote.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    Se os pacotes dependentes forem necessários, eles também são instalados, supondo que uma conexão de internet está disponível.
    
    Neste exemplo, porque o proprietário e o escopo não foi especificado, os pacotes são instalados usando as credenciais do usuário que faz a conexão, no escopo padrão para esse usuário.

### <a name="bkmk_createlibrary"></a>Usar um repositório de miniCRAN e criar biblioteca externa para instalar pacotes 

SQL Server 2017 fornece novos recursos para instalar e gerenciar os pacotes de R usando o T-SQL. No entanto, esse processo exige que um pacote de estar disponível como um local compactado arquivo, em vez de fazer o download da internet. A instrução falhará se todos os pacotes não são preparados com antecedência.

Criar biblioteca externa é suportada sob estas condições:

+ Você está instalando um único pacote sem dependências
+ Você estiver instalando vários pacotes ou pacotes com dependências e preparar todos os pacotes com antecedência. 

**Etapas**

1.  Preparar o pacote em formato compactado ou criar um repositório de miniCRAN que contém o pacote e suas dependências.  

2. Copie o arquivo compactado ou um repositório para uma pasta local no servidor.

     > [!IMPORTANT]
     > O arquivo que você especificar como a origem deve conter o pacote de destino, bem como os pacotes necessários relacionados.

3. Como administrador, execute a instrução T-SQL `CREATE EXTERNAL LIBRARY` para carregar a coleção de pacote compactado para o banco de dados.

    Por exemplo, a instrução a seguir faz referência a um repositório miniCRAN que contém o pacote de randomForest e suas dependências. 

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Downloads\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

    Você não pode usar um nome arbitrário na instrução CREATE; o nome da biblioteca externa deve ter o mesmo nome que você pretende usar ao carregar ou chamar o pacote.

4. Instale o pacote ou pacotes para uso com o SQL Server, executando código em um procedimento armazenado.
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # install randomForest and its dependencies
    library(randomForest)'
    ```

    Se for bem-sucedido, o **mensagens** janela deve relatar uma mensagem, como "o pacote 'randomForest' descompactado com êxito e somas de MD5 verificada" e "Concluído encadeados execução".

    Se a instalação falhar, falham de todos os pacotes de instalação e as tentativas subsequentes ao instalar o pacote de instalação também podem falhar, com esta mensagem: 

    "Erro no rxSqlPkgInstallPackages... Falha ao instalar pacotes - examine o log para obter detalhes"

## <a name="package-installation-tips-and-frequently-asked-questions-faq"></a>Dicas de instalação do pacote e perguntas frequentes (FAQ)

Esta seção fornece dicas variadas e perguntas comuns relacionadas à instalação do pacote de R no SQL Server.

###  <a name="packageVersion"></a>Obter a versão correta do pacote e o formato

Há várias fontes de pacotes R, os mais conhecidos entre eles são CRAN e Bioconductor. O site oficial da linguagem R (<https://www.r-project.org/>) lista vários desses recursos. Muitos pacotes são publicados no GitHub, onde é possível obter o código-fonte. No entanto, você talvez tenha recebido pacotes R desenvolvidos por alguém de sua empresa.

Independentemente da origem, você deve garantir que o pacote que você deseja instalar tem um formato binário para a plataforma Windows. Caso contrário, o pacote baixado não é possível executar no ambiente do SQL Server.

### <a name="bkmk_zipPreparation"></a>Baixe o pacote como um arquivo compactado

Para instalação em um servidor sem acesso à internet, você deve baixar uma cópia do pacote no formato de um arquivo compactado para instalação offline. Não descompacte o pacote.

Por exemplo, o procedimento a seguir descreve agora para obter a versão correta do [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) pacote da Bioconductor, supondo que o computador tem acesso à internet.

1.  Na lista **Arquivos de Pacote** , localize a versão **Binário do Windows** .

2.  Clique no link para o. Arquivo ZIP e selecione **Salvar destino como**.

3.  Navegue até a pasta local onde os pacotes compactados são armazenados e clique em **salvar**.

    Esse processo cria uma cópia local do pacote. Se você receber um erro de download, tente um site diferente do espelho.

4. Depois que o arquivo de pacote foi baixado, você pode instalar o pacote ou copiar o pacote compactado em um servidor que não tenha acesso à internet.

> [!TIP]
> Se por engano, você instalar o pacote em vez de baixar os binários, uma cópia do arquivo compactado baixado também serão salvos em seu computador. Observe as mensagens de status que o pacote for instalado, para determinar o local do arquivo. Você pode copiar o arquivo compactado para o servidor que não tem acesso à internet.
> Se você baixar o pacote usando esse método, as dependências do pacote não são incluídas. 

Para obter mais informações sobre o conteúdo do formato de arquivo zip e como criar um pacote R, é recomendável neste tutorial, o que pode ser baixado no formato PDF no site do projeto R: [criação de pacotes de R](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf).

### <a name="bkmk_packageDependencies"></a>Obter as dependências do pacote

Pacotes de R com frequência dependem de vários pacotes, alguns dos quais podem não estar disponíveis na biblioteca R padrão usada pela instância. Às vezes, um pacote exige uma versão diferente de um pacote dependente que já está instalado.

Se você precisar instalar vários pacotes, ou para garantir que todas as pessoas em sua organização obtém o tipo correto de pacote e versão, é recomendável que você use o [miniCRAN](https://mran.microsoft.com/package/miniCRAN) pacote para criar um repositório local que pode ser compartilhado entre vários usuários ou computador. Para obter mais informações, consulte [criar um repositório de pacote local usando miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="permissions"></a>Permissões

Esta seção descreve os diferentes níveis de permissões necessárias para instalar pacotes no SQL Server 2016 e 2017 do SQL Server. A instalação pode ser feita usando as ferramentas de R ou SQL Server, mas o processo e as permissões de um pouco diferem.

-   SQL Server 2016

    Nesta versão, somente um administrador no computador pode instalar pacotes para o local desejado. Use ferramentas padrão de R para instalar pacotes, mas você deve executar como administrador e use as ferramentas de R associadas com a instância.

-   SQL Server 2017

    Se você tem acesso administrativo, você pode instalar pacotes em toda a instância usando ferramentas de R.

    Se você for um proprietário de banco de dados, você pode instalar pacotes de R de um cliente remoto, se você definir uma conexão e conectar-se à instância usando RxInSqlServer.
    
    Esta versão inclui novos recursos para dar suporte à administração de pacotes de R ou Python por administradores de banco de dados em versões futuras. Para usar esse recurso, um DBA deve primeiro habilitar os recursos de gerenciamento de pacotes em uma base por instância. Depois que esse recurso está habilitado, os usuários individuais podem instalar pacotes de um banco de dados específico, dependendo da função de banco de dados. Para obter mais informações, consulte [habilitar ou desabilitar o gerenciamento de pacotes de R para o SQL Server](../r/r-package-how-to-enable-or-disable.md).

> [!IMPORTANT]
> 
> Usuários experientes do R estão acostumados a instalação de pacotes em uma biblioteca de usuário e, em seguida, referenciar o pacote na pasta como parte da solução R, especificando um caminho de arquivo. No entanto, essa prática não tem suporte no SQL Server. Para obter mais informações e soluções alternativas, consulte [como usar pacotes nas bibliotecas de usuário](packages-installed-in-user-libraries.md).

### <a name="establish-a-single-mirror-site-as-standard"></a>Estabelecer um site único espelho como padrão

Para evitar ter que selecionar um local de espelhamento sempre que adicionar um novo pacote, configure seu ambiente de desenvolvimento R para usar sempre o mesmo repositório. Para fazer isso, edite o arquivo de configurações global do R, **. Rprofile**e adicione a seguinte linha:

`options(repos=structure(c(CRAN="<mirror site URL>")))`

Espelhos CRAN atuais são listados na [este site](https://cran.r-project.org/mirrors.html).

Para obter informações detalhadas sobre as preferências e outros arquivos carregados quando o tempo de execução de R é iniciado, execute este comando em um console R:`?Startup`

### <a name="know-which-library-you-are-using-for-installation"></a>Saber qual biblioteca que você está usando para instalação

Se você modificou anteriormente o ambiente R no computador, antes de instalar qualquer coisa, pausar um momento e certifique-se de que a variável de ambiente R `.libPath` usa apenas um caminho.

Esse caminho deve apontar para a pasta R_SERVICES para a instância. Para obter mais informações, consulte [pacotes R instalados com o SQL Server](installing-and-managing-r-packages.md).

### <a name="side-by-side-installation-with-r-server"></a>Instalação lado a lado com o servidor de R

Se você tiver instalado o Microsoft Machine Learning Server (autônomo) além de serviços de aprendizado de máquina do SQL Server, o computador deve ter instalações separadas do R para cada um, com as duplicatas de todas as bibliotecas e ferramentas de R.

> [!IMPORTANT]
> 
> Pacotes que estão instalados para a biblioteca R_SERVER são usados apenas pelo Microsoft R Server e não podem ser acessados pelo SQL Server.
> 
> Certifique-se de usar o `R_SERVICES` biblioteca ao instalar os pacotes que você deseja usar no SQL Server.

### <a name="how-to-determine-which-packages-are-already-installed"></a>Como determinar quais pacotes já estão instalados?

 Consulte [pacotes R instalados com o SQL Server](installing-and-managing-r-packages.md)