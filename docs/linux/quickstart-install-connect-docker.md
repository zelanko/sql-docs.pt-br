---
title: Introdução ao SQL Server 2017 no Docker | Microsoft Docs
description: Este guia de início rápido mostra como usar o Docker para executar a imagem de contêiner do SQL Server 2017. Em seguida, ele mostra como criar e consultar um banco de dados com sqlcmd.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/07/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.workload: Active
ms.openlocfilehash: d422a4a755061837c08a6f4f8de4e1889768ac5d
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="quickstart-run-the-sql-server-2017-container-image-with-docker"></a>Início rápido: Executar a imagem de contêiner de 2017 do SQL Server com o Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Neste guia de início rápido, você usará o Docker para efetuar pull e executar a imagem de contêiner do SQL Server 2017, ou seja, a [mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/). Em seguida, você se conectará à ferramenta **sqlcmd** para criar seu primeiro banco de dados e executar consultas.

Esta imagem consiste no SQL Server em execução no Linux, com base no Ubuntu 16.04. Ela pode ser usada com o Docker Engine 1.8 ou superior no Linux ou no Docker para Mac/Windows.

> [!NOTE]
> Este guia de início rápido concentra-se especificamente no uso da imagem mssql-server-**linux**. A imagem do Windows não é abordada, mas há mais informações sobre ela na [página de Hub do Docker mssql-server-windows-developer](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/).

## <a id="requirements"></a> Pré-requisitos

- O Docker Engine 1.8 ou superior em qualquer distribuição do Linux ou do Docker para Mac/Windows com suporte. Para obter mais informações, veja [Install Docker](https://docs.docker.com/engine/installation/) (Instalar o Docker).
- Mínimo de 2 GB de espaço em disco
- Mínimo de 2 GB de RAM
- [Requisitos do sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

## <a name="pull-and-run-the-container-image"></a>Efetuar pull e executar a imagem de contêiner

1. Efetue pull da imagem de contêiner do SQL Server 2017 do Linux por meio do Hub do Docker.

   ```bash
   sudo docker pull microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker pull microsoft/mssql-server-linux:2017-latest
   ```

   O comando anterior efetua pull da imagem de contêiner mais recente do SQL Server 2017. Se você quiser efetuar pull de uma imagem específica, adicione dois-pontos e o nome da marca (por exemplo, `microsoft/mssql-server-linux:2017-GA`). Para ver todas as imagens disponíveis, veja [a página de hub do Docker mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/).
   
   Para os comandos de bash neste artigo, `sudo` é usado. Em MacOS, `sudo` talvez não seja necessário. No Linux, se você não quiser usar `sudo` para executar o Docker, você pode configurar um **docker** grupo e adicionar usuários a esse grupo. Para obter mais informações, consulte [as etapas de pós-instalação para Linux](https://docs.docker.com/install/linux/linux-postinstall/).

1. Para executar a imagem de contêiner com o Docker, você pode usar o comando a seguir de um shell bash (Linux/macOS) ou do prompt de comando do PowerShell elevado.

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -p 1401:1433 --name sql1 \
      -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1401:1433 --name sql1 `
      -d microsoft/mssql-server-linux:2017-latest
   ```

   > [!NOTE]
   > A senha deverá seguir a política de senha padrão do SQL Server, caso contrário, o contêiner não poderá instalar o SQL Server e deixará de funcionar. Por padrão, a senha deve ter pelo menos 8 caracteres e conter caracteres de três dos quatro conjuntos a seguir: letras maiúsculas, letras minúsculas, dígitos de Base 10 e símbolos. É possível examinar o log de erros executando o comando [docker logs](https://docs.docker.com/engine/reference/commandline/logs/).

   > [!NOTE]
   > Por padrão, isso cria um contêiner com a edição Developer do SQL Server 2017. O processo para executar edições de produção em contêineres é um pouco diferente. Para obter mais informações, veja [Executar imagens de contêiner de produção](sql-server-linux-configure-docker.md#production).

   A tabela a seguir fornece uma descrição dos parâmetros no exemplo de `docker run` anterior:

   | Parâmetro | Description |
   |-----|-----|
   | **-e 'ACCEPT_EULA=Y'** |  Defina a variável **ACCEPT_EULA** com qualquer valor para confirmar sua aceitação dos [Termos de Licença](http://go.microsoft.com/fwlink/?LinkId=746388). Configuração exigida para a imagem do SQL Server. |
   | **-e 'MSSQL_SA_PASSWORD=\<YourStrong!Passw0rd\>'** | Especifique sua própria senha forte que tenha pelo menos 8 caracteres e atenda aos [Requisitos de senha do SQL Server](../relational-databases/security/password-policy.md). Configuração exigida para a imagem do SQL Server. |
   | **-p 1401:1433** | Mapeie uma porta TCP no ambiente do host (primeiro valor) para uma porta TCP no contêiner (segundo valor). Neste exemplo, o SQL Server está escutando na TCP 1433 no contêiner e isso é exposto para a porta 1401 no host. |
   | **--name sql1** | Especifique um nome personalizado para o contêiner em vez de um nome gerado aleatoriamente. Se você executar mais de um contêiner, não será possível reutilizar esse mesmo nome. |
   | **microsoft/mssql-server-linux:2017-latest** | A imagem de contêiner do SQL Server 2017 do Linux. |

1. Para exibir seus contêineres do Docker, use o comando `docker ps`.

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

   Será exibida uma saída semelhante à captura de tela a seguir:

   ![Saída do comando Docker ps](./media/sql-server-linux-setup-docker/docker-ps-command.png)

1. Se a coluna **STATUS** mostrar o status **Up**, o SQL Server estará em execução no contêiner e será escutado na porta especificada na coluna **PORTS**. Se a coluna **STATUS** do contêiner do SQL Server mostrar **Exited**, confira a [seção Solução de problemas do guia de configuração](sql-server-linux-configure-docker.md#troubleshooting).

O parâmetro `-h` (nome do host) também é útil, mas para simplificar, ele não é usado neste tutorial. Ele altera o nome interno do contêiner para um valor personalizado. Este é o nome que será retornado na consulta Transact-SQL a seguir:

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

Configurar `-h` e `--name` com o mesmo valor é uma boa maneira de identificar facilmente o contêiner de destino.

## <a name="change-the-sa-password"></a>Alterar a senha SA

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="connect-to-sql-server"></a>Conecte-se ao SQL Server

As etapas a seguir usam a ferramenta de linha de comando do SQL Server, a **sqlcmd**, dentro do contêiner para conectar-se ao SQL Server.

1. Use o comando `docker exec -it` para iniciar um shell bash interativo dentro do contêiner em execução. No exemplo a seguir, `sql1` é o nome especificado pelo parâmetro `--name` na criação do contêiner.

   ```bash
   sudo docker exec -it sql1 "bash"
   ```

   ```PowerShell
   docker exec -it sql1 "bash"
   ```

1. Quando estiver dentro do contêiner, conecte-se localmente com a sqlcmd. A sqlcmd não está no caminho por padrão, portanto, você precisará especificar o caminho completo.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourNewStrong!Passw0rd>'
   ```

   > [!TIP]
   > É possível omitir a senha na linha de comando para receber uma solicitação para inseri-la.

1. Se isso funcionar, você será levado a um prompt de comando **sqlcmd**: `1>`.

## <a name="create-and-query-data"></a>Criar e consultar dados

As seções a seguir descrevem como usar o **sqlcmd** e o Transact-SQL para criar um novo banco de dados, adicionar dados e executar uma consulta simples.

### <a name="create-a-new-database"></a>Criar um novo banco de dados

As etapas a seguir criam um novo banco de dados denominado `TestDB`.

1. No prompt de comando **sqlcmd**, cole o seguinte comando Transact-SQL para criar um banco de dados de teste:

   ```sql
   CREATE DATABASE TestDB
   ```

1. Na próxima linha, grave uma consulta para retornar o nome de todos os bancos de dados do servidor:

   ```sql
   SELECT Name from sys.Databases
   ```

1. Os dois comandos anteriores não foram executados imediatamente. Digite `GO` em uma nova linha para executar os comandos anteriores:

   ```sql
   GO
   ```

### <a name="insert-data"></a>Inserir dados

Em seguida, crie uma nova tabela, `Inventory`, e insira duas novas linhas.

1. No prompt de comando **sqlcmd**, altere o contexto para o novo banco de dados `TestDB`:

   ```sql
   USE TestDB
   ```

1. Criar nova tabela denominada `Inventory`:

   ```sql
   CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)
   ```

1. Inserir dados na nova tabela:

   ```sql
   INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
   ```

1. Digite `GO` para executar os comandos anteriores:

   ```sql
   GO
   ```

### <a name="select-data"></a>Selecionar dados

Agora, execute uma consulta para retornar da tabela `Inventory`.

1. No prompt de comando **sqlcmd**, digite uma consulta que retorna linhas de tabela `Inventory` em que a quantidade é maior que 152:

   ```sql
   SELECT * FROM Inventory WHERE quantity > 152;
   ```

1. Execute o comando:

   ```sql
   GO
   ```

### <a name="exit-the-sqlcmd-command-prompt"></a>Saia do prompt de comando sqlcmd

1. Para encerrar a sessão **sqlcmd**, digite `QUIT`:

   ```sql
   QUIT
   ```

1. Para sair do prompt de comando interativo no contêiner, digite `exit`. O contêiner continuará a ser executado depois que você sair do shell bash interativo.

## <a id="connectexternal"></a> Conectar-se de fora do contêiner

Você também pode se conectar à instância do SQL Server em seu computador do Docker usando qualquer ferramenta externa do macOS, do Windows ou do Linux que seja compatível com conexões SQL.

As etapas a seguir usam a **sqlcmd** fora do contêiner para conectar-se ao SQL Server em execução no contêiner. Essas etapas consideram que as ferramentas de linha de comando do SQL Server já estejam instaladas fora do contêiner. Os mesmos princípios são aplicados ao usar outras ferramentas, mas o processo de conexão é exclusivo de cada ferramenta.

1. Localize o endereço IP do computador que hospeda o contêiner. No Linux, use **ifconfig** ou **ip addr**. No Windows, use **ipconfig**.

1. Execute a sqlcmd especificando o endereço IP e a porta mapeada para a porta 1433 no seu contêiner. Neste exemplo, é a porta 1401 no computador host.

   ```bash
   sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourNewStrong!Passw0rd>'
   ```

   ```PowerShell
   sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourNewStrong!Passw0rd>"
   ```

1. Execute comandos Transact-SQL. Quando terminar, digite `QUIT`.

Outras ferramentas comuns para conectar-se ao SQL Server incluem:

- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [SSMS (SQL Server Management Studio) no Windows](sql-server-linux-develop-use-ssms.md)
- [SQL Server Operations Studio (versão prévia)](../sql-operations-studio/what-is.md)
- [mssql-cli (versão prévia)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

## <a name="remove-your-container"></a>Remover o contêiner

Se você quiser remover o contêiner do SQL Server usado neste tutorial, execute os seguintes comandos:

```bash
sudo docker stop sql1
sudo docker rm sql1
```

```PowerShell
docker stop sql1
docker rm sql1
```

> [!WARNING]
> Parar e remover um contêiner permanentemente exclui todos os dados do SQL Server no contêiner. Se você precisar preservar os dados, [crie e copie um arquivo de backup fora do contêiner](tutorial-restore-backup-in-sql-server-container.md) ou use uma [técnica de persistência de dados do contêiner](sql-server-linux-configure-docker.md#persist).

## <a name="docker-demo"></a>Demonstração do Docker

Agora que você já tentou usar a imagem de contêiner do SQL Server para Docker, é interessante saber como o Docker é usado para melhorar o desenvolvimento e o teste. O vídeo a seguir mostra como o Docker pode ser usado em um cenário de implantação e integração contínuas.

> [!VIDEO https://channel9.msdn.com/Events/Connect/2017/T152/player]

## <a name="next-steps"></a>Próximas etapas

Para obter um tutorial sobre como restaurar arquivos de backup do banco de dados em um contêiner, confira [Restaurar um banco de dados do SQL Server em um contêiner do Docker do Linux](tutorial-restore-backup-in-sql-server-container.md). Para explorar outros cenários, como a execução de vários contêineres, a persistência de dados e a solução de problemas, confira [Configurar imagens de contêiner do SQL Server 2017 no Docker](sql-server-linux-configure-docker.md).

Além disso, confira o [repositório do GitHub mssql-docker](https://github.com/Microsoft/mssql-docker) para obter recursos, comentários e problemas conhecidos.
