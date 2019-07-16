---
ms.openlocfilehash: 0cdc343bf4ea6866d1a55672187451a3b6d95ec1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68215586"
---

## <a name="add-a-database-to-the-availability-group"></a>Adicionar um banco de dados ao grupo de disponibilidade

Verifique se o banco de dados adicionado ao grupo de disponibilidade está em modo de recuperação completa e tem um backup de log válido. Se esse for um banco de dados de teste ou um banco de dados recém-criado, faça um backup de banco de dados. No SQL Server primário, execute o seguinte script Transact-SQL para criar e fazer backup de um banco de dados chamado `db1`:

```sql
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1] 
   TO DISK = N'/var/opt/mssql/data/db1.bak';
```

Na réplica primária do SQL Server, execute o seguinte script Transact-SQL para adicionar um banco de dados chamado `db1` a um grupo de disponibilidade denominado `ag1`:

```sql
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>Verificar se o banco de dados foi criado nos servidores secundários

Em cada réplica secundária do SQL Server, execute a consulta a seguir para ver se o banco de dados `db1` foi criado e está sincronizado:

```sql
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
