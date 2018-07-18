---
title: Introdução à segurança do SQL Server no Linux | Microsoft Docs
description: Este artigo descreve as ações de segurança típica.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.custom: sql-linux
ms.openlocfilehash: 0d7f2244a20f117d2886cdee59d54adfa4029721
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38020329"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>Instruções passo a passo para os recursos de segurança do SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Se você for um usuário do Linux que há de novo para o SQL Server, as seguintes tarefas orientarão-lo por meio de algumas das tarefas de segurança. Esses não são exclusivas ou específicas para o Linux, mas ele ajuda a dar uma ideia das áreas para investigar mais. Em cada exemplo é fornecido um link para a documentação detalhada para a área.

>  [!NOTE]
>  Os exemplos a seguir usam o **AdventureWorks2014** banco de dados de exemplo. Para obter instruções sobre como obter e instalar esse banco de dados de exemplo, consulte [restaurar um banco de dados do SQL Server do Windows para Linux](sql-server-linux-migrate-restore-database.md).


## <a name="create-a-login-and-a-database-user"></a>Crie um logon e um usuário de banco de dados 

Conceder acesso a outros para o SQL Server, criando um logon no banco de dados mestre usando o [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) instrução. Por exemplo:

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

>  [!NOTE]
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

Para obter mais informações sobre o sistema de permissão, consulte [Introdução às permissões de mecanismo de banco de dados](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).


## <a name="configure-row-level-security"></a>Configurar a segurança de nível de linha  

[Segurança em nível de linha](../relational-databases/security/row-level-security.md) lhe permite restringir o acesso às linhas em um banco de dados com base no usuário que está executando uma consulta. Esse recurso é útil para cenários como garantir que os clientes possam acessar somente seus próprios dados ou que os funcionários possam acessar somente dados que são relevantes para seus departamentos.   

As etapas a seguir orientam durante a configuração de dois usuários com acesso de nível de linha diferente para o `Sales.SalesOrderHeader` tabela. 

Crie duas contas de usuário para testar a segurança em nível de linha:    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```   

Conceder acesso de leitura no `Sales.SalesOrderHeader` tabela para ambos os usuários:    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;    
```   
   
Crie um novo esquema e embutidas com valor de tabela função. A função retorna 1 quando uma linha na `SalesPersonID` coluna corresponde à ID de um `SalesPerson` logon ou se o usuário que executa a consulta for o gerente.   
   
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

Crie uma política de segurança adicionando a função como um filtro e um predicado de bloqueio na tabela:  

```
CREATE SECURITY POLICY SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

Execute o seguinte para consultar o `SalesOrderHeader` tabela com cada usuário. Verifique `SalesPerson280` vê apenas as 95 linhas das suas próprias vendas e que o `Manager` pode ver todas as linhas na tabela.  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERT; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERT;   
```
 
Altere a política de segurança para desabilitar a política específica.  Agora os usuários podem acessar todas as linhas. 

```
ALTER SECURITY POLICY SalesFilter   
WITH (STATE = OFF);    
``` 


## <a name="enable-dynamic-data-masking"></a>Habilitar o mascaramento de dados dinâmicos

[Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md) permite que você limite a exposição de dados confidenciais a usuários de um aplicativo mascarando totalmente ou parcialmente determinadas colunas. 

Use uma `ALTER TABLE` instrução para adicionar uma função de mascaramento para o `EmailAddress` coluna o `Person.EmailAddress` tabela: 
 
```
USE AdventureWorks2014;
GO
ALTER TABLE Person.EmailAddress    
ALTER COLUMN EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
Criar um novo usuário `TestUser` com `SELECT` permissão na tabela, em seguida, executar uma consulta como `TestUser` para exibir os dados mascarados:   

```  
CREATE USER TestUser WITHOUT LOGIN;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERT;    
```
 
Verifique se que a função de mascaramento altera o endereço de email no primeiro registro de:
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## <a name="enable-transparent-data-encryption"></a>Habilite a criptografia de dados transparente

Uma ameaça para seu banco de dados é o risco de que alguém será roubar os arquivos de banco de dados fora de seu disco rígido. Isso pode acontecer com uma invasão que obtém acesso elevado ao seu sistema, as ações de um funcionário de problema ou pelo roubo do computador que contém os arquivos (por exemplo, um laptop).

Criptografia de dados transparente (TDE) criptografa os arquivos de dados conforme eles são armazenados no disco rígido. O banco de dados mestre do mecanismo de banco de dados do SQL Server tem a chave de criptografia para que o mecanismo de banco de dados pode manipular os dados. Os arquivos de banco de dados não podem ser lidos sem acesso à chave. Os administradores de alto nível podem gerenciar, fazer backup e recriar a chave, então, o banco de dados pode ser movido, mas somente por pessoas selecionadas. Quando a TDE está configurada, o `tempdb` banco de dados também será criptografado automaticamente. 

Uma vez que o mecanismo de banco de dados pode ler os dados, criptografia transparente de dados não protege contra acesso não autorizado por administradores do computador que pode diretamente ler a memória, ou acessar o SQL Server por meio de uma conta de administrador.

### <a name="configure-tde"></a>Configurar a TDE

- Crie uma chave mestra
- Crie ou obtenha um certificado protegido pela chave mestra
- Crie uma chave de criptografia de banco de dados e proteja-a com o certificado
- Defina o banco de dados para usar criptografia

Configurar a TDE requer `CONTROL` permissão no banco de dados mestre e `CONTROL` permissão no banco de dados do usuário. Normalmente, um administrador configura a TDE. 

O exemplo a seguir ilustra criptografia e descriptografia do banco de dados `AdventureWorks2014` usando um certificado instalado no servidor nomeado `MyServerCert`.


```
USE master;  
GO  

CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**********';  
GO  

CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My Database Encryption Key Certificate';  
GO  

USE AdventureWorks2014;  
GO
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO
  
ALTER DATABASE AdventureWorks2014  
SET ENCRYPTION ON;   
```

Para remover o TDE, execute `ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;`   

As operações de criptografia e descriptografia são agendadas em threads em segundo plano pelo SQL Server. É possível exibir o status dessas operações usando exibições do catálogo e de gerenciamento dinâmico na lista mostrada posteriormente neste tópico.   

>  [!WARNING]
>  Os arquivos de backup de bancos de dados com TDE habilitada também são criptografados usando a chave de criptografia do banco de dados. Como resultado, quando você restaura esses backups, o certificado que protege a chave de criptografia do banco de dados deve estar disponível. Isso significa que, além de fazer backup do banco de dados, você deve assegurar que os backups dos certificados de servidor sejam mantidos para evitar perda de dados. Se o certificado não estiver mais disponível, haverá perda de dados. Para obter mais informações, consulte [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  

Para obter mais informações sobre a TDE, consulte [criptografia de dados transparente (TDE)](../relational-databases/security/encryption/transparent-data-encryption-tde.md).   


## <a name="configure-backup-encryption"></a>Configurar a criptografia de backup
SQL Server tem a capacidade de criptografar os dados durante a criação de um backup. Especificando o algoritmo de criptografia e o Criptografador (um certificado ou chave assimétrica) durante a criação de um backup, você pode criar um arquivo de backup criptografado.    
  
> [!WARNING]  
>  É muito importante fazer backup do certificado ou da chave assimétrica e, preferencialmente, em um local diferente do arquivo de backup usado para criptografar. Sem o certificado ou a chave assimétrica, você não pode restaurar o backup, tornando o arquivo de backup inutilizável. 
 
 
O exemplo a seguir cria um certificado e, em seguida, cria um backup protegido pelo certificado.
```
USE master;  
GO  
CREATE CERTIFICATE BackupEncryptCert   
   WITH SUBJECT = 'Database backups';  
GO 
BACKUP DATABASE [AdventureWorks2014]  
TO DISK = N'/var/opt/mssql/backups/AdventureWorks2014.bak'  
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

Para obter mais informações, consulte [criptografia de Backup](../relational-databases/backup-restore/backup-encryption.md).


## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre os recursos de segurança do SQL Server, consulte [Central de segurança do mecanismo de banco de dados do SQL Server e banco de dados SQL](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).
