---
title: Introdução à segurança do SQL Server no Linux
description: Este artigo descreve as ações de segurança típica.
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.openlocfilehash: 9fe29cadaa14168871e7448350d41bc89afed05b
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834745"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>Instruções passo a passo para os recursos de segurança do SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Se você for um usuário do Linux que há de novo para o SQL Server, as seguintes tarefas orientarão-lo por meio de algumas das tarefas de segurança. Esses não são exclusivas ou específicas para o Linux, mas ele ajuda a dar uma ideia das áreas para investigar mais. Em cada exemplo é fornecido um link para a documentação detalhada para a área.

> [!NOTE]
>  Os exemplos a seguir usam o **AdventureWorks2014** banco de dados de exemplo. Para obter instruções sobre como obter e instalar esse banco de dados de exemplo, consulte [restaurar um banco de dados do SQL Server do Windows para Linux](sql-server-linux-migrate-restore-database.md).


## <a name="create-a-login-and-a-database-user"></a>Crie um logon e um usuário de banco de dados 

Conceder acesso a outros para o SQL Server, criando um logon no banco de dados mestre usando o [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) instrução. Por exemplo:

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

> [!NOTE]
>  Sempre use uma senha forte no lugar dos asteriscos no comando anterior.

Logons podem se conectar ao SQL Server e tem acesso (com permissões limitadas) no banco de dados mestre. Para se conectar a um banco de dados do usuário, um logon precisa de uma identidade correspondente no nível do banco de dados, chamado de um usuário de banco de dados. Os usuários são específicos para cada banco de dados e devem ser criados separadamente em cada banco de dados para conceder acesso a eles. O exemplo a seguir move o cursor para o banco de dados AdventureWorks2014 e, em seguida, usa o [criar usuário](../t-sql/statements/create-user-transact-sql.md) instrução para criar um usuário chamado Larry que está associado com o logon chamado Larry. Embora o logon e o usuário relacionados (mapeado para o outro), eles são objetos diferentes. O logon é um princípio de nível de servidor. O usuário é uma entidade de segurança de nível de banco de dados.

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- Uma conta de administrador do SQL Server pode se conectar a qualquer banco de dados e pode criar mais logons e usuários em qualquer banco de dados.  
- Quando alguém cria um banco de dados que eles se tornar o proprietário do banco de dados, o que pode se conectar ao banco de dados. Os proprietários de banco de dados podem criar mais usuários.

Mais tarde você pode autorizar outros logons para criar um mais logons, concedendo a ela o `ALTER ANY LOGIN` permissão. Dentro de um banco de dados, você pode autorizar que outros usuários para criar mais usuários, concedendo a ela o `ALTER ANY USER` permissão. Por exemplo:   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

Agora, o logon Larry pode criar mais logons e o usuário Jerry pode criar mais usuários.


## <a name="granting-access-with-least-privileges"></a>Conceder acesso com privilégios mínimos

As pessoas primeiro para se conectar a um banco de dados do usuário será o administrador e contas do proprietário de banco de dados. No entanto, esses usuários têm todas as permissões disponíveis no banco de dados. Esta é a permissão mais do que a maioria dos usuários deve ter. 

Quando você estiver apenas começando, você pode atribuir algumas categorias gerais de permissões usando o interno *funções de banco de dados fixas*. Por exemplo, o `db_datareader` função de banco de dados fixa pode ler todas as tabelas no banco de dados, mas sem fazer alterações. Conceder a associação em uma função de banco de dados fixa usando o [ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md) instrução. O exemplo a seguir adicionar o usuário `Jerry` para o `db_datareader` função fixa de banco de dados.   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

Para obter uma lista das funções fixas de banco de dados, consulte [funções de nível de banco de dados](../relational-databases/security/authentication-access/database-level-roles.md).

Posteriormente, quando você estiver pronto para configurar o acesso mais preciso aos seus dados (altamente recomendados), crie suas próprias funções de banco de dados definidos pelo usuário usando [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md) instrução. Atribua permissões granulares específicas a você funções personalizadas.

Por exemplo, as instruções a seguir criam uma função de banco de dados denominada `Sales`, concede a `Sales` a capacidade de ver, atualizar e excluir linhas de grupo a `Orders` da tabela e, em seguida, adiciona o usuário `Jerry` para o `Sales` função.   
   
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
Criar SalesFilter de política de segurança   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  EM Sales. SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  EM Sales. SalesOrderHeader   
WITH (STATE = ON);   
```

Execute the following to query the `SalesOrderHeader` table as each user. Verify that `SalesPerson280` only sees the 95 rows from their own sales and that the `Manager` can see all the rows in the table.  

```    
Executar como usuário = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERTER; 
 
Executar como usuário = 'Gerenciador';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERTER;   
```
 
Alter the security policy to disable the policy.  Now both users can access all rows. 

```
ALTER SalesFilter de política de segurança   
COM (ESTADO = OFF);    
``` 


## Enable dynamic data masking

[Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md) enables you to limit the exposure of sensitive data to users of an application by fully or partially masking certain columns. 

Use an `ALTER TABLE` statement to add a masking function to the `EmailAddress` column in the `Person.EmailAddress` table: 
 
```
USE AdventureWorks2014; GO ALTER TABLE Person.EmailAddress     ALTER COLUMN EmailAddress    
Adicionar MASCARADOS com (função = ' email()');
``` 
 
Create a new user `TestUser` with `SELECT` permission on the table, then execute a query as `TestUser` to view the masked data:   

```  
Criar usuário TestUser sem logon;   
GRANT SELECT ON Person.EmailAddress para TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERTER;    
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

Criar certificado MyServerCert com o assunto = 'Meu banco de dados chave certificado de criptografia';  
GO  

USE AdventureWorks2014;   GO
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
CRIPTOGRAFIA MyServerCert de certificado do servidor;  
GO
  
ALTER DATABASE AdventureWorks2014  
DEFINIR CRIPTOGRAFIA;   
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
Mestre USE;   VÁ   criar certificado BackupEncryptCert   com o assunto = 'Database backups';   ACESSE o banco de dados de BACKUP [AdventureWorks2014]   no disco = N'/var/opt/mssql/backups/AdventureWorks2014.bak'  
com  
  COMPACTAÇÃO,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   CERTIFICADO do servidor = BackupEncryptCert  
   ),  
  STATS = 10  
GO  
```

For more information, see [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md).


## Next steps

For more information about the security features of SQL Server, see [Security Center for SQL Server Database Engine and Azure SQL Database](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).
