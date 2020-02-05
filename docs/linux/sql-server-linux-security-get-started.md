---
title: Introdução à segurança do SQL Server em Linux
description: Este artigo descreve as ações de segurança típicas.
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.openlocfilehash: 1e64ce76ef2528c96ecc0206b7a56b31d4c95ef7
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68019503"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>Passo a passo dos recursos de segurança do SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Se você for um usuário do Linux não familiarizado com o SQL Server, as tarefas a seguir o orientarão em algumas das tarefas de segurança. Elas não são exclusivas nem específicas do Linux, mas ajudam a dar uma ideia de áreas para posterior investigação. Em cada exemplo, um link é fornecido para a documentação detalhada dessa área.

> [!NOTE]
>  Os exemplos a seguir usam o banco de dados de exemplo **AdventureWorks2014**. Para obter instruções sobre como obter e instalar esse banco de dados de exemplo, confira [Restaurar um banco de dados do SQL Server do Windows para o Linux](sql-server-linux-migrate-restore-database.md).


## <a name="create-a-login-and-a-database-user"></a>Criar um logon e um usuário de banco de dados 

Permite a outros usuários o acesso ao SQL Server criando um logon no banco de dados mestre usando a instrução [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md). Por exemplo:

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

> [!NOTE]
>  Sempre use uma senha forte no lugar dos asteriscos no comando anterior.

Os logons podem se conectar ao SQL Server e ter acesso (com permissões limitadas) ao banco de dados mestre. Para se conectar a um banco de dados de usuário, um logon precisa ter uma identidade correspondente no nível de banco de dados, chamada usuário de banco de dados. Os usuários são específicos de cada banco de dados e precisam ser criados separadamente em cada banco de dados para permitir acesso a eles. O exemplo a seguir insere você no banco de dados AdventureWorks2014 e, em seguida, usa a instrução [CREATE USER](../t-sql/statements/create-user-transact-sql.md) para criar um usuário chamado Paulo que está associado ao logon chamado Paulo. Embora o logon e o usuário estejam relacionados (mapeados entre si), eles são objetos diferentes. O logon é uma entidade de segurança no nível do servidor. O usuário é uma entidade de segurança no nível do banco de dados.

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- Uma conta de administrador do SQL Server pode se conectar a qualquer banco de dados e pode criar mais logons e usuários em qualquer banco de dados.  
- Quando alguém cria um banco de dados, ele se torna o proprietário do banco de dados, que pode se conectar a esse banco de dados. Os proprietários do banco de dados podem criar mais usuários.

Posteriormente, você pode autorizar outros logons a criar mais logons, concedendo a eles a permissão `ALTER ANY LOGIN`. Em um banco de dados, você pode autorizar outros usuários a criarem mais usuários concedendo a eles a permissão `ALTER ANY USER`. Por exemplo:   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

Agora o logon Paulo pode criar mais logons e o usuário Marco pode criar mais usuários.


## <a name="granting-access-with-least-privileges"></a>Como permitir acesso com privilégios mínimos

As primeiras pessoas a se conectarem a um banco de dados de usuário serão as contas de administrador e proprietário do banco de dados. No entanto, esses usuários têm todas as permissões disponíveis no banco de dados. Isso representa um número de permissões além do que a maioria dos usuários deve ter. 

Quando você estiver apenas começando, poderá atribuir algumas categorias gerais de permissões usando as *funções de banco de dados fixas* internas. Por exemplo, a função de banco de dados fixa `db_datareader` pode ler todas as tabelas no banco de dados, mas não pode fazer nenhuma alteração. Permita a associação em uma função de banco de dados fixa usando a instrução [ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md). O exemplo a seguir adiciona o usuário `Jerry` à função de banco de dados fixa `db_datareader`.   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

Para obter uma lista das funções de banco de dados fixas, confira [Funções no nível do banco de dados](../relational-databases/security/authentication-access/database-level-roles.md).

Posteriormente, quando estiver pronto para configurar o acesso mais preciso aos seus dados (altamente recomendado), crie suas próprias funções de banco de dados definidas pelo usuário usando a instrução [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md). Em seguida, atribua permissões granulares específicas às funções personalizadas.

Por exemplo, as instruções a seguir criam uma função de banco de dados chamada `Sales`, concede ao grupo `Sales` a capacidade de ver, atualizar e excluir linhas da tabela `Orders` e, em seguida, adiciona o usuário `Jerry` à função `Sales`.   
   
```   
CREATE ROLE Sales;   
GRANT SELECT ON Object::Sales TO Orders;   
GRANT UPDATE ON Object::Sales TO Orders;   
GRANT DELETE ON Object::Sales TO Orders;   
ALTER ROLE Sales ADD MEMBER Jerry;   
```   

For more information about the permission system, see [Getting Started with Database Engine Permissions](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).


## Configure row-level security  

[Row-Level Security](../relational-databases/security/row-level-security.md) enables you to restrict access to rows in a database based on the user executing a query. This feature is useful for scenarios like ensuring that customers can only access their own data or that workers can only access data that is pertinent to their department.   

The following steps walk through setting up two Users with different row-level access to the `Sales.SalesOrderHeader` table. 

Create two user accounts to test the row level security:    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```   

Grant read access on the `Sales.SalesOrderHeader` table to both users:    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;    
```   
   
Create a new schema and inline table-valued function. The function returns 1 when a row in the `SalesPersonID` column matches the ID of a `SalesPerson` login or if the user executing the query is the Manager user.   
   
```     
CREATE SCHEMA Security;   
GO   
   
CREATE FUNCTION Security.fn_securitypredicate(@SalesPersonID AS int)     
    RETURNS TABLE   
WITH SCHEMABINDING   
AS     
   RETURN SELECT 1 AS fn_securitypredicate_result    
WHERE ('SalesPerson' + CAST(@SalesPersonId as VARCHAR(16)) = USER_NAME())     
    OR (USER_NAME() = 'Manager');    
```   

Create a security policy adding the function as both a filter and a block predicate on the table:  

```
CREATE SECURITY POLICY SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

Execute the following to query the `SalesOrderHeader` table as each user. Verify that `SalesPerson280` only sees the 95 rows from their own sales and that the `Manager` can see all the rows in the table.  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERT; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERT;   
```
 
Alter the security policy to disable the policy.  Now both users can access all rows. 

```
ALTER SECURITY POLICY SalesFilter   
WITH (STATE = OFF);    
``` 


## Enable dynamic data masking

[Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md) enables you to limit the exposure of sensitive data to users of an application by fully or partially masking certain columns. 

Use an `ALTER TABLE` statement to add a masking function to the `EmailAddress` column in the `Person.EmailAddress` table: 
 
```
USE AdventureWorks2014; GO ALTER TABLE Person.EmailAddress     ALTER COLUMN EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
Create a new user `TestUser` with `SELECT` permission on the table, then execute a query as `TestUser` to view the masked data:   

```  
CREATE USER TestUser WITHOUT LOGIN;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERT;    
```
 
Verify that the masking function changes the email address in the first record from:
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## Enable Transparent Data Encryption

One threat to your database is the risk that someone will steal the database files off of your hard-drive. This could happen with an intrusion that gets elevated access to your system, through the actions of a problem employee, or by theft of the computer containing the files (such as a laptop).

Transparent Data Encryption (TDE) encrypts the data files as they are stored on the hard drive. The master database of the SQL Server database engine has the encryption key, so that the database engine can manipulate the data. The database files cannot be read without access to the key. High-level administrators can manage, backup, and recreate the key, so the database can be moved, but only by selected people. When TDE is configured, the `tempdb` database is also automatically encrypted. 

Since the Database Engine can read the data, Transparent Data Encryption does not protect against unauthorized access by administrators of the computer who can directly read memory, or access SQL Server through an administrator account.

### Configure TDE

- Create a master key
- Create or obtain a certificate protected by the master key
- Create a database encryption key and protect it by the certificate
- Set the database to use encryption

Configuring TDE requires `CONTROL` permission on the master database and `CONTROL` permission on the user database. Typically an administrator configures TDE. 

The following example illustrates encrypting and decrypting the `AdventureWorks2014` database using a certificate installed on the server named `MyServerCert`.


```
USE master;  
GO  

CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**********';  
GO  

CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My Database Encryption Key Certificate';  
GO  

USE AdventureWorks2014;   GO
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO
  
ALTER DATABASE AdventureWorks2014  
SET ENCRYPTION ON;   
```

To remove TDE, execute `ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;`   

The encryption and decryption operations are scheduled on background threads by SQL Server. You can view the status of these operations using the catalog views and dynamic management views in the list that appears later in this topic.   

> [!WARNING]
>  Backup files of databases that have TDE enabled are also encrypted by using the database encryption key. As a result, when you restore these backups, the certificate protecting the database encryption key must be available. This means that in addition to backing up the database, you have to make sure that you maintain backups of the server certificates to prevent data loss. Data loss will result if the certificate is no longer available. For more information, see [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  

For more information about TDE, see [Transparent Data Encryption (TDE)](../relational-databases/security/encryption/transparent-data-encryption-tde.md).   


## Configure backup encryption
SQL Server has the ability to encrypt the data while creating a backup. By specifying the encryption algorithm and the encryptor (a certificate or asymmetric key) when creating a backup, you can create an encrypted backup file.    
  
> [!WARNING]  
>  It is very important to back up the certificate or asymmetric key, and preferably to a different location than the backup file it was used to encrypt. Without the certificate or asymmetric key, you cannot restore the backup, rendering the backup file unusable. 
 
 
The following example creates a certificate, and then creates a backup protected by the certificate.
```
USE master;   GO   CREATE CERTIFICATE BackupEncryptCert   WITH SUBJECT = 'Database backups';   GO BACKUP DATABASE [AdventureWorks2014]   TO DISK = N'/var/opt/mssql/backups/AdventureWorks2014.bak'  
WITH  
  COMPRESSION,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ),  
  STATS = 10  
GO  
```

For more information, see [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md).


## Next steps

For more information about the security features of SQL Server, see [Security Center for SQL Server Database Engine and Azure SQL Database](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).
