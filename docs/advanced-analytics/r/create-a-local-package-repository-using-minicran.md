---
title: Criar um repositório de pacotes de R local usando o miniCRAN - serviços do SQL Server Machine Learning
description: Use miniCran para detectar, montar e instalar as dependências de pacotes de R em um único pacote consolidado.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7dc2e286e6eb80fe1eef3e8b86ed1002a6344cfb
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53431749"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>Criar um repositório de pacotes de R local usando o miniCRAN
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) pacote, criado pelo [Andre de Vries](https://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html), identifica e baixa os pacotes e dependências em uma única pasta, você pode copiar para outros computadores para instalação offline do pacote de R.

Como uma entrada, especifique um ou mais pacotes. **miniCRAN** recursivamente lê a árvore de dependência para esses pacotes e baixa apenas os pacotes listados e suas dependências do CRAN ou repositórios semelhantes.

Como uma saída **miniCRAN** cria um repositório consistente internamente consiste em pacotes selecionados e dependências de todos os itens necessárias. Em seguida, você pode mover esse repositório local para o servidor e continuar para instalar os pacotes sem uma conexão de internet.

> [!NOTE]
> Muitas vezes procuram por usuários experientes do R para obter a lista dos pacotes dependentes no arquivo de descrição para o pacote baixado. No entanto, os pacotes listados na **importações** podem ter dependências de segundo nível. Por esse motivo, recomendamos **miniCRAN** para montando o conjunto completo de pacotes necessários.

## <a name="why-create-a-local-repository"></a>Por que criar um repositório local

O objetivo de criar um repositório de pacote local é fornecer um único local em que um administrador de servidor ou de outros usuários na organização podem usar para instalar novos pacotes de R em um servidor, especialmente para um que não tem acesso à internet. Depois de criar o repositório, você pode modificá-lo adicionando novos pacotes ou atualizando a versão de pacotes existentes.

Repositórios de pacote são úteis nestes cenários:

- **Segurança**: Muitos usuários de R estão acostumados a baixar e instalar novos pacotes do R à vontade, do CRAN ou um dos seus sites de espelho. No entanto, por motivos de segurança, servidores de produção em execução [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] normalmente não têm conectividade com a internet.

- **Fácil instalação offline**: Para instalar o pacote a um servidor offline requer que você também baixar todas as dependências de pacote, usando o miniCRAN torna mais fácil de obter todas as dependências no formato correto.

    Usando o miniCRAN, você pode evitar erros de dependência de pacote ao preparar pacotes para instalar com o [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrução.

- **Melhor gerenciamento de versão**: Em um ambiente multiusuário, existem bons motivos para evitar a instalação sem restrições de várias versões de pacote no servidor. Use um repositório local para fornecer um conjunto consistente de pacotes para uso por seus analistas. 

> [!TIP]
> Você também pode usar miniCRAN para preparar pacotes para usar no Azure Machine Learning. Para obter mais informações, consulte este blog: [Usando o miniCRAN no Azure ML, por Michele Usuelli](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="install-minicran"></a>Instalar o miniCRAN

O **miniCRAN** pacote propriamente dito é dependente de 18 outros pacotes CRAN, entre o que é o **RCurl** pacote, que tem uma dependência do sistema no **curl devel** pacote. Da mesma forma, empacotar **XML** tem uma dependência **libxml2 devel**. Para resolver as dependências, é recomendável que você criar seu repositório local inicialmente em um computador com acesso total à internet. 

Execute os seguintes comandos em um computador com uma base R, ferramentas do R e conexão de internet. Supõe-se que se trata *não* computador SQL Server. Os comandos a seguir instalam o **miniCRAN** pacote e a necessária **igraph** pacote. Este exemplo verifica se o pacote já está instalado, mas você pode ignorar o se instruções e instalar os pacotes diretamente.

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>Defina o instantâneo MRAN e o espelho CRAN

Especifique um site do espelho para usar na obtenção de pacotes. Por exemplo, você pode usar o site MRAN ou qualquer outro site na sua região que contém os pacotes que necessários. Se o download falhar, tente outro site do espelho.

```R
CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>Crie uma pasta local

Criar uma pasta local, como `C:\mylocalrepo` no qual armazenar os pacotes coletados. Se você repetir isso muitas vezes, você provavelmente deverá usar um nome mais descritivo, como "miniCRANZooPackages" ou "miniCRANMyRPackagev2".

Especifique a pasta repositório local. Sintaxe de R usa uma barra invertida para nomes de caminho, o que é o oposto das convenções do Windows.

```R
local_repo <- "C:/mylocalrepo"
```

## <a name="add-packages-to-the-local-repo"></a>Adicionar pacotes ao repositório local

Após **miniCRAN** está instalado e carregado, crie uma lista que especifica os pacotes adicionais que você deseja baixar.

Fazer **não** adicionar dependências a essa lista inicial. O **igraph** pacote usado pelo **miniCRAN** gera a lista de dependências para você. Para obter mais informações sobre como usar o grafo de dependência gerado, consulte [usando o miniCRAN para identificar as dependências do pacote](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html).

1. Adicione pacotes de destino, "zoo" e "forecast" a uma variável.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. Opcionalmente, plotar o grafo de dependência, mas ele pode ser informativo.
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. Crie o repositório local. Certifique-se de alterar a versão do R, se necessário, para a versão instalada em sua instância do SQL Server. Versão 3.2.2 está no SQL Server 2016, versão 3.3 está no SQL Server 2017. Se você fez uma atualização de componente, sua versão pode ser mais recente. Para obter mais informações, consulte [obter R e Python informações do pacote](determine-which-packages-are-installed-on-sql-server.md).

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   Com essas informações, o pacote miniCRAN cria a estrutura de pastas que você precisa copiar os pacotes para o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mais tarde.

Neste ponto, você deve ter uma pasta que contém os pacotes que você precisava, e todos os pacotes adicionais que foram necessários. O caminho deve ser semelhante a este exemplo: C:\mylocalrepo\bin\windows\contrib\3.3 e ele devem conter uma coleção de pacotes compactados. Não descompacte os pacotes ou renomeie todos os arquivos.

Opcionalmente, execute o código a seguir para listar os pacotes contidos no repositório local miniCRAN.

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>Adicionar pacotes para a biblioteca de instância

Depois de ter um repositório local com os pacotes que necessários, mova o repositório de pacote para o computador do SQL Server. O procedimento a seguir descreve como instalar os pacotes usando ferramentas do R.

1. Copie a pasta que contém o repositório miniCRAN, em sua totalidade, para o servidor em que você planeja instalar os pacotes. A pasta geralmente tem esta estrutura: miniCRAN raiz > bin > windows > contrib > versão > todos os pacotes. Os exemplos a seguir, presumimos que uma pasta de unidade raiz: 

2. Abra uma ferramenta de R associada à instância (por exemplo, você poderia usar Rgui.exe). Clique com botão direito **executar como administrador** para permitir que a ferramenta fazer atualizações em seu sistema.

    - Para o SQL Server 2017, é o local do arquivo para o RGUI `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`.

    - Para o SQL Server 2016, o local do arquivo he para RGUI é `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`.

3. Obter o caminho para a biblioteca de instância e adicioná-lo à lista de caminhos de biblioteca. No SQL Server 2017, o caminho é semelhante ao exemplo a seguir.

    ```R
    outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
    ```

4. Especifique o novo local no servidor onde você copiou o **miniCRAN** repositório, como `server_repo`.

    Neste exemplo, vamos supor que você copiou do repositório para uma pasta temporária no servidor.

    ```R
    inputlib <- "C:/temp/mylocalrepo"
    ```

5. Uma vez que você estiver trabalhando em um novo espaço de trabalho do R no servidor, forneça também a lista de pacotes para instalar.

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. Instale os pacotes, fornecendo o caminho para a cópia local do repositório miniCRAN.

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. Na biblioteca de instância, você pode exibir os pacotes instalados usando um comando semelhante ao seguinte:

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>Confira também

+ [Obter informações sobre o pacote](determine-which-packages-are-installed-on-sql-server.md)
+ [Tutoriais de R](../tutorials/sql-server-r-tutorials.md)
+ [Guias de instruções](sql-server-machine-learning-tasks.md)


