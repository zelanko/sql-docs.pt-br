---
title: Instalar os novos pacotes R
description: Saiba como usar o sqlmlutils para instalar novos pacotes de R em uma instância de Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/04/2020
ms.topic: how-to
author: garyericson
ms.author: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: d3f7c61420dc1b85f7f40854dce9931d25aef895
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870487"
---
# <a name="install-new-r-packages-with-sqlmlutils"></a>Instalar novos pacotes de R com sqlmlutils

[!INCLUDE [SQL Server 2019 SQL MI](../../includes/applies-to-version/sqlserver2019-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Este artigo descreve como usar funções no pacote [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) para instalar novos pacotes do R em uma instância dos [Serviços de Machine Learning no SQL Server](../sql-server-machine-learning-services.md) e em [Clusters de Big Data](../../big-data-cluster/machine-learning-services.md). Os pacotes que você instalar poderão ser usados em scripts R em execução no banco de dados usando a instrução T-SQL [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

> [!NOTE]
> O pacote **sqlmlutils** descrito neste artigo é usado para adicionar pacotes do R ao SQL Server 2019 ou posterior. Para o SQL Server 2017 e anterior, confira [Instalar pacotes com ferramentas do R](./install-r-packages-standard-tools.md?view=sql-server-2017).
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
Este artigo descreve como usar funções no pacote [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) para instalar novos pacotes do R em uma instância dos [Serviços de Machine Learning da Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview). Os pacotes que você instalar poderão ser usados em scripts R em execução no banco de dados usando a instrução T-SQL [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
::: moniker-end

## <a name="prerequisites"></a>Pré-requisitos

- Instale o [R](https://www.r-project.org) e o [RStudio Desktop](https://www.rstudio.com/products/rstudio/download/) no computador cliente que você usa para conectar-se ao SQL Server. Você pode usar qualquer IDE do R para executar scripts, mas este artigo pressupõe o RStudio.

- Instale o [Azure Data Studio](../../azure-data-studio/what-is.md) no computador cliente que você usa para se conectar ao SQL Server. Você pode usar outras ferramentas de consulta ou gerenciamento de banco de dados, mas este artigo pressupõe o uso do Azure Data Studio.

### <a name="other-considerations"></a>Outras considerações

- A instalação do pacote é específica da instância SQL, banco de dados e usuários especificados por você nas informações de conexão fornecidas para **sqlmlutils**. Para usar o pacote em várias instâncias ou bancos de dados SQL, ou para diferentes usuários, você precisará instalar o pacote para cada um. Com uma exceção: se o pacote for instalado por um membro de `dbo`, ele será *público* e compartilhado com todos os usuários. Se um usuário instalar uma versão mais recente de um pacote público, este não será afetado, mas o usuário terá acesso à versão mais recente.

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

1. Baixe o arquivo mais recente do **sqlmlutils** (`.zip` para Windows, `.tar.gz` para Linux) de https://github.com/Microsoft/sqlmlutils/tree/master/R/dist para o computador cliente. Não expanda o arquivo.

1. Abra um **Prompt de Comando** e execute os comandos a seguir para instalar os pacotes **RODBCext** e **sqlmlutils**. Substitua o caminho para o arquivo de **sqlmlutils** que você baixou. O pacote **RODBCext** é encontrado online e instalado.

   ::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
   ```console
   R -e "install.packages('RODBCext', repos='https://mran.microsoft.com/snapshot/2019-02-01/')"
   R CMD INSTALL sqlmlutils_0.7.1.zip
   ```
   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
   ```console
   R -e "install.packages('RODBCext', repos='https://mran.microsoft.com/snapshot/2019-02-01/')"
   R CMD INSTALL sqlmlutils_0.7.1.tar.gz
   ```
   ::: moniker-end

### <a name="install-sqlmlutils-offline"></a>Instalar o sqlmlutils offline

Se o computador cliente não tiver uma conexão com a Internet, você precisará baixar os pacotes **RODBCext** e **sqlmlutils** com antecedência usando um computador que tenha acesso à Internet. Em seguida, você pode copiar os arquivos para uma pasta no computador cliente e instalar os pacotes offline.

O pacote **RODBCext** tem vários pacotes dependentes, o que complica a identificação de todas as dependências de um pacote. Recomendamos usar [**miniCRAN**](https://andrie.github.io/miniCRAN/) para criar uma pasta de repositório local para o pacote que inclua todos os pacotes dependentes.
Para mais informações, confira [Criar um repositório de pacotes do R local usando o miniCRAN](create-a-local-package-repository-using-minicran.md).

O pacote **sqlmlutils** consiste em um único arquivo que você pode copiar para o computador cliente e instalar.

Em um computador com acesso à Internet:

1. Instalar o **miniCRAN**. Confira [Instalar o miniCRAN](create-a-local-package-repository-using-minicran.md#install-minicran) para obter detalhes.

1. No RStudio, execute o seguinte script R para criar um repositório local do pacote **RODBCext**. Este exemplo supõe que o repositório será criado na pasta `rodbcext`.

   ::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
   ```R
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2019-02-01/")
   local_repo <- "rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```
   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
   ```R
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2019-02-01/")
   local_repo <- "rodbcext"
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

1. Baixe o arquivo de **sqlmlutils** mais recente (`.zip` para Windows, `.tar.gz` para Linux) de [https://github.com/Microsoft/sqlmlutils/tree/master/R/dist](https://github.com/Microsoft/sqlmlutils/tree/master/R/dist). Não expanda o arquivo.

1. Copie toda a pasta do repositório **RODBCext** e o arquivo de **sqlmlutils** para o computador cliente.

No computador cliente que você usa para se conectar ao SQL Server:

1. Abra um prompt de comando.

1. Execute os comandos a seguir para instalar **RODBCext** e depois **sqlmlutils**. Substitua os caminhos completos para a pasta do repositório **RODBCext** e para o arquivo **sqlmlutils** que você copiou neste computador.

   ::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
   ```console
   R -e "install.packages('RODBCext', repos='rodbcext')"
   R CMD INSTALL sqlmlutils_0.7.1.zip
   ```
   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
   ```console
   R -e "install.packages('RODBCext', repos='rodbcext')"
   R CMD INSTALL sqlmlutils_0.7.1.tar.gz
   ```
   ::: moniker-end

## <a name="add-an-r-package-on-sql-server"></a>Adicionar um pacote do R no SQL Server

No exemplo a seguir, você adicionará o pacote [**glue**](https://cran.r-project.org/web/packages/glue/) ao SQL Server.

### <a name="add-the-package-online"></a>Adicionar o pacote online

Se o computador cliente que você usa para se conectar ao SQL Server tiver acesso à Internet, você poderá usar **sqlmlutils** para localizar o pacote **glue** e qualquer dependência pela Internet e, em seguida, instalar o pacote em uma instância do SQL Server remotamente.

1. No computador cliente, abra o RStudio e crie um novo arquivo de **Script R**.

1. Use o script R a seguir para instalar o pacote **glue** usando **sqlmlutils**. Substitua suas informações de conexão de banco de dados do SQL Server.

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server   = "server",
     database = "database",
     uid      = "username",
     pwd      = "password")

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC")
   ```

   > [!TIP]
   > O **escopo** pode ser **PÚBLICO** ou **PRIVADO**. O escopo público é útil para o administrador de banco de dados instalar pacotes que todos os usuários podem usar. O escopo privado disponibiliza o pacote apenas para o usuário que o instala. Se você não especificar o escopo, o escopo padrão será **PRIVADO**.

### <a name="add-the-package-offline"></a>Adicionar o pacote offline

Se o computador cliente não tiver uma conexão com a Internet, você poderá usar **miniCRAN** para baixar o pacote do **Glue** usando um computador que tenha acesso à Internet. Em seguida, copie o pacote para o computador cliente no qual você pode instalar o pacote offline.
Confira [Instalar o miniCRAN](create-a-local-package-repository-using-minicran.md#install-minicran) para obter informações sobre como instalar o **miniCRAN**.

Em um computador com acesso à Internet:

1. Execute o script R a seguir para criar um repositório local para **glue**. Este exemplo cria a pasta do repositório em `c:\downloads\glue`.

   ::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
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

1. Abra RStudio e crie um arquivo **R Script**.

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
   > O **escopo** pode ser **PÚBLICO** ou **PRIVADO**. O escopo público é útil para o administrador de banco de dados instalar pacotes que todos os usuários podem usar. O escopo privado disponibiliza o pacote apenas para o usuário que o instala. Se você não especificar o escopo, o escopo padrão será **PRIVADO**.

## <a name="use-the-package"></a>Usar o pacote

Depois da instalação do pacote **glue**, você pode usá-lo em um script R no SQL Server com o comando **sp_execute_external_script** do T-SQL.

1. Abra o Azure Data Studio e conecte-se ao seu banco de dados do SQL Server.

1. Execute o comando a seguir:

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
- Para obter mais informações sobre os Serviços de Machine Learning do SQL Server, confira [O que é Serviços de Machine Learning do SQL Server (Python e R)?](../sql-server-machine-learning-services.md)