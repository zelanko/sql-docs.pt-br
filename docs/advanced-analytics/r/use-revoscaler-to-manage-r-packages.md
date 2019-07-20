---
title: Como usar as funções RevoScaleR para localizar ou instalar pacotes do R
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: dafbe12c6304866dc36dde6fffec44da441e582f
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344826"
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>Como usar as funções RevoScaleR para localizar ou instalar pacotes R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O RevoScaleR 9.0.1 e posterior inclui funções para o gerenciamento de pacotes R um SQL Server contexto de computação. Essas funções podem ser usadas por não administradores remotos para instalar pacotes no SQL Server sem acesso direto ao servidor.

SQL Server 2017 Serviços de Machine Learning já inclui uma versão mais recente do RevoScaleR. SQL Server os clientes do 2016 R Services devem fazer uma [atualização de componente](../install/upgrade-r-and-python.md) para obter as funções de gerenciamento de pacote RevoScaleR. Para obter instruções sobre como recuperar a versão e o conteúdo do pacote, consulte [obter informações do pacote](../package-management/installed-package-information.md).

## <a name="revoscaler-functions-for-package-management"></a>Funções do RevoScaleR para gerenciamento de pacotes

A tabela a seguir descreve as funções usadas para a instalação e o gerenciamento do pacote R.

| Função | Descrição |
|----------|-------------|
| [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) | Determine o caminho da biblioteca de instâncias no SQL Server remoto. |
| [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) | Obtém o caminho para um ou mais pacotes no SQL Server remoto. |
| [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) | Chame essa função de um cliente R remoto para instalar pacotes em um SQL Server contexto de computação, seja de um repositório especificado ou lendo pacotes compactados salvos localmente. Essa função verifica se há dependências e garante que todos os pacotes relacionados possam ser instalados em SQL Server, assim como a instalação do pacote R no contexto de computação local. Para usar essa opção, você deve ter habilitado o gerenciamento de pacotes no servidor e no banco de dados. Os ambientes de cliente e de servidor devem ter a mesma versão do RevoScaleR. |
| [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) | Obtém uma lista de pacotes instalados no contexto de computação especificado. |
| [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) | Copie informações sobre uma biblioteca de pacotes entre o sistema de arquivos e o banco de dados, para o contexto de computação especificado. |
| [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages) | Remove pacotes de um contexto de computação especificado. Ele também computa dependências e garante que os pacotes que não são mais usados por outros pacotes no SQL Server sejam removidos, para liberar recursos. |

## <a name="prerequisites"></a>Pré-requisitos

+ [Habilitar o gerenciamento remoto de pacotes de R no SQL Server](r-package-how-to-enable-or-disable.md)

+ As versões do RevoScaleR devem ser as mesmas nos ambientes de cliente e de servidor. Para obter mais informações, consulte [obter informações do pacote](../package-management/installed-package-information.md).

+ Permissão para se conectar ao servidor e a um banco de dados e executar comandos do R. Você deve ser um membro de uma função de banco de dados que permita a instalação de pacotes na instância e no banco de dados especificados.

+ Os pacotes no **escopo compartilhado** podem ser instalados por usuários que pertencem `rpkgs-shared` à função em um banco de dados especificado. Todos os usuários nesta função podem desinstalar pacotes compartilhados.

+ Os pacotes no **escopo privado** podem ser instalados por qualquer usuário que pertença à `rpkgs-private` função em um banco de dados. No entanto, os usuários podem ver e desinstalar apenas seus próprios pacotes.

+ Os proprietários do banco de dados podem trabalhar com pacotes compartilhados ou privados.

## <a name="client-connections"></a>Conexões de cliente

Uma estação de trabalho cliente pode ser [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/install-on-windows) ou um [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) (cientistas de dados geralmente usam o Free Developer Edition) na mesma rede.

Ao chamar funções de gerenciamento de pacotes de um cliente R remoto, você deve criar um objeto de contexto de computação primeiro, usando a função [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) . Depois disso, para cada função de gerenciamento de pacote que você usar, passe o contexto de computação como um argumento.

A identidade do usuário normalmente é especificada ao definir o contexto de computação. Se você não especificar um nome de usuário e uma senha ao criar o contexto de computação, a identidade do usuário que executa o código R será usada.

1. Em uma linha de comando do R, defina uma cadeia de conexão para a instância e o banco de dados.
2. Use o construtor [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) para definir um contexto de computação SQL Server, usando a cadeia de conexão.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. Crie uma lista dos pacotes que você deseja instalar e salve a lista em uma variável de cadeia de caracteres.

    ```R
    packageList <- c("e1071", "mice")
    ```

4. Chame [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) e passe o contexto de computação e a variável de cadeia de caracteres que contém os nomes de pacote.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    Se forem necessários pacotes dependentes, eles também serão instalados, supondo que uma conexão com a Internet esteja disponível no cliente.
    
    Os pacotes são instalados usando as credenciais do usuário que está fazendo a conexão, no escopo padrão desse usuário.

## <a name="call-package-management-functions-in-stored-procedures"></a>Chamar funções de gerenciamento de pacotes em procedimentos armazenados

Você Cam executa funções de gerenciamento de `sp_execute_external_script`pacote dentro do. Quando você fizer isso, a função será executada usando o contexto de segurança do chamador do procedimento armazenado.

## <a name="examples"></a>Exemplos

Esta seção fornece exemplos de como usar essas funções de um cliente remoto ao se conectar a uma SQL Server instância ou banco de dados como o contexto de computação.

Para todos os exemplos, você deve fornecer uma cadeia de conexão ou um contexto de computação, que requer uma cadeia de conexão. Este exemplo fornece uma maneira de criar um contexto de computação para SQL Server:

```R
instance_name <- "computer-name/instance-name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

Dependendo de onde o servidor está localizado e do modelo de segurança, talvez seja necessário fornecer uma especificação de domínio e sub-rede na cadeia de conexão ou usar um logon do SQL. Por exemplo:

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>Obter caminho do pacote em um contexto de computação de SQL Server remota

Este exemplo obtém o caminho para o pacote **RevoScaleR** no contexto de computação, `sqlcc`.

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**Resultados**

"C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

> [!TIP]
> Se você tiver habilitado a opção para ver a saída do console do SQL, poderá obter mensagens de status da função que precede `print` a instrução. Depois de concluir o teste do código, defina `consoleOutput` como false no construtor de contexto de computação para eliminar mensagens.

### <a name="get-locations-for-multiple-packages"></a>Obter locais de vários pacotes

O exemplo a seguir obtém os caminhos para os pacotes **RevoScaleR** e **malha** , no contexto de computação `sqlcc`,. Para obter informações sobre vários pacotes, passe um vetor de cadeia de caracteres contendo os nomes dos pacotes.

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>Obter versões do pacote em um contexto de computação remota

Execute este comando em um console do R para obter o número da compilação e os números de versão dos pacotes instalados no contexto de computação, *sqlServer*.

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

**Resultados**

```text
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

[2] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/lattice"
```

### <a name="install-a-package-on-sql-server"></a>Instalar um pacote no SQL Server

Este exemplo instala o pacote de **previsão** e suas dependências no contexto de computação.

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>Remover um pacote do SQL Server

Este exemplo remove o pacote de **previsão** e suas dependências do contexto de computação.

  ```R
  pkgs <- c("forecast")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="synchronize-packages-between-database-and-file-system"></a>Sincronizar pacotes entre o banco de dados e o sistema de arquivos

O exemplo a seguir verifica o banco de dados **TestDB**e determina se todos os pacotes estão instalados no sistema de arquivos. Se alguns pacotes estiverem ausentes, eles serão instalados no sistema de arquivos.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

A sincronização de pacote funciona em uma base por banco de dados e por usuário. Para obter mais informações, consulte [sincronização de pacote R para SQL Server](../r/package-install-uninstall-and-sync.md).

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>Use um procedimento armazenado para listar pacotes no SQL Server

Execute este comando de Management Studio ou outra ferramenta que ofereça suporte a T-SQL, para obter uma lista de pacotes instalados na instância atual, `rxInstalledPackages` usando em um procedimento armazenado.

```sql
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

A `rxSqlLibPaths` função pode ser usada para determinar a biblioteca ativa usada pelo SQL Server serviços de Machine Learning. Esse script pode retornar apenas o caminho da biblioteca para o servidor atual. 

```sql
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
+ [Dicas para instalar pacotes de R](packages-installed-in-user-libraries.md)
+ [Pacotes padrão](../package-management/default-packages.md)