---
title: Criar um repositório local do pacote de R usando miniCRAN (aprendizado de máquina do SQL Server) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1f7ba3b4acde90d9e416eb092ac80cb0dfcbba8a
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34585638"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>Criar um repositório local do pacote de R usando miniCRAN
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) pacote, criado pela [Andre de Vries](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html), identifica e faz o download de pacotes e dependências em uma única pasta, você pode copiar a outros computadores para instalação de pacote de R offline.

Como uma entrada, especifique um ou mais pacotes. **miniCRAN** recursivamente lê a árvore de dependência para esses pacotes e baixa apenas os pacotes listados e suas dependências de CRAN ou repositórios semelhantes.

Como uma saída, **miniCRAN** cria um repositório consistente internamente consiste dos pacotes selecionados e dependências necessárias. Você pode, em seguida, mova este repositório local para o servidor e continuar a instalar os pacotes sem uma conexão de internet.

> [!NOTE]
> Usuários experientes do R geralmente procuram a lista de pacotes dependentes no arquivo de descrição para o pacote baixado. No entanto, os pacotes listados na **Imports** podem ter dependências de segundo nível. Por esse motivo, é recomendável **miniCRAN** para montar o conjunto completo de pacotes necessários.

## <a name="why-create-a-local-repository"></a>Por que criar um repositório local

O objetivo de criar um repositório de pacote local é fornecer um único local em que um administrador de servidor ou de outros usuários na organização podem usar para instalar novos pacotes de R em um servidor, especialmente aquelas que não tem acesso à internet. Depois de criar o repositório, você pode modificá-lo adicionando novos pacotes ou atualizar a versão de pacotes existentes.

Repositórios de pacote são úteis nestes cenários:

- **Segurança**: os usuários de R muitos estão acostumados a baixar e instalar novos pacotes de R à vontade, da CRAN ou um de seus sites de espelho. No entanto, por motivos de segurança, os servidores de produção executando [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] normalmente não tem conectividade com a internet.

- **Fácil instalação offline**: para instalar o pacote a um servidor offline requer que você também baixar todas as dependências do pacote, usando miniCRAN torna mais fácil de obter todas as dependências no formato correto.

    Usando miniCRAN, você pode evitar erros de dependência de pacote ao preparar pacotes para instalar com o [criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrução.

- **Melhor gerenciamento de versão**: em um ambiente multiusuário, há boas razões para evitar irrestrita instalação de várias versões de pacote no servidor. Use um repositório local para fornecer um conjunto consistente de pacotes para uso por seus analistas. 

> [!TIP]
> Você também pode usar miniCRAN preparar pacotes para uso no aprendizado de máquina do Azure. Para obter mais informações, consulte este blog: [usando miniCRAN no Azure ML, por Michele Usuelli](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="install-minicran"></a>Instalar miniCRAN

O **miniCRAN** pacote propriamente dito é dependente de 18 de outros pacotes CRAN, entre o que é o **RCurl** pacote, que tem uma dependência de sistema no **devel ondulação** pacote. Da mesma forma, o pacote **XML** tem uma dependência em **libxml2 devel**. Para resolver as dependências, recomendamos que você crie seu repositório local inicialmente em um computador com acesso total à internet. 

Execute os seguintes comandos em um computador com uma base R, ferramentas de R e conexão de internet. Supõe-se que isso é *não* computador SQL Server. Os comandos a seguir instalam o **miniCRAN** necessários e pacote **igraph** pacote. Este exemplo verifica se o pacote já está instalado, mas você pode ignorar o se instruções e instale os pacotes diretamente.

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>Definir o espelho CRAN e instantâneo MRAN

Especifique um site do espelho para usar na obtenção de pacotes. Por exemplo, você pode usar o site MRAN ou qualquer outro site em sua região que contém os pacotes que você precisa. Se o download falhar, tente outro site do espelho.

```R
CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>Criar uma pasta local

Criar uma pasta local, como `C:\mylocalrepo` no qual armazenar os pacotes coletados. Se você repetir isso frequentemente, provavelmente você deve usar um nome mais descritivo, como "miniCRANZooPackages" ou "miniCRANMyRPackagev2".

Especifique a pasta como o local do repositório. Sintaxe de R usa uma barra invertida para nomes de caminho, que é o oposto de convenções do Windows.

```R
local_repo <- "C:/mylocalrepo"
```

## <a name="add-packages-to-the-local-repo"></a>Adicionar pacotes ao repositório local

Depois de **miniCRAN** está instalado e carregado, crie uma lista que especifica os pacotes adicionais que você deseja baixar.

Fazer **não** adicionar dependências a essa lista inicial. O **igraph** pacote usado pelo **miniCRAN** gera a lista de dependências para você. Para obter mais informações sobre como usar o gráfico de dependência gerado, consulte [usando miniCRAN para identificar as dependências do pacote](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html).

1. Adicione pacotes de destino, "zoo" e "previsão" a uma variável.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. Opcionalmente, plotar o gráfico de dependência, mas pode ser informativo.
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. Crie o repositório local. Certifique-se de alterar a versão de R, se necessário, para a versão instalada na instância do SQL Server. Versão 3.2.2 é no SQL Server 2016, versão 3.3 está em 2017 do SQL Server. Se você fez uma atualização de componente, a versão pode ser mais recente. Para obter mais informações, consulte [obter R e Python informações do pacote](determine-which-packages-are-installed-on-sql-server.md).

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   Essas informações, o pacote miniCRAN cria a estrutura de pastas que você precisa copiar os pacotes para o [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] mais tarde.

Neste ponto, você deve ter uma pasta que contém os pacotes que você precisava e quaisquer outros pacotes que foram necessárias. O caminho deve ser semelhante a este exemplo: C:\mylocalrepo\bin\windows\contrib\3.3 e devem conter uma coleção de pacotes compactados. Não descompactar os pacotes ou renomeie os arquivos.

Opcionalmente, execute o código a seguir para listar os pacotes contidos no repositório local miniCRAN.

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>Adicionar pacotes para a biblioteca de instância

Depois que você tem um repositório local com os pacotes que necessários, mova o repositório de pacote para o computador do SQL Server. O procedimento a seguir descreve como instalar os pacotes usando ferramentas de R.

1. Copie a pasta que contém o repositório de miniCRAN, em sua totalidade, para o servidor onde você planeja instalar os pacotes. A pasta normalmente tem esta estrutura: miniCRAN raiz > bin > windows > Contribuidor > versão > todos os pacotes. Nos exemplos a seguir, vamos supor que uma pasta de unidade raiz: 

2. Abra uma ferramenta de R associada com a instância (por exemplo, você poderia usar Rgui.exe). Clique com botão direito **executar como administrador** para permitir que a ferramenta fazer atualizações em seu sistema.

    - Para o SQL Server 2017, o local do arquivo para RGUI é `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`.

    - Para o SQL Server 2016, he arquivo local RGUI é `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`.

3. Obter o caminho para a biblioteca de instância e adicioná-lo à lista de caminhos de biblioteca. No SQL Server de 2017, o caminho é semelhante ao exemplo a seguir.

    ```R
    outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
    ```

4. Especifique o novo local no servidor onde você copiou o **miniCRAN** repositório, como `server_repo`.

    Neste exemplo, vamos supor que você copiou do repositório para uma pasta temporária no servidor.

    ```R
    inputlib <- "C:/temp/mylocalrepo"
    ```

5. Desde que você estiver trabalhando em um novo espaço de trabalho de R no servidor, forneça também a lista de pacotes para instalar.

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


