---
title: Instalar os novos pacotes R
description: Saiba como usar o sqlmlutils para instalar novos pacotes do R em uma instância de Serviços de Machine Learning do SQL Server ou SQL Server R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 827e83a0d1b363d3b91477b9ae85fec156ee4fc9
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727500"
---
# <a name="install-new-r-packages-with-sqlmlutils"></a>Instalar novos pacotes de R com sqlmlutils

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve como usar funções no pacote [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) para instalar novos pacotes do R em uma instância dos Serviços de Machine Learning do SQL Server ou o SQL Server R Services. Os pacotes que você instalar poderão ser usados em scripts R em execução no banco de dados usando a instrução T-SQL [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

> [!NOTE]
> O comando do R padrão `install.packages` não é recomendado para adicionar pacotes do R do SQL Server. Em vez disso, use **sqlmlutils**, conforme descrito neste artigo.

## <a name="prerequisites"></a>Prerequisites

- Instale o [R](https://www.r-project.org) e o [RStudio Desktop](https://www.rstudio.com/products/rstudio/download/) no computador cliente que você usa para conectar-se ao SQL Server. Você pode usar qualquer IDE do R para executar scripts, mas este artigo pressupõe o RStudio.

- Instale o [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) ou o [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) no computador cliente que você usa para se conectar ao SQL Server. Você pode usar outras ferramentas de consulta ou gerenciamento de banco de dados, mas este artigo pressupõe o Azure Data Studio ou o SSMS.

### <a name="other-considerations"></a>Outras considerações

- O script R em execução no SQL Server pode usar apenas os pacotes instalados na biblioteca de instâncias padrão. O SQL Server não pode carregar pacotes de bibliotecas externas, mesmo que a biblioteca esteja no mesmo computador. Isso inclui bibliotecas do R instaladas com outros produtos da Microsoft.

- Em um ambiente do SQL Server protegido, talvez você queira evitar o seguinte:
  - Pacotes que exigem acesso à rede
  - Pacotes que exigem acesso elevado ao sistema de arquivos
  - Pacotes usados para desenvolvimento Web ou outras tarefas que não se beneficiam da execução dentro do SQL Server

## <a name="install-sqlmlutils-on-the-client-computer"></a>Instalar sqlmlutils no computador cliente

Para usar **sqlmlutils**, primeiro você precisa instalá-lo no computador cliente que usa para se conectar ao SQL Server.

O pacote **sqlmlutils** depende do pacote **RODBCext**, e **RODBCext** depende de vários outros pacotes. Os procedimentos a seguir instalam todos esses pacotes na ordem correta.

### <a name="install-sqlmlutils-online"></a>Instalar o sqlmlutils online

Se o computador cliente tiver acesso à Internet, você poderá baixar e instalar o **sqlmlutils** e seus pacotes dependentes online.

1. Baixe o arquivo zip mais recente do **sqlmlutils** do https://github.com/Microsoft/sqlmlutils/tree/master/R/dist para o computador cliente. Não descompacte o arquivo.

1. Abra um **prompt de comando** e execute os comandos a seguir para instalar os pacotes **sqlmlutils** e **RODBCext**. Substitua o caminho completo para o arquivo zip do **sqlmlutils** que você baixou (este exemplo supõe o arquivo na sua pasta Documentos). O pacote **RODBCext** é encontrado online e instalado.

   ```console
   R -e "install.packages('RODBCext', repos='https://cran.microsoft.com')"
   R CMD INSTALL %UserProfile%\Documents\sqlmlutils_0.7.1.zip
   ```

### <a name="install-sqlmlutils-offline"></a>Instalar o sqlmlutils offline

Se o computador cliente não tiver uma conexão com a Internet, você precisará baixar os pacotes **sqlmlutils** e **o RODBCext** com antecedência usando um computador que tenha acesso à Internet. Em seguida, você pode copiar os arquivos para uma pasta no computador cliente e instalar os pacotes offline.

O pacote **RODBCext** tem vários pacotes dependentes, o que complica a identificação de todas as dependências de um pacote. Recomendamos usar [**miniCRAN**](https://andrie.github.io/miniCRAN/) para criar uma pasta de repositório local para o pacote que inclua todos os pacotes dependentes.
Para mais informações, confira [Criar um repositório de pacotes do R local usando o miniCRAN](create-a-local-package-repository-using-minicran.md).

O pacote **sqlmlutils** consiste em um único arquivo zip que você pode copiar para o computador cliente e instalar.

Em um computador com acesso à Internet:

1. Instalar o **miniCRAN**. Confira [Instalar o miniCRAN](create-a-local-package-repository-using-minicran.md#install-minicran) para obter detalhes.

1. No RStudio, execute o seguinte script R para criar um repositório local do pacote **RODBCext**. Este exemplo cria o repositório na pasta `c:\downloads\rodbcext`.

   ::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```

   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "source", Rversion = "3.5");
   ```

   ::: moniker-end

   Para o valor `Rversion`, use a versão do R instalada no SQL Server. Para verificar a versão instalada, use o comando T-SQL a seguir.

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. Baixe o arquivo zip **sqlmlutils** mais recente do https://github.com/Microsoft/sqlmlutils/tree/master/R/dist (não descompacte o arquivo). Por exemplo, baixe o arquivo para `c:\downloads\sqlmlutils_0.7.1.zip`.

1. Copie toda a pasta do repositório **RODBCext** (`c:\downloads\rodbcext`) e o arquivo zip **sqlmlutils** (`c:\downloads\sqlmlutils_0.7.1.zip`) para o computador cliente. Por exemplo, copie-os para a pasta `c:\temp\packages` no computador cliente.

No computador cliente que você usa para se conectar ao SQL Server, abra um prompt de comando e execute os seguintes comandos para instalar **RODBCext** e então **sqlmlutils**.

```console
R -e "install.packages('RODBCext', repos='c:\temp\packages\rodbcext')"
R CMD INSTALL c:\temp\packages\sqlmlutils_0.7.1.zip
```

## <a name="add-an-r-package-on-sql-server"></a>Adicionar um pacote do R no SQL Server

No exemplo a seguir, você adicionará o pacote [**glue**](https://cran.r-project.org/web/packages/glue/) ao SQL Server.

### <a name="add-the-package-online"></a>Adicionar o pacote online

Se o computador cliente que você usa para se conectar ao SQL Server tiver acesso à Internet, você poderá usar **sqlmlutils** para localizar o pacote **glue** e qualquer dependência pela Internet e, em seguida, instalar o pacote em uma instância do SQL Server remotamente.

1. No computador cliente, abra o RStudio e crie um novo arquivo de **Script R**.

1. Use o script R a seguir para instalar o pacote **glue** usando **sqlmlutils**. Substitua suas informações de conexão de banco de dados SQL Server (se você não usar a autenticação do Windows, adicione os parâmetros `uid` e `pwd`).

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase")

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC")
   ```

   > [!TIP]
   > O **escopo** pode ser **PUBLIC** ou **PRIVATE**. O escopo público é útil para o administrador de banco de dados instalar pacotes que todos os usuários podem usar. O escopo privado disponibiliza o pacote somente ao usuário que o instala. Se você não especificar o escopo, o padrão será **PRIVATE**.

### <a name="add-the-package-offline"></a>Adicionar o pacote offline

Se o computador cliente não tiver uma conexão com a Internet, você poderá usar **miniCRAN** para baixar o pacote do **Glue** usando um computador que tenha acesso à Internet. Em seguida, copie o pacote para o computador cliente no qual você pode instalar o pacote offline.
Confira [Instalar o miniCRAN](create-a-local-package-repository-using-minicran.md#install-minicran) para obter informações sobre como instalar o **miniCRAN**.

Em um computador com acesso à Internet:

1. Execute o script R a seguir para criar um repositório local para **glue**. Este exemplo cria a pasta do repositório em `c:\downloads\glue`.

   ::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/glue"
   pkgs_needed <- "glue"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```

   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/glue"
   pkgs_needed <- "glue"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "source", Rversion = "3.5");
   ```

   ::: moniker-end


   Para o valor `Rversion`, use a versão do R instalada no SQL Server. Para verificar a versão instalada, use o comando T-SQL a seguir.

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. Copie toda a pasta do repositório **glue** (`c:\downloads\glue`) para o computador cliente. Por exemplo, copie-a para a pasta `c:\temp\packages\glue`.

No computador cliente:

1. Abra o RStudio e crie um novo arquivo de **Script R**.

1. Use o script R a seguir para instalar o pacote **glue** usando **sqlmlutils**. Substitua suas informações de conexão de banco de dados SQL Server (se você não usar a autenticação do Windows, adicione os parâmetros `uid` e `pwd`).

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase")
   localRepo = "c:/temp/packages/glue"

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC", repos=paste0("file:///",localRepo))
   ```

   > [!TIP]
   > O **escopo** pode ser **PUBLIC** ou **PRIVATE**. O escopo público é útil para o administrador de banco de dados instalar pacotes que todos os usuários podem usar. O escopo privado disponibiliza o pacote somente ao usuário que o instala. Se você não especificar o escopo, o padrão será **PRIVATE**.

## <a name="use-the-package"></a>Usar o pacote

Depois da instalação do pacote **glue**, você pode usá-lo em um script R no SQL Server com o comando **sp_execute_external_script** do T-SQL.

1. Abra o Azure Data Studio ou o SSMS e conecte a seu banco de dados do SQL Server.

1. Execute o seguinte comando:

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
       , @script = N'
   library(glue)

   name <- "Fred"
   birthday <- as.Date("2020-06-14")
   text <- glue(''My name is {name} '',
   ''and my birthday is {format(birthday, "%A, %B %d, %Y")}.'')

   print(text)
         ';
   ```

    **Resultados**

    ```text
    My name is Fred and my birthday is Sunday, June 14, 2020.
    ```

## <a name="remove-the-package"></a>Remover o pacote

Se você quiser remover o pacote **glue**, execute o script R a seguir. Use a mesma variável de **conexão** definida anteriormente.

```R
sql_remove.packages(connectionString = connection, pkgs = "glue", scope = "PUBLIC")
```

## <a name="next-steps"></a>Próximas etapas

- Para obter informações sobre pacotes R instalados, confira [Obter informações do pacote R](r-package-information.md)
- Para obter ajuda para trabalhar com pacotes do R, confira [Dicas para usar pacotes do R](tips-for-using-r-packages.md)
- Para obter informações sobre como instalar pacotes do Python, confira [Instalar pacotes do Python com pip](install-additional-python-packages-on-sql-server.md)
- Para obter mais informações sobre os Serviços de Machine Learning do SQL Server, confira [O que é Serviços de Machine Learning do SQL Server (Python e R)?](../what-is-sql-server-machine-learning.md)
