---
title: Restaurar um banco de dados do SQL Server no Docker
description: Este tutorial mostra como restaurar um backup de banco de dados do SQL Server em um novo contêiner do Docker em Linux.
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 0a91e3fd121cf5e49aca3bbe079d41416aca805a
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68476207"
---
# <a name="restore-a-sql-server-database-in-a-linux-docker-container"></a>Restaurar um banco de dados SQL Server em um contêiner do Docker em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Este tutorial demonstra como mover e restaurar um arquivo de backup do SQL Server para uma imagem de contêiner do SQL Server 2017 em Linux em execução no Docker.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Este tutorial demonstra como mover e restaurar um arquivo de backup do SQL Server para uma imagem de contêiner do SQL Server 2019 (versão prévia) em Linux em execução no Docker.

::: moniker-end

> [!div class="checklist"]
> * Efetuar pull e executar a imagem de contêiner mais recente do SQL Server em Linux.
> * Copie o arquivo de banco de dados da Wide World Importers para o contêiner.
> * Restaure o banco de dados no contêiner.
> * Execute instruções Transact-SQL para exibir e modificar o banco de dados.
> * Faça backup do banco de dados modificado.

## <a name="prerequisites"></a>Prerequisites

* O Docker Engine 1.8 ou superior em qualquer distribuição do Linux ou do Docker para Mac/Windows com suporte. Para obter mais informações, veja [Install Docker](https://docs.docker.com/engine/installation/) (Instalar o Docker).
* Mínimo de 2 GB de espaço em disco
* Mínimo de 2 GB de RAM
* [Requisitos do sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

## <a name="pull-and-run-the-container-image"></a>Efetuar pull e executar a imagem de contêiner

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. Abra um terminal Bash no Linux/Mac ou em uma sessão do PowerShell com privilégios elevados no Windows.

1. Efetue pull da imagem de contêiner do SQL Server 2017 do Linux por meio do Hub do Docker.

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   > [!TIP]
   > Ao longo deste tutorial, os exemplos de comando do Docker são fornecidos para o shell de Bash (Linux/Mac) e o PowerShell (Windows).

1. Para executar a imagem de contêiner com o Docker, você pode usar o seguinte comando:

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql1' -p 1401:1433 \
      -v sql1data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql1" -p 1401:1433 `
      -v sql1data:/var/opt/mssql `
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   Esse comando cria um contêiner do SQL Server 2017 com a Developer Edition (padrão). A porta do SQL Server **1433** é exposta no host como a porta **1401**. O parâmetro `-v sql1data:/var/opt/mssql` opcional cria um contêiner de volume de dados chamado **sql1ddata**. Isso é usado para persistir os dados criados pelo SQL Server.

   > [!NOTE]
   > O processo para executar edições de produção do SQL Server em contêineres é um pouco diferente. Para obter mais informações, veja [Executar imagens de contêiner de produção](sql-server-linux-configure-docker.md#production). Se você usar os mesmo nomes e portas de contêiner, o restante deste tutorial ainda funcionará com contêineres de produção.

1. Para exibir seus contêineres do Docker, use o comando `docker ps`.

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

1. Se a coluna **STATUS** mostrar o status **Up**, o SQL Server estará em execução no contêiner e será escutado na porta especificada na coluna **PORTS**. Se a coluna **STATUS** do contêiner do SQL Server mostrar **Exited**, confira a [seção Solução de problemas do guia de configuração](sql-server-linux-configure-docker.md#troubleshooting).

  ```bash
  $ sudo docker ps -a

  CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
  941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
  ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. Abra um terminal Bash no Linux/Mac ou em uma sessão do PowerShell com privilégios elevados no Windows.

1. Efetue pull da imagem de contêiner do SQL Server 2019 (versão prévia) em Linux por meio do Docker Hub.

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2019-CTP3.2-ubuntu
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2019-CTP3.2-ubuntu
   ```

   > [!TIP]
   > Ao longo deste tutorial, os exemplos de comando do Docker são fornecidos para o shell de Bash (Linux/Mac) e o PowerShell (Windows).

1. Para executar a imagem de contêiner com o Docker, você pode usar o seguinte comando:

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql1' -p 1401:1433 \
      -v sql1data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:2019-CTP3.2-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql1" -p 1401:1433 `
      -v sql1data:/var/opt/mssql `
      -d mcr.microsoft.com/mssql/server:2019-CTP3.2-ubuntu
   ```

   Este comando cria um contêiner SQL Server 2019 (versão prévia) com a Developer Edition (padrão). A porta do SQL Server **1433** é exposta no host como a porta **1401**. O parâmetro `-v sql1data:/var/opt/mssql` opcional cria um contêiner de volume de dados chamado **sql1ddata**. Isso é usado para persistir os dados criados pelo SQL Server.

1. Para exibir seus contêineres do Docker, use o comando `docker ps`.

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

1. Se a coluna **STATUS** mostrar o status **Up**, o SQL Server estará em execução no contêiner e será escutado na porta especificada na coluna **PORTS**. Se a coluna **STATUS** do contêiner do SQL Server mostrar **Exited**, confira a [seção Solução de problemas do guia de configuração](sql-server-linux-configure-docker.md#troubleshooting).

   ```bash
   $ sudo docker ps -a

   CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
   941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
   ```

::: moniker-end

## <a name="change-the-sa-password"></a>Alterar a senha SA

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="copy-a-backup-file-into-the-container"></a>Copiar um arquivo de backup para o contêiner

Este tutorial usa o [banco de dados de exemplo da Wide World Importers](../sample/world-wide-importers/wide-world-importers-documentation.md). Use as etapas a seguir para baixar e copiar o arquivo de backup do banco de dados da Wide World Importers para seu contêiner do SQL Server.

1. Primeiro, use o **docker exec** para criar uma pasta de backup. O comando a seguir cria um diretório **/var/opt/mssql/backup** dentro do contêiner do SQL Server.

   ```bash
   sudo docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

   ```PowerShell
   docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

1. Em seguida, baixe o arquivo [WideWorldImporters-Full.bak](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0) no computador host. Os comandos a seguir navegam até o diretório home/user e baixam o arquivo de backup como **wwi.bak**.

   ```bash
   cd ~
   curl -L -o wwi.bak 'https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak'
   ```

   ```PowerShell
   curl -OutFile "wwi.bak" "https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak"
   ```

1. Use o **docker cp** para copiar o arquivo de backup para o contêiner no diretório **/var/opt/MSSQL/backup**.

   ```bash
   sudo docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

   ```PowerShell
   docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

## <a name="restore-the-database"></a>Restaurar o banco de dados

O arquivo de backup agora está localizado dentro do contêiner. Antes de restaurar o backup, é importante saber os nomes do arquivo lógico e os tipos de arquivo dentro do backup. Os comandos Transact-SQL a seguir inspecionam o backup e executam a restauração usando **sqlcmd** no contêiner.

> [!TIP]
> Este tutorial usa o **sqlcmd** dentro do contêiner, pois o contêiner vem com essa ferramenta pré-instalada. No entanto, você também pode executar instruções do Transact-SQL com outras ferramentas de cliente fora do contêiner, como [Visual Studio Code](sql-server-linux-develop-use-vscode.md) ou [SQL Server Management Studio](sql-server-linux-manage-ssms.md). Para conectar-se, use a porta do host que foi mapeada para a porta 1433 no contêiner. Neste exemplo, é **localhost, 1401** no computador host e **Host_IP_Address, 1401** remotamente.

1. Execute o **sqlcmd** dentro do contêiner para listar nomes de arquivos lógicos e caminhos dentro do backup. Isso é feito com a instrução **RESTORE FILELISTONLY** do Transact-SQL.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost \
      -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'RESTORE FILELISTONLY FROM DISK = "/var/opt/mssql/backup/wwi.bak"' \
      | tr -s ' ' | cut -d ' ' -f 1-2
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost `
      -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/wwi.bak'"
   ```

   Será exibida uma saída semelhante à seguinte:

   ```
   LogicalName   PhysicalName
   ------------------------------------------
   WWI_Primary   D:\Data\WideWorldImporters.mdf
   WWI_UserData   D:\Data\WideWorldImporters_UserData.ndf
   WWI_Log   E:\Log\WideWorldImporters.ldf
   WWI_InMemory_Data_1   D:\Data\WideWorldImporters_InMemory_Data_1
   ```

1. Chame o comando **RESTORE DATABASE** para restaurar o banco de dados dentro do contêiner. Especifique novos caminhos para cada um dos arquivos na etapa anterior.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'RESTORE DATABASE WideWorldImporters FROM DISK = "/var/opt/mssql/backup/wwi.bak" WITH MOVE "WWI_Primary" TO "/var/opt/mssql/data/WideWorldImporters.mdf", MOVE "WWI_UserData" TO "/var/opt/mssql/data/WideWorldImporters_userdata.ndf", MOVE "WWI_Log" TO "/var/opt/mssql/data/WideWorldImporters.ldf", MOVE "WWI_InMemory_Data_1" TO "/var/opt/mssql/data/WideWorldImporters_InMemory_Data_1"'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "RESTORE DATABASE WideWorldImporters FROM DISK = '/var/opt/mssql/backup/wwi.bak' WITH MOVE 'WWI_Primary' TO '/var/opt/mssql/data/WideWorldImporters.mdf', MOVE 'WWI_UserData' TO '/var/opt/mssql/data/WideWorldImporters_userdata.ndf', MOVE 'WWI_Log' TO '/var/opt/mssql/data/WideWorldImporters.ldf', MOVE 'WWI_InMemory_Data_1' TO '/var/opt/mssql/data/WideWorldImporters_InMemory_Data_1'"
   ```

   Será exibida uma saída semelhante à seguinte:

   ```
   Processed 1464 pages for database 'WideWorldImporters', file 'WWI_Primary' on file 1.
   Processed 53096 pages for database 'WideWorldImporters', file 'WWI_UserData' on file 1.
   Processed 33 pages for database 'WideWorldImporters', file 'WWI_Log' on file 1.
   Processed 3862 pages for database 'WideWorldImporters', file 'WWI_InMemory_Data_1' on file 1.
   Converting database 'WideWorldImporters' from version 852 to the current version 869.
   Database 'WideWorldImporters' running the upgrade step from version 852 to version 853.
   Database 'WideWorldImporters' running the upgrade step from version 853 to version 854.
   Database 'WideWorldImporters' running the upgrade step from version 854 to version 855.
   Database 'WideWorldImporters' running the upgrade step from version 855 to version 856.
   Database 'WideWorldImporters' running the upgrade step from version 856 to version 857.
   Database 'WideWorldImporters' running the upgrade step from version 857 to version 858.
   Database 'WideWorldImporters' running the upgrade step from version 858 to version 859.
   Database 'WideWorldImporters' running the upgrade step from version 859 to version 860.
   Database 'WideWorldImporters' running the upgrade step from version 860 to version 861.
   Database 'WideWorldImporters' running the upgrade step from version 861 to version 862.
   Database 'WideWorldImporters' running the upgrade step from version 862 to version 863.
   Database 'WideWorldImporters' running the upgrade step from version 863 to version 864.
   Database 'WideWorldImporters' running the upgrade step from version 864 to version 865.
   Database 'WideWorldImporters' running the upgrade step from version 865 to version 866.
   Database 'WideWorldImporters' running the upgrade step from version 866 to version 867.
   Database 'WideWorldImporters' running the upgrade step from version 867 to version 868.
   Database 'WideWorldImporters' running the upgrade step from version 868 to version 869.
   RESTORE DATABASE successfully processed 58455 pages in 18.069 seconds (25.273 MB/sec).
   ```

## <a name="verify-the-restored-database"></a>Verifique o banco de dados restaurado

Execute a consulta a seguir para exibir uma lista de nomes de banco de dados em seu contêiner:

```bash
sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
   -Q 'SELECT Name FROM sys.Databases'
```

```PowerShell
docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
   -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
   -Q "SELECT Name FROM sys.Databases"
```

Você deve ver **WideWorldImporters** na lista de bancos de dados.

## <a name="make-a-change"></a>Fazer uma alteração

As etapas a seguir fazem uma alteração ao banco de dados.

1. Execute uma consulta para exibir os 10 principais itens na tabela **Warehouse.StockItems**.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT TOP 10 StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems ORDER BY StockItemID'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT TOP 10 StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems ORDER BY StockItemID"
   ```

   Você deverá ver uma lista de identificadores e nomes de itens:

   ```
   StockItemID StockItemName
   ----------- -----------------
             1 USB missile launcher (Green)
             2 USB rocket launcher (Gray)
             3 Office cube periscope (Black)
             4 USB food flash drive - sushi roll
             5 USB food flash drive - hamburger
             6 USB food flash drive - hot dog
             7 USB food flash drive - pizza slice
             8 USB food flash drive - dim sum 10 drive variety pack
             9 USB food flash drive - banana
            10 USB food flash drive - chocolate bar
   ```

1. Atualize a descrição do primeiro item com a seguinte instrução **UPDATE**:

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'UPDATE WideWorldImporters.Warehouse.StockItems SET StockItemName="USB missile launcher (Dark Green)" WHERE StockItemID=1; SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "UPDATE WideWorldImporters.Warehouse.StockItems SET StockItemName='USB missile launcher (Dark Green)' WHERE StockItemID=1; SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   Será exibida uma saída semelhante ao texto a seguir:

   ```
   (1 rows affected)
   StockItemID StockItemName
   ----------- ------------------------------------
             1 USB missile launcher (Dark Green)
   ```

## <a name="create-a-new-backup"></a>Criar um novo backup

Depois de restaurar o banco de dados para um contêiner, talvez você também queira criar regularmente backups de banco de dados dentro do contêiner em execução. As etapas seguem um padrão semelhante aos das etapas anteriores, mas na ordem inversa.

1. Use o comando do Transact-SQL **BACKUP DATABASE** para criar um backup de banco de dados no contêiner. Este tutorial cria um novo arquivo de backup, **wwi_2.bak**, no diretório **/var/opt/MSSQL/backup** criado anteriormente.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q "BACKUP DATABASE [WideWorldImporters] TO DISK = N'/var/opt/mssql/backup/wwi_2.bak' WITH NOFORMAT, NOINIT, NAME = 'WideWorldImporters-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "BACKUP DATABASE [WideWorldImporters] TO DISK = N'/var/opt/mssql/backup/wwi_2.bak' WITH NOFORMAT, NOINIT, NAME = 'WideWorldImporters-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
   ```

   Será exibida uma saída semelhante à seguinte:

   ```
   10 percent processed.
   20 percent processed.
   30 percent processed.
   40 percent processed.
   50 percent processed.
   60 percent processed.
   70 percent processed.
   Processed 1200 pages for database 'WideWorldImporters', file 'WWI_Primary' on file 1.
   Processed 53096 pages for database 'WideWorldImporters', file 'WWI_UserData' on file 1.
   80 percent processed.
   Processed 3865 pages for database 'WideWorldImporters', file 'WWI_InMemory_Data_1' on file 1.
   Processed 938 pages for database 'WideWorldImporters', file 'WWI_Log' on file 1.
   100 percent processed.
   BACKUP DATABASE successfully processed 59099 pages in 25.056 seconds (18.427 MB/sec).
   ```

1. Em seguida, copie o arquivo de backup do contêiner para o computador host.

   ```bash
   cd ~
   sudo docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

   ```PowerShell
   cd ~
   docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

## <a name="use-the-persisted-data"></a>Usar os dados persistentes

Além de usar os backups de banco de dados para proteger seus dados, você também pode usar contêineres de volume de dados. O início deste tutorial criou o contêiner **sql1** com o parâmetro `-v sql1data:/var/opt/mssql`. O contêiner de volume de dados **sql1data** persiste os dados de **/var/opt/MSSQL** mesmo depois que o contêiner é removido. As etapas a seguir removem completamente o contêiner **sql1** e, em seguida, criam um novo contêiner, **sql2**, com os dados persistentes.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. Interrompa o contêiner **sql1**.

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. Remova o contêiner. Isso não exclui o contêiner de volume de dados **sql1data** criado anteriormente nem os dados persistentes nele.

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. Crie um novo contêiner, **sql2**, e reutilize o contêiner de volume de dados **sql1data**.

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
      -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
      -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

1. O banco de dados de Importadores Mundiais agora está no novo contêiner. Execute uma consulta para verificar a alteração anterior feita.

   ```bash
   sudo docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   > [!NOTE]
   > A senha SA não é a senha especificada para o contêiner **sql2**, `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`. Todos os dados do SQL Server foram restaurados de **sql1**, incluindo a senha alterada de antes no tutorial. Na verdade, algumas opções como essa são ignoradas devido à restauração dos dados em /var/opt/mssql. Por esse motivo, a senha é `<YourNewStrong!Passw0rd>`, como mostrado aqui.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. Interrompa o contêiner **sql1**.

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. Remova o contêiner. Isso não exclui o contêiner de volume de dados **sql1data** criado anteriormente nem os dados persistentes nele.

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. Crie um novo contêiner, **sql2**, e reutilize o contêiner de volume de dados **sql1data**.

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.2-ubuntu
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.2-ubuntu
    ```

1. O banco de dados de Importadores Mundiais agora está no novo contêiner. Execute uma consulta para verificar a alteração anterior feita.

   ```bash
   sudo docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   > [!NOTE]
   > A senha SA não é a senha especificada para o contêiner **sql2**, `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`. Todos os dados do SQL Server foram restaurados de **sql1**, incluindo a senha alterada de antes no tutorial. Na verdade, algumas opções como essa são ignoradas devido à restauração dos dados em /var/opt/mssql. Por esse motivo, a senha é `<YourNewStrong!Passw0rd>`, como mostrado aqui.

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Neste tutorial, você aprendeu a fazer backup de um banco de dados em Windows e movê-lo para um servidor Linux que executa o SQL Server 2017. Você aprendeu a:

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Neste tutorial, você aprendeu a fazer backup de um banco de dados em Windows e movê-lo para um servidor Linux que executa o SQL Server 2019 (versão prévia). Você aprendeu a:

::: moniker-end

> [!div class="checklist"]
> * Crie imagens de contêiner do Linux do SQL Server.
> * Copie backups de banco de dados do SQL Server para um contêiner.
> * Execute instruções Transact-SQL dentro do contêiner com **sqlcmd**.
> * Crie e extraia arquivos de backup de um contêiner.
> * Use contêineres de volume de dados no Docker para manter dados do SQL Server.

A seguir, examine outros cenários de configuração e solução de problemas do Docker:

> [!div class="nextstepaction"]
>[Guia de configuração do SQL Server 2017 no Docker](sql-server-linux-configure-docker.md)
