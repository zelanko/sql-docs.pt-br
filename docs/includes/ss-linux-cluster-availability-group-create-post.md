
## <a name="add-a-database-to-the-availability-group"></a>Adicionar um banco de dados ao grupo de disponibilidade

Certifique-se de que o banco de dados que você adicionar ao grupo de disponibilidade está em modo de recuperação completa e tem um backup de log válido. Se esse for um banco de dados de teste ou um banco de dados recém-criado, faça um backup de banco de dados. No SQL Server primário, execute o seguinte script do Transact-SQL para criar e fazer backup de um banco de dados chamado `db1`:

```sql
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1] 
   TO DISK = N'/var/opt/mssql/data/db1.bak';
```

Na réplica primária do SQL Server, execute o seguinte script do Transact-SQL para adicionar um banco de dados chamado `db1` para um grupo de disponibilidade chamado `ag1`:

```sql
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>Verificar se o banco de dados foi criado nos servidores secundários

Em cada réplica secundária do SQL Server, execute a seguinte consulta para ver se o `db1` banco de dados foi criado e será sincronizado:

```sql
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
