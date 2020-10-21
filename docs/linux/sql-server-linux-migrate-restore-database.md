---
title: Migrar um banco de dados do SQL Server do Windows para o Linux
description: Este tutorial mostra como tomar um backup de banco de dados do SQL Server em Windows e restaurá-lo em um computador Linux que executa o SQL Server.
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 08/16/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.openlocfilehash: 125e1b8fdadc04a7d3ba08807a72ef594b42388e
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115849"
---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>Migrar um banco de dados do SQL Server do Windows para o Linux usando o recurso de backup e restauração

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

O recurso de backup e restauração do SQL Server é a maneira recomendada de migrar um banco de dados do SQL Server em Windows para o SQL Server em Linux. Neste tutorial, você percorrerá as etapas necessárias para mover um banco de dados para o Linux com as técnicas de backup e restauração.

> [!div class="checklist"]
> * Criar um arquivo de backup em Windows com SSMS
> * Instalar um shell Bash em Windows
> * Mover o arquivo de backup para Linux do shell Bash
> * Restaurar o arquivo de backup no Linux com o Transact-SQL
> * Executar uma consulta para verificar a migração

Você também pode criar um grupo de disponibilidade Always On do SQL Server para migrar um banco de dados do SQL Server do Windows para o Linux. Confira [sql-server-linux-availability-group-cross-platform](sql-server-linux-availability-group-cross-platform.md).

## <a name="prerequisites"></a>Prerequisites

Os pré-requisitos a seguir são necessários para concluir esse tutorial:

* Computador Windows com o seguinte:
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads) instalado.
  * [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md) instalado.
  * Banco de dados de destino a ser migrado.

* Computador Linux com o seguinte instalado:
  * SQL Server ([RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md) ou [Ubuntu](quickstart-install-connect-ubuntu.md)) com ferramentas de linha de comando.

## <a name="create-a-backup-on-windows"></a>Criar um backup em Windows

Há várias maneiras de criar um arquivo de backup de um banco de dados em Windows. As etapas a seguir usam o SSMS (SQL Server Management Studio).

1. Inicie o **SQL Server Management Studio** em seu computador Windows.

1. Na caixa de diálogo de conexão, insira **localhost**.

1. No Pesquisador de Objetos, expanda **Bancos de Dados**.

1. Clique com o botão direito do mouse no banco de dados desejado, selecione **Tarefas** e, em seguida, clique em **Fazer backup...** .

   ![Use o SSMS para criar um arquivo de backup](./media/sql-server-linux-migrate-restore-database/ssms-create-backup.png)

1. Na caixa de diálogo **Fazer backup do banco de dados**, verifique se o **Tipo de backup** está definido como **Completo** e se **Fazer backup em** está definido como **Disk**. Observe o nome e a localização do arquivo. Por exemplo, um banco de dados chamado **YourDB** no SQL Server 2016 terá o caminho de backup padrão igual a `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak`.

1. Clique em **OK** para fazer backup do banco de dados.

> [!NOTE]
> Outra opção é executar uma consulta Transact-SQL para criar o arquivo de backup. O comando Transact-SQL a seguir executa as mesmas ações que as etapas anteriores para um banco de dados chamado **YourDB**:
>
> ```sql
> BACKUP DATABASE [YourDB] TO  DISK =
> N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak'
> WITH NOFORMAT, NOINIT, NAME = N'YourDB-Full Database Backup',
> SKIP, NOREWIND, NOUNLOAD, STATS = 10
> GO
> ```

## <a name="install-a-bash-shell-on-windows"></a>Instalar um shell Bash em Windows

Para restaurar o banco de dados, primeiro você precisa transferir o arquivo de backup do computador Windows para o computador Linux de destino. Neste tutorial, movemos o arquivo para o Linux por meio de um shell Bash (janela de terminal) em execução no Windows.

1. Instale em seu computador Windows um shell Bash compatível com os comandos **scp** (cópia segura) e **ssh** (logon remoto). Dois exemplos são:

   * O [Subsistema Windows para Linux](/windows/wsl/about) (Windows 10)
   * O Shell Bash do Git ([https://git-scm.com/downloads](https://git-scm.com/downloads))

1. Abra uma sessão do Bash em Windows.

## <a name="copy-the-backup-file-to-linux"></a><a id="scp"></a> Copie o arquivo de backup para o Linux

1. Na sessão do Bash, navegue até o diretório que contém o arquivo de backup. Por exemplo:

   ```bash
   cd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'
   ```

1. Use o comando **scp** para transferir o arquivo para o computador Linux de destino. O exemplo a seguir transfere **YourDB.bak** para o diretório base do *user1* no servidor Linux com o endereço IP *192.0.2.9*:

   ```bash
   scp YourDB.bak user1@192.0.2.9:./
   ```
   ![Comando scp](./media/sql-server-linux-migrate-restore-database/scp-command.png)

> [!TIP]
> Há alternativas ao uso do comando scp para transferência de arquivos. Deve-se usar o [Samba](https://help.ubuntu.com/community/Samba) para configurar um compartilhamento de rede de SMB entre o Windows e o Linux. Para obter instruções passo a passo no Ubuntu, confira [Como criar um compartilhamento de rede por meio do Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!). Depois de estabelecido, você pode acessá-lo como um compartilhamento de arquivo de rede do Windows, como **\\\\machinenameorip\\share**.

## <a name="move-the-backup-file-before-restoring"></a>Mova o arquivo de backup antes de restaurar

Neste ponto, o arquivo de backup está no servidor Linux, no diretório base do seu usuário. Antes de restaurar o banco de dados no SQL Server, você deve colocar o backup em um subdiretório de **/var/opt/mssql**.

1. Na mesma sessão do Bash do Windows, conecte-se remotamente ao seu computador Linux de destino com o comando **ssh**. O exemplo a seguir conecta-se ao computador Linux **192.0.2.9** como o usuário **user1**.

   ```bash
   ssh user1@192.0.2.9
   ```

   Agora você está executando comandos no servidor Linux remoto.

1. Entre no modo de superusuário.

   ```bash
   sudo su
   ```

1. Crie um novo diretório de backup. O parâmetro -p não fará nada se o diretório já existir.

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

1. Mova o arquivo de backup para esse diretório. No exemplo a seguir, o arquivo de backup reside no diretório base do *user1*. Altere o comando para corresponder à localização e ao nome do seu arquivo de backup.

   ```bash
   mv /home/user1/YourDB.bak /var/opt/mssql/backup/
   ```

1. Saia do modo de superusuário.

   ```bash
   exit
   ```

## <a name="restore-your-database-on-linux"></a>Restaurar seu banco de dados no Linux

Para restaurar o backup do banco de dados, você pode usar o comando **RESTORE DATABASE** do TQL (Transact-SQL).

> [!NOTE]
> As etapas a seguir usam a ferramenta **sqlcmd**. Caso ainda não tenha instalado as ferramentas do SQL Server, confira [Instalar as ferramentas de linha de comando do SQL Server em Linux](sql-server-linux-setup-tools.md).

1. No mesmo terminal, inicie o **sqlcmd**. O exemplo a seguir conecta-se à instância local do SQL Server com o usuário **SA**. Insira a senha quando solicitado ou especifique a senha adicionando o parâmetro **-P**.

   ```bash
   sqlcmd -S localhost -U SA
   ```

1. No prompt `>1`, insira o comando **RESTORE DATABASE** a seguir, pressionando ENTER após cada linha (você não pode copiar e colar todo o comando de várias linhas de uma só vez). Substitua todas as ocorrências de `YourDB` pelo nome do seu banco de dados.

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```

   Deve ser exibida uma mensagem informando que o banco de dados foi restaurado com sucesso.

   `RESTORE DATABASE` pode retornar um erro como no exemplo a seguir:

   ```bash
   File 'YourDB_Product' cannot be restored to 'Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf'. Use WITH MOVE to identify a valid location for the file.
   Msg 5133, Level 16, State 1, Server servername, Line 1
   Directory lookup for the file "Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf" failed with the operating system error 2(The system cannot find the file specified.).
   ```
   
   Nesse caso, o banco de dados contém arquivos secundários. Se esses arquivos não forem especificados na cláusula `MOVE` de `RESTORE DATABASE`, o procedimento de restauração tentará criá-los no mesmo caminho que o servidor original. 

   Você pode listar todos os arquivos incluídos no backup:
   ```sql
   RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   GO
   ```
   Deve ser exibida uma lista como a seguinte (trazendo apenas as duas primeiras colunas):
   ```sql
   LogicalName         PhysicalName                                                                 ..............
   ----------------------------------------------------------------------------------------------------------------------
   YourDB              Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB.mdf          ..............
   YourDB_Product      Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf  ..............
   YourDB_Customer     Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Customer.ndf ..............
   YourDB_log          Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Log.ldf      ..............
   ```
   
   Você pode usar essa lista para criar cláusulas `MOVE` para os arquivos adicionais. Neste exemplo, `RESTORE DATABASE` é:

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Product' TO '/var/opt/mssql/data/YourDB_Product.ndf',
   MOVE 'YourDB_Customer' TO '/var/opt/mssql/data/YourDB_Customer.ndf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```


1. Verifique a restauração listando todos os bancos de dados do servidor. O banco de dados restaurado deve constar na lista.

   ```sql
   SELECT Name FROM sys.Databases
   GO
   ```

1. Execute outras consultas no banco de dados migrado. O comando a seguir alterna o contexto para o banco de dados **YourDB** e seleciona linhas de uma de suas tabelas.

   ```sql
   USE YourDB
   SELECT * FROM YourTable
   GO
   ```

1. Quando terminar de usar o **sqlcmd**, digite `exit`.

1. Quando terminar de trabalhar na sessão **ssh** remota, digite `exit` novamente.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a fazer backup de um banco de dados em Windows e movê-lo para um servidor Linux que executa o SQL Server. Você aprendeu a:
> [!div class="checklist"]
> * Usar o SSMS e o Transact-SQL para criar um arquivo de backup em Windows
> * Instalar um shell Bash em Windows
> * Usar o comando **scp** para mover arquivos de backup do Windows para o Linux
> * Usar o comando **ssh** para conectar-se remotamente ao seu computador Linux
> * Relocar o arquivo de backup para se preparar para a restauração
> * Usar o **sqlcmd** para executar comandos Transact-SQL
> * Restaurar o backup do banco de dados com o comando **RESTORE DATABASE** 
> * Executar a consulta para verificar a migração

Em seguida, explore outros cenários de migração para o SQL Server em Linux. 

> [!div class="nextstepaction"]
>[Migrar bancos de dados para o SQL Server em Linux](sql-server-linux-migrate-overview.md)