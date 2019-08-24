---
title: Instalar novos pacotes de R com sqlmlutils
description: Saiba como usar o sqlmlutils para instalar novos pacotes de R em uma instância do SQL Server Serviços de Machine Learning ou SQL Server R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 579f4c4e236fcc9ee22067522c47a8286b869d51
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000783"
---
# <a name="install-new-r-packages-with-sqlmlutils"></a>Instalar novos pacotes de R com sqlmlutils

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve como usar funções no pacote [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) para instalar novos pacotes de R em uma instância do SQL Server Serviços de Machine Learning ou SQL Server R Services. Os pacotes que você instala podem ser usados em scripts R em execução no banco de dados usando a instrução T-SQL [SP-execute-external-script-Transact-SQL](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) .

> [!NOTE]
> O comando padrão `install.packages` do r não é recomendado para adicionar pacotes R em SQL Server. Em vez disso, use **sqlmlutils** conforme descrito neste artigo.

## <a name="prerequisites"></a>Pré-requisitos

- Instale o [R](https://www.r-project.org) e o [RStudio desktop](https://www.rstudio.com/products/rstudio/download/) no computador cliente que você usa para se conectar ao SQL Server. Você pode usar qualquer IDE R para executar scripts, mas este artigo pressupõe RStudio.

- Instale o [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) ou o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS) no computador cliente que você usa para se conectar ao SQL Server. Você pode usar outras ferramentas de consulta e gerenciamento de banco de dados, mas este artigo pressupõe Azure Data Studio ou SSMS.

### <a name="other-considerations"></a>Outras considerações

- O script R em execução no SQL Server pode usar apenas os pacotes instalados na biblioteca de instâncias padrão. SQL Server não pode carregar pacotes de bibliotecas externas, mesmo se essa biblioteca estiver no mesmo computador. Isso inclui bibliotecas de R instaladas com outros produtos da Microsoft.

- Em um ambiente de SQL Server protegido, talvez você queira evitar o seguinte:
  - Pacotes que exigem acesso à rede
  - Pacotes que exigem acesso elevado ao sistema de arquivos
  - Pacotes usados para desenvolvimento na Web ou outras tarefas que não se beneficiam com a execução dentro de SQL Server

## <a name="install-sqlmlutils-on-the-client-computer"></a>Instalar o sqlmlutils no computador cliente

Para usar o **sqlmlutils**, primeiro você precisa instalá-lo no computador cliente que você usa para se conectar ao SQL Server.

O pacote **sqlmlutils** depende do pacote **RODBCext** e **RODBCext** depende de vários outros pacotes. Os procedimentos a seguir instalam todos esses pacotes na ordem correta.

### <a name="install-sqlmlutils-online"></a>Instalar o sqlmlutils online

Se o computador cliente tiver acesso à Internet, você poderá baixar e instalar o **sqlmlutils** e seus pacotes dependentes online.

1. Baixe o arquivo zip **sqlmlutils** mais recente https://github.com/Microsoft/sqlmlutils/tree/master/R/dist do no computador cliente. Não Descompacte o arquivo.

1. Abra um **prompt de comando** e execute os comandos a seguir para instalar os pacotes **sqlmlutils** e **RODBCext**. Substitua o caminho completo para o arquivo zip **sqlmlutils** que você baixou (Este exemplo supõe que o arquivo está em sua pasta documentos). O pacote **RODBCext** é encontrado online e instalado.

   ```console
   R -e "install.packages('RODBCext', repos='https://cran.microsoft.com')"
   R CMD INSTALL %UserProfile%\Documents\sqlmlutils_0.7.1.zip
   ```

### <a name="install-sqlmlutils-offline"></a>Instalar o sqlmlutils offline

Se o computador cliente não tiver uma conexão com a Internet, você precisará baixar os pacotes **sqlmlutils** e **RODBCext** com antecedência usando um computador que tenha acesso à Internet. Em seguida, você pode copiar os arquivos para uma pasta no computador cliente e instalar os pacotes offline.

O pacote **RODBCext** tem vários pacotes dependentes, e a identificação de todas as dependências de um pacote é complicada. Recomendamos que você use [**miniCRAN**](https://andrie.github.io/miniCRAN/) para criar uma pasta de repositório local para o pacote que inclui todos os pacotes dependentes.
Para obter mais informações, consulte [criar um repositório de pacote R local usando miniCRAN](../r/create-a-local-package-repository-using-minicran.md).

O pacote **sqlmlutils** consiste em um único arquivo zip que você pode copiar para o computador cliente e instalar o.

Em um computador com acesso à Internet:

1. Instale o **miniCRAN**. Consulte [instalar miniCRAN](../r/create-a-local-package-repository-using-minicran.md#install-minicran) para obter detalhes.

1. No RStudio, execute o script R a seguir para criar um repositório local do pacote **RODBCext**. Este exemplo cria o repositório na pasta `c:\downloads\rodbcext`.

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

   Para o `Rversion` valor, use a versão do R instalada em SQL Server. Para verificar a versão instalada, use o comando T-SQL a seguir.

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. Baixe o arquivo zip **sqlmlutils** mais recente https://github.com/Microsoft/sqlmlutils/tree/master/R/dist de (não Descompacte o arquivo). Por exemplo, baixe o arquivo para `c:\downloads\sqlmlutils_0.7.1.zip`.

1. Copie toda a pasta do repositório RODBCext`c:\downloads\rodbcext`() e o arquivo zip sqlmlutils`c:\downloads\sqlmlutils_0.7.1.zip`() para o computador cliente. Por exemplo, copie-os para a `c:\temp\packages` pasta no computador cliente.

No computador cliente que você usa para se conectar ao SQL Server, abra um prompt de comando e execute os comandos a seguir para instalar o **RODBCext** e, em seguida, **sqlmlutils**.

```console
R -e "install.packages('RODBCext', repos='c:\temp\packages\rodbcext')"
R CMD INSTALL c:\temp\packages\sqlmlutils_0.7.1.zip
```

## <a name="add-an-r-package-on-sql-server"></a>Adicionar um pacote R no SQL Server

No exemplo a seguir, você adicionará o pacote de [**União**](https://cran.r-project.org/web/packages/glue/) a SQL Server.

### <a name="add-the-package-online"></a>Adicionar o pacote online

Se o computador cliente que você usa para se conectar ao SQL Server tiver acesso à Internet, você poderá usar o **sqlmlutils** para localizar o pacote de **União** e quaisquer dependências pela Internet e, em seguida, instalar o pacote em uma instância de SQL Server remotamente.

1. No computador cliente, abra RStudio e crie um novo arquivo de **script R** .

1. Use o script R a seguir para instalar o pacote de **União** usando **sqlmlutils**. Substitua suas próprias informações de conexão de banco de dados SQL Server.

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase",
     uid = "yoursqluser",
     pwd = "yoursqlpassword")

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC")
   ```

   > [!TIP]
   > O **escopo** pode ser **público** ou **privado**. O escopo público é útil para o administrador de banco de dados instalar pacotes que todos os usuários podem usar. O escopo privado disponibiliza o pacote somente para o usuário que o instala. Se você não especificar o escopo, o escopo padrão será **privado**.

### <a name="add-the-package-offline"></a>Adicionar o pacote offline

Se o computador cliente não tiver uma conexão com a Internet, você poderá usar o **miniCRAN** para baixar o pacote de **colagem** usando um computador que tenha acesso à Internet. Em seguida, copie o pacote para o computador cliente onde você pode instalar o pacote offline.
Consulte [instalar o miniCRAN](../r/create-a-local-package-repository-using-minicran.md#install-minicran) para obter informações sobre como instalar o **miniCRAN**.

Em um computador com acesso à Internet:

1. Execute o script R a seguir para criar um repositório local para **colar**. Este exemplo cria a pasta de repositório `c:\downloads\glue`no.

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


   Para o `Rversion` valor, use a versão do R instalada em SQL Server. Para verificar a versão instalada, use o comando T-SQL a seguir.

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. Copie toda a pasta do repositório de`c:\downloads\glue`União () para o computador cliente. Por exemplo, copie-o para a `c:\temp\packages\glue`pasta.

No computador cliente:

1. Abra RStudio e crie um novo arquivo de **script R** .

1. Use o script R a seguir para instalar o pacote de **União** usando **sqlmlutils**. Substitua suas próprias informações de conexão de banco de dados SQL Server.

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase",
     uid = "yoursqluser",
     pwd = "yoursqlpassword")
   localRepo = "c:/temp/packages/glue"

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC", repos=paste0("file:///",localRepo))
   ```

   > [!TIP]
   > O **escopo** pode ser **público** ou **privado**. O escopo público é útil para o administrador de banco de dados instalar pacotes que todos os usuários podem usar. O escopo privado disponibiliza o pacote somente para o usuário que o instala. Se você não especificar o escopo, o escopo padrão será **privado**.

## <a name="use-the-package"></a>Usar o pacote

Depois que o pacote de **colagem** for instalado, você poderá usá-lo em um script R no SQL Server com o comando T-SQL **sp_execute_external_script** .

1. Abra Azure Data Studio ou SSMS e conecte-se ao seu banco de dados de SQL Server.

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

Se você quiser remover o pacote de **cola** , execute o seguinte script R. Use a mesma variável de **conexão** que você definiu anteriormente.

```R
sql_remove.packages(connectionString = connection, pkgs = "glue", scope = "PUBLIC")
```

## <a name="next-steps"></a>Próximas etapas

- Para obter informações sobre pacotes R instalados, consulte [obter informações de pacote de r](r-package-information.md)
- Para obter ajuda para trabalhar com pacotes de R, consulte [dicas para usar pacotes de r](../r/packages-installed-in-user-libraries.md)
- Para obter informações sobre como instalar pacotes do Python, consulte [instalar pacotes do Python com Pip](install-additional-python-packages-on-sql-server.md)
- Para obter mais informações sobre SQL Server Serviços de Machine Learning, consulte [o que é SQL Server serviços de Machine Learning (Python e R)?](../what-is-sql-server-machine-learning.md)
