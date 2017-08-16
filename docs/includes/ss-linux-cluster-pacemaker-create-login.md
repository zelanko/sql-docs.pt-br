1. **Em todos os SQL Servers, crie um logon de servidor para Pacemaker**. O Transact-SQL a seguir cria um logon:

   ```Transact-SQL
   USE [master]
   GO
   CREATE LOGIN [pacemakerLogin] with PASSWORD= N'ComplexP@$$w0rd!'
    
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [pacemakerLogin]
   ```

   Alternativamente, você pode definir as permissões em um nível mais granular. O logon de Pacemaker requer permissão ALTER, CONTROL e VIEW DEFINITION para gerenciar o grupo de disponibilidade, bem como VIEW SERVER STATE para que o logon possa executar sp_server_diagnostics. Para obter mais informações, consulte [Permissões de grupo de disponibilidade GRANT (Transact-SQL)](http://msdn.microsoft.com/library/hh968934.aspx) e [permissões do sp_server_diagnostic](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql#permissions).

   O Transact-SQL a seguir concede somente a permissão necessária para o logon do Pacemaker. A instrução abaixo de 'ag1' é o nome do grupo de disponibilidade que será adicionado como um recurso de cluster.

   ```Transact-SQL
   GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::ag1 TO pacemakerLogin
   GRANT VIEW SERVER STATE TO pacemakerLogin
   ```

1. **Em todos os SQL Servers, salve as credenciais do logon do SQL Server**.

   ```bash
   echo 'pacemakerLogin' >> ~/pacemaker-passwd
   echo 'ComplexP@$$w0rd!' >> ~/pacemaker-passwd
   sudo mv ~/pacemaker-passwd /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd
   sudo chmod 400 /var/opt/mssql/secrets/passwd # Only readable by root
   ```
