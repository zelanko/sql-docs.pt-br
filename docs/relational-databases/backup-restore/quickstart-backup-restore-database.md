---
title: 'Início Rápido: Backup e restauração de banco de dados local do SQL Server'
titleSuffix: SQL Server
description: Este início rápido mostra como executar o SQL Server em Linux na sua nuvem preferida.
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.date: 05/25/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: ''
ms.technology: backup-restore
ms.prod_service: backup-restore
ms.assetid: ''
ms.openlocfilehash: 8453d74227e1007a42adfbd8ac1f91bf1a6d86da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66499669"
---
# <a name="quickstart-backup-and-restore-a-sql-server-database-on-premises"></a>Início Rápido: Backup e restauração de banco de dados local do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste início rápido, você criará um novo banco de dados, fará um backup simples dele e o restaurará. 

Para ver instruções mais detalhadas, confira [Criar um backup completo de banco de dados](create-a-full-database-backup-sql-server.md) e [Restaurar um backup usando o SSMS](restore-a-database-backup-using-ssms.md).

## <a name="prerequisites"></a>Prerequisites
Para concluir este início rápido, você precisará do seguinte: 

- [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [SSMS (SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md)

## <a name="create-a-test-database"></a>Criar um banco de dados de teste 

1. Inicie o [SSMS (SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md) e conecte-se à instância do SQL Server.
1. Abra uma janela **Nova Consulta**. 
1. Execute o seguinte código T-SQL (Transact-SQL) para criar o banco de dados de teste. Atualize o nó **Bancos de Dados** no **Pesquisador de Objetos** para ver o novo banco de dados. 

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest (
    ID INT NOT NULL PRIMARY KEY,
    c1 VARCHAR(100) NOT NULL,
    dt1 DATETIME NOT NULL DEFAULT getdate()
)
GO


USE [SQLTestDB]
GO

INSERT INTO SQLTest (ID, c1) VALUES (1, 'test1')
INSERT INTO SQLTest (ID, c1) VALUES (2, 'test2')
INSERT INTO SQLTest (ID, c1) VALUES (3, 'test3')
INSERT INTO SQLTest (ID, c1) VALUES (4, 'test4')
INSERT INTO SQLTest (ID, c1) VALUES (5, 'test5')
GO

SELECT * FROM SQLTest
GO
```
 
## <a name="take-a-backup"></a>Fazer um backup
Para fazer backup do banco de dados, siga estas instruções: 

1. Inicie o [SSMS (SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md) e conecte-se à instância do SQL Server.
1. Expanda o nó **Bancos de Dados** no **Pesquisador de Objetos**.  
1. Clique com o botão direito do mouse no banco de dados, passe o cursor sobre **Tarefas** e clique em **Fazer Backup...** . 
1. Em **Destino**, confirme se o caminho do backup está correto. Se for necessário alterá-lo, clique em **Remover** para excluir o caminho existente e em **Adicionar** para digitar outro. É possível usar as reticências para navegar para um arquivo específico. 
1. Clique em **OK** para fazer backup do banco de dados. 

![Fazer backup do SQL](media/quickstart-backup-restore-database/backup-db-ssms.png)

Outra alternativa é executar o seguinte comando Transact-SQL para fazer backup do banco de dados: 

```sql
BACKUP DATABASE [SQLTestDB] 
TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Backup\SQLTestDB.bak' 
WITH NOFORMAT, NOINIT,  
NAME = N'SQLTestDB-Full Database Backup', SKIP, NOREWIND, NOUNLOAD,  STATS = 10
GO
```


## <a name="restore-a-backup"></a>Restaurar um backup
Para restaurar o banco de dados, faça o seguinte: 

1. Inicie o [SSMS (SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md) e conecte-se à instância do SQL Server.
1. Clique com o botão direito do mouse no nó **Bancos de Dados** no **Pesquisador de Objetos** e clique em **Restaurar Banco de Dados...** .

    ![Restaurar um banco de dados](media/quickstart-backup-restore-database/restore-db-ssms1.png)

1. Clique em **Dispositivo:** e, em seguida, clique nas reticências (…) para localizar o arquivo de backup. 
1. Clique em **Adicionar** e navegue para o local do arquivo `.bak`. Clique no arquivo `.bak` e em **OK**. 
1. Clique em **OK** para fechar a caixa de diálogo **Selecionar dispositivos de backup**. 
1. Clique em **OK** para restaurar o backup do banco de dados. 

    ![Restaurar o banco de dados](media/quickstart-backup-restore-database/restore-db-ssms2.png)

Outra alternativa é executar o seguinte script Transact-SQL para restaurar o banco de dados:

```sql
USE [master]
RESTORE DATABASE [SQLTestDB] 
FROM DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Backup\SQLTestDB.bak' WITH  FILE = 1,  NOUNLOAD,  STATS = 5
GO
```

### <a name="clean-up-resources"></a>Limpar os recursos
Execute o comando Transact-SQL a seguir para remover o banco de dados criado junto com o histórico de backup no banco de dados MSDB:

```sql
EXEC msdb.dbo.sp_delete_database_backuphistory @database_name = N'SQLTestDB'
GO

USE [master]
DROP DATABASE [SQLTestDB]
GO
```

## <a name="see-more"></a>Ver mais
[Visão geral de como fazer backup e restaurar](back-up-and-restore-of-sql-server-databases.md)
[Backup para URL](sql-server-backup-to-url.md)
[Criar um backup completo](create-a-full-database-backup-sql-server.md)
[Restaurar um backup de banco de dados](restore-a-database-backup-using-ssms.md)
