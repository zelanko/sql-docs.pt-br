---
title: "Introdução ao SQL Server 2017 no Docker | Microsoft Docs"
description: "Este tutorial de início rápido mostra como usar o Docker para executar a imagem de contêiner de 2017 do SQL Server. Em seguida, criar e consultar um banco de dados com sqlcmd."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/12/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.translationtype: MT
ms.sourcegitcommit: 51f60c4fecb56aca3f4fb007f8e6a68601a47d11
ms.openlocfilehash: 99d9395898c4a3ff55bb34278749ec0ea2fae77b
ms.contentlocale: pt-br
ms.lasthandoff: 10/14/2017

---
# <a name="run-the-sql-server-2017-container-image-with-docker"></a>Executar a imagem de contêiner de 2017 do SQL Server com o Docker

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Neste tutorial de início rápido, você deve usar Docker para efetuar pull e executar a imagem de contêiner do SQL Server 2017, [mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/). Conecte-se com **sqlcmd** para criar seu primeiro banco de dados e executar consultas.

Esta imagem consiste em execução no Linux, com base no Ubuntu 16.04 do SQL Server. Ele pode ser usado com o mecanismo do Docker 1.8 + no Linux ou no Docker para Mac/Windows.

> [!NOTE]
> Este guia rápido se concentra especificamente nos usando a imagem mssql-server-linux. A imagem do Windows não é coberta, mas você pode aprender mais sobre ele no [página de Hub do Docker mssql-server-windows](https://hub.docker.com/r/microsoft/mssql-server-windows/).

## <a id="requirements"></a> Pré-requisitos

- Mecanismo do docker 1.8 + em qualquer suporte para a distribuição de Linux ou o Docker para Mac/Windows. Para obter mais informações, consulte [instalar o Docker](https://docs.docker.com/engine/installation/).
- Mínimo de 4 GB de espaço em disco
- Mínimo de 4 GB de RAM
- [Requisitos de sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

> [!IMPORTANT]
> O padrão no Docker para Mac e o Docker para Windows é 2 GB para a VM Moby, portanto você deve alterá-lo a 4 GB. Se você estiver executando em Mac ou Windows, use os procedimentos a seguir para aumentar a memória.

### <a name="increase-docker-memory-to-4-gb-mac"></a>Aumente a memória de Docker para 4 GB (Mac)

As etapas a seguir aumentam a memória para Docker para Mac a 4 GB.

1. Clique no logotipo de Docker na barra de status superior.
1. Selecione **preferências**.
1. Mova o indicador de memória a 4 GB ou mais.
1. Clique o **reiniciar** botão no botão da tela.

### <a name="increase-docker-memory-to-4-gb-windows"></a>Aumente a memória de Docker para 4 GB (Windows)

As etapas a seguir aumentam a memória de Docker para Windows a 4 GB.

1. Clique no ícone na barra de tarefas do Docker.
1. Clique em **configurações** sob esse menu.
1. Clique o **Advanced** guia.
1. Mova o indicador de memória a 4 GB ou mais.
1. Clique o **aplicar** botão.

## <a name="pull-and-run-the-container-image"></a>Pull e executar a imagem de contêiner

1. Baixe a imagem de contêiner do SQL Server 2017 Linux do Hub do Docker.

   ```bash
   docker pull microsoft/mssql-server-linux:2017-latest
   ```

   > [!TIP]
   > Para o Linux, dependendo da configuração do sistema e do usuário, você precisará iniciar cada `docker` com `sudo`.

   > [!NOTE]
   > O comando acima extrai a imagem de contêiner mais recente do SQL Server 2017. Se você quiser receber uma imagem específica, você adicionar um vírgula e o nome da marca (por exemplo, `microsoft/mssql-server-linux:2017-GA`). Para ver todas as imagens disponíveis, consulte [a página de hub do Docker mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/).

1. Para executar a imagem de contêiner com Docker, você pode usar o comando a seguir de um shell bash (Linux/macOS) ou o prompt de comando do PowerShell. A única diferença envolve aspas simples e duplas.

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 --name sql1 -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 --name sql1 -d microsoft/mssql-server-linux:2017-latest
   ```

   > [!NOTE]
   > Por padrão, isso cria um contêiner com a edição de desenvolvedor do SQL Server 2017. O processo de execução de edições de produção em contêineres é ligeiramente diferente. Para obter mais informações, consulte [executar imagens de contêiner de produção](sql-server-linux-configure-docker.md#production).

   A tabela a seguir fornece uma descrição dos parâmetros no anterior `docker run` exemplo:

   | Parâmetro | Description |
   |-----|-----|
   | **-e ' ACCEPT_EULA = Y'** |  Definir o **ACCEPT_EULA** variável qualquer valor para confirmar a sua aceitação do [contrato de licença de usuário final](http://go.microsoft.com/fwlink/?LinkId=746388). Exigida para a imagem do SQL Server. |
   | **-e ' MSSQL_SA_PASSWORD =\<YourStrong! Passw0rd\>'** | Especifique sua própria senha forte que tem pelo menos 8 caracteres e que atenda a [requisitos de senha do SQL Server](../relational-databases/security/password-policy.md). Exigida para a imagem do SQL Server. |
   | **1401:1433 -p** | Mapear uma porta TCP no ambiente de host (primeiro valor) com uma porta TCP no contêiner (segundo valor). Neste exemplo, SQL Server está escutando em TCP 1433 no contêiner e isso é exposto para a porta, 1401 no host. |
   | **-nome sql1** | Especifique um nome personalizado para o contêiner em vez de um nome gerado aleatoriamente. Se você executar mais de um contêiner, você não pode reutilizar esse mesmo nome. |
   | **mssql/Microsoft-server-linux:2017-mais recente** | A imagem de contêiner do SQL Server de 2017 Linux. |

1. Para exibir seus contêineres do Docker, use o `docker ps` comando.

   ```bash
   docker ps -a
   ```

   Você verá uma saída semelhante à captura de tela a seguir:

   ![Saída de comando do docker ps](./media/sql-server-linux-setup-docker/docker-ps-command.png)

1. Se o **STATUS** coluna mostra um status de **backup**, em seguida, o SQL Server for executado no contêiner e escutando na porta especificada no **portas** coluna. Se o **STATUS** coluna para seu mostra de contêiner do SQL Server **Exited**, consulte o [seção do guia de configuração de solução de problemas](sql-server-linux-configure-docker.md#troubleshooting).

O `-h` parâmetro (nome do host) também é útil, mas ele não é usado neste tutorial para simplificar. Isso altera o nome interno do contêiner para um valor personalizado. Este é o nome que você verá retornado na consulta de Transact-SQL a seguir:

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

Configuração `-h` e `--name` com o mesmo valor é uma boa maneira de identificar facilmente o contêiner de destino.

## <a name="change-the-sa-password"></a>Alterar a senha de SA

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="connect-to-sql-server"></a>Conecte-se ao SQL Server

As etapas a seguir usam a ferramenta de linha de comando do SQL Server, **sqlcmd**, dentro do contêiner para se conectar ao SQL Server.

1. Use o `docker exec -it` comando para iniciar um shell bash interativo dentro de seu contêiner em execução. No exemplo a seguir `sql1` é o nome especificado pelo `--name` parâmetro ao criar o contêiner.

   ```bash
   docker exec -it sql1 "bash"
   ```

1. Uma vez dentro do contêiner, conecte-se localmente com o sqlcmd. Sqlcmd não está no caminho por padrão, você precisará especificar o caminho completo.

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

1. Para sair do prompt de comando interativo em seu contêiner, digite `exit`. O contêiner continuará a ser executado depois que você sair shell bash interativo.

## <a id="connectexternal"></a>Conecte-se de fora do contêiner

Você também pode conectar à instância do SQL Server na máquina Docker de qualquer ferramenta externa de macOS, Windows ou Linux que oferece suporte a conexões de SQL.

Use as etapas a seguir **sqlcmd** fora de seu contêiner para se conectar ao SQL Server em execução no contêiner. Essas etapas pressupõem que você já tenha as ferramentas de linha de comando do SQL Server instaladas fora de seu contêiner. Os mesmos princípios se aplicam ao usar outras ferramentas, mas o processo de conexão é exclusivo para cada ferramenta.

1. Localize o endereço IP para o computador que hospeda o contêiner. No Linux, use **ifconfig** ou **endereço ip**. No Windows, use **ipconfig**.

1. Execute o sqlcmd especificando o endereço IP e a porta mapeada para a porta 1433 no seu contêiner. Neste exemplo, que é a porta 1401 no computador host.

   ```bash
   sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourNewStrong!Passw0rd>'
   ```

   ```PowerShell
   sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourNewStrong!Passw0rd>"
   ```

1. Execute comandos Transact-SQL. Quando terminar, digite `QUIT`.

Outras ferramentas comuns para se conectar ao SQL Server incluem:

- [Código do Visual Studio](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) no Windows](sql-server-linux-develop-use-ssms.md)

## <a name="next-steps"></a>Próximas etapas

Para explorar outros cenários, como a execução de vários contêineres, persistência de dados e solução de problemas, consulte [imagens de contêiner de configurar o SQL Server 2017 no Docker](sql-server-linux-configure-docker.md).

Além disso, confira o [repositório do GitHub mssql docker](https://github.com/Microsoft/mssql-docker) para recursos, comentários e problemas conhecidos.

