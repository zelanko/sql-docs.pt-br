1. **Em todos os SQL Servers, crie um logon de servidor para Pacemaker**. O Transact-SQL a seguir cria um logon:

   ```Transact-SQL
   USE [master]
   GO
   CREATE LOGIN [pacemakerLogin] with PASSWORD= N'ComplexP@$$w0rd!'
    
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [pacemakerLogin]
   ```

  No momento da criação do grupo de disponibilidade, o usuário do Pacemaker precisará das permissões ALTERAR, CONTROLAR e EXIBIR DEFINIÇÃO no grupo de disponibilidade, após ele ser criado mas antes que os nós sejam adicionados a ele.

1. **Em todos os SQL Servers, salve as credenciais do logon do SQL Server**.

   ```bash
   echo 'pacemakerLogin' >> ~/pacemaker-passwd
   echo 'ComplexP@$$w0rd!' >> ~/pacemaker-passwd
   sudo mv ~/pacemaker-passwd /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd
   sudo chmod 400 /var/opt/mssql/secrets/passwd # Only readable by root
   ```
