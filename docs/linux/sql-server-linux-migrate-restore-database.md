---
title: Migrar um banco de dados do SQL Server do Windows para Linux | Microsoft Docs
description: Este tutorial mostra como fazer o backup do banco de dados do SQL Server no Windows e restaurá-lo em um computador Linux executando o SQL Server.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/16/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.openlocfilehash: 0da1e0c866d0934671ebe6291c39d2247a28de07
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47729414"
---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>Migrar um banco de dados do SQL Server do Windows para Linux usando o backup e restauração

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Backup do SQL Server e o recurso de restauração é a maneira recomendada de migrar um banco de dados do SQL Server no Windows para o SQL Server no Linux. Neste tutorial, você percorrer as etapas necessárias para mover um banco de dados para Linux com o backup e restaurar técnicas.

> [!div class="checklist"]
> * Criar um arquivo de backup do Windows com o SSMS
> * Instalar um shell Bash no Windows
> * Mover o arquivo de backup para o Linux no shell Bash
> * Restaurar o arquivo de backup no Linux com o Transact-SQL
> * Executar uma consulta para verificar a migração

Você também pode criar um SQL Server sempre no grupo de disponibilidade para migrar um banco de dados do SQL Server do Windows para Linux. Ver [sql-server-linux-availability-group-cross-platform](sql-server-linux-availability-group-cross-platform.md).

## <a name="prerequisites"></a>Prerequisites

Os seguintes pré-requisitos são necessários para concluir este tutorial:

* Computador Windows com o seguinte:
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions) instalado.
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) instalado.
  * Banco de dados de destino para migrar.

* Computador Linux com o seguinte instalado:
  * SQL Server ([RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md), ou [Ubuntu](quickstart-install-connect-ubuntu.md)) com as ferramentas de linha de comando.

## <a name="create-a-backup-on-windows"></a>Criar um backup no Windows

Há várias maneiras de criar um arquivo de backup de um banco de dados no Windows. As etapas a seguir usam o SQL Server Management Studio (SSMS).

1. Inicie **SQL Server Management Studio** em seu computador Windows.

1. Na caixa de diálogo de conexão, insira **localhost**.

1. No Pesquisador de objetos, expanda **bancos de dados**.

1. Clique com botão direito do banco de dados de destino, selecione **tarefas**e, em seguida, clique em **fazer backup...** .

   ![Usar o SSMS para criar um arquivo de backup](./media/sql-server-linux-migrate-restore-database/ssms-create-backup.png)

1. No **Backup do backup de banco de dados** caixa de diálogo, verifique **tipo de Backup** é **completo** e **fazer o backup** é **disco**. Observe o nome e o local do arquivo. Por exemplo, um banco de dados denominado **YourDB** no SQL Server 2016 tem um caminho de backup padrão da `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak`.

1. Clique em **Okey** para fazer backup de seu banco de dados.

> [!NOTE]
> Outra opção é executar uma consulta Transact-SQL para criar o arquivo de backup. O seguinte comando Transact-SQL executa as mesmas ações que as etapas anteriores para um banco de dados chamado **YourDB**:
>
> ```sql
> BACKUP DATABASE [YourDB] TO  DISK =
> N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak'
> WITH NOFORMAT, NOINIT, NAME = N'YourDB-Full Database Backup',
> SKIP, NOREWIND, NOUNLOAD, STATS = 10
> GO
> ```

## <a name="install-a-bash-shell-on-windows"></a>Instalar um shell Bash no Windows

Para restaurar o banco de dados, é necessário primeiro transferir o arquivo de backup do computador Windows para o computador Linux de destino. Neste tutorial, vamos mover o arquivo para o Linux em um shell Bash (janela de terminal) em execução no Windows.

1. Instalar um shell Bash no seu computador Windows que oferece suporte a **scp** (cópia segura) e **ssh** comandos (acesso remoto). Dois exemplos incluem:

   * O [subsistema do Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) (Windows 10)
   * O Shell Bash do Git ([https://git-scm.com/downloads](https://git-scm.com/downloads))

1. Abra uma sessão do Bash no Windows.

## <a id="scp"></a> Copie o arquivo de backup para Linux

1. Na sua sessão do Bash, navegue até o diretório que contém o arquivo de backup. Por exemplo:

   ```bash
   cd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'
   ```

1. Use o **scp** comando para transferir o arquivo para o computador Linux de destino. As transferências de exemplo a seguir **YourDB.bak** para o diretório base do *user1* no servidor Linux com um endereço IP *192.0.2.9*:

   ```bash
   scp YourDB.bak user1@192.0.2.9:./
   ```
   ![comando do SCP](./media/sql-server-linux-migrate-restore-database/scp-command.png)

> [!TIP]
> Existem alternativas para usar o scp para transferência de arquivos. Uma é usar [Samba](https://help.ubuntu.com/community/Samba) para configurar um compartilhamento de rede SMB entre o Windows e Linux. Para obter uma explicação no Ubuntu, consulte [como criar um compartilhamento de rede por meio do Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!). Uma vez estabelecida, você pode acessá-lo como um arquivo de rede compartilhar do Windows, como  **\\ \\machinenameorip\\compartilhar**.

## <a name="move-the-backup-file-before-restoring"></a>Mova o arquivo de backup antes de restaurar

Neste ponto, o arquivo de backup está no servidor Linux no diretório base do seu usuário. Antes de restaurar o banco de dados para o SQL Server, você deve colocar o backup em um subdiretório **/var/opt/mssql**.

1. Na mesma sessão do Windows do Bash, conecte-se remotamente à sua máquina Linux de destino com **ssh**. O exemplo a seguir conecta-se à máquina Linux **192.0.2.9** como usuário **user1**.

   ```bash
   ssh user1@192.0.2.9
   ```

   Agora você está executando comandos no servidor remoto do Linux.

1. Entre no modo de superusuário.

   ```bash
   sudo su
   ```

1. Crie um novo diretório de backup. O parâmetro -p não fará nada se o diretório já existe.

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

1. Mova o arquivo de backup para esse diretório. No exemplo a seguir, o arquivo de backup reside no diretório inicial do *user1*. Altere o comando para coincidir com o local e o nome do arquivo de backup.

   ```bash
   mv /home/user1/YourDB.bak /var/opt/mssql/backup/
   ```

1. Sair do modo de superusuário.

   ```bash
   exit
   ```

## <a name="restore-your-database-on-linux"></a>Restaurar seu banco de dados no Linux

Para restaurar o backup do banco de dados, você pode usar o **RESTAURAR banco de dados** comando Transact-SQL (TQL).

> [!NOTE]
> As seguintes etapas usam o **sqlcmd** ferramenta. Se você ainda não instalar as ferramentas do SQL Server, consulte [ferramentas de linha de comando de instalar o SQL Server no Linux](sql-server-linux-setup-tools.md).

1. No mesmo terminal, inicie **sqlcmd**. O exemplo a seguir conecta-se à instância do SQL Server local com o **SA** usuário. Insira a senha quando solicitado, ou especifique a senha, adicionando a **-P** parâmetro.

   ```bash
   sqlcmd -S localhost -U SA
   ```

1. Com o `>1` prompt, digite o seguinte **RESTAURAR banco de dados** comando, pressionar ENTER após cada linha (não é possível copiar e colar todo o comando de várias linha ao mesmo tempo). Substitua todas as ocorrências de `YourDB` com o nome do banco de dados.

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```

   Você deve receber uma mensagem que o banco de dados é restaurado com êxito.

   `RESTORE DATABASE` pode retornar um erro semelhante ao seguinte exemplo:

   ```bash
   File 'YourDB_Product' cannot be restored to 'Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf'. Use WITH MOVE to identify a valid location for the file.
   Msg 5133, Level 16, State 1, Server servername, Line 1
   Directory lookup for the file "Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf" failed with the operating system error 2(The system cannot find the file specified.).
   ```
   
   Nesse caso, o banco de dados contém arquivos secundários. Se esses arquivos não forem especificados na `MOVE` cláusula de `RESTORE DATABASE`, o procedimento de restauração tentará criá-los no mesmo caminho que o servidor original. 

   Você pode listar todos os arquivos incluídos no backup:
   ```sql
   RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   GO
   ```
   Você deve obter uma lista como a mostrada abaixo (listando apenas as primeiras duas colunas):
   ```sql
   LogicalName         PhysicalName                                                                 ..............
   ----------------------------------------------------------------------------------------------------------------------
   YourDB              Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB.mdf          ..............
   YourDB_Product      Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf  ..............
   YourDB_Customer     Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Customer.ndf ..............
   YourDB_log          Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Log.ldf      ..............
   ```
   
   Você pode usar esta lista para criar `MOVE` cláusulas para os arquivos adicionais. Neste exemplo, o `RESTORE DATABASE` é:

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Product' TO '/var/opt/mssql/data/YourDB_Product.ndf',
   MOVE 'YourDB_Customer' TO '/var/opt/mssql/data/YourDB_Customer.ndf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```


1. Verifique se a restauração, listando todos os bancos de dados no servidor. O banco de dados restaurado deve ser listado.

   ```sql
   SELECT Name FROM sys.Databases
   GO
   ```

1. Execute outras consultas no banco de dados migrado. O comando a seguir alterna o contexto para o **YourDB** de banco de dados e seleciona as linhas de uma de suas tabelas.

   ```sql
   USE YourDB
   SELECT * FROM YourTable
   GO
   ```

1. Quando você terminar usando **sqlcmd**, tipo `exit`.

1. Quando você terminar trabalhando remotamente **ssh** sessão, digite `exit` novamente.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a fazer backup de um banco de dados no Windows e movê-lo para um servidor Linux executando o SQL Server. Você aprendeu como para:
> [!div class="checklist"]
> * Usar SSMS e Transact-SQL para criar um arquivo de backup do Windows
> * Instalar um shell Bash no Windows
> * Use **scp** para mover os arquivos de backup do Windows para Linux
> * Use **ssh** para se conectar remotamente ao seu computador Linux
> * Realocar o arquivo de backup para se preparar para restauração
> * Use **sqlcmd** para executar comandos Transact-SQL
> * Restaure o backup do banco de dados com o **RESTAURAR banco de dados** comando 
> * Execute a consulta para verificar a migração

Em seguida, explore outros cenários de migração para o SQL Server no Linux. 

> [!div class="nextstepaction"]
>[Migrar bancos de dados do SQL Server no Linux](sql-server-linux-migrate-overview.md)
