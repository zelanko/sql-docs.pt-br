---
title: "Introdução ao SQL Server 2017 no Docker | Microsoft Docs"
description: "Este tutorial de início rápido mostra como usar o Docker para executar a imagem de contêiner de 2017 do SQL Server. Em seguida, criar e consultar um banco de dados com sqlcmd."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 95c360dad72a9cd075f2a85d2581dc8021adf941
ms.contentlocale: pt-br
ms.lasthandoff: 08/28/2017

---
# <a name="run-the-sql-server-2017-container-image-with-docker"></a>Executar a imagem de contêiner de 2017 do SQL Server com o Docker

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Neste tutorial de início rápido, você deve usar Docker para efetuar pull e executar a imagem de contêiner do SQL Server de 2017 RC2, [mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/). Conecte-se com **sqlcmd** para criar seu primeiro banco de dados e executar consultas.

Esta imagem consiste em execução no Linux, com base no Ubuntu 16.04 do SQL Server. Ele pode ser usado com o mecanismo do Docker 1.8 + no Linux ou no Docker para Mac/Windows.

> [!NOTE]
> Este guia rápido se concentra especificamente nos usando a imagem mssql-server-linux. A imagem do Windows não é coberta, mas você pode aprender mais sobre ele no [página de Hub do Docker mssql-server-windows](https://hub.docker.com/r/microsoft/mssql-server-windows/).

## <a id="requirements"></a> Pré-requisitos

- Mecanismo do docker 1.8 + em qualquer suporte para a distribuição de Linux ou o Docker para Mac/Windows.
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

1. Baixe a imagem de contêiner do Docker Hub.

    ```bash
    docker pull microsoft/mssql-server-linux
    ```

    > [!TIP]
    > Para o Linux, dependendo da configuração do sistema e do usuário, você precisará iniciar cada `docker` com `sudo`.

1. Para executar a imagem de contêiner com Docker, você pode usar o comando a seguir de um shell bash (Linux/macOS):

    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -e 'MSSQL_PID=Developer' --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
    ```

    Se você estiver usando o Docker para Windows, use o seguinte comando em um prompt de comando do PowerShell com privilégios elevados:

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
    ```

    > [!NOTE]
    > A única diferença entre o exemplo de bash (Linux/macOS) e o exemplo do PowerShell (Windows) está entre aspas simples e aspas duplas em torno de variáveis de ambiente. O comando docker run falhará se você usar uma errado. O restante deste tópico, bash e blocos de código do PowerShell são fornecidos para conveniência. Se houver apenas um exemplo, ele funciona em todas as plataformas, incluindo o Windows.

    A tabela a seguir fornece uma descrição dos parâmetros no anterior `docker run` exemplo:

    | Parâmetro | Description |
    |-----|-----|
    | **-e ' ACCEPT_EULA = Y'** |  Definir o **ACCEPT_EULA** variável qualquer valor para confirmar a sua aceitação do [contrato de licença de usuário final](http://go.microsoft.com/fwlink/?LinkId=746388). Exigida para a imagem do SQL Server. |
    | **-e ' MSSQL_SA_PASSWORD =\<YourStrong! Passw0rd\>'** | Especifique sua própria senha forte que seja pelo menos 8 caracteres e atenda às [requisitos de senha do SQL Server](../relational-databases/security/password-policy.md). Exigida para a imagem do SQL Server. |
    | **-e ' MSSQL_PID = desenvolvedor '** | Especifica a chave de produto ou edição. Neste exemplo, a edição de desenvolvedor livremente licenciada é usada para teste de não produção. Para obter outros valores, consulte [as configurações de configurar o SQL Server com variáveis de ambiente em Linux](sql-server-linux-configure-environment-variables.md). |
    | **– Adicionar limite SYS_PTRACE** | Adiciona a capacidade de Linux de um processo de rastreamento. Isso permite que o SQL Server gerar despejos de memória em uma exceção. |
    | **1401:1433 -p** | Mapear uma porta TCP no ambiente de host (primeiro valor) com uma porta TCP no contêiner (segundo valor). Neste exemplo, SQL Server está escutando em TCP 1433 no contêiner e isso é exposto para a porta, 1401 no host. |
    | **Microsoft/mssql-server-linux** | A imagem de contêiner do Linux do SQL Server. A menos que especificado em contrário, o padrão é o **mais recente** imagem. |

1. Para exibir seus contêineres do Docker, use o `docker ps` comando.

    ```bash
    docker ps -a
    ```

    Você verá uma saída semelhante à captura de tela a seguir:

    ![Saída de comando do docker ps](./media/sql-server-linux-setup-docker/docker-ps-command.png)

1. Se o **STATUS** coluna mostra um status de **backup**, em seguida, o SQL Server for executado no contêiner e escutando na porta especificada no **portas** coluna. Se o **STATUS** coluna para seu mostra de contêiner do SQL Server **Exited**, consulte o [seção do guia de configuração de solução de problemas](sql-server-linux-configure-docker.md#troubleshooting).

Há dois útil `docker run` opções não usadas no exemplo anterior para manter a simplicidade. O `-h` parâmetro (nome do host) altera o nome interno do contêiner para um valor personalizado. Este é o nome que você verá retornado na consulta de Transact-SQL a seguir:

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

Você também pode encontrar o `--name` parâmetro útil para nomear o contêiner em vez de ter um nome de contêiner gerado. Configuração `-h` e `--name` com o mesmo valor é uma boa maneira de identificar facilmente o contêiner de destino.

## <a name="change-the-sa-password"></a>Alterar a senha de SA

A conta SA é um administrador do sistema na instância do SQL Server que é criada durante a instalação. Depois de criar o contêiner do SQL Server, o `MSSQL_SA_PASSWORD` variável de ambiente especificada é detectável executando `echo $MSSQL_SA_PASSWORD` no contêiner. Para fins de segurança, altere sua senha de SA.

1. Escolha uma senha forte para usar para o usuário de SA.

1. Use `docker exec` para executar **sqlcmd** para alterar a senha usando o Transact-SQL. Substituir `<Old Password>` e `<New Password>` com seus valores de senha.

> ```bash
> docker exec -it <Container ID> /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<Old Password>' -Q 'ALTER LOGIN SA WITH PASSWORD="<New Password>";'
> ```

## <a name="connect-to-sql-server"></a>Conecte-se ao SQL Server

As etapas a seguir usam a ferramenta de linha de comando do SQL Server, **sqlcmd**, dentro do contêiner para se conectar ao SQL Server.

1. Use o `docker exec -it` comando para iniciar um shell bash interativo dentro de seu contêiner em execução. No exemplo a seguir `e69e056c702d` é a ID do contêiner.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > Sempre, você não precisa especificar a id de contêiner inteiro. Você só precisa especificar caracteres suficientes para identificá-lo exclusivamente. Portanto, neste exemplo, talvez seja suficiente para usar `e6` ou `e69` em vez da id completa.

1. Uma vez dentro do contêiner, conecte-se localmente com o sqlcmd. Sqlcmd não está no caminho por padrão, você precisará especificar o caminho completo.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
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

## <a name="connect-from-outside-the-container"></a>Conecte-se de fora do contêiner

Você também pode conectar à instância do SQL Server na máquina Docker de qualquer ferramenta externa de macOS, Windows ou Linux que oferece suporte a conexões de SQL.

Use as etapas a seguir **sqlcmd** fora de seu contêiner para se conectar ao SQL Server em execução no contêiner. Essas etapas pressupõem que você já tenha as ferramentas de linha de comando do SQL Server instaladas fora de seu contêiner. Os mesmos princípios se aplicam ao usar outras ferramentas, mas o processo de conexão é exclusivo para cada ferramenta.

1. Localize o endereço IP para o computador que hospeda o contêiner. No Linux, use **ifconfig** ou **endereço ip**. No Windows, use **ipconfig**.

1. Execute o sqlcmd especificando o endereço IP e a porta mapeada para a porta 1433 no seu contêiner. Neste exemplo, que é a porta 1401 no computador host.

   ```bash
   sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
   ```

   ```PowerShell
   sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
   ```

1. Execute comandos Transact-SQL. Quando terminar, digite `QUIT`.

Outras ferramentas comuns para se conectar ao SQL Server incluem:

- [Código do Visual Studio](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) no Windows](sql-server-linux-develop-use-ssms.md)

## <a name="next-steps"></a>Próximas etapas

Para explorar outros cenários, como a execução de vários contêineres de persistência de dados e troublehshooting, consulte [imagens de contêiner de configurar o SQL Server 2017 no Docker](sql-server-linux-configure-docker.md).

Além disso, confira o [repositório do GitHub mssql docker](https://github.com/Microsoft/mssql-docker) para recursos, comentários e problemas conhecidos.

