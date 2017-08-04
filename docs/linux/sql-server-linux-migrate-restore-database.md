---
title: Migrar um banco de dados do SQL Server do Windows para o Linux | Microsoft Docs
description: "Este tópico mostra como fazer o backup do banco de dados do SQL Server no Windows e restaurá-lo para um computador Linux executando o SQL Server de 2017 RC2."
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 2e23ba46381b1fb80b8ac335f6d7630f02a222bb
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>Migrar um banco de dados do SQL Server do Windows para Linux usando backup e restauração

Backup do SQL Server e o recurso de restauração é a maneira recomendada para migrar um banco de dados do SQL Server no Windows para o SQL Server de 2017 RC2 no Linux. Este tópico fornece instruções passo a passo para essa técnica. Neste tutorial, você vai:

- Baixe o arquivo de backup AdventureWorks em um computador Windows
- Transferência de backup para o computador Linux
- Restaurar o banco de dados usando comandos Transact-SQL

> [!NOTE] 
> Este tutorial presume que você instalou [SQL Server 2017 RC2](sql-server-linux-setup.md) e o [ferramentas do SQL Server](sql-server-linux-setup-tools.md) no servidor Linux de destino.

## <a name="download-the-adventureworks-database-backup"></a>Baixar o backup de banco de dados AdventureWorks

Embora você possa usar as mesmas etapas para restaurar qualquer banco de dados, o banco de dados de exemplo AdventureWorks fornece um bom exemplo. Ele é fornecido como um arquivo de backup de banco de dados existente.

>[!NOTE] 
> Para restaurar um banco de dados do SQL Server no Linux, o backup de origem deve ser extraído do SQL Server 2014 ou SQL Server 2016. O número da compilação do SQL Server de backup não deve ser maior que o número da compilação do SQL Server de restauração.  

1. Em seu computador Windows, acesse [https://msftdbprodsamples.codeplex.com/downloads/get/880661](https://msftdbprodsamples.codeplex.com/downloads/get/880661) e baixe o **Backup.zip de banco de dados completo do Adventure Works 2014**.

   > [!TIP] 
   > Embora este tutorial demonstra o backup e restauração entre o Windows e Linux, você também pode usar um navegador no Linux para baixar o exemplo AdventureWorks diretamente computador Linux.

2. Abra o arquivo zip e extraia o arquivo de AdventureWorks2014.bak para uma pasta no seu computador.

## <a name="transfer-the-backup-file-to-linux"></a>Transferir o arquivo de backup para Linux

Para restaurar o banco de dados, é necessário primeiro transferir o arquivo de backup do computador Windows para o computador Linux de destino.

1. Para Windows, instale um shell Bash. Há várias opções, incluindo o seguinte:

   - Baixar um software livre shell Bash, tais como [PuTTY](http://www.putty.org/).
   - Ou, no Windows 10, use o novo [interna do shell Bash (beta)](https://msdn.microsoft.com/en-us/commandline/wsl/about).
   - Ou, se você trabalha com o Git, use o [Git Bash shell](https://git-scm.com/downloads).

2. Abra um shell Bash (terminal) e navegue até o diretório que contém **AdventureWorks2014.bak**.

3. Use o **scp** comando (cópia seguro) para transferir o arquivo para o computador Linux de destino. As transferências de exemplo a seguir **AdventureWorks2014.bak** para o diretório base de *user1* no servidor chamado *linuxserver1*.

   ```bash
   sudo scp AdventureWorks2014.bak user1@linuxserver1:./
   ```
   
   No exemplo anterior, em vez disso, você pode fornecer o endereço IP no lugar do nome do servidor.

Há várias alternativas para usar o scp. Uma é usar [Samba](https://help.ubuntu.com/community/Samba) para configurar um compartilhamento de rede SMB entre o Windows e Linux. Para obter uma explicação sobre Ubuntu, consulte [como criar um compartilhamento de rede por meio do Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!). Depois de estabelecida, você pode acessá-lo como um arquivo de rede compartilham do Windows, tais como  **\\ \\machinenameorip\\compartilhar**.

## <a name="move-the-backup-file"></a>Mover o arquivo de backup

Neste ponto, o arquivo de backup está em seu servidor Linux. Antes de restaurar o banco de dados para o SQL Server, você deve colocar o backup em um subdiretório do **/var/opt/mssql**.

1. Abra um Terminal no computador Linux de destino que contém o backup.

2. Entre no modo de superusuário.

   ```bash
   sudo su
   ```

3. Crie um novo diretório de backup. O parâmetro -p não fará nada se o diretório já existe.

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

4. Mova o arquivo de backup para esse diretório. No exemplo a seguir, o arquivo de backup reside no diretório base do *user1*. Alterar o comando para corresponder à localidade de **AdventureWorks2014.bak** em seu computador.

   ```bash
   mv /home/user1/AdventureWorks2014.bak /var/opt/mssql/backup/
   ```

5. Sair do modo de superusuário.

   ```bash
   exit
   ```

## <a name="restore-the-database-backup"></a>Restaure o backup do banco de dados

Para restaurar o backup, você pode usar o comando de restauração do banco de dados Transact-SQL (TQL).

> [!NOTE] 
> As etapas a seguir usam a ferramenta sqlcmd. Se você ainda não instalar as ferramentas do SQL Server, consulte [instalar o SQL Server no Linux](sql-server-linux-setup.md).

1. No mesmo terminal, inicie **sqlcmd**. O exemplo a seguir se conecta à instância do SQL Server local com o *SA* usuário. Digite a senha quando solicitado ou especifique a senha com o parâmetro -P.

   ```bash
   sqlcmd -S localhost -U SA
   ```

2. Depois de se conectar, digite o seguinte **RESTAURAR banco de dados** comando, pressionar ENTER depois de cada linha. O exemplo a seguir restaura o **AdventureWorks2014.bak** arquivo o */var/opt/mssql/backup* directory.

   ```sql
   RESTORE DATABASE AdventureWorks
   FROM DISK = '/var/opt/mssql/backup/AdventureWorks2014.bak'
   WITH MOVE 'AdventureWorks2014_Data' TO '/var/opt/mssql/data/AdventureWorks2014_Data.mdf',
   MOVE 'AdventureWorks2014_Log' TO '/var/opt/mssql/data/AdventureWorks2014_Log.ldf'
   GO
   ```

   Você deve receber uma mensagem que o banco de dados for restaurado com êxito.

3. Verifique se a restauração pelo primeiro alterar o contexto para o banco de dados AdventureWorks. 

   ```sql
   USE AdventureWorks
   GO
   ```

4. Execute a consulta a seguir que lista os 10 principais produtos no **Production** tabela.

   ```sql
   SELECT TOP 10 Name, ProductNumber FROM Production.Product ORDER BY Name
   GO
   ```

![Saída de consulta Production](./media/sql-server-linux-migrate-restore-database/sql-server-linux-adventureworks-query.png)

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outras técnicas de migração e banco de dados, consulte [Migrar bancos de dados para o SQL Server no Linux](sql-server-linux-migrate-overview.md). 

