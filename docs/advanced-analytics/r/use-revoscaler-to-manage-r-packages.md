---
title: "Como usar funções de RevoScaleR para localizar ou instalar o R pacotes no SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 59f13d7c65818b49025f8578068b348c650e98c2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>Como usar funções de RevoScaleR para localizar ou instalar pacotes R no SQL Server

Versão do Microsoft R Server 9.0.1 introduziu novas funções de RevoScaleR que suportam trabalhar com pacotes instalados em um contexto de computação do SQL Server. Essas novas funções de tornar mais fácil para um cientista de dados executar código R no SQL Server sem acesso direto ao servidor.

Cada cientista de dados pode instalar pacotes privados que não são visíveis para outras pessoas. Como os pacotes podem ser definidos para um banco de dados e cada usuário obtenha uma área restrita do pacote isolado em cada banco de dados, é mais fácil de instalar versões diferentes do mesmo pacote de R.

Se você migrar seu banco de dados do trabalho para um novo servidor, você também pode usar a função de sincronização do pacote para ler uma lista de todos os seus pacotes e instalá-los em um banco de dados no novo servidor.

Este artigo descreve essas funções e fornece exemplos de uso da função.

## <a name="requirements"></a>Requisitos

+ Para executar essas funções, você deve ter permissão para executar comandos de R na instância.

+ Se você não especificar um nome de usuário e senha ao criar o contexto de computação, a identidade do usuário que executa o código R é usada.

+ Ao usar essas funções de um cliente remoto do R, você deve criar um objeto de contexto de computação em primeiro lugar, usando a função RxInSQLServer. Depois disso, para cada função de gerenciamento de pacote que você usar, passe o contexto de computação como um argumento.

+ É possível executar funções de gerenciamento de pacote usando `sp_execute_external_script`. Quando você fizer isso, a função é executada usando o contexto de segurança do chamador do procedimento armazenado.

## <a name="list-of-package-management-functions"></a>Lista de funções de gerenciamento de pacote

As seguintes funções de gerenciamento de pacote são fornecidas em RevoScaleR, para instalação e remoção de pacotes em um contexto de computação especificado:

+ [rxInstalledPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstalledpackages): para obter informações sobre os pacotes instalados no contexto de computação especificado.

+ [rxInstallPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstallpackages): instalar os pacotes em um contexto de computação, de um repositório especificado ou lendo salvos localmente compactados pacotes.

+ [rxRemovePackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxremovepackages): remover os pacotes instalados em um contexto de computação.

+ [rxFindPackage](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxfindpackage): obter o caminho para um ou mais pacotes no contexto de computação especificado.

+ [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages): copia uma biblioteca de pacote entre o sistema de arquivos e bancos de dados em contextos de computação especificado.

+ [rxSqlLibPaths](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqllibpaths): obter o caminho de pesquisa para árvores de biblioteca de pacotes durante a execução dentro do SQL Server.

Esses pacotes são incluídos por padrão no SQL Server 2017. Para obter informações sobre essas funções, consulte as páginas de referência de função RevoScaleR: (https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)

> [!NOTE]
> Funções de R para gerenciamento de pacotes estão disponível a partir do Microsoft R Server 9.0.1. Se você não encontrar as funções RevoScaleR, você provavelmente precisará atualizar para a versão mais recente. 
## <a name="examples"></a>Exemplos

Esta seção contém exemplos de como usar as funções de gerenciamento de pacote com uma instância do SQL Server ou um banco de dados. 

+ As funções de instalação do pacote verificam se há dependências e certificam-se de que todos os pacotes relacionados possam ser instalados no SQL Server, assim como a instalação de pacote do R no contexto de computação local.

+ A função que _desinstala_ pacotes também calcula as dependências e garante que os pacotes que não são mais usados por outros pacotes no SQL Server são removidos para liberar recursos.

+ Você pode usar uma combinação de usuários e o escopo para localizar pacotes ou adicionar pacotes para um determinado banco de dados:

    + Pacotes em **escopo compartilhado** podem ser instalados pelos usuários que pertencem ao `rpkgs-shared` função em um banco de dados especificado. Todos os usuários nesta função podem desinstalar pacotes compartilhados.
    + Pacotes em **escopo particular** pode ser instalado por qualquer usuário que pertencem ao `rpkgs-private` função em um banco de dados. No entanto, os usuários podem ver e desinstalar somente seus próprios pacotes.
    + Os proprietários do banco de dados podem trabalhar com pacotes compartilhados ou privados.

**No código de R**

Se você tiver permissão para instalar os pacotes, executar um pacote funções de gerenciamento de seu cliente de R e especifique o contexto de computação onde os pacotes devem ser adicionados ou removidos.  O contexto de computação pode ser seu computador local ou um banco de dados na instância do SQL Server. Suas credenciais de determinam se é possível concluir a operação no servidor.

**No Transact-SQL**

Para executar funções de gerenciamento de pacote de um procedimento armazenado, encapsulá-los em uma chamada para `sp_execute_external_script`.

### <a name="get-list-of-packages-in-a-sql-server-compute-context"></a>Obter lista de pacotes em um contexto de computação do SQL Server

Este exemplo verifica pacotes que foram instalados na instância `myServer`, no banco de dados `TestDB`. Gerenciamento de pacote está no escopo para um banco de dados específico e um usuário. Se o usuário não for especificado, o usuário que executa a chamada de contexto de computação será assumido. Para obter mais informações, consulte [escopo de pacotes por função](#bkmk_scope).

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;");
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerCompute);
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>Obter o caminho de pacote em um contexto de computação do SQL Server remoto

Este exemplo obtém o caminho para o pacote **RevoScaleR** no contexto de computação *sqlServer*.

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```

### <a name="get-locations-for-multiple-packages"></a>Obter locais de vários pacotes

O exemplo a seguir obtém os caminhos para os pacotes **RevoScaleR** e **lattice** , no contexto de computação *sqlServer*. Para obter informações sobre os vários pacotes, passe um vetor de cadeia de caracteres que contém os nomes de pacote.

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```


### <a name="get-package-versions-on-a-remote-compute-context"></a>Obter versões de pacote em um contexto de computação remota

Execute este comando em um console de R para obter o número da compilação e os números de versão de pacotes instalados no contexto de computação, *sqlServer*.

  ```R
  sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

### <a name="install-a-package-on-sql-server"></a>Instalar um pacote no SQL Server

Este exemplo instala o **previsão** pacote e suas dependências no contexto de computação, *sqlServer*.

  ```R
  pkgs <- c("ggplot2")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

### <a name="remove-a-package-from-sql-server"></a>Remover um pacote do SQL Server

Este exemplo remove o pacote **ggplot2** e suas dependências do contexto de computação *sqlServer*.

  ```R
  pkgs <- c("ggplot2")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
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
