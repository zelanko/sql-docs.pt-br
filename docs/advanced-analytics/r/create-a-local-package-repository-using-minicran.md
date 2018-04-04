---
title: Criar um repositório de pacote local usando miniCRAN | Microsoft Docs
titleSuffix: SQL Server
ms.custom: ''
ms.date: 02/20/2018
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
ms.workload: Inactive
ms.openlocfilehash: 6dfaa01607bb25e1afe41301e655025a8d2b059f
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2018
---
# <a name="create-a-local-package-repository-using-minicran"></a>Criar um repositório de pacote local usando miniCRAN
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) pacote foi criado pelo Andre de Vries para dar suporte a esses cenários comuns: 

+ Analisando dependências do pacote para um único pacote ou conjunto de pacotes
+ Preparando um conjunto de pacotes de R para instalação em um servidor sem acesso à internet.

O usuário Especifica um conjunto de pacotes desejados e miniCRAN recursivamente lê a árvore de dependência para esses pacotes e baixa apenas os pacotes listados e suas dependências de CRAN ou repositórios semelhantes.

Como uma saída, miniCRAN cria um repositório consistente internamente consiste os pacotes selecionados e todas as dependências necessárias. Você pode, em seguida, mova este repositório local para o servidor e continuar a instalar os pacotes sem usar a internet.

Usuários experientes do R geralmente procuram a lista de pacotes dependentes no arquivo de descrição para o pacote baixado. No entanto, os pacotes listados na **Imports** podem ter dependências de segundo nível. Por esse motivo, é recomendável o uso do **miniCRAN** método.

## <a name="what-is-a-package-repository"></a>O que é um repositório de pacotes

O objetivo de criar um repositório de pacote local é fornecer um único local em que um administrador de servidor ou de outros usuários na organização podem usar para instalar novos pacotes de R em um servidor que não tem acesso à internet. Depois de criar o repositório, você pode modificá-lo adicionando novos pacotes ou atualizar a versão de pacotes existentes.

O [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) do pacote de R foi escrito por [Andre de Vries](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html) para tornar mais fácil criar consistente, gerenciado por conjunto de pacotes de R para uma organização. 

Repositórios de pacote são úteis nestes cenários:

- **Segurança**: os usuários de R muitos estão acostumados a baixar e instalar novos pacotes de R à vontade, da CRAN ou um de seus sites de espelho. No entanto, por motivos de segurança, os servidores de produção executando [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] normalmente não tem conectividade com a internet.

- **Fácil instalação offline**: para instalar o pacote a um servidor offline requer que você também baixar todas as dependências do pacote, usando miniCRAN torna mais fácil de obter todas as dependências no formato correto.

    Usando miniCRAN, você pode evitar erros de dependência de pacote ao preparar pacotes para instalar com o [criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrução.

- **Melhor gerenciamento de versão**: em um ambiente multiusuário, há boas razões para evitar irrestrita instalação de várias versões de pacote no servidor. Use um repositório local para fornecer um conjunto consistente de pacotes para uso por seus analistas. 

> [!TIP]
> Você também pode usar miniCRAN preparar pacotes para uso no aprendizado de máquina do Azure. Para obter mais informações, consulte este blog: [usando miniCRAN no Azure ML, por Michele Usuelli](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="prepare-packages-using-minicran"></a>Preparar pacotes usando miniCRAN

O **miniCRAN** pacote propriamente dito é dependente de 18 de outros pacotes CRAN, entre o que é o **RCurl** pacote, que tem uma dependência de sistema no **devel ondulação** pacote. Da mesma forma, o pacote **XML** tem uma dependência em **libxml2 devel**. 

Por esses motivos, recomendamos que você crie seu repositório local inicialmente em um computador com acesso total à Internet, para que você pode facilmente atender a todas essas dependências. 

Depois que o repositório tiver sido criado, você pode mover o repositório para um local diferente.

### <a name="step-1-install-the-minicran-package"></a>Etapa 1. Instalar o pacote de miniCRAN

Comece criando uma **miniCRAN** repositório para usar como uma fonte. Você deve criar esse repositório em um computador que tenha acesso à internet.

1. Instalar o **miniCRAN** necessários e pacote **igraph** pacote. Este exemplo verifica se o pacote já está instalado, mas você pode ignorar o se instruções e instale os pacotes diretamente.

    ```R
    if(!require("miniCRAN")) install.packages("miniCRAN") 
    if(!require("igraph")) install.packages("igraph") 
    library("miniCRAN")
    ```

### <a name="step-2-define-a-package-source-a-cran-mirror-or-an-mran-snapshot"></a>Etapa 2. Definir uma origem de pacote: um espelho CRAN ou um instantâneo MRAN

1. Especifique um site do espelho para usar na obtenção de pacotes. Por exemplo, você pode usar o site MRAN ou qualquer outro site em sua região que contém os pacotes que você precisa. Se o download falhar, tente outro site do espelho.

    ```R
    CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
    CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
    ```

2. Digite o nome de uma pasta local no qual armazenar os pacotes coletados. 

    Certifique-se de criar a pasta com antecedência. Um erro será gerado se o `local_repo` pasta não existir quando você executar o código de R mais tarde.

    A pasta deve ter um nome descritivo. Aqui usamos "miniCRAN", mas se você repetir isso frequentemente, provavelmente você deve usar um nome mais descritivo, como "miniCRANZooPackages" ou "miniCRANMyRPackagev2".

    ```R
    local_repo <- "~/miniCRAN"
    ```

    O operador de expansão til retorna uma variável de ambiente, com resultados equivalentes a `Sys.getenv("R_USER")`.

### <a name="step-3-add-packages-to-the-repository"></a>Etapa 3. Adicionar pacotes ao repositório

1. Depois de **miniCRAN** é instalado, crie uma lista que especifica os pacotes adicionais que você deseja baixar.

    Fazer **não** adicionar dependências a essa lista inicial. O **igraph** pacote usado pelo **miniCRAN** gera a lista de dependências para você. Para obter mais informações sobre como usar o gráfico de dependência gerado, consulte [usando miniCRAN para identificar as dependências do pacote](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html).

    O script R a seguir adiciona os pacotes de destino, "zoo" e "previsão" a uma variável.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```
2. Não é necessário que você plotar o gráfico de dependência, mas pode ser informativo.
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. Crie o repositório local. Certifique-se de alterar a versão de R, se necessário

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

    Essas informações, o pacote miniCRAN cria a estrutura de pastas que você precisa copiar os pacotes para o [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] mais tarde.

4. Neste ponto, você deve ter uma pasta que contém os pacotes que você precisava e quaisquer outros pacotes que foram necessárias.

    Você pode executar o código a seguir para listar os pacotes contidos no repositório miniCRAN.

    ```R
    pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
    head(pdb);
    pdb$Package;
    pdb[, c("Package", "Version", "License")]
    ```

### <a name="step-4-use-the-repository-to-add-r-packages-to-the-instance-library"></a>Etapa 4. Usar o repositório para adicionar pacotes de R para a biblioteca de instância

Depois que você tiver criado o repositório e adicionado os pacotes que necessários, você deve mover o repositório do pacote para o computador do servidor e certifique-se de que os pacotes de R são instalados na biblioteca correta para uso do SQL Server.

O procedimento a seguir descreve como instalar os pacotes usando ferramentas de R.

1. Copie a pasta que contém o repositório de miniCRAN, em sua totalidade, para o servidor onde você planeja instalar os pacotes. A pasta normalmente tem esta estrutura: miniCRAN raiz > -> bin -> windows -> Contribuidor -> versão de não -> todos os pacotes.

2. Abra um prompt de comando de R usando a ferramenta de R associada com a instância.

    - Para o SQL Server 2017, a pasta padrão é `C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library`.

    - Para o SQL Server 2016, a pasta padrão é `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library`.

    - Para uma instância nomeada, o caminho padrão seria algo como: `<instance_path>.RTEST/R_SERVICES/library`.

    -  Se você tiver instalado o SQL Server em uma unidade diferente ou tiver feito outras alterações no caminho de instalação, certifique-se de fazer essas alterações também.

3. Obter o caminho para a biblioteca de instância e adicioná-lo à lista de caminhos de biblioteca.

    ```R
    .libPaths()[1];
    lib <- .libPaths()[1]
    ```

    No SQL Server, esse comando deve retornar o caminho da biblioteca associado com a instância, como: "SQL de arquivos/Microsoft Server/MSSQL14 da unidade c: / programa. R_SERVICES/MSSQLSERVER/biblioteca"

4. Especifique o novo local no servidor onde você copiou o **miniCRAN** repositório, como `server_repo`.

    Neste exemplo, vamos supor que você copiou do repositório para uma pasta temporária no servidor.

    ```R
    source_repo <- "C:\\temp\\miniCRAN"
    ```

5. Desde que você estiver trabalhando em um novo espaço de trabalho de R no servidor, forneça também a lista de pacotes para instalar.

    ```R
    tspackages <- c("zoo", "forecast")
    ```

6. Instale os pacotes, fornecendo o caminho para a cópia local do repositório miniCRAN.

    ```R
    install.packages(tspackages, repos = file.path("file://", normalizePath;(source_repo, winslash = "/")), lib = lib, type = "win.binary", dependencies = TRUE);
    ```

7. Na biblioteca de instância, você pode exibir os pacotes instalados usando um comando semelhante ao seguinte:

    ```R
    installed.packages()
    ```

> [!NOTE] 
> Para usar o pacote no SQL Server, os pacotes devem ser instalados para a biblioteca padrão usada pela instância. 

## <a name="manually-install-a-single-package-from-a-zipped-file"></a>Instalar manualmente um único pacote de um arquivo compactado

Se você estiver instalando um único pacote que não tem nenhuma dependência ou não é possível usar **miniCRAN**, você pode baixar manualmente o pacote que você precisa. Para fazer isso requer que você está um administrador ou um único proprietário de um servidor.

Depois de baixar os pacotes, você pode instalar os pacotes de R do local de arquivo compactado.

1. Baixar o pacote como um arquivo compactado e salvá-lo em uma pasta local

2. Copie essa pasta para o [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] computador.

3. Instale os pacotes para a biblioteca de instância do SQL Server usando comandos de R convencionais. Se o pacote tem dependências que não estão instaladas e que não incluiu, a instalação poderá falhar. 

Você também pode carregar pacotes individuais em uma instância do SQL Server de 2017, usando o [instrução Criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql). Esse processo também requer acesso administrativo.
