---
title: Migrar um banco de dados do SQL Server do Windows para o Linux | Microsoft Docs
description: "Este tutorial mostra como fazer o backup do banco de dados do SQL Server no Windows e restaurá-lo para um computador Linux executando o SQL Server 2017."
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/16/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.workload: On Demand
ms.openlocfilehash: f50be15e4d778ffb9c77caa375dc6b963b5821cd
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>Migrar um banco de dados do SQL Server do Windows para Linux usando backup e restauração

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Backup do SQL Server e o recurso de restauração é a maneira recomendada para migrar um banco de dados do SQL Server no Windows para 2017 do SQL Server no Linux. Neste tutorial, você verá as etapas necessárias para mover um banco de dados para o Linux com backup e restauração técnicas.

> [!div class="checklist"]
> * Criar um arquivo de backup no Windows com o SSMS
> * Instalar um shell Bash no Windows
> * Mover o arquivo de backup para o Linux no shell Bash
> * Restaurar o arquivo de backup no Linux com o Transact-SQL
> * Executar uma consulta para verificar a migração

Você também pode criar um SQL Server sempre no grupo de disponibilidade para migrar um banco de dados do SQL Server do Windows para o Linux. Consulte [sql-server-linux-availability-group-cross-platform](sql-server-linux-availability-group-cross-platform.md).

## <a name="prerequisites"></a>Prerequisites

Os seguintes pré-requisitos são necessários para concluir este tutorial:

* Computador Windows com o seguinte:
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions) instalado.
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) instalado.
  * Banco de dados de destino para migrar.

* Computador Linux com os seguintes itens instalados:
  * SQL Server 2017 ([RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md), ou [Ubuntu](quickstart-install-connect-ubuntu.md)) com as ferramentas de linha de comando.

## <a name="create-a-backup-on-windows"></a>Criar um backup no Windows

Há várias maneiras de criar um arquivo de backup de um banco de dados no Windows. As etapas a seguir usam o SQL Server Management Studio (SSMS).

1. Iniciar **SQL Server Management Studio** em seu computador Windows.

1. Na caixa de diálogo de conexão, digite **localhost**.

1. No Pesquisador de objetos, expanda **bancos de dados**.

1. Clique duas vezes o banco de dados de destino, selecione **tarefas**e, em seguida, clique em **backup...** .

   ![Use o SSMS para criar um arquivo de backup](./media/sql-server-linux-migrate-restore-database/ssms-create-backup.png)

1. No **Backup backup de banco de dados** caixa de diálogo, verifique **o tipo de Backup** é **completo** e **backup** é **disco**. Observe o nome e o local do arquivo. Por exemplo, um banco de dados denominado **YourDB** no SQL Server 2016 tem um caminho de backup padrão `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak`.

1. Clique em **Okey** para fazer backup de seu banco de dados.

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

## <a name="install-a-bash-shell-on-windows"></a>Instalar um shell Bash no Windows

Para restaurar o banco de dados, é necessário primeiro transferir o arquivo de backup do computador Windows para o computador Linux de destino. Neste tutorial, podemos mover o arquivo para o Linux de um shell Bash (janela de terminal) em execução no Windows.

1. Instalar um shell Bash no seu computador Windows que oferece suporte a **scp** (cópia segura) e **ssh** comandos (logon remoto). Dois exemplos incluem:

   * O [subsistema do Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) (Windows 10)
   * O Shell Bash Git ([https://git-scm.com/downloads](https://git-scm.com/downloads))

1. Abra uma sessão de Bash no Windows.

## <a id="scp"></a>Copie o arquivo de backup para Linux

1. Na sua sessão Bash, navegue até o diretório que contém o arquivo de backup. Por exemplo:

   ```bash
   cd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'
   ```

1. Use o **scp** comando para transferir o arquivo para o computador Linux de destino. As transferências de exemplo a seguir **YourDB.bak** para o diretório base de *user1* no servidor Linux com um endereço IP de *192.0.2.9*:

   ```bash
   scp YourDB.bak user1@192.0.2.9:./
   ```
   ![comando SCP](./media/sql-server-linux-migrate-restore-database/scp-command.png)

> [!TIP]
> Existem alternativas para usar o scp para transferência de arquivos. Uma é usar [Samba](https://help.ubuntu.com/community/Samba) para configurar um compartilhamento de rede SMB entre o Windows e Linux. Para obter uma explicação sobre Ubuntu, consulte [como criar um compartilhamento de rede por meio do Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!). Depois de estabelecida, você pode acessá-lo como um arquivo de rede compartilham do Windows, tais como  **\\ \\machinenameorip\\compartilhar**.

## <a name="move-the-backup-file-before-restoring"></a>Mova o arquivo de backup antes de restaurar

Neste ponto, o arquivo de backup está no servidor Linux no diretório base do usuário. Antes de restaurar o banco de dados para o SQL Server, você deve colocar o backup em um subdiretório do **/var/opt/mssql**.

1. Na mesma sessão do Windows Bash, conecte-se remotamente ao seu computador Linux de destino por **ssh**. O exemplo a seguir se conecta ao computador Linux **192.0.2.9** como usuário **user1**.

   ```bash
   ssh user1@192.0.2.9
   ```

   Você está executando comandos no servidor remoto do Linux.

1. Entre no modo de superusuário.

   ```bash
   sudo su
   ```

1. Crie um novo diretório de backup. O parâmetro -p não fará nada se o diretório já existe.

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

1. Mova o arquivo de backup para esse diretório. No exemplo a seguir, o arquivo de backup reside no diretório base do *user1*. Altere o comando para coincidir com o local e o nome do arquivo de backup.

   ```bash
   mv /home/user1/YourDB.bak /var/opt/mssql/backup/
   ```

1. Sair do modo de superusuário.

   ```bash
   exit
   ```

## <a name="restore-your-database-on-linux"></a>Restaurar o banco de dados no Linux

Para restaurar o backup do banco de dados, você pode usar o **RESTAURAR banco de dados** comando Transact-SQL (TQL).

> [!NOTE]
> As seguintes etapas usam o **sqlcmd** ferramenta. Se você ainda não instalar as ferramentas do SQL Server, consulte [ferramentas de linha de comando de instalar o SQL Server no Linux](sql-server-linux-setup-tools.md).

1. No mesmo terminal, inicie **sqlcmd**. O exemplo a seguir se conecta à instância do SQL Server local com o **SA** usuário. Digite a senha quando solicitado, ou especifique a senha, adicionando o **-P** parâmetro.

   ```bash
   sqlcmd -S localhost -U SA
   ```

1. No `>1` prompt, digite o seguinte **RESTAURAR banco de dados** comando, pressionar ENTER depois de cada linha (você não pode copiar e colar todo o comando de várias linha de uma vez). Substitua todas as ocorrências de `YourDB` com o nome do banco de dados.

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```

   Você deve receber uma mensagem que o banco de dados for restaurado com êxito.

1. Verifique se a restauração, listando todos os bancos de dados no servidor. O banco de dados restaurado deve ser listado.

   ```sql
   SELECT Name FROM sys.Databases
   GO
   ```

1. Execute outras consultas no banco de dados migrado. O comando a seguir alterna contexto para o **YourDB** banco de dados e seleciona as linhas de uma de suas tabelas.

   ```sql
   USE YourDB
   SELECT * FROM YourTable
   GO
   ```

1. Quando você terminar usando **sqlcmd**, tipo `exit`.

1. Quando você terminar trabalhando remotamente **ssh** sessão, digite `exit` novamente.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como fazer backup de um banco de dados no Windows e movê-lo para um servidor Linux executando o SQL Server 2017. Você aprendeu como para:
> [!div class="checklist"]
> * Use o SSMS e Transact-SQL para criar um arquivo de backup no Windows
> * Instalar um shell Bash no Windows
> * Use **scp** para mover arquivos de backup do Windows para Linux
> * Use **ssh** se conectar remotamente ao computador Linux
> * Realocar o arquivo de backup para a preparação para restauração
> * Use **sqlcmd** para executar comandos Transact-SQL
> * Restaure o backup do banco de dados com o **RESTAURAR banco de dados** comando 
> * Execute a consulta para verificar a migração

Em seguida, explore a outros cenários de migração para o SQL Server no Linux. 

> [!div class="nextstepaction"]
>[Migrar bancos de dados para o SQL Server no Linux](sql-server-linux-migrate-overview.md)
