---
title: Criar um repositório com miniCRAN
description: Saiba como instalar pacotes do R offline usando o pacote miniCRAN para criar um repositório local de pacotes e dependências.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/20/2019
ms.topic: how-to
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: bf93d618ad03122cc7eecf641573d70b2b72158e
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88173508"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>Criar um repositório local de pacotes do R usando o miniCRAN
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

Este artigo descreve como instalar pacotes do R offline usando o [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) para criar um repositório local de pacotes e dependências. O **miniCRAN** identifica e baixa os pacotes e dependências em uma única pasta que você copia para outros computadores para instalação offline do pacote do R.

Você pode especificar um ou mais pacotes e o **miniCRAN** lê recursivamente a árvore de dependência para esses pacotes. Em seguida, ele baixa apenas os pacotes listados e as respectivas dependências do CRAN ou de repositórios semelhantes.

Quando isso é concluído, o **miniCRAN** cria um repositório internamente consistente, formado pelos pacotes selecionados e por todas as dependências necessárias. Você pode mover esse repositório local para o servidor e prosseguir para instalar os pacotes sem uma conexão com a Internet.

Os usuários experientes do R costumam procurar a lista de pacotes dependentes no arquivo DESCRIPTION de um pacote baixado. No entanto, os pacotes listados em **Importações** podem ter dependências de segundo nível. Por esse motivo, recomendamos o uso do **miniCRAN** para montar a coleção completa de pacotes necessários.

## <a name="why-create-a-local-repository"></a>Por que criar um repositório local

O objetivo de criar um repositório de pacotes local é fornecer uma única localização que um administrador do servidor ou outros usuários da organização possam usar para instalar novos pacotes do R em um servidor, especialmente um que não tenha acesso à Internet. Depois de criar o repositório, você pode modificá-lo adicionando novos pacotes ou atualizando a versão dos pacotes existentes.

Os repositórios de pacote são úteis nestes cenários:

- **Segurança**: Muitos usuários do R estão acostumados a baixar e instalar novos pacotes do R segundo sua própria vontade, por meio do CRAN ou de um de seus locais de espelhamento. No entanto, por motivos de segurança, os servidores de produção executando o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] normalmente não têm conectividade com a Internet.

- **Instalação offline mais fácil**: Para instalar um pacote em um servidor offline, é necessário que você também baixe todas as dependências desse pacote. O uso do miniCRAN facilita a obtenção de todas as dependências no formato correto e evita erros de dependência.

- **Gerenciamento de versões aprimorado**: Em um ambiente de vários usuários, há bons motivos para evitar a instalação irrestrita de várias versões de pacote no servidor. Use um repositório local para fornecer um conjunto consistente de pacotes para seus usuários.

## <a name="install-minicran"></a>Instalar o miniCRAN

O pacote do **miniCRAN** propriamente dito depende de 18 outros pacotes CRAN, entre os quais está o pacote **RCurl**, que tem uma dependência do sistema do pacote **curl-devel**. Da mesma forma, o pacote **XML** tem uma dependência de **libxml2-devel**. Para resolver as dependências, recomendamos que você crie inicialmente seu repositório local em um computador com acesso total à Internet.

Execute os comandos a seguir em um computador com R base, ferramentas do R e uma conexão com a Internet. Supõe-se que esse não seja o computador do SQL Server. Os comandos a seguir instalam o pacote **miniCRAN** e o pacote **igraph**. Este exemplo verifica se o pacote já está instalado, mas você pode ignorar as instruções de `if` e instalar os pacotes diretamente.

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>Definir o espelho do CRAN e o instantâneo do MRAN

Especificar um local de espelhamento a ser usado na obtenção de pacotes. Por exemplo, você pode usar o site do MRAN ou qualquer outro site na sua região que contenha os pacotes necessários. Se um download falhar, tente usar outro local de espelhamento.

```R
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>Criar uma pasta local

Crie uma pasta local na qual armazenar os pacotes coletados. Se você repetir isso com frequência, talvez você queira usar um nome descritivo, tal como "miniCRANZooPackages" ou "miniCRANMyRPackageV2".

Especifique a pasta como o repositório local. A sintaxe do R usa uma barra invertida para nomes de caminho, que é oposto das convenções do Windows.

```R
local_repo <- "C:/miniCRANZooPackages"
```

## <a name="add-packages-to-the-local-repo"></a>Adicionar pacotes ao repositório local

Depois que o **miniCRAN** for instalado e carregado, crie uma lista que especifique os pacotes adicionais que você deseja baixar.

**Não** adicione dependências a essa lista inicial. O pacote **igraph** usado por **miniCRAN** gera a lista de dependências automaticamente. Para obter mais informações sobre como usar o grafo de dependência gerado, confira [Usar o miniCRAN para identificar dependências de pacote](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html).

1. Adicione os pacotes de destino "zoo" e "forecast" a uma variável.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. Opcionalmente, plote o grafo de dependência. Isso não é necessário, mas pode oferecer informações interessantes.

    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. Crie o repositório local. Se necessário, não se esqueça de alterar a versão do R para a versão instalada em sua instância do SQL Server. Se você fez uma atualização de componente, sua versão pode ser mais recente do que a versão original. Para obter mais informações, confira [Obter informações sobre o pacote do R](../package-management/r-package-information.md).

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   Com base nessas informações, o pacote miniCRAN cria a estrutura de pastas que você precisa para copiar os pacotes para o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] posteriormente.

Neste ponto, você deve ter uma pasta contendo os pacotes necessários e eventuais pacotes adicionais requeridos. A pasta deve conter uma coleção de pacotes compactados. Não descompacte os pacotes nem renomeie nenhum arquivo.

Opcionalmente, execute o código a seguir para listar os pacotes contidos no repositório local do miniCRAN.

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>Adicionar pacotes à biblioteca de instâncias

Depois de ter um repositório local com os pacotes necessários, mova o repositório de pacotes para o computador do SQL Server. O procedimento a seguir descreve como instalar os pacotes usando as ferramentas do R.

::: moniker range=">sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"
> [!NOTE]
> O método recomendado para instalar pacotes está usando **sqlmlutils**. Confira [Instalar novos pacotes de R com sqlmlutils](install-additional-r-packages-on-sql-server.md).
::: moniker-end

1. Copie toda a pasta que contém o repositório do miniCRAN para o servidor no qual você planeja instalar os pacotes. A pasta normalmente tem esta estrutura: 

   `<miniCRAN root>/bin/windows/contrib/version/<all packages>`

   Neste procedimento, pressupomos uma pasta fora da unidade raiz.

2. Abra uma ferramenta do R associada à instância (por exemplo, você pode usar Rgui.exe). Clique com o botão direito do mouse e selecione **Executar como administrador** para permitir que a ferramenta faça atualizações em seu sistema.

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   - Por exemplo, a localização do arquivo padrão para RGUI é `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`.
   ::: moniker-end

   ::: moniker range"=sql-server-2017||=sqlallproducts-allversions"
   - Por exemplo, a localização do arquivo para RGUI é `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`.
   ::: moniker-end

   ::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
   - Por exemplo, a localização do arquivo para RGUI é `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\bin\x64`.
   ::: moniker-end

3. Obtenha o caminho para a biblioteca de instâncias e adicione-a à lista de caminhos de biblioteca.

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   Por exemplo,

   ```R
   outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library"
   ```

   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   Por exemplo,

   ```R
   outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
   ```

   ::: moniker-end

   ::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
   Por exemplo,

   ```R
   outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL15.MSSQLSERVER/R_SERVICES/library"
   ```

   ::: moniker-end

4. Especifique a nova localização no servidor em que você copiou o repositório **miniCRAN** como `server_repo`.

    Neste exemplo, presumimos que você copiou o repositório para uma pasta temporária no servidor.

    ```R
    inputlib <- "C:/miniCRANZooPackages"
    ```

5. Já que você está trabalhando em um novo workspace do R no servidor, você também precisa fornecer a lista de pacotes a serem instalados.

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

+ [Obter informações sobre o pacote do R](../package-management/r-package-information.md)
+ [Tutoriais do R](../tutorials/sql-server-r-tutorials.md)
