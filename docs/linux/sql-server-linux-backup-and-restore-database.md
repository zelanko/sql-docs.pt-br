---
title: Fazer backup e restaurar bancos de dados do SQL Server no Linux | Microsoft Docs
description: Saiba como fazer backup e restaurar bancos de dados do SQL Server no Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/14/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.openlocfilehash: f07885aaef22da63d1c94e669db17e7536ccc933
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713351"
---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>Backup e restauração de bancos de dados do SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Você pode fazer backups de bancos de dados do SQL Server 2017 no Linux com as mesmas ferramentas que outras plataformas. Em um servidor Linux, você pode usar **sqlcmd** para se conectar ao SQL Server e fazer backups. Do Windows, você pode se conectar ao SQL Server no Linux e fazer backups com a interface do usuário. A funcionalidade de backup é o mesmo entre plataformas. Por exemplo, você pode fazer backup de bancos de dados localmente, em unidades remotas ou a [serviço de armazenamento de BLOBs do Microsoft Azure](../relational-databases/backup-restore/sql-server-backup-to-url.md).

## <a name="backup-a-database"></a>Fazer backup de um banco de dados

No exemplo a seguir **sqlcmd** conecta-se à instância do SQL Server local e usa uma completa de backup de um usuário de banco de dados chamado `demodb`.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'/var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
```

Quando você executar o comando, o SQL Server solicitará uma senha. Depois de inserir a senha, o shell retornará os resultados do andamento do backup. Por exemplo:

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

### <a name="backup-the-transaction-log"></a>Fazer backup do log de transação

Se seu banco de dados no modelo de recuperação completa, você também pode fazer backups de log de transações para as opções de restauração mais granulares. No exemplo a seguir **sqlcmd** conecta-se à instância do SQL Server local e faz um log de transações backup.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP LOG [demodb] TO DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak' WITH NOFORMAT, NOINIT, NAME = N'demodb_LogBackup', NOSKIP, NOREWIND, NOUNLOAD, STATS = 5"
```

## <a name="restore-a-database"></a>Restaurar um banco de dados

No exemplo a seguir **sqlcmd** conecta-se à instância local do SQL Server e restaura o banco de dados demodb. Observe que o `NORECOVERY` opção é usada para permitir que as restaurações de backups de arquivos de log adicionais. Se você não planeja restaurar os arquivos de log adicionais, remova o `NORECOVERY` opção.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE DATABASE [demodb] FROM DISK = N'/var/opt/mssql/data/demodb.bak' WITH FILE = 1, NOUNLOAD, REPLACE, NORECOVERY, STATS = 5"
```

> [!TIP]
> Se você acidentalmente use NORECOVERY, mas não tem backups de arquivos de log adicionais, execute o comando `RESTORE DATABASE demodb` sem parâmetros adicionais. Isso conclui a restauração e deixa seu banco de dados operacional.

### <a name="restore-the-transaction-log"></a>Restaurar o log de transações

O comando a seguir restaura o backup de log de transação anterior.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE LOG demodb FROM DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak'"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>Backup e restauração com o SQL Server Management Studio (SSMS)

Você pode usar o SSMS em um computador Windows para se conectar a um banco de dados do Linux e faça um backup por meio da interface do usuário.

>[!NOTE] 
> Use a versão mais recente do SSMS para conectar-se ao SQL Server. Para baixar e instalar a versão mais recente, consulte [baixar o SSMS](../ssms/download-sql-server-management-studio-ssms.md). Para obter mais informações sobre como usar o SSMS, consulte [usar o SSMS para gerenciar o SQL Server no Linux](sql-server-linux-manage-ssms.md).

As seguintes etapas orientam por meio de um backup com o SSMS. 

1. Inicie o SSMS e conecte-se ao seu servidor no SQL Server 2017 no Linux.

1. No Pesquisador de objetos, clique com botão direito no banco de dados, clique em **tarefas**e, em seguida, clique em **fazer backup...** .

1. No **Backup do backup de banco de dados** caixa de diálogo, verifique se os parâmetros e as opções e, em seguida, clique em **Okey**.
 
SQL Server conclui o backup do banco de dados.

### <a name="restore-with-sql-server-management-studio-ssms"></a>Restauração com o SQL Server Management Studio (SSMS) 

As etapas a seguir orientam você pelo processo de restauração de um banco de dados com o SSMS.

1. No SSMS com o botão direito **bancos de dados** e clique em **restaurar bancos de dados...** . 

1. Sob **fonte** clique em **dispositivo:** e, em seguida, clique nas reticências (...).

1. Localize o arquivo de backup do banco de dados e clique em **Okey**. 

1. Sob **plano de restauração**, verifique se as configurações e o arquivo de backup. Clique em **OK**. 

1. SQL Server restaura o banco de dados. 

## <a name="see-also"></a>Confira também

* [Criar um Backup de banco de dados completo (SQL Server)](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
* [Fazer backup de um Log de transações (SQL Server)](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)
* [BACKUP (Transact-SQL)](../t-sql/statements/backup-transact-sql.md)
* [Backup do SQL Server para URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)
