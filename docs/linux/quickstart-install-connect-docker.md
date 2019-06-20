---
title: Introdução aos contêineres do Linux do SQL Server no Docker
titleSuffix: SQL Server
description: Neste início rápido mostra como usar o Docker para executar o SQL Server 2017 e imagens de contêiner de 2019. Em seguida, ele mostra como criar e consultar um banco de dados com sqlcmd.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/14/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.custom: sqlfreshmay19
ms.prod_service: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
zone_pivot_groups: cs1-command-shell
ms.openlocfilehash: 55061de57903d33c5f31c532f680fcf0c66684f9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66506559"
---
# <a name="quickstart-run-sql-server-container-images-with-docker"></a>Início Rápido: Executar imagens de contêiner do SQL Server com o Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Neste guia de início rápido, você usará o Docker para efetuar pull e executar a imagem de contêiner do SQL Server 2017, ou seja, a [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server). Em seguida, você se conectará à ferramenta **sqlcmd** para criar seu primeiro banco de dados e executar consultas.

> [!TIP]
> Se você quiser experimentar a imagem de visualização de 2019 do SQL Server, consulte o [versão de visualização do SQL Server 2019 deste artigo](quickstart-install-connect-docker.md?view=sql-server-linux-ver15).

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Neste início rápido, use o Docker para efetuar pull e executar a imagem de contêiner do SQL Server 2019 preview [mssql-server](https://hub.docker.com/r/microsoft/mssql-server). Em seguida, você se conectará à ferramenta **sqlcmd** para criar seu primeiro banco de dados e executar consultas.

> [!TIP]
> Neste início rápido cria contêineres de visualização do SQL Server 2019. Se você preferir criar contêineres do SQL Server 2017, consulte o [SQL Server 2017 versão deste artigo](quickstart-install-connect-docker.md?view=sql-server-linux-2017).
::: moniker-end

Esta imagem consiste no SQL Server em execução no Linux, com base no Ubuntu 16.04. Ela pode ser usada com o Docker Engine 1.8 ou superior no Linux ou no Docker para Mac/Windows. Este início rápido foca especificamente sobre como usar o SQL Server no **linux** imagem. A imagem do Windows não é abordada, mas há mais informações sobre ela na [página de Hub do Docker mssql-server-windows-developer](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/).

## <a id="requirements"></a> Pré-requisitos

- O Docker Engine 1.8 ou superior em qualquer distribuição do Linux ou do Docker para Mac/Windows com suporte. Para obter mais informações, veja [Install Docker](https://docs.docker.com/engine/installation/) (Instalar o Docker).
- Docker **overlay2** driver de armazenamento. Esse é o padrão para a maioria dos usuários. Se você achar que você não estiver usando esse provedor de armazenamento e precisa alterar, consulte as instruções e avisos na [documentação do docker para a configuração overlay2](https://docs.docker.com/storage/storagedriver/overlayfs-driver/#configure-docker-with-the-overlay-or-overlay2-storage-driver).
- Mínimo de 2 GB de espaço em disco.
- Mínimo de 2 GB de RAM.
- [Requisitos do sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

<!--The following H2 is versioned for 2017 and 2019. Much of the content is duplicated, so
any changes to one section should be duplicated in the other-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="pullandrun2017"></a> Efetuar pull e executar a imagem de contêiner

Antes de iniciar as etapas a seguir, certifique-se de que você selecionou o shell preferencial (bash, PowerShell ou cmd) na parte superior deste artigo.

1. Extrair a imagem de contêiner do SQL Server 2017 Linux de registro de contêiner do Microsoft.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   > [!TIP]
   > Se você quiser experimentar a imagem de visualização de 2019 do SQL Server, consulte o [versão de visualização do SQL Server 2019 deste artigo](quickstart-install-connect-docker.md?view=sql-server-linux-ver15#pullandrun2019).

   O comando anterior efetua pull da imagem de contêiner mais recente do SQL Server 2017. Se você quiser efetuar pull de uma imagem específica, adicione dois-pontos e o nome da marca (por exemplo, `mcr.microsoft.com/mssql/server:2017-GA-ubuntu`). Para ver todas as imagens disponíveis, consulte [a página de hub do Docker mssql-server](https://hub.docker.com/r/microsoft/mssql-server).

   ::: zone pivot="cs1-bash"
   Para os comandos de bash neste artigo, `sudo` é usado. No MacOS, `sudo` pode não ser necessário. No Linux, se você não quiser usar `sudo` para executar o Docker, você pode configurar uma **docker** de grupo e adicionar usuários a esse grupo. Para obter mais informações, consulte [etapas de pós-instalação para Linux](https://docs.docker.com/install/linux/linux-postinstall/).
   ::: zone-end

2. Para executar a imagem de contêiner com o Docker, você pode usar o comando a seguir de um shell bash (Linux/macOS) ou do prompt de comando do PowerShell elevado.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
      -p 1433:1433 --name sql1 \
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1433:1433 --name sql1 `
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1433:1433 --name sql1 `
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   > [!NOTE]
   > A senha deverá seguir a política de senha padrão do SQL Server, caso contrário, o contêiner não poderá instalar o SQL Server e deixará de funcionar. Por padrão, a senha deve ter pelo menos 8 caracteres e conter caracteres de três dos quatro conjuntos a seguir: Letras maiusculas, letras minúsculas, dígitos de Base 10 e símbolos. É possível examinar o log de erros executando o comando [docker logs](https://docs.docker.com/engine/reference/commandline/logs/).

   > [!NOTE]
   > Por padrão, isso cria um contêiner com a edição Developer do SQL Server 2017. O processo para executar edições de produção em contêineres é um pouco diferente. Para obter mais informações, veja [Executar imagens de contêiner de produção](sql-server-linux-configure-docker.md#production).

   A tabela a seguir fornece uma descrição dos parâmetros no exemplo de `docker run` anterior:

   | Parâmetro | Descrição |
   |-----|-----|
   | **-e 'ACCEPT_EULA=Y'** |  Defina a variável **ACCEPT_EULA** com qualquer valor para confirmar sua aceitação dos [Termos de Licença](https://go.microsoft.com/fwlink/?LinkId=746388). Configuração exigida para a imagem do SQL Server. |
   | **-e ' SA_PASSWORD =\<YourStrong! Passw0rd\>'** | Especifique sua própria senha forte que tenha pelo menos 8 caracteres e atenda aos [Requisitos de senha do SQL Server](../relational-databases/security/password-policy.md). Configuração exigida para a imagem do SQL Server. |
   | **-p 1433:1433** | Mapeie uma porta TCP no ambiente do host (primeiro valor) para uma porta TCP no contêiner (segundo valor). Neste exemplo, SQL Server está escutando na TCP 1433 no contêiner e isso é exposto para a porta 1433 no host. |
   | **--name sql1** | Especifique um nome personalizado para o contêiner em vez de um nome gerado aleatoriamente. Se você executar mais de um contêiner, não será possível reutilizar esse mesmo nome. |
   | **mcr.microsoft.com/mssql/server:2017-latest** | A imagem de contêiner do SQL Server 2017 do Linux. |

3. Para exibir seus contêineres do Docker, use o comando `docker ps`.


   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker ps -a
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker ps -a
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker ps -a
   ```
   ::: zone-end

   Será exibida uma saída semelhante à captura de tela a seguir:

   ![Saída do comando Docker ps](./media/sql-server-linux-setup-docker/docker-ps-command.png)

4. Se a coluna **STATUS** mostrar o status **Up**, o SQL Server estará em execução no contêiner e será escutado na porta especificada na coluna **PORTS**. Se a coluna **STATUS** do contêiner do SQL Server mostrar **Exited**, confira a [seção Solução de problemas do guia de configuração](sql-server-linux-configure-docker.md#troubleshooting).

O parâmetro `-h` (nome do host) também é útil, mas para simplificar, ele não é usado neste tutorial. Ele altera o nome interno do contêiner para um valor personalizado. Este é o nome que será retornado na consulta Transact-SQL a seguir:

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

Configurar `-h` e `--name` com o mesmo valor é uma boa maneira de identificar facilmente o contêiner de destino.

::: moniker-end
<!--End of 2017 "Pull and run" section-->

<!--This is the 2019 version of the "Pull and run" section-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="pullandrun2019"></a> Efetuar pull e executar a imagem de contêiner

Antes de iniciar as etapas a seguir, certifique-se de que você selecionou o shell preferencial (bash, PowerShell ou cmd) na parte superior deste artigo.

1. Extrair a visualização do SQL Server 2019 imagem de contêiner do Linux de Hub do Docker.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2019-CTP3.0-ubuntu
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2019-CTP3.0-ubuntu
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker pull mcr.microsoft.com/mssql/server:2019-CTP3.0-ubuntu
   ```
   ::: zone-end

   > [!TIP]
   > Este início rápido usa a imagem do Docker de visualização do SQL Server 2019. Se você quiser executar a imagem do SQL Server 2017, consulte o [SQL Server 2017 versão deste artigo](quickstart-install-connect-docker.md?view=sql-server-linux-2017#pullandrun2017).

   O comando anterior efetua pull de imagem de contêiner de visualização 2019 do SQL Server com base no Ubuntu. Em vez de usar imagens de contêiner com base no RedHat, consulte [imagens de contêiner com base em RHEL executar](sql-server-linux-configure-docker.md#rhel). Para ver todas as imagens disponíveis, veja [a página de hub do Docker mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server).

   ::: zone pivot="cs1-bash"
   Para os comandos de bash neste artigo, `sudo` é usado. No MacOS, `sudo` pode não ser necessário. No Linux, se você não quiser usar `sudo` para executar o Docker, você pode configurar uma **docker** de grupo e adicionar usuários a esse grupo. Para obter mais informações, consulte [etapas de pós-instalação para Linux](https://docs.docker.com/install/linux/linux-postinstall/).
   ::: zone-end

2. Para executar a imagem de contêiner com o Docker, você pode usar o comando a seguir de um shell bash (Linux/macOS) ou do prompt de comando do PowerShell elevado.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
      -p 1433:1433 --name sql1 \
      -d mcr.microsoft.com/mssql/server:2019-CTP3.0-ubuntu
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1433:1433 --name sql1 `
      -d mcr.microsoft.com/mssql/server:2019-CTP3.0-ubuntu
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1433:1433 --name sql1 `
      -d mcr.microsoft.com/mssql/server:2019-CTP3.0-ubuntu
   ```
   ::: zone-end

   > [!NOTE]
   > A senha deverá seguir a política de senha padrão do SQL Server, caso contrário, o contêiner não poderá instalar o SQL Server e deixará de funcionar. Por padrão, a senha deve ter pelo menos 8 caracteres e conter caracteres de três dos quatro conjuntos a seguir: Letras maiusculas, letras minúsculas, dígitos de Base 10 e símbolos. É possível examinar o log de erros executando o comando [docker logs](https://docs.docker.com/engine/reference/commandline/logs/).

   > [!NOTE]
   > Por padrão, isso cria um contêiner com a edição Developer do SQL Server 2019 visualização.

   A tabela a seguir fornece uma descrição dos parâmetros no exemplo de `docker run` anterior:

   | Parâmetro | Descrição |
   |-----|-----|
   | **-e 'ACCEPT_EULA=Y'** |  Defina a variável **ACCEPT_EULA** com qualquer valor para confirmar sua aceitação dos [Termos de Licença](https://go.microsoft.com/fwlink/?LinkId=746388). Configuração exigida para a imagem do SQL Server. |
   | **-e ' SA_PASSWORD =\<YourStrong! Passw0rd\>'** | Especifique sua própria senha forte que tenha pelo menos 8 caracteres e atenda aos [Requisitos de senha do SQL Server](../relational-databases/security/password-policy.md). Configuração exigida para a imagem do SQL Server. |
   | **-p 1433:1433** | Mapeie uma porta TCP no ambiente do host (primeiro valor) para uma porta TCP no contêiner (segundo valor). Neste exemplo, SQL Server está escutando na TCP 1433 no contêiner e isso é exposto para a porta 1433 no host. |
   | **--name sql1** | Especifique um nome personalizado para o contêiner em vez de um nome gerado aleatoriamente. Se você executar mais de um contêiner, não será possível reutilizar esse mesmo nome. |
   | **mcr.microsoft.com/mssql/server:2019-CTP3.0-ubuntu** | A imagem de contêiner do SQL Server de 2019 CTP3.0 Linux. |

3. Para exibir seus contêineres do Docker, use o comando `docker ps`.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker ps -a
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker ps -a
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker ps -a
   ```
   ::: zone-end

   Será exibida uma saída semelhante à captura de tela a seguir:

   ![Saída do comando Docker ps](./media/sql-server-linux-setup-docker/docker-ps-command.png)

4. Se a coluna **STATUS** mostrar o status **Up**, o SQL Server estará em execução no contêiner e será escutado na porta especificada na coluna **PORTS**. Se a coluna **STATUS** do contêiner do SQL Server mostrar **Exited**, confira a [seção Solução de problemas do guia de configuração](sql-server-linux-configure-docker.md#troubleshooting).

O parâmetro `-h` (nome do host) também é útil, mas para simplificar, ele não é usado neste tutorial. Ele altera o nome interno do contêiner para um valor personalizado. Este é o nome que será retornado na consulta Transact-SQL a seguir:

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

Configurar `-h` e `--name` com o mesmo valor é uma boa maneira de identificar facilmente o contêiner de destino.

::: moniker-end
<!--End of 2019 "Pull and run" section-->

## <a id="sapassword"></a> Alterar a senha SA

<!-- This section was pasted in from includes/sql-server-linux-change-docker-password.md, to better support zone pivots. 2019/02/11 -->

A conta **SA** é um administrador do sistema na instância do SQL Server que é criada durante a instalação. Depois de criar o contêiner do SQL Server, a variável de ambiente `MSSQL_SA_PASSWORD` especificada é detectável executando `echo $MSSQL_SA_PASSWORD` no contêiner. Para fins de segurança, altere sua senha SA.

1. Escolha uma senha forte para usar no usuário de SA.

1. Use `docker exec` para executar **sqlcmd** para alterar a senha usando o Transact-SQL. No exemplo a seguir, substitua a senha antiga `<YourStrong!Passw0rd>`e a nova senha, `<YourNewStrong!Passw0rd>`, com seus próprios valores de senha.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourStrong!Passw0rd>' \
      -Q 'ALTER LOGIN SA WITH PASSWORD="<YourNewStrong!Passw0rd>"'
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourStrong!Passw0rd>" `
      -Q "ALTER LOGIN SA WITH PASSWORD='<YourNewStrong!Passw0rd>'"
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourStrong!Passw0rd>" `
      -Q "ALTER LOGIN SA WITH PASSWORD='<YourNewStrong!Passw0rd>'"
   ```
   ::: zone-end

## <a name="connect-to-sql-server"></a>Conecte-se ao SQL Server

As etapas a seguir usam a ferramenta de linha de comando do SQL Server, a **sqlcmd**, dentro do contêiner para conectar-se ao SQL Server.

1. Use o comando `docker exec -it` para iniciar um shell bash interativo dentro do contêiner em execução. No exemplo a seguir, `sql1` é o nome especificado pelo parâmetro `--name` na criação do contêiner.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker exec -it sql1 "bash"
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker exec -it sql1 "bash"
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker exec -it sql1 "bash"
   ```
   ::: zone-end

2. Quando estiver dentro do contêiner, conecte-se localmente com a sqlcmd. A sqlcmd não está no caminho por padrão, portanto, você precisará especificar o caminho completo.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourNewStrong!Passw0rd>'
   ```

   > [!TIP]
   > É possível omitir a senha na linha de comando para receber uma solicitação para inseri-la.

3. Se isso funcionar, você será levado a um prompt de comando **sqlcmd**: `1>`.

## <a name="create-and-query-data"></a>Criar e consultar dados

As seções a seguir descrevem como usar o **sqlcmd** e o Transact-SQL para criar um novo banco de dados, adicionar dados e executar uma consulta simples.

### <a name="create-a-new-database"></a>Criar um novo banco de dados

As etapas a seguir criam um novo banco de dados denominado `TestDB`.

1. No prompt de comando **sqlcmd**, cole o seguinte comando Transact-SQL para criar um banco de dados de teste:

   ```sql
   CREATE DATABASE TestDB
   ```

2. Na próxima linha, grave uma consulta para retornar o nome de todos os bancos de dados do servidor:

   ```sql
   SELECT Name from sys.Databases
   ```

3. Os dois comandos anteriores não foram executados imediatamente. Digite `GO` em uma nova linha para executar os comandos anteriores:

   ```sql
   GO
   ```

### <a name="insert-data"></a>Inserir dados

Em seguida, crie uma nova tabela, `Inventory`, e insira duas novas linhas.

1. No prompt de comando **sqlcmd**, altere o contexto para o novo banco de dados `TestDB`:

   ```sql
   USE TestDB
   ```

2. Criar nova tabela denominada `Inventory`:

   ```sql
   CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)
   ```

3. Inserir dados na nova tabela:

   ```sql
   INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
   ```

4. Digite `GO` para executar os comandos anteriores:

   ```sql
   GO
   ```

### <a name="select-data"></a>Selecionar dados

Agora, execute uma consulta para retornar da tabela `Inventory`.

1. No prompt de comando **sqlcmd**, digite uma consulta que retorna linhas de tabela `Inventory` em que a quantidade é maior que 152:

   ```sql
   SELECT * FROM Inventory WHERE quantity > 152;
   ```

2. Execute o comando:

   ```sql
   GO
   ```

### <a name="exit-the-sqlcmd-command-prompt"></a>Saia do prompt de comando sqlcmd

1. Para encerrar a sessão **sqlcmd**, digite `QUIT`:

   ```sql
   QUIT
   ```

2. Para sair do prompt de comando interativo no contêiner, digite `exit`. O contêiner continuará a ser executado depois que você sair do shell bash interativo.

## <a id="connectexternal"></a> Conectar-se de fora do contêiner

Você também pode se conectar à instância do SQL Server em seu computador do Docker usando qualquer ferramenta externa do macOS, do Windows ou do Linux que seja compatível com conexões SQL.

As etapas a seguir usam a **sqlcmd** fora do contêiner para conectar-se ao SQL Server em execução no contêiner. Essas etapas consideram que as ferramentas de linha de comando do SQL Server já estejam instaladas fora do contêiner. Os mesmos princípios se aplicam ao usar outras ferramentas, mas o processo de conexão é exclusivo para cada ferramenta.

1. Localize o endereço IP do computador que hospeda o contêiner. No Linux, use **ifconfig** ou **ip addr**. No Windows, use **ipconfig**.

1. Neste exemplo, instale o **sqlcmd** ferramenta no computador cliente. Para obter mais informações, consulte [instalar o sqlcmd no Windows](../tools/sqlcmd-utility.md) ou [instalar sqlcmd no Linux](sql-server-linux-setup-tools.md).

1. Execute a sqlcmd especificando o endereço IP e a porta mapeada para a porta 1433 no seu contêiner. Neste exemplo, que é a mesma porta, 1433, na máquina host. Se você tiver especificado uma porta diferente de mapeada no computador host, você deve usá-lo aqui.

   ::: zone pivot="cs1-bash"
   ```bash
   sqlcmd -S <ip_address>,1433 -U SA -P '<YourNewStrong!Passw0rd>'
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   sqlcmd -S <ip_address>,1433 -U SA -P "<YourNewStrong!Passw0rd>"
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   sqlcmd -S <ip_address>,1433 -U SA -P "<YourNewStrong!Passw0rd>"
   ```
   ::: zone-end

1. Execute comandos Transact-SQL. Quando terminar, digite `QUIT`.

Outras ferramentas comuns para conectar-se ao SQL Server incluem:

- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [SSMS (SQL Server Management Studio) no Windows](sql-server-linux-manage-ssms.md)
- [Azure Data Studio](../azure-data-studio/what-is.md)
- [mssql-cli (Preview)](https://github.com/dbcli/mssql-cli/blob/master/doc/usage_guide.md)
- [O PowerShell Core](sql-server-linux-manage-powershell-core.md)

## <a name="remove-your-container"></a>Remover o contêiner

Se você quiser remover o contêiner do SQL Server usado neste tutorial, execute os seguintes comandos:

::: zone pivot="cs1-bash"
```bash
sudo docker stop sql1
sudo docker rm sql1
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker stop sql1
docker rm sql1
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker stop sql1
docker rm sql1
```
::: zone-end

> [!WARNING]
> Parar e remover um contêiner permanentemente exclui todos os dados do SQL Server no contêiner. Se você precisar preservar os dados, [crie e copie um arquivo de backup fora do contêiner](tutorial-restore-backup-in-sql-server-container.md) ou use uma [técnica de persistência de dados do contêiner](sql-server-linux-configure-docker.md#persist).

## <a name="docker-demo"></a>Demonstração do Docker

Agora que você já tentou usar a imagem de contêiner do SQL Server para Docker, é interessante saber como o Docker é usado para melhorar o desenvolvimento e o teste. O vídeo a seguir mostra como o Docker pode ser usado em um cenário de implantação e integração contínuas.

> [!VIDEO https://channel9.msdn.com/Events/Connect/2017/T152/player]

## <a name="next-steps"></a>Próximas etapas

Para obter um tutorial sobre como restaurar arquivos de backup do banco de dados em um contêiner, confira [Restaurar um banco de dados do SQL Server em um contêiner do Docker do Linux](tutorial-restore-backup-in-sql-server-container.md). Para explorar outros cenários, como a execução de vários contêineres, persistência de dados e solução de problemas, consulte [imagens de contêiner de configurar o SQL Server no Docker](sql-server-linux-configure-docker.md).

Além disso, confira o [repositório do GitHub mssql-docker](https://github.com/Microsoft/mssql-docker) para obter recursos, comentários e problemas conhecidos.
