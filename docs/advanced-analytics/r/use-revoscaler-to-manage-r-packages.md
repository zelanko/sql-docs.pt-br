---
title: Como usar funções de RevoScaleR para localizar ou instalar o R pacotes no SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d92b3e993968ce48d7489b0c17d6bdba005809a3
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707524"
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>Como usar funções de RevoScaleR para localizar ou instalar pacotes R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR 9.0.1 e posteriores, inclui funções de gerenciamento de pacotes de R um contexto de computação do SQL Server. Essas funções podem ser usadas por não administradores remotos, para instalar os pacotes no SQL Server sem acesso direto ao servidor.

Serviços de aprendizado de máquina do SQL Server 2017 já inclui uma versão mais recente do RevoScaleR. Os clientes do SQL Server 2016 R Services devem fazer uma [atualização de componente](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md) obter funções de gerenciamento de pacote RevoScaleR. Para obter instruções sobre como recuperar o pacote de versão e o conteúdo, consulte [obter informações de pacote](determine-which-packages-are-installed-on-sql-server.md).

## <a name="revoscaler-functions-for-package-management"></a>Funções de RevoScaleR para gerenciamento de pacotes

A tabela a seguir descreve as funções usadas para gerenciamento e instalação de pacote de R.

| Função | Description |
|----------|-------------|
| [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) | Determine o caminho da biblioteca de instância no SQL Server remoto. |
| [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) | Obtém o caminho para um ou mais pacotes no SQL Server remoto. |
| [rxInstallPackages](https://docs.microsoft.com/en-us/machine-learning-server/r-reference/revoscaler/rxinstallpackages) | Chamar essa função de um cliente remoto do R para instalar os pacotes em um contexto de computação do SQL Server, a partir de um repositório especificado, ou lendo salvos localmente os pacotes compactados. Essa função verifica se há dependências e garante que todos os pacotes relacionados podem ser instalados no SQL Server, assim como a instalação do pacote de R no contexto de computação local. Para usar essa opção, você deve ter habilitado o gerenciamento de pacotes no servidor e banco de dados. Ambientes de cliente e o servidor devem ter a mesma versão do RevoScaleR. |
| [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) | Obtém uma lista de pacotes instalados no contexto de computação especificado. |
| [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) | Copie informações sobre uma biblioteca de pacote entre o sistema de arquivos e o banco de dados, para o contexto de computação especificado. |
| [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages) | Remove os pacotes de um contexto de computação especificado. Ele também calcula as dependências e garante que os pacotes que não são mais usados por outros pacotes no SQL Server são removidos para liberar recursos. |

## <a name="prerequisites"></a>Prerequisites

+ [Habilitar o gerenciamento remoto de pacote de R no SQL Server](r-package-how-to-enable-or-disable.md)

+ Versões de RevoScaleR devem ser o mesmo em ambientes de cliente e servidor. Para obter mais informações, consulte [obter informações de pacote](determine-which-packages-are-installed-on-sql-server.md).

+ Permissão para se conectar ao servidor e um banco de dados e executar comandos de R. Você deve ser um membro de uma função de banco de dados que permite que você instale os pacotes na instância especificada e banco de dados.

+ Pacotes em **escopo compartilhado** podem ser instalados pelos usuários que pertencem ao `rpkgs-shared` função em um banco de dados especificado. Todos os usuários nesta função podem desinstalar pacotes compartilhados.

+ Pacotes em **escopo particular** pode ser instalado por qualquer usuário que pertencem ao `rpkgs-private` função em um banco de dados. No entanto, os usuários podem ver e desinstalar somente seus próprios pacotes.

+ Os proprietários do banco de dados podem trabalhar com pacotes compartilhados ou privados.

## <a name="client-connections"></a>Conexões de cliente

Uma estação de trabalho cliente pode ser [o cliente do Microsoft R](https://docs.microsoft.com/machine-learning-server/r-client/install-on-windows) ou um [Microsoft Server de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) (cientistas de dados geralmente usam a edição de desenvolvedor gratuitas) na mesma rede.

Ao chamar funções de gerenciamento de pacote de um cliente remoto do R, você deve criar um objeto de contexto de computação em primeiro lugar, usando o [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) função. Depois disso, para cada função de gerenciamento de pacote que você usar, passe o contexto de computação como um argumento.

A identidade do usuário geralmente é especificada ao definir o contexto de computação. Se você não especificar um nome de usuário e senha ao criar o contexto de computação, a identidade do usuário que executa o código R é usada.

1. Em uma linha de comando de R, defina uma cadeia de conexão para a instância e banco de dados.
2. Use o [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) construtor para definir um contexto de computação do SQL Server, usando a cadeia de conexão.

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

    Se os pacotes dependentes forem necessários, eles também são instalados, supondo que uma conexão de internet está disponível no cliente.
    
    Os pacotes são instalados usando as credenciais do usuário que faz a conexão, no escopo padrão para esse usuário.

## <a name="call-package-management-functions-in-stored-procedures"></a>Chamar funções de gerenciamento de pacote em procedimentos armazenados

Cam executar funções de gerenciamento de pacote em `sp_execute_external_script`. Quando você fizer isso, a função é executada usando o contexto de segurança do chamador do procedimento armazenado.

## <a name="examples"></a>Exemplos

Esta seção fornece exemplos de como usar essas funções de um cliente remoto ao se conectar a uma instância do SQL Server ou banco de dados como o contexto de computação.

Para obter todos os exemplos, você deve fornecer uma cadeia de caracteres de conexão ou um contexto de computação, o que requer uma cadeia de caracteres de conexão. Este exemplo fornece uma maneira de criar um contexto de computação para o SQL Server:

```R
instance_name <- "computer-name/instance-name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

Dependendo de onde se encontra o servidor e o modelo de segurança, talvez seja necessário fornecer uma especificação de domínio e a sub-rede na cadeia de conexão, ou usar um logon do SQL. Por exemplo:

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>Obter o caminho de pacote em um contexto de computação do SQL Server remoto

Este exemplo obtém o caminho para o **RevoScaleR** pacote no contexto de computação, `sqlcc`.

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**Resultados**

"SQL de arquivos/Microsoft Server/MSSQL14 da unidade c: / programa. MSSQLSERVER/R_SERVICES/biblioteca/RevoScaleR"

> [!TIP]
> Se você tiver ativado a opção de ver a saída do console SQL, poderá receber mensagens de status da função que precede o `print` instrução. Depois de concluir o teste seu código, defina `consoleOutput` como FALSE no construtor de contexto de computação para eliminar as mensagens.

### <a name="get-locations-for-multiple-packages"></a>Obter locais de vários pacotes

O exemplo a seguir obtém os caminhos para a **RevoScaleR** e **entrelaçadas** pacotes, no contexto de computação, `sqlcc`. Para obter informações sobre os vários pacotes, passe um vetor de cadeia de caracteres que contém os nomes de pacote.

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>Obter versões de pacote em um contexto de computação remota

Execute este comando em um console de R para obter o número da compilação e os números de versão de pacotes instalados no contexto de computação, *sqlServer*.

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

**Resultados**

```text
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

[2] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/lattice"
```

### <a name="install-a-package-on-sql-server"></a>Instalar um pacote no SQL Server

Este exemplo instala o **previsão** pacote e suas dependências no contexto de computação.

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>Remover um pacote do SQL Server

Este exemplo remove o **previsão** pacote e suas dependências do contexto de computação.

  ```R
  pkgs <- c("forecast")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="synchronize-packages-between-database-and-file-system"></a>Sincronizar pacotes entre o banco de dados e sistema de arquivos

O exemplo a seguir verifica o banco de dados **TestDB**e determina se todos os pacotes estão instalados no sistema de arquivos. Se alguns pacotes estiverem ausentes, elas são instaladas no sistema de arquivos.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

A sincronização do pacote funciona em um por banco de dados e por usuário. Para obter mais informações, consulte [sincronização de pacotes de R para o SQL Server](../r/package-install-uninstall-and-sync.md).

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>Use um procedimento armazenado para listar os pacotes no SQL Server

Execute este comando do Management Studio ou outra ferramenta que dá suporte a T-SQL, para obter uma lista de pacotes instalados na instância atual, usando `rxInstalledPackages` em um procedimento armazenado.

```SQL
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

O `rxSqlLibPaths` função pode ser usada para determinar a biblioteca do active usada por serviços de aprendizado de máquina do SQL Server. Esse script pode retornar apenas o caminho da biblioteca para o servidor atual. 

```SQL
declare @instance_name nvarchar(100) = @@SERVERNAME, @database_name nvarchar(128) = db_name();
exec sp_execute_external_script 
  @language = N'R',
  @script = N'
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    .libPaths(rxSqlLibPaths(connStr));
    print(.libPaths());
  ', 
  @input_data_1 = N'', 
  @params = N'@instance_name nvarchar(100), @database_name nvarchar(128)',
  @instance_name = @instance_name, 
  @database_name = @database_name;
```

## <a name="see-also"></a>Confira também

+ [Habilitar o gerenciamento remoto de pacotes R](r-package-how-to-enable-or-disable.md)
+ [Sincronizar os pacotes R](package-install-uninstall-and-sync.md)
+ [Dicas para a instalação de pacotes de R](packages-installed-in-user-libraries.md)
+ [Pacotes padrão](installing-and-managing-r-packages.md)