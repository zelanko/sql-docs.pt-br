---
title: Gerenciamento de pacotes de R para o SQL Server | Microsoft Docs
ms.custom: 
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 7
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f19982251b629d12215595685c0633b4c6b61c98
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="r-package-management-for-sql-server"></a>Gerenciamento de pacotes de R para o SQL Server

Este tópico descreve os recursos de gerenciamento de pacote que você pode usar para gerenciar pacotes de R em execução em uma instância do SQL Server.

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 serviços de aprendizado de máquina

## <a name="package-management-using-t-sql"></a>Gerenciamento de pacotes usando o T-SQL

Você pode continuar a instalar pacotes R como um administrador no computador, se você tiver esses privilégios, e se você for a única pessoa usando o servidor para trabalhos de aprendizado de máquina.

No entanto, se você precisa compartilhar pacotes com outras pessoas ou se precisam de várias pessoas executar tarefas de aprendizado de máquina no servidor, é mais eficiente para configurar uma biblioteca compartilhada de pacote. SQL Server oferece suporte a isso por meio de funções de banco de dados.

O administrador de banco de dados é responsável por configurar funções e adicionar usuários às funções. Por meio de funções, o administrador de banco de dados pode controlar quem tem permissão para adicionar ou remover pacotes de R de ambiente do SQL Server e pode fazer a auditoria de instalação do pacote.

### <a name="database-roles-for-package-management"></a>Funções de banco de dados para gerenciamento de pacotes

As novas funções de banco de dados a seguir dão suporte a uma instalação segura e gerenciamento de pacotes de R no SQL Server:

- `rpkgs-users`: Permite que os usuários usem qualquer compartilhados pacotes que foram instalados por membros do `rpkgs-shared` função.

- `rpkgs-private`: Fornece acesso aos pacotes compartilhados com as mesmas permissões que o `rpkgs-users` função. Os membros desta função também podem instalar, remover e usar pacotes com escopo definido como particular.

-  `rpkgs-shared`: Fornece as mesmas permissões que o `rpkgs-private` função. Os usuários que são membros dessa função também podem instalar ou remover pacotes compartilhados.

- `db_owner`: Tem as mesmas permissões que o `rpkgs-shared` função. Também pode conceder o aos usuários o direito de instalar ou remover pacotes compartilhados e privados.

### <a name="creating-an-external-package-library-using-t-sql"></a>Criar uma biblioteca de pacote externo usando o T-SQL

Além disso, o SQL Server 2017 suporta a instrução T-SQL, **criar biblioteca externa**, para dar suporte ao gerenciamento pelo administrador de banco de dados de bibliotecas externas. No momento, você pode usar essa instrução para criar bibliotecas com base em Windows adicionais de R. o suporte está planejado no futuro para pacotes do Python e para pacotes desenvolvidos para execução em outras plataformas, como o Linux.

Para obter mais informações, consulte [criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="package-management-using-r"></a>Gerenciamento de pacotes usando o R

O **RevoScaleR** pacote agora inclui funções para oferecer suporte a mais fácil instalação e gerenciamento de pacotes de R. Essas novas funções, combinadas com as funções de banco de dados para o gerenciamento de pacote, dá suporte a estes cenários:

- O cientista de dados pode instalar pacotes de R necessários no SQL Server sem ter acesso administrativo ao computador do SQL Server.
- Os pacotes são instalados em uma base por banco de dados, e quando o banco de dados é movido, os pacotes são movidas com ela.
- É fácil compartilhar pacotes com outras pessoas. Se você configurar um repositório de pacotes local, cada cientista de dados pode usar o repositório para instalar os pacotes em seu próprio banco de dados.
- O administrador de banco de dados não precisa saber como executar comandos de R e não precisa controlar as dependências de pacote complexo.
- O DBA pode usar funções de banco de dados familiares para controlar quais usuários do SQL Server têm permissão para instalar, desinstalar ou usar os pacotes.

### <a name="r-package-management-functions"></a>Funções de gerenciamento de pacote de R

As seguintes funções de gerenciamento de pacote são fornecidas em RevoScaleR, para instalação e remoção de pacotes em um contexto de computação especificado:

+ [rxInstalledPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstalledpackages): para obter informações sobre os pacotes instalados no contexto de computação especificado.

+ [rxInstallPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstallpackages): instalar os pacotes em um contexto de computação, de um repositório especificado ou lendo salvos localmente compactados pacotes.

+ [rxRemovePackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxremovepackages): remover os pacotes instalados em um contexto de computação.

+ [rxFindPackage](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxfindpackage): obter o caminho para um ou mais pacotes no contexto de computação especificado.

+ [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages): copia uma biblioteca de pacote entre o sistema de arquivos e bancos de dados em contextos de computação especificado.

+ [rxSqlLibPaths](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqllibpaths): obter o caminho de pesquisa para árvores de biblioteca de pacotes durante a execução dentro do SQL Server.

Esses pacotes também são incluídos por padrão no SQL Server 2017. Você pode adicionar os pacotes para uma instância do SQL Server 2016, se você atualizar a instância a ser usada pelo menos Microsoft R 9.0.1. Para obter mais informações, consulte [SqlBindR.exe usando atualizar R](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

Para obter informações sobre essas funções, consulte as páginas de referência de função RevoScaleR: (https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)

## <a name="how-package-management-works"></a>Como funciona o pacote de gerenciamento

Se você tiver permissão para instalar pacotes, você executa uma das funções de gerenciamento de pacote no código R e especifica o contexto de computação no qual pacotes devem ser adicionados ou removidos. O contexto de computação pode ser seu computador local ou um banco de dados na instância do SQL Server. Se a chamada para instalar pacotes é executada no SQL Server, suas credenciais vão determinar se é possível concluir a operação no servidor. As funções de instalação do pacote verificam se há dependências e certificam-se de que todos os pacotes relacionados possam ser instalados no SQL Server, assim como a instalação de pacote do R no contexto de computação local. A função que desinstala pacotes também calcula as dependências e garante que os pacotes que não são mais usados por outros pacotes no SQL Server sejam removidos para liberar recursos.

Cada cientista de dados pode instalar pacotes privados que não são visíveis para outras pessoas, a criação de uma área restrita privada pacotes R. Como os pacotes podem ser definidos para um banco de dados e cada usuário obtenha uma área restrita do pacote isolado em cada banco de dados, é mais fácil de instalar versões diferentes do mesmo pacote de R.

Se você migrar seu banco de dados do trabalho para um novo servidor, você pode usar a função de sincronização do pacote para ler uma lista de todos os seus pacotes e instalá-los em um banco de dados no novo servidor.

> [!NOTE]
> 
> As funções de R para o gerenciamento de pacote são fornecidas, começando com o Microsoft R Server 9.0.1. Se você não encontrar as funções RevoScaleR, você provavelmente precisará atualizar para a versão mais recente.

### <a name="bkmk_scope"></a>Escopo de pacotes por função

As novas funções de gerenciamento de pacote fornecem dois escopos para a instalação e o uso de pacotes no SQL Server em um determinado banco de dados:

- **Escopo compartilhado**

  *Escopo compartilhado* significa que os usuários que receberam permissão para a função de escopo compartilhado (`rpkgs-shared`) pode instalar e desinstalar pacotes para um banco de dados especificado. Um pacote que é instalado em uma biblioteca de escopo compartilhado pode ser usado por outros usuários do banco de dados do SQL Server, contanto que esses usuários tenham permissão para usar pacotes de R instalados.

- **Escopo particular**

  *Escopo particular* significa que os usuários que receberam associação na função de escopo particular (`rpkgs-private`) pode instalar ou desinstalar pacotes em um local de biblioteca particular definido por usuário. Portanto, todos os pacotes instalados no escopo particular podem ser usados somente pelo usuário que os instalou. Em outras palavras, um usuário do SQL Server não pode usar pacotes particulares que foram instalados por outro usuário.

Esses modelos de escopo *compartilhado* e *particular* podem ser combinados para desenvolver sistemas seguros personalizados para implantar e gerenciar pacotes no SQL Server.

Por exemplo, ao usar o escopo compartilhado, o líder ou o gerente de um grupo de cientistas de dados pode receber permissão para instalar pacotes e esses pacotes podem ser usados por todos os outros usuários ou os cientistas de dados na mesma instância do SQL Server.

Outro cenário poderia exigir maior isolamento entre usuários, ou o uso de diferentes versões de pacotes. Nesse caso, o escopo particular pode ser usado para fornecer permissões individuais aos cientistas de dados, que seriam responsáveis por instalar e usar apenas os pacotes que precisam. Como os pacotes são instalados em uma base individual, os pacotes instalados por um usuário não afetariam o trabalho de outros usuários que estão usando o mesmo banco de dados do SQL Server.

### <a name="synchronizing-r-package-libraries"></a>Sincronizando as bibliotecas do pacote de R

A versão do CTP 2.0 do SQL Server 2017 (e a versão de abril de 2017 do Microsoft R Server) incluem novas funções de R para *sincronizando pacotes*.

A sincronização do pacote significa que o mecanismo de banco de dados controla os pacotes que são usados por um proprietário específico e um grupo e podem gravar esses pacotes ao sistema de arquivos, se necessário. Você pode usar a sincronização do pacote nestes cenários:

+ Você deseja mover os pacotes de R entre instâncias do SQL Server
+ Você precisa reinstalar pacotes para um determinado usuário ou grupo depois de restaurar um banco de dados

Para obter mais informações, consulte [rxSyncPackages](../r/package-install-uninstall-and-sync.md).

## <a name="examples"></a>Exemplos

Esses exemplos demonstram o uso básico para as funções de gerenciamento de pacote. Para executar esses comandos requer que você tem permissão para executar comandos de R na instância.

+ Durante a execução de um terminal de R remoto, você cria um objeto de contexto de computação especificando uma instância do SQL Server e, em seguida, executar as funções, passando o contexto de computação como um argumento.

+ Para executar funções de gerenciamento de pacote de um procedimento armazenado, você deve colocá-los em uma chamada para `sp_execute_external_script`.

### <a name="package-scoping"></a>Escopo de pacote

Este exemplo verifica pacotes que foram instalados na instância `myServer`, no banco de dados `TestDB`. Gerenciamento de pacote está no escopo para um banco de dados específico e um usuário. Se o usuário não for especificado, o usuário que executa a chamada de contexto de computação será assumido. Para obter mais informações, consulte [escopo de pacotes por função](#bkmk_scope).

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;");
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerCompute);
```

### <a name="get-package-location-on-a-remote-sql-server-compute-context"></a>Obter o local do pacote em um contexto de computação do SQL Server remoto

Este exemplo obtém o caminho para o pacote **RevoScaleR** no contexto de computação *sqlServer*.

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```

### <a name="get-locations-for-multiple-packages"></a>Obter locais de vários pacotes

O exemplo a seguir obtém os caminhos para os pacotes **RevoScaleR** e **lattice** , no contexto de computação *sqlServer*. Para obter informações sobre os vários pacotes, passe um vetor de cadeia de caracteres que contém os nomes de pacote.

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```

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

### <a name="get-package-versions-on-a-remote-compute-context"></a>Obter versões de pacote em um contexto de computação remota

Execute este comando em um console de R para obter o número da compilação e os números de versão de pacotes instalados no contexto de computação, *sqlServer*.

  ```R
  sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

### <a name="install-a-package-on-sql-server"></a>Instalar um pacote no SQL Server

Este exemplo instala o pacote **ggplot2** e suas dependências no contexto de computação *sqlServer*.

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

### <a name="package-synchronization"></a>Sincronização de pacotes

O exemplo a seguir sincroniza os pacotes instalados no sistema de arquivos com a lista de pacotes gerenciados no banco de dados. Se alguns pacotes estiverem ausentes, elas são instaladas no sistema de arquivos.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

## <a name="next-steps"></a>Próximas etapas

[Como habilitar ou desabilitar o gerenciamento de pacotes de R](../r/r-package-how-to-enable-or-disable.md)

