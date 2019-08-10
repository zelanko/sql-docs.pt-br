---
title: Fazer backup dos bancos de dados do SQL Server no Linux e restaurá-los
description: Aprenda a backup dos bancos de dados do SQL Server no Linux e restaurá-los.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 11/14/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.openlocfilehash: f3e27b283156bb23754a93161fc796e15baec7ea
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077688"
---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>Fazer backup dos bancos de dados do SQL Server no Linux e restaurá-los

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Você pode fazer backups de bancos de dados do SQL Server 2017 no Linux com as mesmas ferramentas que em outras plataformas. Em um servidor Linux, você pode usar o **sqlcmd** para se conectar ao SQL Server e fazer backups. No Windows, você pode se conectar a SQL Server em Linux e fazer backups com a interface do usuário. A funcionalidade de backup é a mesma entre plataformas. Por exemplo, você pode fazer backup de bancos de dados localmente, em unidades remotas ou no [serviço de Armazenamento de Blobs do Microsoft Azure](../relational-databases/backup-restore/sql-server-backup-to-url.md).

## <a name="backup-a-database"></a>Fazer backup de um banco de dados

No exemplo a seguir, o **sqlcmd** se conecta à instância de SQL Server local e faz um backup completo de um banco de dados de usuário chamado `demodb`.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'/var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
```

Quando você executa o comando, o SQL Server solicita uma senha. Depois de inserir a senha, o Shell retornará os resultados do progresso do backup. Por exemplo:

```
Password:
10 percent processed.
21 percent processed.
32 percent processed.
40 percent processed.
51 percent processed.
61 percent processed.
72 percent processed.
80 percent processed.
91 percent processed.
Processed 296 pages for database 'demodb', file 'demodb' on file 1.
100 percent processed.
Processed 2 pages for database 'demodb', file 'demodb_log' on file 1.
BACKUP DATABASE successfully processed 298 pages in 0.064 seconds (36.376 MB/sec).
```

### <a name="backup-the-transaction-log"></a>Fazer backup do log de transações

Se o banco de dados estiver no modelo de recuperação completa, você também poderá fazer backups de log de transações para obter opções de restauração mais granulares. No exemplo a seguir, o **sqlcmd** se conecta à instância do SQL Server local e faz um backup completo do log de transações.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP LOG [demodb] TO DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak' WITH NOFORMAT, NOINIT, NAME = N'demodb_LogBackup', NOSKIP, NOREWIND, NOUNLOAD, STATS = 5"
```

## <a name="restore-a-database"></a>Restaurar um banco de dados

No exemplo a seguir, o **sqlcmd** se conecta à instância local do SQL Server e restaura o banco de dados demodb. Observe que a opção `NORECOVERY` é usada para permitir restaurações adicionais de backups de arquivo de log. Se você não planeja restaurar arquivos de log adicionais, remova a opção `NORECOVERY`.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE DATABASE [demodb] FROM DISK = N'/var/opt/mssql/data/demodb.bak' WITH FILE = 1, NOUNLOAD, REPLACE, NORECOVERY, STATS = 5"
```

> [!TIP]
> Se você usar NORECOVERY acidentalmente, mas não tiver backups de arquivo de log adicionais, execute o comando `RESTORE DATABASE demodb` sem parâmetros adicionais. Isso conclui a restauração e deixa o banco de dados operacional.

### <a name="restore-the-transaction-log"></a>Restaurar o log de transações

O comando a seguir restaura o backup de log de transações anterior.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE LOG demodb FROM DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak'"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>Backup e restauração com SSMS (SQL Server Management Studio)

Você pode usar o SSMS de um computador Windows para se conectar a um banco de dados Linux e fazer um backup por meio da interface do usuário.

>[!NOTE] 
> Use a versão mais recente do SSMS para se conectar ao SQL Server. Para baixar e instalar a última versão, confira [Baixar o SSMS](../ssms/download-sql-server-management-studio-ssms.md). Para obter mais informações sobre como usar o SSMS, confira [Usar o SSMS para gerenciar o SQL Server em Linux](sql-server-linux-manage-ssms.md).

As etapas a seguir demonstram como fazer um backup com o SSMS. 

1. Inicie o SSMS e conecte-se ao servidor no SQL Server 2017 em Linux.

1. No Pesquisador de Objetos, clique com o botão direito do mouse no banco de dados, clique em **Tarefas** e clique na página **Fazer Backup...** .

1. Na caixa de diálogo **Fazer Backup de Banco de Dados**, verifique os parâmetros e as opções e clique em **OK**.
 
O SQL Server conclui o backup do banco de dados.

### <a name="restore-with-sql-server-management-studio-ssms"></a>Restauração com SSMS (SQL Server Management Studio) 

As etapas a seguir orientarão você pela restauração de um banco de dados com o SSMS.

1. No SSMS, clique com o botão direito do mouse em **Bancos de Dados** e clique em **Restaurar Bancos de Dados...** . 

1. Em **Origem**, clique em **Dispositivo:** e, em seguida, clique nas reticências (...).

1. Localize o arquivo de backup do banco de dados e clique em **OK**. 

1. Em **Restaurar plano**, verifique as configurações e o arquivo de backup. Clique em **OK**. 

1. O SQL Server restaura o banco de dados. 

## <a name="see-also"></a>Confira também

* [Criar um backup completo de banco de dados (SQL Server)](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
* [Fazer backup de um log de transações (SQL Server)](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)
* [BACKUP (Transact-SQL)](../t-sql/statements/backup-transact-sql.md)
* [Backup do SQL Server para URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)
