---
title: Criar um repositório local de pacotes do R usando miniCRAN
description: Use o miniCran para detectar, montar e instalar as dependências do pacote R em um único pacote consolidado.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 34b7fee6b5eef1503f56dd72c6d8ff10911bbdc1
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470219"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>Criar um repositório local de pacotes do R usando miniCRAN
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

o pacote [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) , criado por [Andre de Vries](https://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html), identifica e baixa pacotes e dependências em uma única pasta, que você pode copiar para outros computadores para instalação offline do pacote R.

Como uma entrada, especifique um ou mais pacotes. **miniCRAN** lê recursivamente a árvore de dependência para esses pacotes e baixa apenas os pacotes listados e suas dependências de Cran ou repositórios semelhantes.

Como saída, o **miniCRAN** cria um repositório internamente consistente que consiste nos pacotes selecionados e todas as dependências necessárias. Você pode mover esse repositório local para o servidor e prosseguir para instalar os pacotes sem uma conexão com a Internet.

> [!NOTE]
> Os usuários experientes do R geralmente procuram a lista de pacotes dependentes no arquivo de descrição do pacote baixado. No entanto, os pacotes listados em **importações** podem ter dependências de segundo nível. Por esse motivo, recomendamos **miniCRAN** para montar a coleção completa de pacotes necessários.

## <a name="why-create-a-local-repository"></a>Por que criar um repositório local

O objetivo de criar um repositório de pacotes local é fornecer um único local que um administrador de servidor ou outros usuários da organização possam usar para instalar novos pacotes de R em um servidor, especialmente um que não tenha acesso à Internet. Depois de criar o repositório, você pode modificá-lo adicionando novos pacotes ou atualizando a versão dos pacotes existentes.

Os repositórios de pacote são úteis nestes cenários:

- **Segurança**: Muitos usuários do R estão acostumados a baixar e instalar novos pacotes de R a partir de CRAN ou de um de seus sites de espelhamento. No entanto, por motivos de segurança, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] os servidores de produção em execução normalmente não têm conectividade com a Internet.

- **Instalação offline mais fácil**: Para instalar o pacote em um servidor offline, é necessário que você também Baixe todas as dependências do pacote, usando miniCRAN torna mais fácil obter todas as dependências no formato correto.

    Usando o miniCRAN, você pode evitar erros de dependência do pacote ao preparar pacotes para instalação com a instrução [criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) .

- **Gerenciamento de versão aprimorado**: Em um ambiente multiusuário, há bons motivos para evitar a instalação irrestrita de várias versões de pacote no servidor. Use um repositório local para fornecer um conjunto consistente de pacotes para uso pelos analistas. 

> [!TIP]
> Você também pode usar o miniCRAN para preparar pacotes para uso no Azure Machine Learning. Para obter mais informações, consulte este blog: [Usando miniCRAN no Azure ML, por Michele Usuelli](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="install-minicran"></a>Instalar o miniCRAN

O pacote **miniCRAN** em si depende de 18 outros pacotes Cran, entre os quais está o pacote **as** , que tem uma dependência do sistema no pacote de **rotação-desenvolvedor** . Da mesma forma, o **XML** do pacote tem uma dependência em **libxml2-desenvolvedor**. Para resolver as dependências, recomendamos que você crie seu repositório local inicialmente em um computador com acesso total à Internet. 

Execute os comandos a seguir em um computador com um R, ferramentas de R e conexão com a Internet. Supõe-se que esse *não* seja o computador SQL Server. Os comandos a seguir instalam o pacote **miniCRAN** e o pacote **igraph** necessário. Este exemplo verifica se o pacote já está instalado, mas você pode ignorar as instruções IF e instalar os pacotes diretamente.

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>Definir o espelho do CRAN e o instantâneo do MRAN

Especifique um site de espelhamento a ser usado na obtenção de pacotes. Por exemplo, você pode usar o site MRAN ou qualquer outro site na sua região que contenha os pacotes necessários. Se o download falhar, tente outro site de espelhamento.

```R
CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>Criar uma pasta local

Crie uma pasta local, `C:\mylocalrepo` como na qual armazenar os pacotes coletados. Se você repetir isso com frequência, provavelmente usará um nome mais descritivo, como "miniCRANZooPackages" ou "miniCRANMyRPackagev2".

Especifique a pasta como o repositório local. A sintaxe do R usa uma barra invertida para nomes de caminho, que é oposto das convenções do Windows.

```R
local_repo <- "C:/mylocalrepo"
```

## <a name="add-packages-to-the-local-repo"></a>Adicionar pacotes ao repositório local

Depois que o **miniCRAN** for instalado e carregado, crie uma lista que especifica os pacotes adicionais que você deseja baixar.

**Não** adicione dependências a esta lista inicial. O pacote **igraph** usado pelo **miniCRAN** gera a lista de dependências para você. Para obter mais informações sobre como usar o grafo de dependência gerado, consulte [usando miniCRAN para identificar dependências de pacote](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html).

1. Adicione pacotes de destino, "Zoo" e "Forecast" a uma variável.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. Opcionalmente, plote o grafo de dependência, mas pode ser informativo.
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. Crie o repositório local. Certifique-se de alterar a versão do R, se necessário, para a versão instalada em sua instância do SQL Server. A versão 3.2.2 está em SQL Server 2016, a versão 3,3 está em SQL Server 2017. Se você fez uma atualização de componente, sua versão pode ser mais recente. Para obter mais informações, consulte [obter informações do pacote R e Python](../package-management/installed-package-information.md).

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   A partir dessas informações, o pacote miniCRAN cria a estrutura de pastas que você precisa para copiar os pacotes [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] para o mais tarde.

Neste ponto, você deve ter uma pasta que contém os pacotes necessários e todos os pacotes adicionais que foram necessários. O caminho deve ser semelhante a este exemplo: C:\mylocalrepo\bin\windows\contrib\3.3 e deve conter uma coleção de pacotes compactados. Não descompacte os pacotes ou renomeie os arquivos.

Opcionalmente, execute o código a seguir para listar os pacotes contidos no repositório miniCRAN local.

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>Adicionar pacotes à biblioteca de instâncias

Depois de ter um repositório local com os pacotes necessários, mova o repositório de pacotes para o computador SQL Server. O procedimento a seguir descreve como instalar os pacotes usando as ferramentas do R.

1. Copie a pasta que contém o repositório miniCRAN, em sua totalidade, para o servidor no qual você planeja instalar os pacotes. A pasta normalmente tem essa estrutura: miniCRAN root > bin > Windows > contrib > versão > todos os pacotes. Nos exemplos a seguir, vamos supor uma pasta fora da unidade raiz: 

2. Abra uma ferramenta do R associada à instância do (por exemplo, você pode usar Rgui. exe). Clique com o botão direito do mouse em **Executar como administrador** para permitir que a ferramenta faça atualizações em seu sistema.

    - Para SQL Server 2017, o local do arquivo para RGUI `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`é.

    - Para SQL Server 2016, o local do arquivo para RGUI `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`é.

3. Obtenha o caminho para a biblioteca de instâncias e adicione-a à lista de caminhos de biblioteca. No SQL Server 2017, o caminho é semelhante ao exemplo a seguir.

    ```R
    outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
    ```

4. Especifique o novo local no servidor em que você copiou o repositório **miniCRAN** , como `server_repo`.

    Neste exemplo, presumimos que você copiou o repositório para uma pasta temporária no servidor.

    ```R
    inputlib <- "C:/temp/mylocalrepo"
    ```

5. Como você está trabalhando em um novo espaço de trabalho do R no servidor, você também deve fornecer a lista de pacotes a serem instalados.

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. Instale os pacotes, fornecendo o caminho para a cópia local do repositório miniCRAN.

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. Na biblioteca de instâncias, você pode exibir os pacotes instalados usando um comando como o seguinte:

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>Confira também

+ [Obter informações sobre o pacote](../package-management/installed-package-information.md)
+ [Tutoriais de R](../tutorials/sql-server-r-tutorials.md)
