---
title: Restaurar um banco de dados do SQL Server no Docker | Microsoft Docs
description: "Este tutorial mostra como restaura um backup de banco de dados do SQL Server em um novo contêiner de Docker do Linux."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.translationtype: MT
ms.sourcegitcommit: 51f60c4fecb56aca3f4fb007f8e6a68601a47d11
ms.openlocfilehash: 1f3cc214be4eaac2199c17c3bea1da7fd02956f1
ms.contentlocale: pt-br
ms.lasthandoff: 10/14/2017

---
# <a name="restore-a-sql-server-database-in-a-linux-docker-container"></a>Restaurar um banco de dados do SQL Server em um contêiner do Docker do Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Este tutorial demonstra como mover e restaurar um arquivo de backup do SQL Server em uma imagem de contêiner do SQL Server de 2017 Linux em execução no Docker.

> [!div class="checklist"]
> * Pull e executar a imagem de contêiner mais recente do SQL Server de 2017 Linux.
> * Copie o arquivo de banco de dados do World Wide Importers no contêiner.
> * Restaure o banco de dados no contêiner.
> * Execute instruções Transact-SQL para exibir e modificar o banco de dados.
> * Fazer backup do banco de dados modificado.

## <a name="prerequisites"></a>Pré-requisitos

* Mecanismo do docker 1.8 + em qualquer suporte para a distribuição de Linux ou o Docker para Mac/Windows. Para obter mais informações, consulte [instalar o Docker](https://docs.docker.com/engine/installation/).
* Mínimo de 4 GB de espaço em disco
* Mínimo de 4 GB de RAM
* [Requisitos de sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

> [!IMPORTANT]
> O padrão no Docker para Mac e o Docker para Windows é 2 GB para a VM Moby, portanto você deve alterá-lo a 4 GB. Se você estiver executando em Mac ou Windows, aumente as configurações de memória usando o [instruções no início rápido Docker](quickstart-install-connect-docker.md).

## <a name="pull-and-run-the-container-image"></a>Pull e executar a imagem de contêiner

1. Abra um terminal bash no Linux/Mac ou uma sessão do PowerShell com privilégios elevados no Windows.

1. Baixe a imagem de contêiner do SQL Server 2017 Linux do Hub do Docker.

    ```bash
    sudo docker pull microsoft/mssql-server-linux:2017-latest
    ```

    ```PowerShell
    docker pull microsoft/mssql-server-linux:2017-latest
    ```

    > [!TIP]
    > Em todo este tutorial, são fornecidos exemplos de comando do docker para o shell bash (Linux/Mac) e do PowerShell (Windows).

1. Para executar a imagem de contêiner com Docker, você pode usar o seguinte comando:

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql1' -p 1401:1433 \
       -v sql1data:/var/opt/mssql \
       -d microsoft/mssql-server-linux:2017-latest
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql1" -p 1401:1433 `
       -v sql1data:/var/opt/mssql `
       -d microsoft/mssql-server-linux:2017-latest
    ```

    Este comando cria um contêiner de 2017 do SQL Server com a edição de desenvolvedor (padrão). Porta do SQL Server **1433** é exposta no host como porta **1401**. Opcional `-v sql1data:/var/opt/mssql` parâmetro cria um contêiner de volume de dados denominado **sql1ddata**. Isso é usado para manter os dados criados pelo SQL Server.

   > [!NOTE]
   > O processo para executar edições do SQL Server de produção em contêineres é ligeiramente diferente. Para obter mais informações, consulte [executar imagens de contêiner de produção](sql-server-linux-configure-docker.md#production). Se você usar o mesmo nomes de contêiner e portas, o restante deste passo a passo ainda funciona com contêineres de produção.

1. Para exibir seus contêineres do Docker, use o `docker ps` comando.

    ```bash
    sudo docker ps -a
    ```

    ```PowerShell
    docker ps -a
    ```
 
1. Se o **STATUS** coluna mostra um status de **backup**, em seguida, o SQL Server for executado no contêiner e escutando na porta especificada no **portas** coluna. Se o **STATUS** coluna para seu mostra de contêiner do SQL Server **Exited**, consulte o [seção do guia de configuração de solução de problemas](sql-server-linux-configure-docker.md#troubleshooting).

   ```
   $ sudo docker ps -a

   CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
   941e1bdf8e1d        microsoft/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
   ```

## <a name="change-the-sa-password"></a>Alterar a senha de SA

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="copy-a-backup-file-into-the-container"></a>Copiar um arquivo de backup no contêiner

Este tutorial usa o [banco de dados de exemplo Wide World Importers](../sample/world-wide-importers/wide-world-importers-documentation.md). Use as etapas a seguir para baixar e copie o arquivo de backup do banco de dados Wide World Importers no seu contêiner do SQL Server.

1. Primeiro, use **a execução do docker** para criar uma pasta de backup. O comando a seguir cria um **/var/opt/mssql/** diretório dentro do contêiner do SQL Server.

   ```bash
   sudo docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

   ```PowerShell
   docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

1. Em seguida, baixe o [wideworldimporters-Full.bak](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0) arquivo à sua máquina host. Os seguintes comandos, navegue até o diretório inicial/usuário e baixa o arquivo de backup como **wwi.bak**.

   ```bash
   cd ~
   curl -L -o wwi.bak 'https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak'
   ```

   ```PowerShell
   curl -OutFile "wwi.bak" "https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak"
   ```

1. Use **docker cp** para copiar o arquivo de backup para o contêiner no **/var/opt/mssql/backup** directory.

   ```bash
   sudo docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

   ```PowerShell
   docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

## <a name="restore-the-database"></a>Restaurar o banco de dados

O arquivo de backup agora está localizado dentro do contêiner. Antes de restaurar o backup, é importante saber os nomes de arquivo lógico e tipos de arquivo dentro do backup. Os seguintes comandos Transact-SQL inspecionar o backup e executar a restauração usando **sqlcmd** no contêiner.

> [!TIP]
> Este tutorial usa **sqlcmd** dentro do contêiner, como o contêiner é fornecido com essa ferramenta pré-instalado. No entanto, você também pode executar instruções Transact-SQL com outro cliente de ferramentas fora do contêiner, como [código do Visual Studio](sql-server-linux-develop-use-vscode.md) ou [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md). Para se conectar, use a porta de host foi mapeada para a porta 1433 no contêiner. Neste exemplo, que é **localhost, 1401** no computador host e **Host_IP_Address, 1401** remotamente.

1. Executar **sqlcmd** dentro do contêiner à lista de nomes de arquivo lógicos e caminhos dentro do backup. Isso é feito com o **RESTORE FILELISTONLY** instrução Transact-SQL.

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

   Você verá uma saída semelhante à seguinte:

   ```
   LogicalName   PhysicalName
   ------------------------------------------
   WWI_Primary   D:\Data\WideWorldImporters.mdf
   WWI_UserData   D:\Data\WideWorldImporters_UserData.ndf
   WWI_Log   E:\Log\WideWorldImporters.ldf
   WWI_InMemory_Data_1   D:\Data\WideWorldImporters_InMemory_Data_1
   ```

1. Chamar o **RESTAURAR banco de dados** comando para restaurar o banco de dados dentro do contêiner. Especifique novos caminhos para cada um dos arquivos na etapa anterior.

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

   Você verá uma saída semelhante à seguinte:

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

## <a name="verify-the-restored-database"></a>Verifique se o banco de dados restaurado

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

As etapas a seguir fazer uma alteração no banco de dados.

1. Executar uma consulta para exibir os itens top 10 a **Warehouse.StockItems** tabela.

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

   Você verá uma lista de nomes e identificadores de item:

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

1. Atualize a descrição do primeiro item com o seguinte **atualização** instrução:

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

   Você verá uma saída semelhante ao seguinte:

   ```
   (1 rows affected)
   StockItemID StockItemName
   ----------- ------------------------------------
             1 USB missile launcher (Dark Green)
   ```

## <a name="create-a-new-backup"></a>Crie um novo backup

Depois que você tiver restaurado o banco de dados em um contêiner, você também poderá criar backups de banco de dados dentro do contêiner em execução regularmente. As etapas a seguem um padrão semelhante para as etapas anteriores, mas na ordem inversa.

1. Use o **BACKUP de banco de dados** comando Transact-SQL para criar um backup de banco de dados no contêiner. Este tutorial cria um novo arquivo de backup, **wwi_2.bak**, em criado anteriormente **/var/opt/mssql/backup** directory.

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

   Você verá uma saída semelhante à seguinte:

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

1. Em seguida, copie o arquivo de backup para fora do contêiner e a máquina host.

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

## <a name="use-the-persisted-data"></a>Use os dados persistentes

Além de fazer backups de banco de dados para proteger seus dados, você também pode usar contêineres de volume de dados. O início deste tutorial criado o **sql1** contêiner com o `-v sql1data:/var/opt/mssql` parâmetro. O **sql1data** contêiner de volume de dados persiste o **/var/opt/mssql** dados mesmo depois que o contêiner é removido. As etapas a seguir removem completamente o **sql1** contêiner e, em seguida, crie um novo contêiner, **sql2**, com os dados persistentes.

1. Parar o **sql1** contêiner.

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. Remova o contêiner. Isso não exclui criado anteriormente **sql1data** contêiner de volume de dados e os dados persistentes nele.

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. Criar um novo contêiner, **sql2**e reutilize o **sql1data** contêiner de volume de dados.

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
       -v sql1data:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
       -v sql1data:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
    ```

1. O banco de dados do Wide World Importers está agora o novo contêiner. Execute uma consulta para verificar a alteração anterior feita.

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
   > A senha de SA não é a senha especificada para o **sql2** contêiner, `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`. Todos os dados do SQL Server foi restaurado de **sql1**, incluindo a senha alterada de anteriormente no tutorial. Na verdade, algumas opções como esta são ignoradas devido a restauração dos dados no /var/opt/mssql. Por esse motivo, a senha é `<YourNewStrong!Passw0rd>` conforme mostrado aqui.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como fazer backup de um banco de dados no Windows e movê-lo para um servidor Linux executando o SQL Server de 2017 RC2. Você aprendeu como para:
> [!div class="checklist"]
> * Crie imagens de contêiner do SQL Server de 2017 Linux.
> * Copie os backups de banco de dados do SQL Server em um contêiner.
> * Executar instruções Transact-SQL dentro do contêiner com **sqlcmd**.
> * Criar e extrair arquivos de backup de um contêiner.
> * Use contêineres de volume de dados no Docker para manter os dados do SQL Server.

Em seguida, examine a outra configuração do Docker e cenários de solução de problemas:

> [!div class="nextstepaction"]
>[Guia de configuração para o SQL Server 2017 no Docker](sql-server-linux-configure-docker.md)

