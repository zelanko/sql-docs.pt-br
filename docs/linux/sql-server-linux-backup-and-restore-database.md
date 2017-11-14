---
title: Fazer backup e restaurar bancos de dados do SQL Server no Linux | Microsoft Docs
description: Saiba como fazer backup e restaurar bancos de dados do SQL Server no Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: a34954f14ad4c40fdc7376f3f35c6a3def6e2ec7
ms.contentlocale: pt-br
ms.lasthandoff: 10/02/2017

---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>Backup e restauração de bancos de dados do SQL Server no Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Você pode usar backups de bancos de dados do 2017 do SQL Server no Linux com as mesmas ferramentas de outras plataformas. Em um servidor Linux, você pode usar `sqlcmd` para se conectar ao SQL Server e fazer backups. No Windows, você pode se conectar ao SQL Server no Linux e fazer backups com a interface do usuário. A funcionalidade de backup é o mesmo entre plataformas. Por exemplo, você pode fazer backup de bancos de dados localmente, para unidades remotas ou a [serviço de armazenamento de BLOBs do Microsoft Azure](http://msdn.microsoft.com/library/dn435916.aspx). 

## <a name="backup-with-sqlcmd"></a>Backup com sqlcmd

No exemplo a seguir `sqlcmd` conecta-se à instância do SQL Server local e faz um completo backup de um banco de dados de usuário chamado `demodb`.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'/var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
```

Quando você executar o comando, o SQL Server solicitará uma senha. Depois de inserir a senha, o shell retornará os resultados do progresso do backup. Por exemplo:

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

### <a name="backup-log-with-sqlcmd"></a>Log de backup com sqlcmd

No exemplo a seguir, `sqlcmd` se conecta à instância do SQL Server local e faz uma final do log backup. Após o backup da parte final do log, o banco de dados estará no estado de restauração. 

```bash
sqlcmd -S localhost -U SA -Q "BACKUP LOG [demodb] TO  DISK = N'/var/opt/mssql/data/demodb_LogBackup_2016-11-14_18-09-53.bak' WITH NOFORMAT, NOINIT,  NAME = N'demodb_LogBackup_2016-11-14_18-09-53', NOSKIP, NOREWIND, NOUNLOAD,  NORECOVERY ,  STATS = 5"
```

## <a name="restore-with-sqlcmd"></a>Restaurar com sqlcmd

No exemplo a seguir `sqlcmd` conecta-se à instância local do SQL Server e restaura um banco de dados.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE DATABASE [demodb] FROM  DISK = N'/var/opt/mssql/data/demodb.bak' WITH  FILE = 1,  NOUNLOAD,  REPLACE,  STATS = 5"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>Backup e restauração com o SQL Server Management Studio (SSMS)

Você pode usar o SSMS em um computador Windows para se conectar a um banco de dados do Linux e faça um backup por meio da interface de usuário. 

>[!NOTE] 
> Use a versão mais recente do SSMS para conectar-se ao SQL Server. Para baixar e instalar a versão mais recente, consulte [baixar o SSMS](http://msdn.microsoft.com/library/mt238290.aspx). 

As etapas a seguir percorrer fazer um backup com o SSMS. 

1. Inicie o SSMS e conectar-se ao seu servidor no SQL Server 2017 no Linux.

1. No Pesquisador de objetos, clique com botão direito no banco de dados, clique em **tarefas**e, em seguida, clique em **backup...** .

1. No **Backup backup de banco de dados** caixa de diálogo, verifique se os parâmetros e as opções e, em seguida, clique em **Okey**.
 
SQL Server conclui o backup do banco de dados.

Para obter mais informações, consulte [Use SSMS para gerenciar o SQL Server no Linux](sql-server-linux-manage-ssms.md).

### <a name="restore-with-sql-server-management-studio-ssms"></a>Restaurar com o SQL Server Management Studio (SSMS) 

As etapas a seguir orientam você durante a restauração de um banco de dados com o SSMS.

1. No SSMS clique **bancos de dados** e clique em **restaurar bancos de dados...** . 

1. Em **fonte** clique **dispositivo:** e, em seguida, clique nas reticências (...).

1. Localize o arquivo de backup do banco de dados e clique em **Okey**. 

1. Em **plano de restauração**, verifique se o arquivo de backup e configurações. Clique em **OK**. 

1. SQL Server restaura o banco de dados. 

## <a name="see-also"></a>Consulte também

* [Criar um Backup de banco de dados completo (SQL Server)](http://msdn.microsoft.com/library/ms187510.aspx)
* [Fazer backup de um Log de transações (SQL Server)](http://msdn.microsoft.com/library/ms179478.aspx)
* [BACKUP (Transact-SQL)](http://msdn.microsoft.com/library/ms186865.aspx)
* [Backup do SQL Server para URL](http://msdn.microsoft.com/library/dn435916.aspx)

