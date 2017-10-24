---
title: "Criar um repositório de pacote local usando miniCRAN | Microsoft Docs"
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 1dd7e8f1a0054818849b3b9672a5df6286bdabce
ms.contentlocale: pt-br
ms.lasthandoff: 10/10/2017

---
# <a name="create-a-local-package-repository-using-minicran"></a>Criar um repositório de pacote local usando miniCRAN

Há duas maneiras que você pode preparar os pacotes de R para instalação em um servidor sem acesso à internet.

-   [Use o pacote miniCRAN para criar um único repositório local](#bkmk_miniCRAN)

    O [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) cria um repositório consistente internamente consiste de repositórios de CRAN os pacotes selecionados. O usuário Especifica um conjunto de pacotes desejados e miniCRAN recursivamente lê a árvore de dependência para esses pacotes e baixa apenas os pacotes listados e suas dependências.

    Você pode, em seguida, mova este repositório local para o servidor e continuar a instalar os pacotes sem usar a internet.

-   [O download manual e copiar pacotes uma](#bkmk_manual)

Este artigo descreve como você pode criar um repositório de pacotes de R usando ambos os métodos e recomenda usa o **miniCRAN** pacote.

## <a name="prepare-packages-using-minicran"></a>Preparar pacotes usando miniCRAN

O objetivo de criar um repositório de pacote local é fornecer um único local em que um administrador de servidor ou de outros usuários na organização podem usar para instalar novos pacotes de R em um servidor que não tem acesso à internet.

O [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) do pacote de R foi escrito por [Andre de Vries](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html) para tornar mais fácil criar consistente, gerenciado por conjunto de pacotes de R para uma organização. 

Há muitas vantagens em usar miniCRAN para criar o repositório:

-   **Segurança**: os usuários de R muitos estão acostumados a baixar e instalar novos pacotes de R à vontade, da CRAN ou um de seus sites de espelho. No entanto, por motivos de segurança, os servidores de produção executando [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] normalmente não tem conectividade com a internet.

-   **Fácil instalação offline**: para instalar o pacote a um servidor offline requer que você também baixar todas as dependências do pacote, usando miniCRAN torna mais fácil de obter todas as dependências no formato correto.

-   **Melhor gerenciamento de versão**: em um ambiente multiusuário, há boas razões para evitar irrestrita instalação de várias versões de pacote no servidor.

Depois de criar o repositório, você pode modificá-lo adicionando novos pacotes ou atualizar a versão de pacotes existentes.

### <a name="step-1-install-the-minicran-package"></a>Etapa 1. Instalar o pacote de miniCRAN

Você começa criando um repositório miniCRAN para usar como uma fonte. Você deve criar esse repositório em um computador que tenha acesso à internet.

1.  Instalar o pacote de miniCRAN e obrigatório **igraph** pacote.

    ```R
    if(!require("miniCRAN")) install.packages("miniCRAN") if(!require("igraph"))
    install.packages("igraph") library(miniCRAN)
    ```

### <a name="step-2-define-a-package-source-a-cran-mirror-or-an-mran-snapshot"></a>Etapa 2. Definir uma origem de pacote: um espelho CRAN ou um instantâneo MRAN

1. Especifique um site do espelho para usar na obtenção de pacotes.

    ```R
    CRAN_mirror \<- c(CRAN = "https://mran.microsoft.com/snapshot/2017-08-01")
    ```

2.  Indica uma pasta local no qual armazenar os pacotes coletados. Você não precisa nomear miniCRAN a pasta; pode ser um nome mais descritivo, como "GeneticsPackages" ou "ClientRPackages1.0.2".

    Apenas certifique-se de criar a pasta com antecedência. Um erro será gerado se o `local_repo` pasta não existir quando você executar o código de R mais tarde.

    ```R
    local_repo <- "~/miniCRAN"
    ```

    O operador de expansão til retorna uma variável de ambiente, com resultados equivalentes a `Sys.getenv("R_USER")`.

### <a name="step-3-add-packages-to-the-repository"></a>Etapa 3. Adicionar pacotes ao repositório

1.  Após a instalação miniCRAN, crie uma lista que especifica os pacotes adicionais que você deseja baixar.

    Não adicionar dependências a essa lista inicial; o **igraph** pacote usado pelo miniCRAN gera a lista de dependências para você. Para obter mais informações sobre como usar esse gráfico, consulte [usando miniCRAN para identificar as dependências do pacote](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html).

    O script R a seguir demonstra como obter os pacotes de destino, "zoo" e "previsão".

    ```R
    pkgs_needed <- c("zoo", "forecast")

2. Optionally, plot the dependency graph, which can be informative and looks cool.
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. Crie o repositório local. Certifique-se de alterar a versão de R, se necessário

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror)
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3")
    ```

    Essas informações, o pacote miniCRAN cria a estrutura de pastas que você precisa copiar os pacotes para o [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] mais tarde.

4. Neste ponto, você deve ter uma pasta que contém os pacotes que você precisava e quaisquer outros pacotes que foram necessárias.

    Você pode executar o código a seguir para listar os pacotes contidos no repositório miniCRAN.

    ```R
    pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE)
    head(pdb)
    pdb$Package
    pdb[, c("Package", "Version", "License")]
    ```

### <a name="step-4-use-the-repository-to-add-r-packages-to-the-instance-library"></a>Etapa 4. Usar o repositório para adicionar pacotes de R para a biblioteca de instância

Depois que você tiver criado o repositório e adicionado os pacotes que necessários, você deve mover o repositório do pacote para o computador do servidor e certifique-se de que os pacotes de R são instalados na biblioteca correta para uso do SQL Server.

Dependendo da versão do SQL Server, há duas opções para adicionar novos pacotes para a biblioteca de R associada com a instância do SQL Server:

-   Instale a biblioteca de instância usando as ferramentas de R e miniCRAN repositório.

-   Carregar pacotes de um banco de dados SQL e instalar pacotes em uma base por banco de dados, usando a instrução Criar biblioteca externa. Consulte [instalar pacotes R adicionais no SQL Server](install-additional-r-packages-on-sql-server.md).

O procedimento a seguir descreve como instalar os pacotes usando ferramentas de R.

1.  Copie a pasta que contém o repositório de miniCRAN, em sua totalidade, para o servidor onde você instalará os pacotes.

2.  Abra um prompt de comando de R usando a ferramenta de R associada com a instância.

    - Para o SQL Server 2017, a pasta padrão é `C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library`.

    - Para o SQL Server 2016, a pasta padrão é `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library`.

    - Para uma instância nomeada, o caminho padrão seria algo como: `<instance_path>.RTEST/R_SERVICES/library`.

    -  Se você tiver instalado o SQL Server em uma unidade diferente ou tiver feito outras alterações no caminho de instalação, certifique-se de fazer essas alterações também.

3.  Obter o caminho para a biblioteca de instância (no caso que você esteja em um diretório de usuário) e adicioná-lo à lista de caminhos de biblioteca.

    ```R
    .libPaths()[1]  
    lib \<- .libPaths()[1]
    ```

    Isso deve retornar o caminho da instância, "SQL de arquivos/Microsoft Server/MSSQL14 da unidade c: / programa. R_SERVICES/MSSQLSERVER/biblioteca"

2.  Especifique o local no servidor onde você copiou o repositório mininCRAN em `server_repo`.

    Neste exemplo, vamos supor que você copiou do repositório para sua pasta de usuário no servidor.

    ```R
    R server_repo <- "C:\\Users\\MyUserName\\miniCRAN"
    ```

3.  Desde que você estiver trabalhando em um novo espaço de trabalho de R no servidor, forneça também a lista de pacotes para instalar.

    ```R
    tspackages <- c("zoo", "forecast")
    ```

4.  Instale os pacotes, usando o caminho para a cópia local do repositório miniCRAN.

    ```R
    install.packages(tspackages, repos = file.path("file://", normalizePath(server_repo, winslash = "/")), lib = lib, type = "win.binary", dependencies = TRUE)
    ```

5.  Agora exiba os pacotes instalados.

    ```R
    installed.packages()
    ```

> [!NOTE] 
> 
> No SQL Server de 2017, funções de banco de dados adicionais e instruções T-SQL são fornecidas para ajudar os administradores de servidor gerenciar permissões em pacotes. O administrador de banco de dados pode ter a tarefa de instalar pacotes, usando o R ou T-SQL, se desejado. No entanto, o DBA também pode usar funções para conceder aos usuários a capacidade de instalar seus próprios pacotes. Para obter mais informações, consulte [gerenciamento de pacotes de R para o SQL Server](r-package-management-for-sql-server-r-services.md).
> 
> No SQL Server 2016, um administrador de servidor deve instalar pacotes do repositório miniCRAN na biblioteca padrão usada pela instância. Para fazer isso, use as ferramentas de R, conforme descrito no [anterior seção](#bkmk_Rtools).

## <a name="manually-download-single-packages"></a>Baixar manualmente os pacotes único

Se você não quiser usar miniCRAN, você pode baixar manualmente os pacotes que necessários e suas dependências. Para fazer isso requer que você está um administrador ou um único proprietário de um servidor.

Depois de baixar os pacotes, você pode instalar os pacotes de R do local de arquivo compactado.

1.  Baixe os arquivos zip de pacotes e salvá-los em uma pasta local

2.  Copie essa pasta para o [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] computador.

3.  Instale os pacotes para a biblioteca de instância do SQL Server.

> [!NOTE]
> Quando você usa ferramentas R para instalar os pacotes, elas são instaladas para a instância como um todo. 
> 
> Se você quiser instalar o pacote em um banco de dados e compartilhe o pacote com usuários que usam funções de banco de dados, você deve carregar a biblioteca usando a instrução Criar biblioteca externa. Consulte [instalar pacotes R adicionais no SQL Server](install-additional-r-packages-on-sql-server.md)

