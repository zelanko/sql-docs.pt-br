---
title: Usar o RevoScaleR para instalar pacotes de R
description: Saiba como usar as funções do RevoScaleR para instalar pacotes de R no SQL Server com Serviços de Machine Learning ou R Services.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/20/2019
ms.topic: how-to
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 7f2978cd971f2259d7155d9d6c69c32ffe923ee5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723933"
---
# <a name="use-revoscaler-to-install-r-packages"></a>Usar o RevoScaleR para instalar pacotes de R

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este artigo descreve como usar as funções do [RevoScaleR](../r/ref-r-revoscaler.md) (versão 9.0.1 e posterior) para instalar pacotes de R no SQL Server com os Serviços de Machine Learning ou R Services. As funções do RevoScaleR podem ser usadas por usuários remotos e não administradores para instalar pacotes no SQL Server sem acesso direto ao servidor.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
> [!NOTE]
> Clientes do SQL Server R Services devem fazer uma [atualização de componente](../install/upgrade-r-and-python.md) para obter funções de gerenciamento de pacotes do RevoScaleR. Para obter instruções sobre como recuperar a versão e o conteúdo do pacote, confira [obter informações do pacote do R](../package-management/r-package-information.md).
::: moniker-end

## <a name="revoscaler-functions-for-package-management"></a>Funções do RevoScaleR para o gerenciamento de pacotes

A tabela a seguir descreve as funções usadas para a instalação e o gerenciamento do pacote do R.

| Função | DESCRIÇÃO |
|----------|-------------|
| [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) | Determine o caminho da biblioteca de instâncias no SQL Server remoto. |
| [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) | Obtém o caminho para um ou mais pacotes no SQL Server remoto. |
| [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) | Chame essa função de um cliente R remoto para instalar pacotes em um contexto de computação do SQL Server, de um repositório especificado ou lendo pacotes compactados salvos localmente. Essa função verifica se há dependências e garante que todos os pacotes relacionados possam ser instalados no SQL Server, assim como a instalação de pacote do R no contexto de computação local. Para usar essa opção, você deve ter habilitado o gerenciamento de pacotes no servidor e no banco de dados. Os ambientes de cliente e de servidor devem ter a mesma versão do RevoScaleR. |
| [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) | Obtém uma lista de pacotes instalados no contexto de computação especificado. |
| [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) | Copie informações sobre uma biblioteca de pacotes entre o sistema de arquivos e o banco de dados, para o contexto de computação especificado. |
| [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages) | Remove pacotes de um contexto de computação especificado. Ela também calcula as dependências e garante que os pacotes que não são mais usados por outros pacotes no SQL Server sejam removidos para liberar recursos. |

## <a name="prerequisites"></a>Prerequisites

+ Gerenciamento remoto habilitado no SQL Server. Para obter mais informações, confira [Habilitar o gerenciamento de pacotes do R no SQL Server](r-package-how-to-enable-or-disable.md).

+ As versões do RevoScaleR são as mesmas em ambientes de cliente e de servidor. Para obter mais informações, confira [Obter informações sobre o pacote do R](../package-management/r-package-information.md).

+ Você tem permissão para se conectar ao servidor e a um banco de dados e executar comandos do R. Você deve ser um membro de uma função de banco de dados que permita a instalação de pacotes na instância e no banco de dados especificados.

  + Os pacotes no **escopo compartilhado** podem ser instalados por usuários que pertencem à função de `rpkgs-shared` em um banco de dados especificado. Todos os usuários nesta função podem desinstalar pacotes compartilhados.

  + Os pacotes no **escopo particular** podem ser instalados por usuários que pertencem à função de `rpkgs-private` em um banco de dados. No entanto, os usuários podem ver e desinstalar apenas os próprios pacotes.

  + Proprietários de banco de dados podem trabalhar com pacotes compartilhados ou particulares.

## <a name="client-connections"></a>Conexões de cliente

Uma estação de trabalho cliente pode ser [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/install-on-windows) ou um [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) (os cientistas de dados geralmente usam a edição de desenvolvedor gratuita) na mesma rede.

Ao chamar funções de gerenciamento de pacotes de um cliente R remoto, você deve criar um objeto de contexto de computação primeiro, usando a função [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver). Depois disso, para cada função de gerenciamento de pacotes que você usar, passe o contexto de computação como um argumento.

A identidade do usuário normalmente é especificada ao configurar o contexto de computação. Se você não especificar um nome de usuário e uma senha ao criar o contexto de computação, a identidade do usuário que executa o código R será usada.

1. Em uma linha de comando do R, defina uma cadeia de conexão para a instância e o banco de dados.
2. Use o construtor [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) para definir um contexto de computação do SQL Server, usando a cadeia de conexão.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. Crie uma lista dos pacotes que você deseja instalar e salve a lista em uma variável de cadeia de caracteres.

    ```R
    packageList <- c("e1071", "mice")
    ```

4. Chame [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) e passe o contexto de computação e a variável de cadeia de caracteres que contém os nomes dos pacotes.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    Se forem necessários pacotes dependentes, eles também serão instalados, supondo que uma conexão de Internet esteja disponível no cliente.
    
    Os pacotes são instalados usando as credenciais do usuário que está fazendo a conexão, no escopo padrão desse usuário.

## <a name="call-package-management-functions-in-stored-procedures"></a>Chamar funções de gerenciamento de pacotes em procedimentos armazenados

Você pode executar funções de gerenciamento de pacotes dentro de `sp_execute_external_script`. Quando você fizer isso, a função será executada usando o contexto de segurança do chamador do procedimento armazenado.

## <a name="examples"></a>Exemplos

Esta seção fornece exemplos de como usar essas funções de um cliente remoto ao se conectar a uma instância do SQL Server ou banco de dados como o contexto de computação.

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

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>Obter o caminho do pacote em um contexto de computação do SQL Server remoto

Este exemplo obtém o caminho para o pacote **RevoScaleR** no contexto de computação `sqlcc`.

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**Resultados**

"C:/Arquivos de Programas/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

> [!TIP]
> Se você tiver habilitado a opção para ver a saída do console do SQL, poderá obter mensagens de status da função que precede a instrução `print`. Após concluir o teste do código, defina `consoleOutput` como FALSE no construtor de contexto de computação para eliminar mensagens.

### <a name="get-locations-for-multiple-packages"></a>Obter locais de vários pacotes

O exemplo a seguir obtém os caminhos para os pacotes **RevoScaleR** e **lattice** no contexto de computação `sqlcc`. Ao encontrar informações sobre vários pacotes, passa um vetor de cadeia de caracteres que contém os nomes dos pacotes.

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>Obter versões do pacote em um contexto de computação remota

Execute este comando de um console do R para obter o número de build e os números de versão para pacotes instalados no contexto de computação *sqlServer*.

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

### <a name="install-a-package-on-sql-server"></a>Instalar um pacote no SQL Server

Este exemplo instala o pacote **forecast** e suas dependências no contexto de computação.

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>Remover um pacote do SQL Server

Este exemplo remove o pacote **forecast** e suas dependências do contexto de computação.

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

A sincronização de pacotes funciona em uma base por banco de dados e por usuário. Para obter mais informações, confira [Sincronização de Pacotes do R para o SQL Server](package-install-uninstall-and-sync.md).

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>Usar um procedimento armazenado para listar pacotes no SQL Server

Execute este comando do Management Studio ou outra ferramenta que dê suporte ao T-SQL, para obter uma lista de pacotes instalados na instância atual, usando `rxInstalledPackages` em um procedimento armazenado.

```sql
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

A função `rxSqlLibPaths` pode ser usada para determinar a biblioteca ativa usada por Serviços de Machine Learning do SQL Server. Esse script pode retornar apenas o caminho da biblioteca para o servidor atual. 

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
+ [Dicas para usar pacotes de R](tips-for-using-r-packages.md)
+ [Obter informações sobre o pacote do R](../package-management/r-package-information.md)